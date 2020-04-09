```cpp
#include <iostream>
#include <queue>

using namespace std;

class Event {
public:
    int fired;
    queue<Callback> q;
    mutex mtx;

    Event(void) {
        fired = false;
    }

    void Register(CallBack & cb) {
        mtx.lock();
        if (!fired) {
            q.push_back(cb);
            mtx.unlock();
        } else {
            mtx.unlock();
            cb();
        }
        return;
    }

    // case 1 register callback may be invoked IN BETWEEN the callbacks called by Event.
    void FireEvent(void) {
        mtx.lock();
        fired = true;

        while (!q.empty()) {
            Callback & cb = q.front();
            q.pop_front();
            mtx.unlock();
            cb();
            mtx.lock();
        }
        mtx.unlock();
        return;
    }

    // case 2: race condition, register callback may be invoked BEFORE the calbacks in queue.
    void FireEvent(void) {
        mtx.lock();
        fired = true;
        mtx.unlock();

        while (!q.empty()) {
            Callback & cb = q.front();
            q.pop_front();
            cb();
        }
        mtx.unlock();
        return;
    }

    // case 3: Sequence is garented, register callback may be invoked BEFORE the calbacks in queue.
    void FireEvent(void) {
        mtx.lock();

        while (true) {
            if (!q.empty()) {
                Callback & cb = q.front();
                q.pop_front();
                mtx.unlock();
                cb();
                mtx.lock();
            } else {
                fired = true;
                mtx.unlock();
                break;
            }
        }

        return;
    }
};

//bitmap
#include <iostream>
#include <vector>

using namespace std;

int clearBitMap(vector<int> & map, int start, int len) {
    int left = start, right = start + len - 1;
    int size = map.size();

    if (map.empty() || left < 0 || right > size)
        return -1;

    // clear ancestor
    map[0] = 0;
    while (left != 0 || right != 0) {
        for (int i = left; i <= right; ++i) {
            map[i] = 0;
        }
        cout << "l:" << left << right << endl;
        left = (left > 0) ? (left - 1) >> 1 : 0;
        right = (right > 0) ? (right - 1) >> 1 : 0;
    }

    // clear descendent
    left = start;
    right = start + len - 1;
    while (left < size) {
        for (int i = left; i <= right && i < size; ++i) {
            map[i] = 0;
        }

        cout << "dl:" << left << right << endl;
        left = (left << 1) + 1;
        right = (right + 1) << 1;
    }

    return 0;
}

int setBitMap(vector<int> & map, int start, int len) {
    int left = start, right = start + len - 1;
    int size = map.size();

    if (map.empty() || left < 0 || right >= size)
        return -1;

    // set ancestor
    map[0] = 0;
    while ((left != 0 || right != 0) && (left <= right)) {
        for (int i = left; i <= right; ++i) {
            map[i] = 1;
        }
        cout << "sal:" << left << right << endl;

        if (left % 2 == 0) {
            left = map[left - 1] ? left >> 1 : (left + 1) >> 1;
        } else {
            left = (left > 0) ? (left - 1) >> 1 : 0;
        }

        if (right % 2 && right < size - 1) {
            right = map[right + 1] ? right >> 1 : (right >> 1) - 1;
        } else {
            right = (right > 0) ? (right - 1) >> 1 : 0;
        }
    }

    // set descendent
    left = start;
    right = start + len - 1;
    while (left < size) {
        for (int i = left; i <= right && i < size; ++i) {
            map[i] = 1;
        }

        cout << "sdl:" << left << right << endl;
        left = (left << 1) + 1;
        right = (right + 1) << 1;
    }

    return 0;
}
```

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
```

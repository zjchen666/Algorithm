## stack ##
* 链表相关
* 字符串相关
* 执行一些操作

### 解法
   Go through input list, 根据题意选择出栈的时机
  
```python
   stack = []
   for index, num in enumerate(list):
       while s and condition 1:
          stack.pop()
          // calculate
       stack.append()
   return
```
   

## circule buffer ##
```cpp
typedef struct {
    void*   address;
    size_t  size;
    size_t* pi;
    size_t* ci;    
} cb;

int BufferAlloc( cb* buf, size_t size ) {
    void* p = NULL;
    p = malloc(size);
    if (NULL == p) {
        return ERR_NO_MEMORY;

} else {
        cb->address = p;
        cb->size = size;
        cb->pi = 0;
        cb->ci = 0;
    }
    return SUCCESS;
}

int BufferFree( cb* buf ) {
    if (NULL != buf->address) {
        free(buf->address);
        cb->address = NULL;
        cb->size = 0;
        cb->pi = 0;
        cb->ci = 0;
        return SUCESS;
    } 
    return FAILURE;
}

int GetFreeSpace ( cb* buf ) {
    if (buf->pi > buf->ci) {
        return buf->size - buf->pi + buf->ci - 1;
    } else {
        return buf->ci - buf->pi;
    }
}

int GetDataSize ( cb* buf ) {
    if (buf->pi < buf->ci) {
        return buf->size - buf->ci + buf->pi;
    } else {
        return buf->ci - buf->pi;
    }
}

int PutData (cb* buf, size_t size, void* data) {
    if (size <= cb->size - cb->pi) {
        memcpy( cb->address + cb->pi, data, size);
    } else {
        memcpy( cb->address + cb->pi, data, cb->size - cb->pi);
        memcpy( cb->address, (char*)data + (cb->size - cb->pi), size - cb->size - cb->pi);
        cb->pi = size - cb->size - cb->pi;
    }
    return 0;
}

int GetData (cb* buf, size_t size, void* data) {
    if (size <= cb->size - cb->ci) {
        memcpy( data, cb->address + cb->ci, size);
    } else {
        memcpy( data, cb->address + cb->ci, cb->size - cb->ci);
        memcpy( (char*)data + (cb->size - cb->ci), cb->address, size - cb->size - cb->pi);
        cb->ci = size - cb->size - cb->ci;
    }
    return 0;
}

```

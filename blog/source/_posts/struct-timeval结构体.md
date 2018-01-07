---
title: struct timeval结构体
date: 2018-01-07 20:12:07
tags: 学习
---

# struct timeval

struct timeval是在linux中的一个关于时间的定义，在time.h中进行定义，原型是：

```
struct timeval  
{  
__time_t tv_sec;        /* Seconds. */  
__suseconds_t tv_usec;  /* Microseconds. */  
}; 
```
其中，tv_sec为Epoch到创建struct timeval的秒数，tv_usec为微秒数。使用demo如下：

```
#include<iostream>
#include <unistd.h>
#include <sys/time.h>
using namespace std;

int main(int argc,char *argv[]){
    int i;
    struct timeval tv;

    for(i = 0;i < 10; i++) {
        gettimeofday(&tv, NULL);
        cout << tv.tv_sec << " " << tv.tv_usec << endl;
        sleep(1);
    }
    return 0;
}

/* vim: set ts=4 sw=4 sts=4 tw=100 */
```

运行结果如下：

```
1510467679 792342
1510467680 792449
1510467681 792503
1510467682 792577
1510467683 792646
1510467684 792691
1510467685 792764
1510467686 792829
1510467687 792896
1510467688 792959
```

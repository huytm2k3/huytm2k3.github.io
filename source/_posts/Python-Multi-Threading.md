---
title: Python Multi Threading
date: 2023-03-23 22:11:45
tags:
---

Đa luồng

```py
from threading import Thread
import time

def counter_1():
    for i in range(1,5):
        print(i)
        time.sleep(1)
def counter_2():
    for i in range(6, 10):
        print(i)
        time.sleep(1)

# Try catch

try:
    t = time.time()
    
    t1 = Thread(target=counter_1, args=())
    t2 = Thread(target=counter_2, args=())

    t1.start()
    t2.start()

    ## Đồng bộ 2 thread, để in ra print sau khi 2 hàm hoàn thành

    # t1.join()
    # t2.join()

    print("done in", time.time() - t)
except:
    print("error")
```

output

```sh
1
6
done in 0.000946044921875
2
7
8
3
4
9
```


Nếu thêm join

```py
    ## Đồng bộ 2 thread, để in ra print sau khi 2 hàm hoàn thành

    t1.join()
    t2.join()
```

Output:

```sh
1
6
2
7
3
8
4
9
done in 4.004803419113159
```
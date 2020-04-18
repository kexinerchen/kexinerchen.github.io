---
layout: post
title: C Programing Language
author: Kexiner

---

<br>

## 遞歸
C語言支持一個函數調用自身
### 階乘
```c
#include <stdio.h>
 
double factorial(unsigned int i)
{
   if(i <= 1)
   {
      return 1;
   }
   return i * factorial(i - 1);
}
int  main()
{
    int i = 15;
    printf("%d!=: %f\n", i, factorial(i));
    return 0;
}

```

<br>

### 斐波那契數列
```c
#include <stdio.h>
 
int fibonaci(int i)
{
   if(i == 0)
   {
      return 0;
   }
   if(i == 1)
   {
      return 1;
   }
   return fibonaci(i-1) + fibonaci(i-2);
}
 
int  main()
{
    int i;
    for (i = 0; i < 10; i++)
    {
       printf("%d\t\n", fibonaci(i));
    }
    return 0;
}

```

<br>
<br>
<br>


## 排序


<br>
<br>
<br>


---
layout: post
title: C Programing Language
author: Kexiner

---

<br>


## 數組,字符串和指針
```c
double a[3] = {1000.0, 3.4, 7.0}; //a是指向數組第一個元素地址&a[0]的指針,a=&a[0],*a=a[0],*(a+1)=a[1]
int b[2][3] = {0,1,2,3,4,5};    //其中a[1]={0,1,2}
```
### 字符指針,字符數組
//因爲只有char類型,字符串要用數組來表示
```c
char a[][10];   //串最大長度10

char *p = "hello";
char q[] = "hello";
printf ("p: %s\n", p);
printf ("q: %s\n", q);
//p和q存儲的是一樣的地址,輸出一樣
//但char指針p的數據沒有分配,不能修改,這兩個使用內存方式不同
```
<br>
<br>

### 指針
算術運算: ++  --  +  -  ==  >  <    

可指向整型,浮點型,字符型,數組,**函數**

### 指針數組
存儲指針的數組
```c
//存儲char指針的數組
char *arr[4] = {"hello", "world", "shannxi", "xi\'an"};
//相當於四個指針,每個指針存一個字符串:
char *p1 = "hello";
char *p1 = "world";
char *p3 = "shannxi";
char *p4 = "xi\'an";
```
```c
#include <stdio.h> 
const int MAX = 3;
int main ()
{
   int  var[] = {10, 100, 200};
   //存儲int指針的數組
   int i, *ptr[MAX];
 
   for ( i = 0; i < MAX; i++)
   {
      ptr[i] = &var[i]; //賦值地址
   }
   for ( i = 0; i < MAX; i++)
   {
      printf("Value of var[%d] = %d\n", i, *ptr[i] );
   }
   return 0;
}

```
<br>
<br>

### 數組指針
```c
char (*pa)[4];
char a[4];
//pa是一個指針,指向一個char[4]數組,每個數組元素是一個char類型的變量
//a是數組首地址,pa是指向數組的指針
//可以使用*(a+1)訪問a[1]

```
<br>
<br>

### 指向指針的指針
```c
int var=300, *ptr, **pptr;
ptr=&var;
pptr=&ptr;
//var = *ptr = **pptr

```
<br>

### 傳遞指針/數組給函數
```c
#include <stdio.h>
#include <time.h>
void getSeconds(unsigned long *par);
int main ()
{
   unsigned long sec;
   getSeconds( &sec );  //sec的地址&sec傳給getSeconds
   printf("Number of seconds: %ld\n", sec );
   return 0;
}
//par = &sec, *par=sec
void getSeconds(unsigned long *par)
{
   *par = time( NULL ); //當前秒數
   return;
}
```
```c
void Func(int *param){}     //形參是指針
void Func(int param[10]){}  //形參是已知大小的數組
void Func(int param[]){}    //形參是未知大小的數組
```
```c
void swap(int *x, int *y)
{
   int temp;
   temp = *x;    
   *x = *y;      
   *y = temp;  
   return;
}
swap(&a, &b);

```
<br>
<br>

### 從函數返回指針/數組
C語言不允許返回一個完整的數組,但可以通過返回不帶索引的數組名來返回一個指向數組的指針
另外C不支持在函數外返回局部變量的地址,除非定義局部變量爲static變量
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
int * getRandom( )
{
  static int  r[10];
  int i;
  
  srand( (unsigned)time( NULL ) );
  for ( i = 0; i < 10; ++i)
  {
     r[i] = rand();
     printf( "r[%d] = %d\n", i, r[i]);
   }
  return r;
}
 
int main ()
{
   int *p;
   int i; 
   p = getRandom();
   for ( i = 0; i < 10; i++ )
   {
       printf( "*(p + %d) : %d\n", i, *(p + i));
   }
   return 0;
}

```
<br>
<br>
<br>
<br>


## 指針數組的參數傳遞
```c
//指針數組在主函數傳參中, argc確定傳入參數個數, argv是傳入參數的地址
int main(int argc, char *argv[])

//子函數傳參中,傳遞的是指針數組的地址,
void fun(char **pp);//子函数中的形参
fun(char *p[]);//主函数中的实参
```
```c
#include <stdio.h>
#include <string.h>
//冒泡法
void sort(char **pa, int n)
{
    int i, j;
    char *tmp = NULL;

    for(i = 0; i < n-1; i++){
        for(j = 0; j < n-1-i; j++){
            if((strcmp(*(pa+j), *(pa+j+1))) > 0){
                tmp = *(pa + j);
                *(pa + j) = *(pa + j + 1);
                *(pa + j + 1) = tmp;
            }
        }
    }
}

int main ()
{
    char *pa[4] = {"abc", "xyz", "opq", "ijk"};
    int i;
    sort(pa,4);
    for(i=0;i<4;i++){
    printf("%s\n", pa[i] );
    }
    return 0;
}

```


<br>
<br>
<br>


## 函數指針,回調函數
函數指針是指向函數的指針
```c
#include <stdio.h>
int max(int x, int y)
{
    return x > y ? x : y;
}
int main(void)
{
    int (* p)(int, int) = & max; // &可以省略
    int a, b, c, d;
    printf("please input 3 numbers:");
    scanf("%d %d %d", & a, & b, & c);
 
    d = p(p(a, b), c); // same as call function max
    printf("max number is: %d\n", d); 
    return 0;
}

```
回調函數是函数指针作为某个函数的参数
```c
#include <stdio.h>
#include <stdlib.h>

// size_t: stdlib中定義的无符号整型
void populateArray(int *array, size_t arraySize, int (*getNextValue)(void))
{
    for (size_t i=0; i<arraySize; i++){
        array[i] = getNextValue();
    }
} 
int getNextRandomValue(void)
{
    return rand();
}

int main(void)
{
    int myarray[10];
    populateArray(myarray, 10, getNextRandomValue);
    for(int i = 0; i < 10; i++) {
        printf("%d ", myarray[i]);
    }
    printf("\n");
    return 0;
}

```
<br>
<br>
<br>


## 指針函數
**指針函數**, \*的优先级低于(), 也就意味着,pfun是个函数,返回值爲整型指針的函數
```c
int *pfun(int, int);
```
**函數指針**, pfun是個指針,指向返回值爲整型函數的指針
```c
int (*pfun)(int, int);

```

<br>
<br>
<br>


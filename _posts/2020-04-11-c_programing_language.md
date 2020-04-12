---
layout: post
title: C Programing Language
author: kexiner

---

---
---
---


```shell
$ gcc addtwonum.c test.c -o main
$ ./main

```
---

<br>

### Basics

字符型常量,單引號: 'a', 'b'

字符串常量,雙引號: "abc"

數據類型轉換,自動: 浮點數賦給整型,小數部分省去


Lvalues和Rvalues: 變量是Lvalues,數值型的字面值是Rvalues,不能出現在賦值號的左側, e.g.10=20

八進制(零開頭): 021       十六進制: 0x46      帶符號的指數由e或E引入: 314159E-5L

定義常量: 預處理器(#define a 100),      const關鍵字(const int a=10)        typeof,取別名

C存儲類: 定義C中變量/函數的範圍(可見性)和生命週期
```c
auto: //所有局部變量默認的,只能用在函數內修飾局部變量
register: //存儲在寄存器中的局部變量,可快速訪問
static: //修飾局部變量,可以在函數調用之間保持變量的值;修飾全局變量(全局變量默認static),會使變量作用域限制在聲明它的文件內
extern: //聲明已經定義的變量或函數,不是新的定義
extern int i;   //聲明,不是定義
int i;          //聲明,也是定義

```

<br>
<br>
<br>


### 枚舉類型
定義只能賦予一些離散整數值的變量
enum　枚举名　{枚举元素1,枚举元素2,……};
#### 先定义枚举类型，再定义枚举变量
```c
enum DAY
{
      MON=1, TUE, WED, THU, FRI, SAT, SUN
};
enum DAY day;
```
#### 定义枚举类型的同时定义枚举变量
```c
enum DAY
{
      MON=1, TUE, WED, THU, FRI, SAT, SUN
} day;
```
#### 省略枚举名称，直接定义枚举变量
```c
enum
{
      MON=1, TUE, WED, THU, FRI, SAT, SUN
} day;
```
```c
#include<stdio.h>
enum DAY
{
      MON=1, TUE, WED, THU, FRI, SAT, SUN
};
int main()
{
    enum DAY day;
    // DAY連續,遍歷枚舉元素
    for (day = MON; day <= SUN; day++) {
        printf("枚舉元素：%d \n", day);
    }
}
```
```c
//第一個元素默認爲0,spring=0,不連續,沒有指定值的元素,其值爲前一元素加1
enum season {spring, summer=3, autumn, winter};

```
<br>
<br>


### 運算符
```
算術: +  -  *  /  %  ++  --
關係: ==  !=  >  <  >=  <= 
邏輯: &&  ||  !
位:   &  |  ~  ^  <<  >>
賦值: =  +=  -=  *=  /=  %=  <<=  >>=  &=  |=  ^=
```
```
其它: sizeof()返回變量大小(位數), &返回變量地址, *返回變量內容, ?:條件表達式
int b = (a == 1) ? 20: 30; //如果a==1賦值20,否則賦值30
^: 0^0=0; 0^1=1; 1^0=1; 1^1=0;
<<: 左邊的丟棄,右邊的補0
>>: 正數左邊補0,負數左邊補1,右邊丟棄

```
<br>
<br>


### 選擇語句
```c
if...else...

switch(expression){
    case constant-expression  :
       statement;
       break; // 可選的
    case constant-expression  :
       statement;
       break; //可選的
  
    default : //可選的
       statement;
}
//expression是一個常量表達式,必須時整型或枚舉類型
//如果case語句不包含break,將繼續執行後面的case,直到遇見break才跳出switch
//default用在最後,如果上面所有的case都不爲真時,執行default,default中的break不是必須的

```
<br>
<br>

### 循環語句
```c
while(condition)
{
   statement(s);
}

for ( init; condition; increment )
{
   statement(s);
}

do
{
   statement(s);

}while( condition );
```
```c
break; //終止循環或者switch語句
continue; //終止本次循環,開始下次循環迭代
goto;//無條件轉移到被標記語句

goto label;
..
.
label: statement;

```
<br>
<br>
<br>
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
char *arr[4] = {"hello", "world", "shannxi", "xi'an"};
//相當於四個指針,每個指針存一個字符串:
char *p1 = “hello";
char *p1 = “world”;
char *p3 = “shannxi”;
char *p4 = “xi'an”;
```
```c
#include <stdio.h> 
const int MAX = 3;
int main ()
{
   int  var[] = {10, 100, 200};
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
//C語言不允許返回一個完整的數組,但可以通過返回不帶索引的數組名來返回一個指向數組的指針
//另外C不支持在函數外返回局部變量的地址,除非定義局部變量爲static變量
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
```


```


## 函數指針
```


```


## 指針函數
```



```




## 結構體和共用體
```



```
## 文件讀寫
```




```






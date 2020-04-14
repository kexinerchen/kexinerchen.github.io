---
layout: post
title: C Programing Language
author: kexiner

---

<br>
<br>


## 枚舉類型
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
<br>


## 結構體和共用體
結構體允許存儲不同類型的數據項
```c
struct tag { 
    member-list
    member-list 
    member-list  
    ...
} variable-list ;
```
結構體的成員可以是其他的結構體
```c
struct COMPLEX
{
    char string[100];
    struct SIMPLE a;
};
```
成員可以包含指向自己的結構體,通常爲了實現高級數據結構,如鏈表,樹
```c
struct NODE
{
    char string[100];
    struct NODE *next_node;
};

```
兩個結構體互相包含
```c
struct B;    //對結構體B進行不完整聲明
struct A
{
    struct B *partner;
    //other members;
};
struct B
{
    struct A *partner;
    //other members;
};

```
結構體變量的初始化和成員訪問
```c
struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
} book = {"C Language", "RUNOOB", "Programing", 123};
```
成员访问运算符是句號 .
```c
struct Books Book1;
strcpy( Book1.title, "C Programming");
strcpy( Book1.author, "Nuha Ali"); 
strcpy( Book1.subject, "C Programming Tutorial");
Book1.book_id = 6495407;

```
結構體作爲函數參數
```c
void printBook(struct Books book){}    //定義
printBook(Book1);   //引用
```
定義結構體指針
```c
struct Books *struct_pointer;
struct_pointer = &Book1;
struct_pointer->title;  //結構體指針的成員訪問,運算符 ->

```

### 位域
位域是指把字節中的二進制位劃分爲幾個不同的區域,位域不允許跨兩個字節
例如用1位二進制位存放開關變量,只有0和1兩種狀態
```c
struct bs{
    int a:8;
    int b:2;
    int c:6;
}data;
//data是bs變量,共兩個字節,其中位域a佔8位,b佔2位,c佔6位
```
位域可以是無名位域,只用來填充或調整位置,不能引用
```c
struct k{
    int a:1;
    int  :2;  //無名位域
    int b:3;
    int c:2;
};

```
位域的使用和結構體的使用相同
```c
main(){
    struct bs{
        unsigned a:1;
        unsigned b:3;
        unsigned c:4;
    } bit,*pbit;

    bit.a=1;    //賦值不能超過該位域的允許範圍, a最大爲1
    bit.b=7;    
    bit.c=15;   
    printf("%d,%d,%d\n",bit.a,bit.b,bit.c);
    pbit=&bit;    //把位域bitde地址賦予位域指針變量
    pbit->a=0;    //用指針方式對a重新賦值
    pbit->b&=3;    // 複合運算符,相當於pbit->b=pbit->b&3, 7與3按位與運(111&011=011)
    pbit->c|=1;    //按位或,pbit->c=pbit->c|1, 結果爲15 
    printf("%d,%d,%d\n",pbit->a,pbit->b,pbit->c);
}
```

<br>

### 共用體
允許在相同的內存位置存儲不同的數據類型
共用體佔用的內存是存儲最大成員所需的內存
```c
union [union tag]
{
   member definition;
   member definition;
   ...
   member definition;
} [one or more union variables];
```
```c
#include <stdio.h>
#include <string.h>
 
union Data
{
   int i;
   float f;
   char  str[20];
};
 
int main( )
{
   union Data data;        
 
   data.i = 10;
   data.f = 220.5;
   strcpy( data.str, "C Programming");
 
   printf( "data.i : %d\n", data.i);
   printf( "data.f : %f\n", data.f);
   printf( "data.str : %s\n", data.str);
 
   return 0;
}

output:
data.i : 1917853763
data.f : 4122360580327794860452759994368.000000
data.str : C Programming
//因str佔用了位置,i和f的值損壞

```
<br>
<br>
<br>







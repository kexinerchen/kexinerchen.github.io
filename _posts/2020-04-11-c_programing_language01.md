---
layout: post
title: C Programing Language
author: Kexiner

---

<br>


```shell
$ gcc test.c -o main
$ ./main

```

<br>

## Basics

字符型常量,單引號: 'a', 'b'

字符串常量,雙引號: "abc"

數據類型轉換,自動: 浮點數賦給整型,小數部分省去


Lvalues和Rvalues: 變量是Lvalues,數值型的字面值是Rvalues,不能出現在賦值號的左側, e.g.10=20

八進制(零開頭): 021       十六進制: 0x46      帶符號的指數由e或E引入: 314159E-5L

定義常量: 預處理器(#define a 100),      const關鍵字(const int a=10)        typeof返回類型

printf輸出時,double和float都可以用%f, double還可以用%lf

scanf輸入時, double必須用%lf,float必須用%f

<br>

```c
#include <stdio.h>

int main(){
    printf("len of float: %lu \n", sizeof(float));
    printf("len of double: %lu \n", sizeof(double));

    return 0;
}
```

<br>
<br>

#### typedef: 取別名
typedef 僅限於爲類型定義別名, 由編譯器解釋

**#define** 不僅可以爲類型取別名, 還可以爲數值定義別名,比如可以定義1爲ONE, 由預編譯器進行處理


```c
typedef unsigned char BYTE;
```
```c
#include <stdio.h>
#include <string.h>
 
typedef struct Books
{
   char  title[50];
   char  author[50];
   char  subject[100];
   int   book_id;
} Book;
 
int main( )
{
   Book book; 
   strcpy( book.title, "C Programing Language");
   strcpy( book.author, "Runoob"); 
   strcpy( book.subject, "Programing");
   book.book_id = 12345;
 
   printf( "Title : %s\n", book.title);
   printf( "Author : %s\n", book.author);
   printf( "Subject : %s\n", book.subject);
   printf( "Book ID : %d\n", book.book_id);
 
   return 0;
}

```
<br>

#### C存儲類: 定義C中變量/函數的範圍(可見性)和生命週期
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

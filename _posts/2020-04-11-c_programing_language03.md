---
layout: post
title: C Programing Language
author: kexiner

---



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

## 文件讀寫
<span style="color:#ff8000"> C語言把所有設備當做文件,文件指針是訪問文件的方式 </span>

### 訪問頂層(顯示屏,鍵盤)
```c
int scanf(const char *format, ...)
//從標準輸入流stdin讀取輸入,並根據提供的format來瀏覽輸入

int printf(const char *format,...)
//把輸出寫出到標準輸出流stdout,並根據格式輸出

```
```c
int getchar(void)
//從屏幕讀取下一個可用的字符,並把它返回爲一個整數,一次只讀取一個字符

int putchar(int c)
//把字符輸出到屏幕,並返回相同的字符,一次只輸出一個字符
```
```c
#include <stdio.h>
int main( )
{
   int c;
   printf( "Enter a value :");
   c = getchar( );
 
   printf( "\nYou entered: ");
   putchar( c );
   printf( "\n");
   return 0;
}

```
```c
char *gets(char *s)
//從stdin讀取一行到s所指向的緩衝區,直到遇到終止符

int puts(const char *s)
//把字符串s和一個尾隨的換行符寫入到stdout
```
```c
#include <stdio.h>
int main( )
{
   char str[100];
   printf("Enter a value :");
   gets(str);
 
   printf("\nYou entered: ");
   puts(str);
   return 0;
}

```
<br>

### 訪問底層(存儲設備上的文件)

```c
FILE *fopen( const char * filename, const char * mode );
//fopen()用來創建或者讀取文件, 有r w a r+ w+ a+等多種模式

int fclose( FILE *fp );
//fclose()返回0表示成功,返回EOF表示發生錯誤. EOF是一個定義在stdio.h中的常量
```
```c
int fputc( int c, FILE *fp );
//fputc()把參數c的字符值寫入到fp所指的輸入流中, 成功則返回寫入的字符, 發生錯誤則返回EOF

int fgetc( FILE * fp );
//fgetc()從fp所指向的輸入文件中讀取一個字符, 
```
```c
int fputs( const char *s, FILE *fp );
//fputs()把一個以null結尾的字符串s寫入到fp所指的輸入流中, 成功返回非負值, 發生錯誤返回EOF

char *fgets( char *buf, int n, FILE *fp );
//fgets()從fp所指向的輸入流中讀取n-1個字符,最後加一個null字符來終止字符串
//如在最後一個字符前遇到換行符"\n"或文件終止符EOF,則終止, 遇到換行符不終止

```
<br>

```c
#include <stdio.h>
int main()
{
   FILE *fp = NULL;
   fp = fopen("/tmp/test.txt", "w+");
   fprintf(fp, "This is testing for fprintf...\n");
   fputs("This is testing for fputs...\n", fp);
   fclose(fp);
}

```
```c
#include <stdio.h>
int main()
{
   FILE *fp = NULL;
   char buff[255];
 
   fp = fopen("/tmp/test.txt", "r");
   fscanf(fp, "%s", buff);
   //從文件中讀取字符串,遇到空格或換行符停止讀取
   printf("1: %s\n", buff );
 
   fgets(buff, 255, (FILE*)fp);
   printf("2: %s\n", buff );
   
   fgets(buff, 255, (FILE*)fp);
   printf("3: %s\n", buff );
   fclose(fp);
}

out:
1: This
2: is testing for fprintf...

3: This is testing for fputs...

```
<br>

### 二進制I/O
```c
size_t fread(void *ptr, size_t size_of_elements, 
             size_t number_of_elements, FILE *a_file);
              
size_t fwrite(const void *ptr, size_t size_of_elements, 
             size_t number_of_elements, FILE *a_file);

```
<br>
<br>
<br>

## 預處理器







聲明:本文內容主要總結自runoob.com, 僅供學習使用
<br>




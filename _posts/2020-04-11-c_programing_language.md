---
layout: post
title: C Programing Language
author: kexiner

---


```shell
$ gcc test.c -o main
$ ./main

```

<br>

### Basics

字符型常量,單引號: 'a', 'b'

字符串常量,雙引號: "abc"

數據類型轉換,自動: 浮點數賦給整型,小數部分省去


Lvalues和Rvalues: 變量是Lvalues,數值型的字面值是Rvalues,不能出現在賦值號的左側, e.g.10=20

八進制(零開頭): 021       十六進制: 0x46      帶符號的指數由e或E引入: 314159E-5L

定義常量: 預處理器(#define a 100),      const關鍵字(const int a=10)        typeof返回類型

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
```




```

<br>
<br>
<br>


聲明:本文內容主要總結自runoob.com, 僅供學習使用
<br>




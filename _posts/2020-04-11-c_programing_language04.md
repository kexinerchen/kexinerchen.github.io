---
layout: post
title: C Programing Language
author: Kexiner

---

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
c預處理器是個文本替換工具,在實際編譯之前進行. 所有的預處理器命令都以<span style="color:#ff8000"> #<span>開頭
```c
#define     \\定義宏
#include    \\包含源代碼文件
#undef      \\取消已定義的宏
#ifdef      \\如果宏已經定義,則返回真
#ifndef     \\如果宏沒有定義,則返回真
#if         \\如果條件爲真,編譯下面代碼
#else       
#elif       
#endif      \\結束一個#if...#else...條件編譯塊
#error      遇到標準錯誤時,輸出錯誤信息
#pragma 像編譯器發送特殊的命令
```
```c
#ifndef MESSAGE
   #define MESSAGE "You wish!"
#endif
```
```c
#ifdef DEBUG
   /* Your debugging statements here */
#endif
```
<br>

### 預定義宏
```c
__DATE__  __TIME__  //時間
__FILE__  //當前文件名
__LINE__  //當前行
__DTDC__  //當編譯器以ANSI標準編譯時,返回1
```
```c
#include <stdio.h>
main()
{
   printf("File :%s\n", __FILE__ );
   printf("Date :%s\n", __DATE__ );
   printf("Time :%s\n", __TIME__ );
   printf("Line :%d\n", __LINE__ );
   printf("ANSI :%d\n", __STDC__ );

}

out:
File :test.c
Date :Jun 2 2012
Time :03:36:24
Line :7
ANSI :1
```
<br>

### 預處理器運算符
宏延續運算符 \
```c
#define  message_for(a, b)  \
    printf(#a " and " #b ": We love you!\n")
```
字符串常量化運算符 #
```c
#include <stdio.h>
#define  message_for(a, b)  \
    printf(#a " and " #b ": We love you!\n")

int main(void)
{
   message_for(Carole, Debra);
   return 0;
}
```
標記粘貼運算符 ##
```c
#include <stdio.h>
#define tokenpaster(n) printf ("token" #n " = %d", token##n)

int main(void)
{
   int token34 = 40;
   
   tokenpaster(34);
   return 0;
}

out:
token34 = 40
//相當於
printf ("token34 = %d", token34);
```

defined()運算符
```c
#include <stdio.h>

#if !defined (MESSAGE)
   #define MESSAGE "You wish!"
#endif

int main(void)
{
   printf("Here is the message: %s\n", MESSAGE);  
   return 0;
}
```
<br>

### 參數化的宏
```c
#define square(x) ((x) * (x))
```
``c
#include <stdio.h>

#define MAX(x,y) ((x) > (y) ? (x) : (y))

int main(void)
{
   printf("Max between 20 and 10 is %d\n", MAX(10, 20));  
   return 0;
}
```
<br>
<br>
<br>

## 頭文件
```c
#include <file>     //引用系統頭文件,先在編譯器路徑裏尋找
#include "file"     //引用用戶頭文件,先在用戶目錄尋找
```
只引用一次頭文件, 兩次會編譯出錯
```c
#ifndef HEADER_FILE
#define HEADER_FILE
the entire header file
#endif
```
有條件引用
```c
#if SYSTEM_1
   # include "system_1.h"
#elif SYSTEM_2
   # include "system_2.h"
#elif SYSTEM_3
   ...
#endif
```
```c
 #define SYSTEM_H "system_1.h"
 ...
 #include SYSTEM_H
```

<br>
<br>
<br>

## 強制類型轉換
```c
int sum = 17, count = 5;
double mean;
mean = (double) sum / count;
//優先級大於加減乘數, 先蔣sum轉換爲double,然後除
```
```c
int  i = 17;
char c = 'c'; /* ascii 值是 99 */
int sum;
sum = i + c;
//把c轉換爲99後相加,sum爲116
```
算術轉換(自動轉換)
```c
short,char -> int -> long -> float -> double
```

<br>
<br>
<br>

## 錯誤處理
C不提供對錯誤處理的直接支持,但可以通過返回值的形式訪問底層數據

在初始化是把errno設置爲0, 表示沒有錯誤, 當發生錯誤時, 函數調用會返回1或者NULL

```c
perror()    //返回error文本消息
strerror()  //返回指向errno文本消息的指針
```
```c
#include <stdio.h>
#include <errno.h>
#include <string.h>
 
extern int errno ;
 
int main ()
{
   FILE * pf;
   int errnum;
   pf = fopen ("unexist.txt", "rb");
   if (pf == NULL)
   {
      errnum = errno;
      fprintf(stderr, "error number: %d\n", errno);
      perror("perror message");
      fprintf(stderr, "strerror message:%s\n", strerror( errnum ));
   }
   else
   {
      fclose (pf);
   }
   return 0;
}
```

<br>
<br>
<br>

## 命令行參數
```c
#include <stdio.h>

int main( int argc, char *argv[] )  
{
   printf("Program name %s\n", argv[0]);

   if( argc == 2 )
   {
      printf("The argument supplied is %s\n", argv[1]);
   }
   else if( argc > 2 )
   {
      printf("Too many arguments supplied.\n");
   }
   else
   {
      printf("At least one argument expected.\n");
   }
}
```
```shell
$./a.out testing
The argument supplied is testing

$./a.out testing1 testing2
Too many arguments supplied.

$./a.out "testing1 testing2"
Progranm name ./a.out
The argument supplied is testing1 testing2

```
如果沒有參數, argc爲1

argv[0]存儲程序名稱,argv[1]是指向第一個命令行參數的指針

argc和argv可以換testc,testv等


### linux下可以用getopt和getopt_long對命令行參數進行解析

```c
int main(int argc, char *argv[]){
    char *optstr = "p:n:m:c:";
    struct option opts[] = {
        {"path", 1, NULL, 'p'},
        {"name", 1, NULL, 'n'},
        {"mtime", 1, NULL, 'm'},
        {"ctime", 1, NULL, 'c'},
        {0, 0, 0, 0},
    };
    int opt;
    while((opt = getopt_long(argc, argv, optstr, opts, NULL)) != -1){
        switch(opt) {
            case 'p':
                strcpy(path, optarg);
                break;
            case 'n':
                strcpy(targetname, optarg);
                break;
            case 'm':
                modifiedtime = atoi(optarg);
                break;
            case 'c':
                changetime = atoi(optarg);
                break;
            case '?':
                if(strchr(optstr, optopt) == NULL){
                    fprintf(stderr, "unknown option '-%c'\n", optopt);
                }else{
                    fprintf(stderr, "option requires an argument '-%c'\n", optopt);
                }
                return 1;
        }
    }
    findInDir(path);
    return 0;
}

```











<br>
<br>
<br>



























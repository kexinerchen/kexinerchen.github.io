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


程式在執行的過程中，需要運算許多的資訊，也需要儲存許多的資訊，資訊是儲存在記憶體空間中，由於資料的型態各不相同，在儲存時所需要的容量不一，不同的資料必須要配給不同的空間大小來儲存，因而有了資料型態（Data type）的規範。

C 的基本資料型態主要區分為整數（Integer）、浮點數（Float）、字元（Character），而這幾種還可以細分，如下所示：

整數

用來表示整數值，可以區分為 short、int、與 long，配置的記憶體長度在不同編譯器上各不相同，可容納的大小各不相同，在 64 位元 Ubuntu 16.04 中的 gcc 編譯器下，short 為 2 位元組、int 與 long 為 8 位元組，型態的長度越長，表示可表示的整數值範圍越大。

浮點數

用來表示小數值，可以區分為 float、double 與 long double，在 64 位元 Ubuntu 16.04 中的 gcc 編譯器下，float 的長度為 4 個位元組，double 的長度為 8 個位元組，long double 長度為 12 個位元組。

字元

用來儲存字元，長度為 1 個位元組，其字元編碼主要依 ASCII 表而來，由於字元在記憶體中所佔有的空間較小，所以它也可以用來儲存較小範圍的整數。

在新的 C11 標準中，建議包括 stdint.h 程式庫，使用 int8_t、int16_t、int32_t、int64_t uint8_t、uint16_t、uint32_t、uint64_t 等作為整數型態的宣告，以避免平台相依性的問題。這邊的文件作為一個過渡（也因目前還沒有心力整個改寫），暫時還是使用舊的 int、long 等型態來撰寫。

以上的資料型態在記憶體中佔有的大小依編譯器而有所差異，想知道這些資料型態在使用的平台上，佔有的記憶體空間有多少，可以使用 sizeof() 運算子，它可以告訴您確實的記憶體大小，下面這個程式是個簡單的示範：

```
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    printf("型態\t\t大小（bytes）\n");
    printf("short\t\t%lu\n", sizeof(short));
    printf("int\t\t%lu\n", sizeof(int));
    printf("long\t\t%lu\n", sizeof(long));
    printf("float\t\t%lu\n", sizeof(float));
    printf("double\t\t%lu\n", sizeof(double));
    printf("long double\t%lu\n", sizeof(long double));
    printf("char\t\t%lu\n", sizeof(char));

    return 0;
}
```

其中 '\t' 是跳格字元，它相當於在主控台中按下 Tab 鍵的效果，可以用來對齊下一個顯示位置，%lu 為格式指定碼，表示該位置將放置一個 long unsigned 型態的整數，也就是由 sizeof() 所計算出來的數字取代，在 主控台輸出輸入（Input/Output） 中，將針對格式控制作進一步說明。

以下是執行結果：

```
型態      大小（bytes）
short       2
int         4
long        8
float       4
double      8
long double 16
char        1
```

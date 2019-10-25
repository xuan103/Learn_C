可以在程式中寫下 1、1.0、3.14159 這樣的數值，這類數值稱之為字面常量（Literal constant），程式中若寫下一個整數值，例如 1 這個數值的話，預設是個 int 型態，若在程式中寫下 1.0，3.14 等，預設會是 double 型態的數值，例如下面這個程式顯示出來的分別是 int與 double 的大小：

```
#include <stdio.h>

int main(void) {
    printf("sizeof(1):\t %lu\n", sizeof(1));
    printf("sizeof(1.0):\t %lu\n", sizeof(1.0));

    return 0;
}
```
執行結果：
```
sizeof(1):      4
sizeof(1.0):    8
```
整數字面常量可以用 8 進位、10 進位與 16 進位表示，一般習慣使用 10 進位，如果要使用 8 進位的字面常量，開頭加上 0 就可以了，如果要使用 16 進位的字面常量，開頭加上 0x。

例如下面的程式各顯示 10 進位制 26 的 8 進位與 16 進位寫法：
```
#include <stdio.h>

int main(void) {
    printf("%d\n", 26);
    printf("%d\n", 032);
    printf("%d\n", 0x1A);

    return 0;
}
```
由於 printf 指定格式控制字元 %d 輸出整數時，都會以 10 進位制顯示，所以上面的程式中三行陳述都會顯示 26。

可以在整數值之後加上 L 或 l，表示該整數值要是 long 型態，因為 l 容易與數字 1 搞混，因此常使用 L，例如 1L，也可以指定為無號整數，可使用 U 或 u 來指定，例如 1U，L 與 U 可以同時指定，例如 1UL 或 1LU。

對於浮點數的話，則可以在寫下浮點數值時以 F 或 f 表示數值要使用 float 型態，例如 3.14f，也可以使用科學記號，例如 20000 可以表示為 2e4。

字元字面常量是以單引號來包括一個字元，例如 'A'、'1' 都表示一個字元字面常量，而有一些字元與C中所使用的相同，例如 “、'、\ 等，要在程式中 表現這些字元則要使用轉義序列（escape sequence），即 \"、\'、\\，其它還有一些不可見字元，也要以轉義序列來表示，下表列出常用的轉義序列：
```
轉義序列	說明
\n	換行、新行（newline）
\t	水平定位點（horizontal tab）
\v	垂直定位點（vertical tab）
\b	退回一格（backspace）
\r	返回（carriage return）
\f	換頁（formfeed）
\a	嗶聲（alert bell）
\\	倒斜線（backslash）
\'	單引號
\"	雙引號
\ddd	八進位 ASCII 碼
\xdd	十六進位 ASCII 碼
```
八進位 ASCII 碼如 '\062' 則是字元 '2'，十六進位 ASCII 碼如 "\x48" 為字元 'H'，一個輸出的例子如下所示，以十六進位 ASCII 碼顯示 "2 個HELLO"：
```
#include <stdio.h>

int main(void) {
    char c = '\'';
    printf("單引號字元 %c \n", c);
    printf(" \" \062 個 \x48\x45\x4c\x4c\x4f\x21 \" \n");

    return 0;
}
```
char 宣告一個字元 變數，而在 printf() 中要顯示該變數時，使用格式指定碼（format specifier）%c來指定，執行結果如下：

單引號字元 '
 " 2 個 HELLO! "
更多的格式指定碼之使用，將在 printf() 與 scanf() 中介紹。

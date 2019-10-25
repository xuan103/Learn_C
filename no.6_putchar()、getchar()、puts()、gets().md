
如果只想取得使用者輸入的字元，則可以使用 getchar()，它直接取得使用者輸入的字元並傳回，如果只想要輸出一個字元，則也可以直接使用 putchar()，以下是個簡單的示範：

#include <stdio.h>

int main(void) {
    char c;

    printf("請輸入一個字元：");
    c = getchar();

    putchar(c);
    putchar('\n');

    return 0;
}
執行結果：

請輸入一個字元：A
A
如果輸入了兩個以上的字元，則 getchar() 會取得第一個字元，並將第二個字元留在緩衝區中，直到再使用 getchar() 或 scanf() 取得輸入。

如果想要取得使用者輸入的整個字串，有一段日子是使用 gets()，它會取得使用者的輸入字串，不包括按下 Enter 的換行字元碼，而想要輸出整個字串，也可以直接使用 puts()，它在輸出字串後，會直接進行換行，例如：

#include <stdio.h>

int main(void) {
    char str[20];

    puts("請輸入字串：");
    gets(str);

    puts("輸入的字串為：");
    puts(str);

    return 0;
}
不過，如果你使用較新的編譯器，就會發現有警訊：

警告： the `gets' function is dangerous and should not be used.
這是因為 gets() 函式無法知道字元陣列的大小，而是依賴換行符號或 EOF 才會結束輸入，因此有可能引發緩衝區溢位的安全問題，有興趣可以參考〈Why is the gets function so dangerous that it should not be used?〉。

從 C11 之後，gets() 已經不再是標準函式之一，你可以使用 fget() 來取代 get()，使用時必須指定字元陣列、大小以及 stdin：

#include <stdio.h>

int main(void) {
    char str[20];

    puts("請輸入字串：");
    fgets(str, sizeof(str), stdin);

    puts("輸入的字串為：");
    puts(str);

    return 0;
}
char str[20] 這行宣告一個可以容納 20 個字元的字元陣列，這是 C 語言中儲存字串的方式，之後還會介紹陣列與C語言的字串。

執行結果：

請輸入字串：
This is a test!
輸入的字串為：
This is a test!

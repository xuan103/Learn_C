字面常量 儲存於記憶體之中，並與一個資料型態相關聯，若要將一個數值儲存在記憶體中，並在稍後再取回這個數值來使用，該如何進行？顯然地，你無法取得方才寫下的字面常數，因為沒有任何關於字面常數儲存位置的資訊。

變數（Variable）提供具名稱的記憶體儲存空間，一個變數關聯一個資料型態、儲存的值與儲存空間的位址值。

變數資料型態決定了變數分配到的記憶體大小；變數儲存的值是指儲存於記憶體中的某個數值，你可以透過變數名稱取得這個數值，這個數值又稱為 rvalue 或 read value；而儲存空間的位址值則是指變數分配到的記憶體位置，變數本身又稱為 lvalue 或 location value。

在 C 中要使用變數，必須先宣告變數名稱與 資料型態，例如：
```
int intNum;      // 宣告一個整數變數
double dblNum;   // 宣告一個倍精度浮點數變數
```
如上面所舉的例子，可使用 int、float、double、char、bool 等關鍵字（Keyword）來宣告變數名稱並指定資料型態，變數在命名時有些規則，不可以使用數字作為開頭，也不可以使用特殊字元，像是 *&^% 之類的字元，而變數名稱不可以與 C 內定的關鍵字同名，例如 int、float、struct 等。

變數的命名有幾個風格，主要以清楚易懂為主，初學者為了方便，當使用一些簡單的字母來作為變數名稱，這會造成日後程式維護的困難，命名變數時發生同名的情況也會增加。

上面範例示範的是匈牙利命名法，也就是在變數名稱前加上變數的資料型態名稱縮寫，例如 intNum 用來表示這個變數是 int 整數資料型態，fltNum 表示一個 float 資料型態，這種方式在需要留意資料型態的場合，可作為提示之用，而在其他場合，這種命名方式已經不被鼓勵。

現在比較鼓勵用清楚的名稱或助憶文字來表明變數作用，通常會以小寫字母作為開始，並在每個單字開始時第一個字母使用大寫，例如：
```
int ageOfStudent;
int ageOfTeacher;```
像這樣的名稱可以讓人一眼就看出這個變數的作用，還可以考慮用底線來區隔變數中的每個字面，例如：
```
int age_of_student;
int age_of_teacher;```
在 C 中宣告一個變數，就會配置一塊記憶體空間給變數，空間長度依宣告時的資料型態而定，被配置的這塊空間中原先可能就有資料，也因此變數在宣告後的值是不可預期的，所以應該在在變數宣告後初始其值，可以使用指定運算子（Assignment operator）= 來指定變數的值，例如：
```
int ageOfStudent = 0;
double scoreOfStudent = 0.0;
char levelOfStudent = 'A';```
這邊也看到如何指定字元給字元變數，字元在指定時需使用引數 '' 來包括，在宣告變數之後，可以直接使用變數名稱來取得儲存的值，下面這個程式是個簡單的示範：
```
#include <stdio.h>

int main(void) {
    // 宣告變數但未初始值
    int ageOfStudent;
    double scoreOfStudent;
    char levelOfStudent;
    printf("\n年級\t得分\t等級\n");
    printf("%d\t%f\t%d\n", ageOfStudent, scoreOfStudent, levelOfStudent);

    ageOfStudent = 5;
    scoreOfStudent = 80.0;
    levelOfStudent = 'B';
    printf("\n年級\t得分\t等級\n");
    printf("%d\t%.2f\t%c\n", ageOfStudent, scoreOfStudent, levelOfStudent);

    return 0;
}```
在這個程式中首先宣告變數，但並沒有初始其值，所以第一次顯示時會出現不可預期的資料，而在指定變數的值之後，顯示變數值時就會出現指定的資料了，執行結果如下所示：
```
年級      得分          等級
32767   0.000000    63

年級      得分          等級
5       80.00        B```
在 printf() 中，針對浮點數的部份，使用格式指定字 %f，其中再加上 .2，表示顯示浮點數時只顯示至小數後第二位，更多的格式指定碼之使用，將在 printf() 與 scanf() 中介紹。

也可以在使用宣告變數後，使用指定運算子將變數的值初始為 0：
```
int ageForStudent = 5;
double scoreForStudent = 80.0;
char levelForStudent = 'B';```
有時候一但將數值指定給變數之後，就不允許再重新指定給同一變數，這時可以在宣告變數時使用 const 關鍵字來限定，若程式中有其它程式碼試圖重新設定變數，編譯器會先檢查出這個錯誤，例如：
```
const double PI = 3.14; 
PI = 3.14159;```
這一段程式碼中的 maxNum 變數使用了 const 來限定，所以在指定為 10 之後，就不可以再指定值給它，所以第二次指定會被編譯器指出錯誤，在 gcc 編譯器下，會出現這樣的錯誤訊息：
```
assignment of read-only variable `PI'```
使用 const 來限定變數，通常就是不希望其它的程式碼來變動它的值，例如用於迴圈計數次數的指定（迴圈之後就會學到），或是像圓周率PI的指定。

如果要宣告無號的整數變數，則可以加上unsigned關鍵字，例如：
```
unsigned int i;```

# PHP學習筆記

## PHP的資料型態
- Bollean布林值

    算是最簡單的資料型態，可以為true跟false不區分大小寫。
    ```php
    <?php 
    $foo = true; // 設置foo變數為true 
    ?>
    ```
    常用在判斷式
    ```php
    <?php
    // 兩個等於代表操作符，檢測兩個遍量是否相等，返回布林值
    if ($password == '123'){
        echo 'pass';
    }
    
    // 這樣寫是不必要的
    if ($check == true){
        echo 'check in';
    }
    
    // 可以使用以下方式
    if ($check){
        echo 'check in';
    }
    ?>
    ```
- Integer整數型態

    整型值 int 可以使用十进制，十六进制，八进制或二进制表示，前面可以加上可選的符號（- 或者 +）。 可以用負運算符 来表示一个負的int。
    ```php
    <?php
    $a = 10; // 十進位
    $a = 012; // 八進位 (等於十進位 10)
    $a = 0xa; // 十六進位 (等于十進制 10)
    $a = 0b1010; // 二進制数字 (等于十進制 10)
    $a = 1_0_1_0_; // 整型数值 (PHP 7.4.0 以后)輸出1010
    ?>
    ```
    整數溢出，如果超過int範圍會轉換成float型態。
    ```php
    <?php
    // var_dump()方法是判斷一個變量的類型與長度,並輸出變量的數值
    $large_number = 2147483647;
    var_dump($large_number); // int(2147483647)

    $large_number = 2147483648;
    var_dump($large_number); // float(2147483648)
    ?>
    ```
- Float符點數

    擁有小數點的正負數值，
    通常最大值是 1.8e308 並具有 14 位十進制數字的精度。
    ```php
    <?php
    $num = 99.01;
    $num = -50.30;
    ?>
    ```
- string字符串

    由字符組成，每個字符等同於一個字節。這意味著 PHP 只能支持 256 的字符集，因此不支持 Unicode 。
    
    >注意:在 32 位版本中，string 最大可以達到 2GB（最多 2147483647 字節）。
    
    定義一個字符串最簡單就是用''單引號刮起來。
    ```php
    <?php
    $text = 'This is test string';
    echo $text; // 輸出: This is test string
    ?>
    ```
    如果包含在雙引號內就可以對特殊字符進行解析。
    ```php
    <?php
    // 可以直接將變數帶入
    $food = 'noodles';
    echo "Hi \n"; // 換行
    echo "I like to eat $food";
    ?>
    ```
- Array數組

    PHP中的array 實際上是一個有序映射。映射是一種把 values 關聯到 keys 的類型。
    
    可以用 array() 方法來結構一個 array 。接受任意數量用逗號分隔的 鍵（key） => 值（value） 。以下範例:
    ```php
    <?php
    $arry = array( 0 => 'apple', 
                   1 => 'tomato',
                   2 => 'banana',);
    echo $arry[0]; // apple
    
    // 可以使用以下短數組語法
    $arry = [ 0 => 'apple', 
              1 => 'tomato',
              2 => 'banana',];
    echo $arry[0]; // apple
    ?>
    ```
    沒有鍵名的索引數組
    ```php
    <?php
    $array = array("apple", "tomato", "banana", );
    var_dump($array);
    
    // 輸出
    array(4) {
      [0]=>
      string(5) "apple"
      [1]=>
      string(6) "tomato"
      [2]=>
      string(6) "banana"
    }   
    ?>
    ```
    數組可以用在許多地方，以下有些範例
    ```php
    <?php
    $map = array( 'version' => 4,
                  'OS' => 'Linux',
                  'lang' => 'english',
                  'short_tags' => true
            );
    
    // . . .完全等同於:
    $a = array();
    $a['version'] = 4;
    $a['os'] = 'Linux';
    $a['lang'] = 'english';
    $a['short_tags']  = true;
    
    unset($a['os']); // 刪除 "Linux"
    ?>
    ```
    輸出集合
    ```php
    <?php
    $maps = array( 'version' => 4,
                  'OS' => 'Linux',
                  'lang' => 'english',
                  'short_tags' => true
            );

    foreach ($maps as $key => $value) {
        echo "$key is $value\n";
    }
    // version is 4
    // OS is Linux
    // lang is english
    // short_tags is 1
    ?>
    ```
    Array 是有序的。也可以使用不同的排序函数来改變順序。
    
    數組排序範例
    ```php
    <?php
    sort($files); // 對value排序
    print_r($files);
    ?>
    ```
- Iterable可迭代對象

  它接受任何 array 或實現了 Traversable(可遍歷) 接口的對象。
  這些類型都能用 foreach 迭代， 也可以和 生成器 里的 yield from 一起使用。
  ```php
  <?php
    function gen(): iterable { // 建立一個可迭代生成器
        yield 1;
        yield 2;
        yield 3;
    }
    $iterable = gen(); // 實例化
    foreach($iterable as $value){
        echo "$value\n";
    }
    // 輸出
    // 1
    // 2
    // 3
    
    // 答案相同
    function gen(): iterable {
	    return [1, 2, 3];
    }
    $iterable = gen();
    foreach($iterable as $value){
        echo "$value\n";
    }
  ?>
  ```
- Object 對象
    要創建一个新的對象 object，使用 new 語句實例化一个類：
    ```php
    <?php
    class SayHi
    {
        function do_sayhi()
        {
            echo "Hello."; 
        }
    }

    $bar = new foo;
    $bar->do_sayhi(); // Hello
    ?>
    ```
    如果將Object轉換成Object將不會有任何變化，如果其它任何類型的值被轉換成對象，將會創建一个内置類 stdClass 的實例。如果该值为 null，則新的實例為空。
    array 轉換成 object 將使Key值成為屬性名並具有相對應的值，參考以下範例
    ```php
    <?php
    $obj = (object) array('1' => 'foo');
    var_dump(isset($obj->{'1'})); // PHP 7.2.0 後輸出 'bool(true)'，之前版本會輸出 'bool(false)' 
    var_dump(key($obj)); // PHP 7.2.0 後輸出 'string(1) "1"'，之前版本輸出  'int(1)' 
    ?>
    ```
    
    對於其他值，會包含進成員變量名 scalar。
    ```php
    <?php
    $obj = (object) 'hello';
    echo $obj->scalar;  // outputs 'hello'
    ?>
    ```
    
- Null類型

    特殊的 null 值表示一个變數没有值。NULL 類型唯一可能的值就是 null。

    在下列情况下一个變數被认为是 null：

    - 被賦值为 null。

    - 尚未被賦值。

    - 被 unset()。

    null 類型只有一个值，就是不區分大小寫的常量 null。
    ```php
    <?php
    $var = NULL;       
    ?>
    ```

## PHP變數命名規則

PHP 中的變數用一个美元符號後面跟變數名稱来表示。變數名是區分大小寫的。

變數名與 PHP 中其它的標籤一样遵循相同的規則。一个有效的變量名由字母或者底線開頭，後面加上任意数量的字母，数字，或者底線。 按照正常的正規表示法，他將被表達為：'\^[a-zA-Z_\x80-\xff][a-zA-Z0-9_\x80-\xff]*$'。

> $this 是一個特殊變數，他不能被賦值。

```php=
<?php
$firstName = 'Wang';
$lastName = 'Joe';
echo "$firstName, $lastName";      // 输出 "Wang, Joe"

$4site = 'not yet';     // 非法變數名；以數字開頭
$_4site = 'not yet';    // 合法變數名；以底線開頭
$i站點is = 'TW';  // 合法變數名；可以用中文
?>
```

## PHP常量

可以使用 const 關鍵字或 define() 函數兩種方法來定義一個常量。函數 define() 允許將常量定義為一個表達式，而 const 關鍵字有一些限制。一個常量一旦被定義，就不能再改變或者取消定義。

使用 const 關鍵字定義常量時，只能包含標量數據（bool、int、float 、string）。可以將常量定義為一個表達式，也可以定義為一個 array。還可以定義 resource 為常量，但應盡量避免，因為可能會造成不可預料的結果。

可以簡單的通過指定其名字來取得常量的值，與變量不同，不應該在常量前面加上 $ 符號。如果常量名是動態的，也可以用函數 constant() 來獲取常量的值。用 get_defined_constants() 可以獲得所有已定義的常量列表。

以下為定義常量範例
```php=
<?php
define("CONSTANT", "Hello world.");
echo CONSTANT; // 輸出 "Hello world."
echo Constant; // 拋出錯誤：未定義的常量 "Constant"
               // 在 PHP 8.0.0 之前，输出 "Constant" 會併發出一個提示級別錯誤訊息
?>
```

以下範例為使用關鍵字 const 定義常量
```php=
<?php
// 簡單的標量值
const CONSTANT = 'Hello World';

echo CONSTANT;

// 標量表達式
const ANOTHER_CONST = CONSTANT.'; Goodbye World';
echo ANOTHER_CONST;

const ANIMALS = array('dog', 'cat', 'bird');
echo ANIMALS[1]; // 將輸出 "cat"

// 常量數組
define('ANIMALS', array(
    'dog',
    'cat',
    'bird'
));
echo ANIMALS[1]; // 將輸出 "cat"
?>
```

魔術常量

| 名字             | 說明                                                                                                                                         |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| __LINE__         | 文件中的當前行號                                                                                                                             |
| __FILE__         | 文件的完整路徑和文件名。如果用在被包含文件中，則返回被包含的文件名。                                                                         |
| __DIR__          | 文件所在的目錄。如果用在被包括文件中，則返回被包括的文件所在的目錄。它等價於 dirname(__FILE__)。除非是根目錄，否則目錄中名不包括末尾的斜杠。 |
| __FUNCTION__     | 當前函數的名稱。匿名函數則為 {closure}。                                                                                                     |
| __CLASS__        | 當前類的名稱。類名包括其被聲明的作用域（例如 Foo\Bar）。當用在 trait 方法中時，__CLASS__ 是調用 trait 方法的類的名字                         |
| __TRAIT__        | Trait 的名字。 Trait 名包括其被聲明的作用域（例如 Foo\Bar）。                                                                                |
| __METHOD__       | class的方法名                                                                                                                                |
| __NAMESPACE__    | 當前命名空間名稱                                                                                                                             |
| ClassName::class | 完整的class名稱                                                                                                                              |

## PHP運算符

- 算數運算符

    跟國中小數學基本數學知識相同。
    ```php=
    <?php
    $a = 1;
    $b = 2;
    echo $a + 1 * $b; // output: 3
    ?>
    ```
    
    以下圖表為算術運算符

    | 例子     | 名称 | 结果                                |
    | -------- | ---- | ----------------------------------- |
    | +$a      | 標識 | 根據情况將 $a 轉化為 int 或 float。 |
    | -$a      | 取反 | $a 的負值。                         |
    | $a + $b  | 加法 | $a 和 $b 的和。                     |
    | $a - $b  | 减法 | $a 和 $b 的差。                     |
    | $a * $b  | 乘法 | $a 和 $b 的積。                     |
    | $a / $b  | 除法 | $a 除以 $b 的商。                   |
    | $a % $b  | 取模 | $a 除以 $b 的餘數。                 |
    | $a ** $b | 求幂 | $a 的 $b次方的值。                  |

- 賦值運算符

    基本的賦值運算符是“=”。一開始可能會以為它是“等於”，其實不是的。它實際上意味著把右邊表達式的值賦給左邊的運算數
    
    下圖為算術賦值運算符

    | 例子      | 等同於        | 操作   |
    | --------- | ------------- | ------ |
    | $a += $b  | $a = $a + $b  | 加法   |
    | $a -= $b  | $a = $a - $b  | 减法   |
    | $a *= $b  | $a = $a * $b  | 乘法   |
    | $a /= $b  | $a = $a / $b  | 除法   |
    | $a %= $b  | $a = $a % $b  | 取餘數 |
    | $a **= $b | $a = $a ** $b | 指數   |

    下圖為其他賦值運算符

    | 例子     | 等同於        | 操作       |
    | -------- | ------------- | ---------- |
    | $a .= $b | $a = $a . $b  | 字符串拼接 |
    | $a ?? $b | $a = $a ?? $b | NULL合併   |

- 位元運算

    位運算符允許對整型數中指定的位進行求值和操作。
    
    下圖為位元運算符號
    | 例子     | 名稱                | 结果                                                     |
    | -------- | ------------------- | -------------------------------------------------------- |
    | $a & $b  | And（按位與）       | 將把 $a 和 $b 中都為 1 的位設為 1。                      |
    | $a \| $b | Or（按位或）        | 將把 $a 和 $b 中任何一個為 1 的位設為 1。                |
    | $a ^ $b  | Xor（按位異或）     | 將把 $a 和 $b 中一個為 1 另一個為 0 的位設為 1。         |
    | ~ $a     | Not（按位取反）     | 將 $a 中為 0 的位設為 1，反之亦然。                      |
    | $a << $b | Shift left（左移）  | 将 $a 中的位向左移動 $b 次（每一次移動都表示“乘以 2”）。 |
    | $a >> $b | Shift right（右移） | 将 $a 中的位向右移動 $b 次（每一次移動都表示“除以 2”）。 |

- 比較運算符

    比較運算符，如同它們名稱所暗示的，允許對兩個值進行比較。
    
    | 例子      | 名稱                       | 結果                                                               |
    | --------- | -------------------------- | ------------------------------------------------------------------ |
    | $a == $b  | 等於                       | true，如果類型轉換後 $a 等於 $b。                                  |
    | $a === $b | 全等於                       | true，如果 $a 等於 $b，並且它們的類型也相同。                      |
    | $a != $b  | 不等於                       | true，如果類型轉換後 $a 不等於 $b。                                |
    | $a <> $b  | 不等於                       | true，如果類型轉換後 $a 不等於 $b。                                |
    | $a !== $b | 不全等                     | true，如果 $a 不等於 $b，或者它們的類型不同。                      |
    | $a < $b   | 小於                       | true，如果 $a 嚴格小於 $b。                                        |
    | $a > $b   | 大於                       | true，如果 $a 嚴格大於 $b。                                        |
    | $a <= $b  | 小於等於                   | true，如果 $a 小於或者等於 $b。                                    |
    | $a >= $b  | 大於等於                   | true，如果 $a 大於或者等於 $b。                                    |
    | $a <=> $b | 太空船運算符（組合比較符） | 當$a小於、等於、大於 $b時 分别返回一個小於、等於、大於0的 int 值。 |

- 執行運算符

    PHP 支持一個執行運算符：反引號（\`\`）。注意這不是單引號！ PHP 將嘗試將反引號中的內容作為 shell 命令來執行，並將其輸出信息返回（即，可以賦給一個變量而不是簡單地丟棄到標準輸出）。使用反引號運算符“\`”的效果與函數 shell_exec() 相同。
    
    ```php
    <?php
    $output = `ipconfig /all`;
    echo "<pre>$output</pre>"; // 輸出所有IP資訊
    ?>
    ```
    
- 遞增/遞減運算符
    > 注意: 遞增／遞減運算符不影響布爾值。遞減 null 值也沒有效果，但是遞增 null 的結果是 1。

    | 例子 | 名称 |            效果             |
    | ---- | ---- | --------------------------|
    | ++$a | 先加 | $a 的值加一，然後返回 $a。    |
    | $a++ | 後加 | 返回 $a，然後將 $a 的值加一。 |
    | --$a | 先减 | $a 的值减一， 然后返回 $a。   |
    | $a-- | 後减 | 返回 $a，然後將 $a 的值减一。 |
    
    簡易的範例
    ```php
    <?php
    echo "後增量(PostIncrement)\n";
    $a = 5;
    echo "Should be 5: " . $a++ . "<br />\n";
    echo "Should be 6: " . $a . "<br />\n";

    echo "先增量(PreIncrement)\n";
    $a = 5;
    echo "Should be 6: " . ++$a . "<br />\n";
    echo "Should be 6: " . $a . "<br />\n";

    echo "後減(PostDecrement)\n";
    $a = 5;
    echo "Should be 5: " . $a-- . "<br />\n";
    echo "Should be 4: " . $a . "<br />\n";

    echo "先減(Predecrement)\n";
    $a = 5;
    echo "Should be 4: " . --$a . "<br />\n";
    echo "Should be 4: " . $a . "<br />\n";
    ?>
    ```
    
- 邏輯運算符

    | 例子      | 名稱            | 结果   |                    
    | --------- | --------------- |----|
    | $a and $b | And（和）   | true，如果 $a 和 $b 都為 true。|                 
    | $a or $b  | Or（或）    | true，如果 $a 或 $b 任一為 true。| 
    | $a xor $b | Xor（異或） | true，如果 $a 或 $b 任一為 true，但不同時是。|     
    | ! $a      | Not（非）   | true，如果 $a 不為 true。 | 
    | $a && $b  | And（與）   | true，如果 $a 和 $b 都為 true。| 
    | $a \|\| $b  | Or（或）    | true，如果 $a 或 $b 任一為 true。 |
    
- 字符串運算符

    有兩個字符串（string）運算符。第一個是連接運算符（“.”），它返回其左右參數連接後的字符串。第二個是連接賦值運算符（“.=”），它將右邊參數附加到左邊的參數之後。
    
    範例程式碼
    ```php
    <?php
    $a = "Hello ";
    $b = $a . "World!";
    echo $b."\n"; // output "Hello World!"

    $a = "Hello ";
    $a .= "World!";     // output "Hello World!"
    echo $a;
    ?>
    ```
- 數組運算符
    
    |例子      |	名稱  |	结果         |
    |------   |-------|----------------|
    |$a + $b  |	聯合   |	$a 和 $b 的联合。|
    |$a == $b |	相等   |	如果 $a 和 $b 具有相同的键／值，則為 true。|
    |$a === $b|	全等   |	如果 $a 和 $b 具有相同的键／值，並且順序和類型都相同則為 true。|
    |$a != $b |	不等於   |	如果 $a 不等於 $b 則為 true。|
    |$a <> $b |	不等於   |	如果 $a 不等於 $b 則為 true。|
    |$a !== $b|	不相等|	如果 $a 不全等於 $b 則為 true。|
    
    如果是運用運算符將數組相加，會把加號右邊的附加到加號左邊數組，
    兩個數組中都有的鍵名，則只用左邊數組中的，右邊的被忽略
    
    以下簡單範例示範:
    ```php
    <?php
    $a = array("a" => "apple", "b" => "banana");
    $b = array("a" => "pear", "b" => "strawberry", "c" => "cherry");

    $c = $a + $b; // Union of $a and $b
    var_dump($c);

    $c = $b + $a; // Union of $b and $a
    var_dump($c);
    
    // 輸出:
    // array(3) {
    //   ["a"]=>
    //   string(5) "apple"
    //   ["b"]=>
    //   string(6) "banana"
    //   ["c"]=>
    //   string(6) "cherry"
    // }

    // array(3) {
    //   ["a"]=>
    //   string(4) "pear"
    //   ["b"]=>
    //   string(10) "strawberry"
    //   ["c"]=>
    //   string(6) "cherry"
    // }
    ?>
    ```
    
    以下示範比較數組
    ```php
    <?php
    $a = array("apple", "banana");
    $b = array(1 => "banana", "0" => "apple");

    var_dump($a == $b); // bool(true)
    var_dump($a === $b); // bool(false)
    ?>
    ```
    
- 類型運算符
    
    instanceof 方法用於確定一個 PHP 變數是否屬於某一類 class 的實例，
    也可以用來確認某一個變數，是否繼承自某一父類或子類的實例。
    
    以下範例
    ```php
    <?php
    class MyClass
    {
    }

    class NotMyClass
    {
    }
    $a = new MyClass;

    var_dump($a instanceof MyClass);
    var_dump($a instanceof NotMyClass);
    ?>
    
    // 輸出
    // bool(True)
    // bool(False)
    ```
    
## PHP流程控制

- If Else 判斷句
    If 可以使用在判斷某條件達成時執行語句，else則是在不滿該條下執行。
    
    以下使用範例示範
    ```php
    <?php
    if ($a > $b){
    console.log("a win");
    }else {
    console.log("b win");
    }
    ?>
    ```
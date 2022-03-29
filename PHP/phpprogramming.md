# BAISC STATEMENT

> **object and array**
> 
> ```php
> $a = [1, 2];
> $b = (object)$a;
> $c = (array)$b;
> ```

> **xor**
> 
> one is true and another is false, then true. both are true or false return false.

> **`` signal can run the command**

> **对于语句块，花括号可以用冒号来转换**
> 
> ```php
> if():
>     statement
> else:
>     statment
> endif;
> 
> switch():
> case 'x':
> break;
> default:
> break;
> endswitch;
> 
> while(): endwhile;
> for(): endfor;
> foreach(): endforeach;
> ```

> **break 2 or continue 2** 跳出整个循环

> **declare()** 有三个参数
> 
> * ticks
>   
>   * 配合register_tick_function() 
>     
>     * ```php
>       register_tick_function("somefunction");
>       declare(ticks = 3) {
>           for ($i = 0; $i < 10; $i++) {
>               // so somthing 每执行到第三次就执行一次function
>           }
>       }
>       ```
> 
> * encoding 进行输出编码格式的配置
> 
> * strict_types

> **goto** 跳转到指定代码块
> 
> ```php
> goto cleanup:
> 
> cleanup:
>     statement
> ```

> **echo**直接输出变量
> 
> ```php
> <?= $a; ?> = <?php echo $a; ?>
> ```

> function里的可变参数，配合三个方法获取
> 
> ```php
> $array = func_get_args();
> $count = func_num_args();
> $value = func_get_arg(argument_number);
> ```

> 引用函数 **&function()**

> *变量变量* 和*变量函数*  $$var $var() 配合**function_exists()**

> 匿名函数 用use可调用自定义变量
> 
> `usort($array, function($a, $b) use ($sortopt))`

> **string offset syntax** $string{$i}

> **url协议** `urlrawencode()` `urlrawdecode()`

> **转义** `addslashes()`  `stripslashes()`常用在数据库query语句，*单引号 双引号 null 反斜杠* 
> 
> `addclashes()` `stripcslashes()` 常用在文本\n \t的转义

# STRING

> `substr_count()` 较小字符串在较大字符串中出现的次数

> `substr_replace(original, new, start [, length ])` 
> 
> 基础的替换，长度为0为插入，替换为空为删除， 00开头插入，负数从后替换

> `str_pad()`填充
> 
> ```php
> $padded = str_pad(to_pad, length [, with [, pad_type ]]);
> ```
> 
> 第四个参数 STR_PAD_RIGHT（默认值）STR_PAD_LEFT、 或STR_PAD_BOTH（居中）

> `strtok()`遍历一个字符串 初始化**strtok(string, sep)**  next = **strtok(sep)**
> 
> ```php
> $string = "Fred,Flintstone,35,Wilma";
> $token = strtok($string, ",");
> 
> while ($token !== false) {
>  echo("{$token}<br />");
>  $token = strtok(",");
> }
> Fred
> Flintstone
> 35
> Wilma
> ```

> `sscanf()`解析 对应 `sprintf()`  如果没有第三个参数，则返回的数组
> 
> ```php
> $string = "Fred\tFlintstone (35)";
> $n = sscanf($string, "%s\t%s (%d)", $first, $last, $age);
> echo "Matched {$n} fields: {$first} {$last} is {$age} years old";
> Matched 3 fields: Fred Flintstone is 35 years old
> ```

> `strpos()`最先匹配到的 `strrpos()`最后匹配到的
> 
> `strstr()`返回的是字符串  `strrstr()`返回的是最后匹配的字符串

> `parse_url()`url的解析

## 正则（preg）

> `preg_match()`
> 
> `preg_replace()`
> 
> `preg_split()`

# ARRAY

> `count()` `sizeof()`获取数组的元素数量

> `array_pad()`数组的填充 第二个参数是数组的长度（负数则从前填充），第三个参数是数组的填充物

> `list()`提取数组 常用于数据库读取单条数据
> 
> ```php
> $person = array("Fred", 35, "Betty");
> list($name, $age) = $person; // $name is "Fred", $age is 35
> $values = array("hello", "world");
> list($a, $b, $c) = $values; // $a is "hello", $b is "world", $c is NULL
> $values = range('a', 'e'); // use range to populate the array
> list($m, , $n, , $o) = $values; // $m is "a", $n is "c", $o is "e"
> ```

> `array_slice()` 切割有序数组
> 
> ```php
> $people = array("Tom", "Dick", "Harriet", "Brenda", "Jo");
> $middle = array_slice($people, 2, 2); // $middle is array("Harriet", "Brenda")
> ```

> `array_chunk()`平分数组为小的数组， 如果第三个参数是true，则保留原索引
> 
> ```php
> $nums = range(1, 7);
> $rows = array_chunk($nums, 3);
> print_r($rows);
> 
> Array (
>  [0] => Array (
>      [0] => 1
>      [1] => 2
>      [2] => 3
>  )
>  [1] => Array (
>      [0] => 4
>      [1] => 5
>      [2] => 6
>  )
>  [2] => Array (
>      [0] => 7
>  )
> )
> ```

> `array_key_exists(key, array)`判断是否有此key。和`isset()`的却别就是， **null**值对isset来说是false，但是array_key_exists识别**null**

> `array_splice(array, start [, length [, replacement ] ])` 删除和插入元素，且返回删除的数组
> 
> length为0的话就是纯插入

> `extract()`第二个参数可写可不写，有用的是**EXTR_PREFIX_ALL**，决定第三个参数作为前缀
> 
> ```php
> $shape = "round";
> $array = array('cover' => "bird", 'shape' => "rectangular");
> 
> extract($array, EXTR_PREFIX_ALL, "book");
> echo "Cover: {$book_cover}, Book Shape: {$book_shape}, Shape: {$shape}";
> ```

> `compact()` 将变量名变成参数传递个数组
> 
> ```php
> $color = "indigo";
> $shape = "curvy";
> $floppy = "none";
> 
> $a = compact("color", "shape", "floppy");
> // or
> $names = array("color", "shape", "floppy");
> $a = compact($names);
> ```

> **数组迭代器函数（Iterator）**
> 
> | 函数        | 说明                            |
> | --------- | ----------------------------- |
> | current() | 返回当前迭代器指向的元素                  |
> | reset()   | 将迭代器移动到第一个元素并返回               |
> | next()    | 将迭代器移动到下一个元素并返回               |
> | prev()    | 将迭代器移动到上一个元素并返回               |
> | end()     | 将迭代器移动到最后一个元素并返回              |
> | each()    | 将当前元素的键和值最为数组返回，并将迭代器移动到下一个元素 |
> | key()     | 返回当前元素的键                      |
> 
> ```php
> reset($addresses);
> 
> while (list($key, $value) = each($addresses)) {
>  echo "{$key} is {$value}<br />\n";
> }
> ```

> `array_walk(array, callable)` 对数组元素进行函数调用。 自定义的函数可以接受函数第三个参数作为参数
> 
> ```php
> function printRow($value, $key, $color);
> array_walk($person, "printRow", "lightblue");  
> ```
> 
> 也可以传数组
> 
> ```php
> $extraData = array('border' => 2, 'color' => "red");
> $baseArray = array("Ford", "Chrysler", "Volkswagen", "Honda", "Toyota");
> array_walk($baseArray, "walkFunction", $extraData);
> ```
> 
> **这个函数没有返回值，没法改变数组的内容，除非在内部直接修改数组的值**
> 
> ```php
> $testArr = ['asdf', 'zxc', 'cvx', 'xcb'];
> function mergeArr($value, $key, $str) {
>     $value .= $str;
>     global $testArr;
>     $testArr[$key] = $value;
> };
> 
> array_walk($testArr, "mergeArr", '111');
> 
> print_r($testArr);
> ```

> `array_reduce(array, callable[, default])` 函数需要调用的function有**返回值**，调用的函数有两个参数，running total和current value。
> 
> ```php
> $addItUp = function ($runningTotal, $currentValue)
> {
>  $runningTotal += $currentValue * $currentValue;
> 
>  return $runningTotal;
> };
> 
> $numbers = array(2, 3, 5, 7);
> $total = array_reduce($numbers, $addItUp);
> 
> echo $total;
> ```

> **Array Sort**
> 
> | effect     | 升降        | 降序         | 自定义排序      |
> | ---------- | --------- | ---------- | ---------- |
> | 值排序，并给新的索引 | `sort()`  | `rsort()`  | `usort()`  |
> | 值排序        | `asort()` | `arsort()` | `uasort()` |
> | 键排序        | `ksort()` | `krsort()` | `uksort()` |
> 
> User-defined ordering requires that you provide a function that takes two values and returns a value that specifies the order of the two values in the sorted array. The function should return `1` if the first value is greater than the second, `−1` if the first value is less than the second, and `0` if the values are the same for the purposes of your custom sort order.

> **Natural Sort** 对包含字符串和数字的字符串进行排序，用于文件名的排序
> 
> `natsort()`  and `natcasesort()` 后者不区分大小写

> `array_multisort(array1 [, array2, ...])` 一次对多个数组进行排序（由`SORT_ASC`或`SORT_DESC`常量标识）
> 
> ```php
> array_multisort($ages, SORT_ASC, $zips, SORT_DESC, $names, SORT_ASC);
> ```

> `array_reverse(array)` 反转数组
> 
> `array_flip(array)` 反转键值对

> **随机数组的顺序** `shuffle()`
> 
> ```php
> $weekdays = array("Monday", "Tuesday", "Wednesday", "Thursday", "Friday");
> shuffle($weekdays);
> ```

> **常用的几个数组**
> 
> `array_sum()` 将值相加
> 
> `array_merge()` 合并数组 ***如果相同字符串键重复，则后面的值会替换前面的值*** 
> 
> `array_diff()` 返回一数组，包含第一个数组中其他数组没有的值
> 
> `array_filter()` 返回一数组，保留回调函数里返回true的元素
> 
> `array_map()` 返回一数组，值过一遍回调函数
> 
> `array_unique()` 删除重复的值
> 
> `array_search($value, array)`  返回key ，如果第三个参数为true，则用===比较

> **数组的并，交，差集**
> 
> **并集**
> 
> ```php
> $union = array_merge($a, $b); // duplicates may still exist
> $union = array_unique($union);
> ```
> 
> **交集**
> 
> `array_intersect()` 任意数量数组里相同的值

> **数组的堆栈**
> 
> `array_push()` 向数组尾插入值，返回数组的数量  `array_pop()` 删除数组尾部的值，返回数组的删除的值
> 
> `array_unshift()` 在数组头部插入值，返回数组的数量 `array_shift()`  删除数组头部的值，返回删除的值

> **Iterator Interface**
> 
> 必须实现五个方法
> 
> * current()
> * key()
> * next()
> * rewind()
> * valid()
> 
> ```php
> class BasicArray implements Iterator
> {
>  private $position = 0;
>  private $array = ["first", "second", "third"];
> 
>  public function __construct()
>  {
>  $this->position = 0;
>  }
> 
>  public function rewind()
>  {
>  $this->position = 0;
>  }
> 
>  public function current()
>  {
>  return $this->array[$this->position];
>  }
> 
>  public function key()
>  {
>  return $this->position;
>  }
> 
>  public function next()
>  {
>  $this->position += 1;
>  }
> 
>  public function valid()
>  {
>  return isset($this->array[$this->position]);
>  }
> }
> 
> $basicArray = new BasicArray;
> 
> foreach ($basicArray as $value) {
>  echo "{$value}\n";
> }
> 
> foreach ($basicArray as $key => $value) {
>  echo "{$key} => {$value}\n";
> }
> 
> first
> second
> third
> 
> 0 => first
> 1 => second
> 2 => third
> ```

# OBJECT

> **使用多个定义相同的traits会报错，可用`insteadof()`解决冲突**
> 
> ```php
> trait Command {
>  function run() {
>  echo "Executing a command\n";
>  }
> }
> 
> trait Marathon {
>  function run() {
>  echo "Running a marathon\n";
>  }
> }
> 
> class Person {
>  use Command, Marathon {
>  Marathon::run insteadof Command;
>  }
> }
> 
> $person = new Person;
> $person->run();
> Running a marathon
> ```

> **traits可用as进行别名**
> 
> ```php
> class Person {
>  use Command, Marathon {
>  Command::run as runCommand;
>  Marathon::run insteadof Command;
>  }
> }
> ```

## Introspection

> `class_exists()`  **确定类是否存在**
> 
> `get_declared_classes()` **返回定义的所有类**
> 
> ```php
> $doesClassExist = class_exists(classname);
> 
> $classes = get_declared_classes();
> $doesClassExist = in_array(classname, $classes);
> ```

> `get_class_methods()` **获取类的方法**
> 
> `get_class_vars()` **获取类的属性,只返回当前范围内可见的属性**
> 
> `get_parent_class()` **获取父类名字**
> 
> ```php
> $methods = get_class_methods(classname);
> $properties = get_class_vars(classname);
> ```

> **检查对象**
> 
> ```php
> $isObject = is_object(var);
> $classname = get_class(object);
> ```
> 
> `method_exists()` 检查对象方法是否存在
> 
> ```php
> $methodExists = method_exists(object, method);
> ```
> 
> `get_object_vars()` 返回设置的对象属性，可访问的属性
> 
> ```php
> $array = get_object_vars(object);
> ```

> 关于**RelectionClass()**获取对象的属性和方法
> 
> ```php
> #常用的方法
> $reflection = new ReflectionClass($Ojbect);
> $method = $reflection->getMethods();
> $parent = $reflection->getParentClass();
> $name = $reflection->getName();
> $check  = $reflection->isSubclassOf("class");
> $properties = $reflection->getProperties();
> ```

> **序列化Serialization** 
> 
> `__sleep()` 序列化调用之前   `__wakeup()` 序列化调用之后

# Dates and Times

> 原始的时间函数无法处理1901之前和2038后的日期，建议用**DateTime类进行处理**
> 
> `DateTime类`处理时间
> 
> `DateTimeZone类`处理时区
> 
> `DateInterval类`处理时间间隔
> 
> `DatePeriod类`处理时间区间

> **时间初始化**
> 
> ```php
> $dt = new DateTime("2019-06-27 16:42:33", new DateTimeZone("America/Halifax"));
> 
> $dtz = new DateTimeZone("America/Halifax");
> $dt = new DateTime("2019-06-27 16:42:33", $dtz);
> 
> $tz = ini_get('date.timezone');
> $dtz = new DateTimeZone($tz);
> $dt = new DateTime("2019-06-27 16:42:33", $dtz);
> ```
> 
> **时间的格式化**`format()`
> 
> ```php
> echo "date: " . $dt->format("Y-m-d h:i:s");
> date: 2019-06-27 04:42:33
> ```
> 
> **当前时间now**
> 
> ```php
> $tz = ini_get('date.timezone');
> $dtz = new DateTimeZone($tz);
> $dt = new DateTime("now", $dtz);
> 
> echo "date: " . $dt->format("Y-m-d h:i:s");
> date: 2019-06-27 04:02:54
> ```
> 
> **两时间只差** `diff()` ， 是DateInterval类的实例
> 
> ```php
> $tz = ini_get('date.timezone');
> $dtz = new DateTimeZone($tz);
> 
> $past = new DateTime("2019-02-12 16:42:33", $dtz);
> $current = new DateTime("now", $dtz);
> 
> // creates a new instance of DateInterval
> $diff = $past->diff($current);
> 
> $pastString = $past->format("Y-m-d");
> $currentString = $current->format("Y-m-d");
> $diffString = $diff->format("%yy %mm, %dd");
> 
> echo "Difference between {$pastString} and {$currentString} is {$diffString}";
> Difference between 2019-02-12 and 2019-06-27 is 0y 4m, 14d
> 
> ```
> 
> | 字符  | 效果                                    |
> | --- | ------------------------------------- |
> | `a` | 天数（例如，23）                             |
> | `d` | 未包含在月数中的天数                            |
> | `D` | 天数，如果少于 10 天，则包括前导零（例如，02 和 125）      |
> | `f` | 数字微秒（例如，6602 或 41569）                 |
> | `F` | 带前导零的数字微秒，长度至少为六位（例如，006602 或 041569） |
> | `h` | 小时数                                   |
> | `H` | 小时数，如果少于 10 小时，则包括前导零（例如，12 和 04）     |
> | `i` | 分钟数                                   |
> | `I` | 分钟数，如果少于 10 分钟，则包括前导零（例如，05 和 33）     |
> | `m` | 月数                                    |
> | `M` | 月数，如果少于 10 个月，则包括前导零（例如，05 和 1533）    |
> | `r` | `–`如果差值为负；如果差为正则为空                    |
> | `R` | `–`如果差值为负；`+`如果差异是正的                  |
> | `s` | 秒数                                    |
> | `S` | 秒数，如果小于 10 秒，则包括前导零（例如，05 和 15）       |
> | `y` | 年数                                    |

> **DateTimeZone类** 的`getLocation()`方法能够获取国家，经纬度。
> 
> ```php
> $tz = ini_get('date.timezone');
> $dtz = new DateTimeZone($tz);
> 
> echo "Server's Time Zone: {$tz}<br/>";
> 
> foreach ($dtz->getLocation() as $key => $value) {
>  echo "{$key} {$value}<br/>";
> }
> Server's Time Zone: America/Halifax
> country_code CA
> latitude 44.65
> longitude -63.6
> comments Atlantic - NS (most areas); PE
> ```

# Web Techniques

> **Six Global Arrays**
> 
> * $_ENV
> * $_GET
> * $_COOKIE
> * $_POST
> * $_SERVER
> * $_FILES

> **$_SERVER的常用的一些键值**
> 
> ```
> PHP_SELF
> ```
> 
> The name of the current script, relative to the document root (e.g., `/store/cart.php`). You have already seen this used in some of the sample code in earlier chapters. This variable is useful when creating self-referencing scripts, as we’ll see later.
> 
> ```
> SERVER_SOFTWARE
> ```
> 
> A string that identifies the server (e.g., `"Apache/1.3.33 (Unix) mod_perl/1.26 PHP/5.0.4"`).
> 
> ```
> SERVER_NAME
> ```
> 
> The hostname, DNS alias, or IP address for self-referencing URLs (e.g., `www.``example.com`).
> 
> ```
> GATEWAY_INTERFACE
> ```
> 
> The version of the CGI standard being followed (e.g., `CGI/1.1`).
> 
> ```
> SERVER_PROTOCOL
> ```
> 
> The name and revision of the request protocol (e.g., `HTTP/1.1`).
> 
> ```
> SERVER_PORT
> ```
> 
> The server port number to which the request was sent (e.g., `80`).
> 
> ```php
> REQUEST_METHOD
> ```
> 
> **The method the client used to fetch the document (e.g., `GET`).**
> 
> ```
> PATH_INFO
> ```
> 
> **Extra path elements given by the client (e.g., `/list/users`).**
> 
> ```
> PATH_TRANSLATED
> ```
> 
> **The value of `PATH_INFO`, translated by the server into a filename (e.g., `/home/httpd/htdocs/list/users`).**
> 
> ```
> SCRIPT_NAME
> ```
> 
> The URL path to the current page, which is useful for self-referencing scripts (e.g., `/~me/menu.php`).
> 
> ```
> QUERY_STRING
> ```
> 
> **Everything after the `?` in the URL (e.g., `name=Fred+age=35`).**
> 
> ```
> REMOTE_HOST
> ```
> 
> The hostname of the machine that requested this page (e.g., `http://dialup-192-168-0-1.example.com`). If there’s no DNS for the machine, this is blank and `REMOTE_ADDR` is the only information given.
> 
> ```
> REMOTE_ADDR
> ```
> 
> A string containing the IP address of the machine that requested this page (e.g., `"192.168.0.250"`).
> 
> ```
> AUTH_TYPE
> ```
> 
> The authentication method used to protect the page, if the page is password-protected (e.g., `basic`).
> 
> ```
> REMOTE_USER
> ```
> 
> The username with which the client authenticated, if the page is password-protected (e.g., `fred`). Note that there’s no way to find out what password was used.
> 
> ```
> HTTP_USER_AGENT
> ```
> 
> The string the browser used to identify itself (e.g., `"Mozilla/5.0 (Windows 2000; U) Opera 6.0 [en]"`).
> 
> ```
> HTTP_REFERER
> ```
> 
> The page the browser said it came from to get to the current page (e.g., `http://www.example.com/last_page.html`).

> **File Upload**
> 
> **$_FILES**的几个keys
> 
> * name
> * type
> * size
> * tmp_name
> 
> `is_uploaded_file(tmpfile)` 测试上传成功
> 
> `move_uploaded_file(tmpfile, path)` 移动上传的文件 

> **COOKIE**
> 
> ```php
> setcookie(name [, value [, expires [, path [, domain [, secure [, 
> httponly ]]]]]]);
> ```

> **SSL**
> 
> ```php
> if ($_SERVER['HTTPS'] !== 'on') {
>  die("Must be a secure connection.");
> }
> ```

# Databases

## SQLite

> | Data type | Explanation                                                                                                                                                  |
> |:--------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------ |
> | Text      | Stores data as `NULL`, `TEXT`, or `BLOB` content. If a number is supplied to a text field, it is converted to text before it is stored.                      |
> | Numeric   | Can store either integer or real data. If text data is supplied, SQLite attempts to convert the information to numerical format.                             |
> | Integer   | Behaves the same as the numeric data type. However, if data of the real type is supplied, it is stored as an integer. This may affect data storage accuracy. |
> | Real      | Behaves the same as the numeric data type, except that it forces integer values into floating-point representation.                                          |
> | None      | This is a catchall data type; it does not prefer one base type to another. Data is stored exactly as supplied.                                               |

> **例子**（how about sqlite3, or pdo）
> 
> ```php
> $db = new SQLiteDatabase("library.sqlite");
> 
> $sql = "CREATE TABLE 'books' ('bookid' INTEGER PRIMARY KEY,
>  'authorid' INTEGER,
>  'title' TEXT,
>  'ISBN' TEXT,
>  'pub_year' INTEGER,
>  'available' INTEGER,
> )";
> 
> if ($db->queryExec($sql, $error) == FALSE) {
>  echo "Create Failure - {$error}<br />";
> } else {
>  echo "Table Books was created<br />";
> }
> 
> $sql = <<<SQL
> INSERT INTO books ('authorid', 'title', 'ISBN', 'pub_year', 'available')
> VALUES (1, 'The Two Towers', '0-261-10236-2', 1954, 1);
> 
> INSERT INTO books ('authorid', 'title', 'ISBN', 'pub_year', 'available')
> VALUES (1, 'The Return of The King', '0-261-10237-0', 1955, 1);
> 
> INSERT INTO books ('authorid', 'title', 'ISBN', 'pub_year', 'available')
> VALUES (2, 'Roots', '0-440-17464-3', 1974, 1);
> 
> INSERT INTO books ('authorid', 'title', 'ISBN', 'pub_year', 'available')
> VALUES (4, 'I, Robot', '0-553-29438-5', 1950, 1);
> 
> INSERT INTO books ('authorid', 'title', 'ISBN', 'pub_year', 'available')
> VALUES (4, 'Foundation', '0-553-80371-9', 1951, 1);
> SQL;
> 
> if (!$db->queryExec($sql, $error)) {
>  echo "Insert Failure - {$error}<br />";
> } else {
>  echo "INSERT to Books - OK<br />";
> }
> ```
> 
> ```php
> $db = new SQLiteDatabase("c:/copy/library.sqlite");
> 
> $sql = "SELECT a.name, b.title FROM books b, authors a WHERE a.authorid=b.authorid";
> $result = $db->query($sql);
> 
> while ($row = $result->fetch()) {
>  echo "{$row['a.name']} is the author of: {$row['b.title']}<br/>";
> }
> ```

## File System

> | Function name   | Description of use                                                                             |
> |:--------------- |:---------------------------------------------------------------------------------------------- |
> | `mkdir()`       | Used to make a directory on the server.                                                        |
> | `file_exists()` | Used to determine if a file or directory exists at the supplied location.                      |
> | `fopen()`       | Used to open an existing file for reading or writing (see detailed options for correct usage). |
> | `fread()`       | Used to read in the contents of a file to a variable for PHP use.                              |
> | `flock()`       | Used to gain an exclusive lock on a file for writing.                                          |
> | `fwrite()`      | Used to write the contents of a variable to a file.                                            |
> | `filesize()`    | When reading in a file, this is used to determine how many bytes to read in at a time.         |
> | `fclose()`      | Used to close the file once its usefulness has passed.                                         |
> 
> **other useful function**
> 
> `fgets()` `fputs()` `pathinfo()` `unlink()` `basename()` `feof()`

## MongoDB

> ```php
> $mongo = new Mongo();
> $db = $mongo->library;
> $authors = $db->authors;
> 
> $author = array('authorid' => 1, 'name' => "J.R.R. Tolkien");
> $authors->insert($author);
> 
> $author = array('authorid' => 2, 'name' => "Alex Haley");
> $authors->insert($author);
> 
> $author = array('authorid' => 3, 'name' => "Tom Clancy");
> $authors->save($author);
> 
> $author = array('authorid' => 4, 'name' => "Isaac Asimov");
> $authors->save($author);
> 
> 
> 
> $mongo = new Mongo();
> $db = $mongo->library;
> $authors = $db->authors;
> 
> $data = $authors->findone(array('authorid' => 4));
> 
> echo "Generated Primary Key: {$data['_id']}<br />";
> echo "Author name: {$data['name']}";
> 
> 
> 
> ## 更新
> $mongo = new Mongo();
> $db = $mongo->library;
> $authors = $db->authors;
> 
> $authors->update(
>  array('name' => "Isaac Asimov"),
>  array('$set' =>
>  array('books' =>
>  array(
>  "0-425-17034-9" => "Foundation",
>  "0-261-10236-2" => "I, Robot",
>  "0-440-17464-3" => "Second Foundation",
>  "0-425-13354-0" => "Pebble In The Sky",
>  )
>  )
>  )
> );
> 
> 
> ## 更新
> $mongo = new Mongo();
> $db = $mongo->library;
> $authors = $db->authors;
> 
> $data = $authors->findone(array('name' => "Isaac Asimov"));
> 
> $bookData = array(
>  array(
>  "ISBN" => "0-553-29337-0",
>  "title" => "Foundation",
>  "pub_year" => 1951,
>  "available" => 1,
>  ),
>  array(
>  "ISBN" => "0-553-29438-5",
>  "title" => "I, Robot",
>  "pub_year" => 1950,
>  "available" => 1,
>  ),
>  array(
>  "ISBN" => "0-517-546671",
>  "title" => "Exploring the Earth and the Cosmos",
>  "pub_year" => 1982,
>  "available" => 1,
>  ),
>  array(
>  "ISBN' => "0-553-29336-2",
>  'title" => "Second Foundation",
>  "pub_year" => 1953,
>  "available" => 1,
>  ),
> );
> 
> $authors->update(
>  array("_id" => $data["_id"]),
>  array("$set" => array("books" => $bookData))
> );
> ```

# Security

## **html的转义**

> `htmlentities()` 
> 
> - ENT_COMPAT - Default. Encodes only double quotes
> - ENT_QUOTES - Encodes double and single quotes
> - ENT_NOQUOTES - Does not encode any quotes
> 
> ```php
> htmlentities($k, ENT_QUOTES, "UTF-8");
> ```

## **SQL注入**

> pdo数据绑定
> 
> `bool PDOStatement::bindParam ( mixed $parameter , mixed &$variable [, int $data_type = PDO::PARAM_STR [, int $length [, mixed $driver_options ]]] )`
> 
> ```php
> PDO::PARAM_BOOL (integer)
> Represents a boolean data type.
> PDO::PARAM_NULL (integer)
> Represents the SQL NULL data type.
> PDO::PARAM_INT (integer)
> Represents the SQL INTEGER data type.
> PDO::PARAM_STR (integer)
> Represents the SQL CHAR, VARCHAR, or other string data type.
> PDO::PARAM_LOB (integer)
> Represents the SQL large object data type.
> PDO::PARAM_STMT (integer)
> Represents a recordset type. Not currently supported by any drivers.
> PDO::PARAM_INPUT_OUTPUT (integer)
> Specifies that the parameter is an INOUT parameter for a stored procedure. You must bitwise-OR this value with an explicit PDO::PARAM_* data type.
> ```

## **文件命漏洞**

> 可以使用 `realpath()`和`basename()`函数来确保文件名是它应该的样子
> 
> ```php
> $filename = $_POST['username'];
> $vetted = basename(realpath($filename));
> 
> if ($filename !== $vetted) {
>  die("{$filename} is not a good username");
> }
> ```

## **会话固定**

> ```php
> if (check_auth($_POST['username'], $_POST['password'])) {
>  $_SESSION['auth'] = TRUE;
>  session_regenerate_id(TRUE);
> }
> ```

## **文件权限**

> 您可以设置 `open_basedir`限制从 PHP 脚本访问特定目录的选项。如果`open_basedir`在您的*php.ini 中*设置，PHP 会限制文件系统和 I/O 功能，以便它们只能在该目录或其任何子目录中运行。

> 在http.conf配置虚拟主机
> 
> ```
> <VirtualHost 1.2.3.4> 
> ServerName domainA.com 
> DocumentRoot /web/sites/domainA 
> php_admin_value open_basedir /web/sites/domainA 
> </VirtualHost>
> ```
> 
> 或在http.conf按目录或url配置
> 
> ```php
> # 通过目录
> <Directory /home/httpd/html/app1> 
>  php_admin_value open_basedir /home/httpd/html/app1 
> </Directory> 
> 
> # 通过 URL 
> <Location /app2> 
>  php_admin_value open_basedir /home/httpd/html/app2 
> </Location>
> ```

# Web的应用

## 输出缓冲

> `ob_start([callback])` 打开缓冲功能 
> 
> `ob_get_length()` 获取缓冲区长度
> 
> `ob_get_contents()` 获取缓冲区内容
> 
> `ob_clean()` 擦除缓冲区
> 
> `ob_end_clean()` 擦除缓冲区并关闭后续输出缓冲
> 
> `ob_flush()`
> 
> `ob_end_flush()`  

> `ob_start("ob_gzhandler")` 输出压缩

## Apache的ab测试

> ```
> $/usr/local/apache/bin/ab -c 10-n 1000http://localhost/info.php
> ```

## 优化执行时间

* echo比`printf()`快

* 避免在循环内部重新计算.
  
  ```php
   for ($i = 0; $i < count($array); $i++) { /* do something */ }
  # 每次循环都会计算一次count()
  ```

* 使用持久化数据库连接

* 简单的字符串操作可使用字符串函数,而不是正则

## 优化内存

* 尽可能使用数字而不是字符串
* 处理完大字符串后,将保存该字符串的变量设置为空字符串.这释放了内存
* 用`include_once()` 和 `require_once()` 
* 数据库结果集的释放

## 反向代理和复制 (Reverse Proxies and Replication)

> 流量扩展问题
> 
> * 反向代理缓存
> * 负载均衡服务器
> * 数据库复制

# Web Services

> **HTTP code**
> 
> ```
> 200 OK
> ```
> 
> 请求已成功完成。
> 
> ```
> 201 Created
> ```
> 
> 创建新资源的请求已成功完成。
> 
> ```
> 400 Bad Request
> ```
> 
> 请求命中了有效端点，但格式错误且无法完成。
> 
> ```
> 401 Unauthorized
> ```
> 
> 与 一起`403 Forbidden`表示一个有效的请求，但由于缺乏权限而无法完成。通常，此响应表示需要授权但尚未提供。
> 
> ```
> 403 Forbidden
> ```
> 
> 与 类似`401 Unauthorized`，此响应表示有效请求，但由于缺乏权限而无法完成。通常，此响应表明授权可用，但用户缺乏执行请求操作的权限。
> 
> ```
> 404 Not Found
> ```
> 
> 未找到资源（例如，尝试删除 ID 不存在的作者）。
> 
> ```
> 500 Internal Server Error
> ```
> 
> 服务器端发生错误。

> **CURL 检索资源**
> 
> ```php
> $authorID = "ktatroe";
> $url = "http://example.com/api/authors/{$authorID}";
> 
> $ch = curl_init();
> curl_setopt($ch, CURLOPT_URL, $url);
> 
> $response = curl_exec($ch);
> $resultInfo = curl_getinfo($ch);
> 
> curl_close($ch);
> 
> // decode the JSON and use a Factory to instantiate an Author object
> $authorJSON = json_decode($response);
> $author = ResourceFactory::authorFromJSON($authorJSON);
> ```

> **CURL 更新资源**(数据用文件流的方式传到远程服务)
> 
> ```php
> $bookID = "ProgrammingPHP";
> $url = "http://example.com/api/books/{$bookID}";
> 
> $data = array(
>  'edition' => 4,
> );    
> 
> $requestData = http_build_query($data, '', '&');
> 
> $ch = curl_init();
> curl_setopt($ch, CURLOPT_URL, $url);
> 
> $fh = fopen("php://memory", 'rw');
> fwrite($fh, $requestData);
> rewind($fh);
> 
> curl_setopt($ch, CURLOPT_INFILE, $fh);
> curl_setopt($ch, CURLOPT_INFILESIZE, mb_strlen($requestData));
> curl_setopt($ch, CURLOPT_PUT, true);
> 
> $response = curl_exec($ch);
> $resultInfo = curl_getinfo($ch);
> 
> curl_close($ch);
> fclose($fh);
> ```
> 
> `http_build_query($query_data,$numeric_prefix,$arg_separator,$enc_type = PHP_QUERY_RFC1738)` 
> 
> * 第一个数组
> * 第二个,如果数组下标是自然排序的,这个参数作为前缀
> * 第三个分割参数
> * 默认PHP_QUERY_RFC1738

> **CURL创建资源**
> 
> ```php
> <?php $newAuthor = new Author('pbmacintyre');
> $newAuthor->name = "Peter Macintyre";
> 
> $url = "http://example.com/api/authors";
> 
> $data = array(
>  'data' => json_encode($newAuthor)
> );
> 
> $requestData = http_build_query($data, '', '&');
> 
> $ch = curl_init();
> curl_setopt($ch, CURLOPT_URL, $url);
> 
> curl_setopt($ch, CURLOPT_POSTFIELDS, $requestData);
> curl_setopt($ch, CURLOPT_POST, true);
> 
> $response = curl_exec($ch);
> $resultInfo = curl_getinfo($ch);
> 
> curl_close($ch);
> ```
> 
> **CURL删除资源**
> 
> ```php
> <?php $authorID = "ktatroe";
> $bookID = "ProgrammingPHP";
> $url = "http://example.com/api/authors/{$authorID}/books/{$bookID}";
> 
> $ch = curl_init();
> curl_setopt($ch, CURLOPT_URL, $url);
> 
> curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'DELETE');
> 
> $result = curl_exec($ch);
> $resultInfo = curl_getinfo($ch);
> 
> curl_close($ch);
> ```

# PHP调试

## php.ini设置

> * `display_errors` 控制php显示错误的开关,开发环境应该设置为0(off)
> 
> * `error_reporting` 向错误日志和/或 Web 浏览器报告 PHP 遇到的任何错误.
>   
>   * E_ALL 用于报告任何类型的所有错误和警告
>   * E_WARNING 仅向浏览器显示警告（非致命错误）
>   * E_DEPRECATED 显示有关代码的运行时通知警告，这些代码将在 PHP 的未来版本中失败
>   * 例子: `E_ALL & ~E_NOTICE`，它告诉 PHP 报告除生成的通知之外的所有错误
> 
> * `error_log` 错误日志的位置
> 
> * `variables_order` 设置超全局数组加载信息的优先顺序。默认顺序是`EGPCS`, env,get,post,cookie,server
> 
> * `request_order` 描述了$_REQUEST里面的get,post,cookie
> 
> * `zend.assertions` 确定是否运行断言,抛出错误. 禁用时,调用的`assert()` 永远不会运行.
> 
> * `assert.exception` 异常系统的开启与否

| 价值                  | 意义                           |
|:------------------- |:---------------------------- |
| `E_ERROR`           | 运行时错误                        |
| `E_WARNING`         | 运行时警告                        |
| `E_PARSE`           | 编译时解析错误                      |
| `E_NOTICE`          | 运行时通知                        |
| `E_CORE_ERROR`      | PHP 内部产生的错误                  |
| `E_CORE_WARNING`    | PHP 内部生成的警告                  |
| `E_COMPILE_ERROR`   | Zend 脚本引擎内部生成的错误             |
| `E_COMPILE_WARNING` | Zend 脚本引擎内部生成的警告             |
| `E_USER_ERROR`      | 调用生成的运行时错误 `trigger_error()` |
| `E_USER_WARNING`    | 调用生成的运行时警告 `trigger_error()` |
| `E_USER_NOTICE`     | 调用生成的运行时通知 `trigger_error()` |
| `E_ALL`             | 以上所有选项                       |

> `error_reporting(0)` 关闭错误报告

## **自定义错误处理**

> `set_error_handler()`
> 
> 调用完后重新调用`set_error_handler()` 或是 调用`restore_error_handler()`使用默认处理程序
> 
> ```php
> function displayError($error, $errorString, $filename, $line, $symbols)
> {
>  echo "<p>Error '<b>{$errorString}</b>' occurred.<br />";
>  echo "-- in file '<i>{$filename}</i>', line $line.</p>";
> }
> 
> set_error_handler('displayError');
> $value = 4 / 0; // divide by zero error
> 
> <p>Error '<b>Division by zero</b>' occurred.
> -- in file '<i>err-2.php</i>', line 8.</p>
> ```

## 日志错误处理

> `error_log()` 
> 
> ```php
> error_log(message, type [, destination [, extra_headers ]]);
> ```
> 
> * 第一个参数: 错误信息
> * 第二个参数: 错误存储的类型, 0:默认日志, 1:email到第三个参数的地址,第四个参数作为头部.3:存储文件
> 
> ```php
> error_log('A connection to the database could not be opened.', 0);
> 
> error_log('A connection to the database could not be opened.',
>  1, 'errors@php.net');
> 
> error_log('A connection to the database could not be opened.',
>  3, '/var/log/php_errors.log');
> ```
> 
> `trigger_error()` 输出错误
> 
> ```php
> function logRoller($error, $errorString) {
>  $file = '/var/log/php_errors.log';
> 
>  if (filesize($file) > 1024) {
>  rename($file, $file . (string) time());
>  clearstatcache();
>  }
> 
>  error_log($errorString, 3, $file);
> }
> 
> set_error_handler('logRoller');
> 
> for ($i = 0; $i < 5000; $i++) {
>  trigger_error(time() . ": Just an error, ma'am.\n");
> }
> 
> restore_error_handler();
> ```

> 到了生产环境,一切的错误往日志里放
> 
> 可以设置为:
> 
> ```
> display_errors = Off
> log_errors = On
> error_log = /tmp/errors.log
> ```

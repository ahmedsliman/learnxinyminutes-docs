---
name: PHP
contributors:
    - ["Malcolm Fell", "http://emarref.net/"]
    - ["Trismegiste", "https://github.com/Trismegiste"]
translators:
    - ["Ahmad Soliman", "https://github.com/ahmedsliman"]
filename: learnphp.php
---

يُقدّم هذا المستند شرحاً لـ PHP 5+.

```php
<?php // يجب أن يكون كود PHP محاطاً بعلامات <?php

// إذا كان ملف PHP يحتوي على كود PHP فقط، فمن الأفضل
// حذف علامة إغلاق PHP لمنع الإخراج العرضي.

// علامتان مائلتان للأمام تبدأ تعليقاً من سطر واحد.

# وكذلك علامة الهاش (المعروفة أيضاً برمز الجنيه) لكن // أكثر شيوعاً

/*
     إحاطة النص بعلامة مائلة-نجمة ونجمة-مائلة
     يجعلها تعليقاً متعدد الأسطر.
*/

// استخدم "echo" أو "print" لطباعة المخرجات
print('Hello '); // يطبع "Hello " بدون سطر جديد

// الأقواس () اختيارية لـ print و echo
echo "World\n"; // يطبع "World" مع سطر جديد
// (يجب أن تنتهي جميع العبارات بفاصلة منقوطة)

// أي شيء خارج علامات <?php يتم طباعته تلقائياً
?>
Hello World Again!
<?php
// ذلك لأن PHP بدأ تاريخياً كمحرك قوالب


/************************************
 * الأنواع والمتغيرات
 */

// تبدأ المتغيرات برمز $.
// اسم المتغير الصالح يبدأ بحرف أو شرطة سفلية،
// متبوعاً بأي عدد من الأحرف أو الأرقام أو الشرط السفلية.

// لا تحتاج إلى (ولا يمكنك) إعلان المتغيرات.
// بمجرد تعيين قيمة، سينشئ PHP المتغير بالأنواع الصحيحة.

// قيم البولين غير حساسة لحالة الأحرف
$boolean = true;  // أو TRUE أو True
$boolean = FALSE; // أو false أو False

// الأعداد الصحيحة
$int1 = 12;   // => 12
$int2 = -12;  // => -12
$int3 = 012;  // => 10 (الرقم 0 في البداية يدل على رقم ثماني)
$int4 = 0x0F; // => 15 (الرقم 0x في البداية يدل على رقم ست عشري)
// الأرقام الثنائية متاحة منذ PHP 5.4.0.
$int5 = 0b11111111; // 255 (الرقم 0b في البداية يدل على رقم ثنائي)

// الأرقام العشرية (المعروفة أيضاً بالـ doubles)
$float = 1.234;
$float = 1.2e3;
$float = 7E-10;

// حذف متغير
unset($int1);

// العمليات الحسابية
$sum        = 1 + 1; // 2
$difference = 2 - 1; // 1
$product    = 2 * 2; // 4
$quotient   = 2 / 1; // 2

// العمليات الحسابية المختصرة
$number = 0;
$number += 1;      // زيادة $number بمقدار 1
echo $number++;    // يطبع 1 (يزيد بعد التقييم)
echo ++$number;    // يطبع 3 (يزيد قبل التقييم)
$number /= $float; // قسمة وتعيين الناتج إلى $number

// يجب أن تكون النصوص محاطة بعلامات اقتباس مفردة؛
$sgl_quotes = '$String'; // => '$String'

// تجنب استخدام علامات الاقتباس المزدوجة إلا لتضمين متغيرات أخرى
$dbl_quotes = "This is a $sgl_quotes."; // => 'This is a $String.'

// الأحرف الخاصة يتم تهريبها فقط في علامات الاقتباس المزدوجة
$escaped   = "This contains a \t tab character.";
$unescaped = 'This just contains a slash and a t: \t';

// أحط المتغير بأقواس مجعدة إذا لزم الأمر
$number = 23;
$apples = "I have {$number} apples to eat.";   // => I have 23 apples to eat.
$oranges = "I have ${number} oranges to eat."; // => I have 23 oranges to eat.
$money = "I have $${number} in the bank.";     // => I have $23 in the bank.

// منذ PHP 5.3، يمكن استخدام nowdocs للنصوص متعددة الأسطر غير المفسرة
$nowdoc = <<<'END'
Multi line
string
END;

// Heredocs ستفعل تفسير النصوص
$heredoc = <<<END
Multi line
$sgl_quotes
END;

// ربط النصوص يتم بـ .
echo 'This string ' . 'is concatenated';  // Returns 'This string is concatenated'

// يمكن تمرير النصوص كمعاملات إلى echo
echo 'Multiple', 'Parameters', 'Valid';  // Returns 'MultipleParametersValid'


/********************************
 * الثوابت
 */

// يتم تعريف الثابت باستخدام define()
// ولا يمكن تغييره أبداً أثناء التشغيل!

// اسم الثابت الصالح يبدأ بحرف أو شرطة سفلية،
// متبوعاً بأي عدد من الأحرف أو الأرقام أو الشرط السفلية.
define("FOO", "something");

// الوصول إلى الثابت ممكن عن طريق استدعاء الاسم المختار بدون $
echo FOO; // Returns 'something'
echo 'This outputs ' . FOO;  // Returns 'This outputs something'



/********************************
 * المصفوفات
 */

// جميع المصفوفات في PHP هي مصفوفات ترابطية (hashmaps في بعض اللغات)

// يعمل مع جميع إصدارات PHP
$associative = array('One' => 1, 'Two' => 2, 'Three' => 3);

// PHP 5.4 قدم صيغة جديدة
$associative = ['One' => 1, 'Two' => 2, 'Three' => 3];

echo $associative['One']; // يطبع 1

// إضافة عنصر إلى مصفوفة ترابطية
$associative['Four'] = 4;

// قوائم الحرفيات تعين مفاتيح أعداد صحيحة ضمناً
$array = ['One', 'Two', 'Three'];
echo $array[0]; // => "One"

// إضافة عنصر إلى نهاية المصفوفة
$array[] = 'Four';
// أو
array_push($array, 'Five');

// إزالة عنصر من المصفوفة
unset($array[3]);

/********************************
 * المخرجات
 */

echo('Hello World!');
// يطبع Hello World! إلى stdout.
// Stdout هي صفحة الويب إذا كان يعمل في متصفح.

print('Hello World!'); // نفس echo

// echo و print هما أيضاً تركيبات لغة، لذا يمكنك حذف الأقواس
echo 'Hello World!';
print 'Hello World!';

$paragraph = 'paragraph';

echo 100;        // اطبع المتغيرات العددية مباشرة
echo $paragraph; // أو المتغيرات

// إذا كانت علامات الفتح القصيرة مُعدة، أو إصدار PHP الخاص بك
// 5.4.0 أو أكبر، يمكنك استخدام صيغة echo القصيرة
?>
<p><?= $paragraph ?></p>
<?php

$x = 1;
$y = 2;
$x = $y; // $x يحتوي الآن على نفس قيمة $y
$z = &$y;
// $z يحتوي الآن على مرجع إلى $y. تغيير قيمة
// $z سيغير قيمة $y أيضاً، والعكس صحيح.
// $x سيبقى دون تغيير كالقيمة الأصلية لـ $y

echo $x; // => 2
echo $z; // => 2
$y = 0;
echo $x; // => 2
echo $z; // => 0

// يطبع نوع وقيمة المتغير إلى stdout
var_dump($z); // يطبع int(0)

// يطبع المتغير إلى stdout بتنسيق مقروء للإنسان
print_r($array); // يطبع: Array ( [0] => One [1] => Two [2] => Three )

/********************************
 * المنطق
 */
$a = 0;
$b = '0';
$c = '1';
$d = '1';

// assert يلقي تحذيراً إذا لم يكن معاملها صحيحاً

// هذه المقارنات ستكون دائماً صحيحة، حتى لو لم تكن الأنواع متطابقة.
assert($a == $b); // المساواة
assert($c != $a); // عدم المساواة
assert($c <> $a); // عدم المساواة البديل
assert($a < $c);
assert($c > $b);
assert($a <= $b);
assert($c >= $d);

// التالي سيكون صحيحاً فقط إذا تطابقت القيم وكانت من نفس النوع.
assert($c === $d);
assert($a !== $d);
assert(1 === '1');
assert(1 !== '1');

// عامل 'Spaceship' (منذ PHP 7)
// يرجع 0 إذا كانت القيم على كلا الجانبين متساوية
// يرجع 1 إذا كانت القيمة على اليسار أكبر
// يرجع -1 إذا كانت القيمة على اليمين أكبر

$a = 100;
$b = 1000;

echo $a <=> $a; // 0 بما أنهما متساويان
echo $a <=> $b; // -1 بما أن $a < $b
echo $b <=> $a; // 1 بما أن $b > $a

// يمكن تحويل المتغيرات بين الأنواع، حسب استخدامها.

$integer = 1;
echo $integer + $integer; // => 2

$string = '1';
echo $string + $string; // => 2 (النصوص تُجبر إلى أعداد صحيحة)

$string = 'one';
echo $string + $string; // => 0
// يطبع 0 لأن عامل + لا يمكنه تحويل النص 'one' إلى رقم

// يمكن استخدام تحويل النوع لمعاملة متغير كنوع آخر

$boolean = (boolean) 1; // => true

$zero = 0;
$boolean = (boolean) $zero; // => false

// هناك أيضاً دوال مخصصة لتحويل معظم الأنواع
$integer = 5;
$string = strval($integer);

$var = null; // قيمة فارغة


/********************************
 * هياكل التحكم
 */

if (true) {
    print 'I get printed';
}

if (false) {
    print 'I don\'t';
} else {
    print 'I get printed';
}

if (false) {
    print 'Does not get printed';
} elseif (true) {
    print 'Does';
}

// العامل الثلاثي
print (false ? 'Does not get printed' : 'Does');

// العامل الثلاثي المختصر منذ PHP 5.3
// مكافئ لـ "$x ? $x : 'Does'"
$x = false;
print($x ?: 'Does');

// عامل null coalesce منذ php 7
$a = null;
$b = 'Does print';
echo $a ?? 'a is not set'; // يطبع 'a is not set'
echo $b ?? 'b is not set'; // يطبع 'Does print'


$x = 0;
if ($x === '0') {
    print 'Does not print';
} elseif ($x == '1') {
    print 'Does not print';
} else {
    print 'Does print';
}



// هذه الصيغة البديلة مفيدة للقوالب:
?>

<?php if ($x): ?>
This is displayed if the test is truthy.
<?php else: ?>
This is displayed otherwise.
<?php endif; ?>

<?php

// استخدم switch لتوفير بعض المنطق.
switch ($x) {
    case '0':
        print 'Switch does type coercion';
        break; // يجب أن تتضمن break، وإلا ستسقط
               // إلى الحالات 'two' و 'three'
    case 'two':
    case 'three':
        // افعل شيئاً إذا كان $variable إما 'two' أو 'three'
        break;
    default:
        // افعل شيئاً افتراضياً
}

// الحلقات while و do...while و for مألوفة على الأرجح
$i = 0;
while ($i < 5) {
    echo $i++;
} // يطبع "01234"

echo "\n";

$i = 0;
do {
    echo $i++;
} while ($i < 5); // يطبع "01234"

echo "\n";

for ($x = 0; $x < 10; $x++) {
    echo $x;
} // يطبع "0123456789"

echo "\n";

$wheels = ['bicycle' => 2, 'car' => 4];

// حلقات Foreach يمكن أن تتكرر على المصفوفات
foreach ($wheels as $wheel_count) {
    echo $wheel_count;
} // يطبع "24"

echo "\n";

// يمكنك التكرار على المفاتيح وكذلك القيم
foreach ($wheels as $vehicle => $wheel_count) {
    echo "A $vehicle has $wheel_count wheels";
}

echo "\n";

$i = 0;
while ($i < 5) {
    if ($i === 3) {
        break; // خروج من حلقة while
    }
    echo $i++;
} // يطبع "012"

for ($i = 0; $i < 5; $i++) {
    if ($i === 3) {
        continue; // تخطي هذا التكرار من الحلقة
    }
    echo $i;
} // يطبع "0124"


/********************************
 * الدوال
 */

// عرّف دالة بـ "function":
function my_function () {
    return 'Hello';
}

echo my_function(); // => "Hello"

// اسم الدالة الصالح يبدأ بحرف أو شرطة سفلية، متبوعاً بأي
// عدد من الأحرف أو الأرقام أو الشرط السفلية.

function add ($x, $y = 1) { // $y اختياري وافتراضي 1
    $result = $x + $y;
    return $result;
}

echo add(4); // => 5
echo add(4, 2); // => 6

// $result غير متاح خارج الدالة
// print $result; // يعطي تحذيراً.

// منذ PHP 5.3 يمكنك إعلان دوال مجهولة؛
$inc = function ($x) {
    return $x + 1;
};

echo $inc(2); // => 3

function foo ($x, $y, $z) {
    echo "$x - $y - $z";
}

// يمكن للدوال أن ترجع دوال
function bar ($x, $y) {
    // استخدم 'use' لجلب متغيرات خارجية
    return function ($z) use ($x, $y) {
        foo($x, $y, $z);
    };
}

$bar = bar('A', 'B');
$bar('C'); // يطبع "A - B - C"

// يمكنك استدعاء دوال مسماة باستخدام نصوص
$function_name = 'add';
echo $function_name(1, 2); // => 3
// مفيد لتحديد أي دالة لتشغيلها برمجياً.
// أو، استخدم call_user_func(callable $callback [, $parameter [, ... ]]);


// يمكنك الحصول على جميع المعاملات الممررة إلى دالة
function parameters() {
    $numargs = func_num_args();
    if ($numargs > 0) {
        echo func_get_arg(0) . ' | ';
    }
    $args_array = func_get_args();
    foreach ($args_array as $key => $arg) {
        echo $key . ' - ' . $arg . ' | ';
    }
}

parameters('Hello', 'World'); // Hello | 0 - Hello | 1 - World |

// منذ PHP 5.6 يمكنك الحصول على عدد متغير من المعاملات
function variable($word, ...$list) {
	echo $word . " || ";
	foreach ($list as $item) {
		echo $item . ' | ';
	}
}

variable("Separate", "Hello", "World"); // Separate || Hello | World |

/********************************
 * التضمين
 */

<?php
// PHP داخل الملفات المضمنة يجب أن يبدأ أيضاً بعلامة فتح PHP.

include 'my-file.php';
// الكود في my-file.php متاح الآن في النطاق الحالي.
// إذا لم يمكن تضمين الملف (مثل عدم العثور على الملف)، يتم إطلاق تحذير.

include_once 'my-file.php';
// إذا كان الكود في my-file.php قد تم تضمينه في مكان آخر، فلن
// يتم تضمينه مرة أخرى. هذا يمنع أخطاء إعلان الفئات المتعددة

require 'my-file.php';
require_once 'my-file.php';
// نفس include()، إلا أن require() ستسبب خطأ قاتل إذا لم
// يمكن تضمين الملف.

// محتوى my-include.php:
<?php

return 'Anything you like.';
// نهاية الملف

// التضمين والطلب يمكن أن يرجعا قيمة أيضاً.
$value = include 'my-include.php';

// الملفات تُضمن بناءً على مسار الملف المعطى أو، إذا لم يُعطَ أي،
// توجيه include_path. إذا لم يُوجد الملف في
// include_path، سيتحقق include أخيراً في دليل السكريبت المُستدعي
// والدليل الحالي قبل الفشل.
/* */

/********************************
 * الفئات
 */

// تُعرّف الفئات بكلمة class

class MyClass
{
    const MY_CONST      = 'value'; // ثابت

    static $staticVar   = 'static';

    // المتغيرات الثابتة ورؤيتها
    public static $publicStaticVar = 'publicStatic';
    // متاح داخل الفئة فقط
    private static $privateStaticVar = 'privateStatic';
    // متاح من الفئة والفئات الفرعية
    protected static $protectedStaticVar = 'protectedStatic';

    // الخصائص يجب أن تعلن رؤيتها
    public $property    = 'public';
    public $instanceProp;
    protected $prot = 'protected'; // متاح من الفئة والفئات الفرعية
    private $priv   = 'private';   // متاح داخل الفئة فقط

    // أنشئ مُنشئ بـ __construct
    public function __construct($instanceProp)
    {
        // الوصول إلى متغيرات المثيل بـ $this
        $this->instanceProp = $instanceProp;
    }

    // الدوال تُعلن كدوال داخل فئة
    public function myMethod()
    {
        print 'MyClass';
    }

    // كلمة final ستجعل الدالة غير قابلة للتجاوز
    final function youCannotOverrideMe()
    {
    }

    // الدوال السحرية

    // ماذا تفعل إذا عومل الكائن كنص
    public function __toString()
    {
        return $property;
    }

    // عكس __construct()
    // تُستدعى عندما لا يُشار إلى الكائن
    public function __destruct()
    {
        print "Destroying";
    }

/*
 * إعلان خصائص أو دوال الفئة كـ static يجعلها متاحة بدون
 * الحاجة لإنشاء مثيل للفئة. خاصية مُعلنة كـ static لا يمكن
 * الوصول إليها بكائن فئة مُنشأ (رغم أن الدالة الثابتة يمكن).
 */

    public static function myStaticMethod()
    {
        print 'I am static';
    }
}

// ثوابت الفئة يمكن الوصول إليها دائماً بشكل ثابت
echo MyClass::MY_CONST;    // Outputs 'value';

echo MyClass::$staticVar;  // Outputs 'static';
MyClass::myStaticMethod(); // Outputs 'I am static';

// أنشئ فئات باستخدام new
$my_class = new MyClass('An instance property');
// الأقواس اختيارية إذا لم تمرر معامل.

// الوصول إلى أعضاء الفئة باستخدام ->
echo $my_class->property;     // => "public"
echo $my_class->instanceProp; // => "An instance property"
$my_class->myMethod();        // => "MyClass"

// عوامل nullsafe منذ PHP 8
// يمكنك استخدام هذا عندما تكون غير متأكد من أن التجريد لـ $my_class يحتوي على خاصية/دالة
// يمكن استخدامه مع عامل nullish coalesce لضمان القيمة الصحيحة
echo $my_class->invalid_property // يتم إطلاق خطأ
echo $my_class?->invalid_property // => NULL
echo $my_class?->invalid_property ?? "public" // => "public"

// ورث الفئات باستخدام "extends"
class MyOtherClass extends MyClass
{
    function printProtectedProperty()
    {
        echo $this->prot;
    }

    // تجاوز دالة
    function myMethod()
    {
        parent::myMethod();
        print ' > MyOtherClass';
    }
}

$my_other_class = new MyOtherClass('Instance prop');
$my_other_class->printProtectedProperty(); // => يطبع "protected"
$my_other_class->myMethod();               // يطبع "MyClass > MyOtherClass"

final class YouCannotExtendMe
{
}

// يمكنك استخدام "الدوال السحرية" لإنشاء getters و setters
class MyMapClass
{
    private $property;

    public function __get($key)
    {
        return $this->$key;
    }

    public function __set($key, $value)
    {
        $this->$key = $value;
    }
}

$x = new MyMapClass();
echo $x->property; // سيستخدم الدالة __get()
$x->property = 'Something'; // سيستخدم الدالة __set()

// يمكن أن تكون الفئات مجردة (باستخدام كلمة abstract) أو
// تنفذ واجهات (باستخدام كلمة implements).
// تُعلن الواجهة بكلمة interface.

interface InterfaceOne
{
    public function doSomething();
}

interface InterfaceTwo
{
    public function doSomethingElse();
}

// يمكن وراثة الواجهات
interface InterfaceThree extends InterfaceTwo
{
    public function doAnotherContract();
}

abstract class MyAbstractClass implements InterfaceOne
{
    public $x = 'doSomething';
}

class MyConcreteClass extends MyAbstractClass implements InterfaceTwo
{
    public function doSomething()
    {
        echo $x;
    }

    public function doSomethingElse()
    {
        echo 'doSomethingElse';
    }
}


// يمكن للفئات أن تنفذ أكثر من واجهة واحدة
class SomeOtherClass implements InterfaceOne, InterfaceTwo
{
    public function doSomething()
    {
        echo 'doSomething';
    }

    public function doSomethingElse()
    {
        echo 'doSomethingElse';
    }
}


/********************************
 * السمات
 */

// السمات متاحة من PHP 5.4.0 وتُعلن باستخدام "trait"

trait MyTrait
{
    public function myTraitMethod()
    {
        print 'I have MyTrait';
    }
}

class MyTraitfulClass
{
    use MyTrait;
}

$cls = new MyTraitfulClass();
$cls->myTraitMethod(); // يطبع "I have MyTrait"


/********************************
 * مساحات الأسماء
 */

// هذا القسم منفصل، لأن إعلان مساحة الاسم
// يجب أن يكون أول عبارة في الملف. دعنا نتظاهر أن هذا ليس الحالة

<?php

// افتراضياً، الفئات موجودة في مساحة الاسم العامة، ويمكن
// استدعاؤها صراحةً بشرطة مائلة للخلف.

$cls = new \MyClass();



// عيّن مساحة الاسم لملف
namespace My\Namespace;

class MyClass
{
}

// (من ملف آخر)
$cls = new My\Namespace\MyClass;

//أو من داخل مساحة اسم أخرى.
namespace My\Other\Namespace;

use My\Namespace\MyClass;

$cls = new MyClass();

// أو يمكنك إعطاء اسم مستعار لمساحة الاسم؛

namespace My\Other\Namespace;

use My\Namespace as SomeOtherNamespace;

$cls = new SomeOtherNamespace\MyClass();


/**********************
* الربط الثابت المتأخر
*
*/

class ParentClass
{
    public static function who()
    {
        echo "I'm a " . __CLASS__ . "\n";
    }

    public static function test()
    {
        // self يشير إلى الفئة التي عُرّفت فيها الدالة
        self::who();
        // static يشير إلى الفئة التي استُدعيت عليها الدالة
        static::who();
    }
}

ParentClass::test();
/*
I'm a ParentClass
I'm a ParentClass
*/

class ChildClass extends ParentClass
{
    public static function who()
    {
        echo "But I'm " . __CLASS__ . "\n";
    }
}

ChildClass::test();
/*
I'm a ParentClass
But I'm ChildClass
*/

/**********************
*  الثوابت السحرية
*
*/

// احصل على اسم الفئة الحالية. يجب استخدامها داخل إعلان فئة.
echo "Current class name is " . __CLASS__;

// احصل على مسار الدليل الكامل لملف
echo "Current directory is " . __DIR__;

    // الاستخدام النموذجي
    require __DIR__ . '/vendor/autoload.php';

// احصل على مسار الملف الكامل
echo "Current file path is " . __FILE__;

// احصل على اسم الدالة الحالية
echo "Current function name is " . __FUNCTION__;

// احصل على رقم السطر الحالي
echo "Current line number is " . __LINE__;

// احصل على اسم الدالة الحالية. يرجع قيمة فقط عند استخدامها داخل سمة أو إعلان كائن.
echo "Current method is " . __METHOD__;

// احصل على اسم مساحة الاسم الحالية
echo "Current namespace is " . __NAMESPACE__;

// احصل على اسم السمة الحالية. يرجع قيمة فقط عند استخدامها داخل سمة أو إعلان كائن.
echo "Current trait is " . __TRAIT__;

/**********************
*  معالجة الأخطاء
*
*/

// يمكن عمل معالجة أخطاء بسيطة مع كتلة try catch

try {
    // افعل شيئاً
} catch (Exception $e) {
    // عالج الاستثناء
}

// عند استخدام كتل try catch في بيئة مساحة اسم، من المهم
// الهروب إلى مساحة الاسم العامة، لأن الاستثناءات فئات، وفئة
// Exception موجودة في مساحة الاسم العامة. يمكن عمل هذا باستخدام
// شرطة مائلة للخلف في البداية لالتقاط الاستثناء.

try {
    // افعل شيئاً
} catch (\Exception $e) {
    // عالج الاستثناء
}

// استثناءات مخصصة

class MyException extends Exception {}

try {

    $condition = true;

    if ($condition) {
        throw new MyException('Something just happened');
    }

} catch (MyException $e) {
    // عالج استثنائي
}
```

## معلومات إضافية

زر [وثائق PHP الرسمية](http://www.php.net/manual/) للمرجع
والمدخلات المجتمعية.

إذا كنت مهتماً بأفضل الممارسات الحديثة، زر
[PHP الطريقة الصحيحة](http://www.phptherightway.com/).

درس يغطي أساسيات اللغة، إعداد بيئة البرمجة وصنع
بعض المشاريع العملية في [Codecourse - أساسيات PHP](https://www.youtube.com/playlist?list=PLfdtiltiRHWHjTPiFDRdTOPtSyYfz3iLW).

إذا كنت قادماً من لغة بإدارة حزم جيدة، تحقق من
[Composer](http://getcomposer.org/).

للمعايير الشائعة، زر مجموعة توافق أطر عمل PHP
[معايير PSR](https://github.com/php-fig/fig-standards).

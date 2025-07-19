---
name: PHP
contributors:
    - ["Malcolm Fell", "http://emarref.net/"]
    - ["Trismegiste", "https://github.com/Trismegiste"]
translators:
    - ["Ahmad Soliman", "https://github.com/ahmedsliman"]
filename: learnphp.php
---

Dieses Dokument beschreibt PHP 5+.

```php
<?php // PHP-Code muss in <?php-Tags eingeschlossen werden

// Wenn Ihre PHP-Datei nur PHP-Code enthält, ist es Best Practice,
// das PHP-Schließtag wegzulassen, um versehentliche Ausgaben zu verhindern.

// Zwei Schrägstriche beginnen einen einzeiligen Kommentar.

# Das gilt auch für ein Hash-Symbol (auch Pfund-Symbol genannt), aber // ist häufiger

/*
     Text in Schrägstrich-Stern und Stern-Schrägstrich einzuschließen
     macht ihn zu einem mehrzeiligen Kommentar.
*/

// Verwenden Sie "echo" oder "print" zum Ausgeben
print('Hello '); // Gibt "Hello " ohne Zeilenumbruch aus

// Die Klammern () sind optional für print und echo
echo "World\n"; // Gibt "World" mit Zeilenumbruch aus
// (alle Anweisungen müssen mit Semikolon enden)

// Alles außerhalb der <?php-Tags wird automatisch ausgegeben
?>
Hello World Again!
<?php
// Das liegt daran, dass PHP historisch als Template-Engine begann


/************************************
 * Typen & Variablen
 */

// Variablen beginnen mit dem $-Symbol.
// Ein gültiger Variablenname beginnt mit einem Buchstaben oder Unterstrich,
// gefolgt von beliebig vielen Buchstaben, Zahlen oder Unterstrichen.

// Sie müssen (und können) Variablen nicht deklarieren.
// Sobald Sie einen Wert zuweisen, erstellt PHP die Variable mit dem richtigen Typ.

// Boolean-Werte sind case-insensitive
$boolean = true;  // oder TRUE oder True
$boolean = FALSE; // oder false oder False

// Ganzzahlen
$int1 = 12;   // => 12
$int2 = -12;  // => -12
$int3 = 012;  // => 10 (eine führende 0 bezeichnet eine Oktalzahl)
$int4 = 0x0F; // => 15 (ein führendes 0x bezeichnet ein Hex-Literal)
// Binäre Ganzzahl-Literale sind seit PHP 5.4.0 verfügbar.
$int5 = 0b11111111; // 255 (ein führendes 0b bezeichnet eine Binärzahl)

// Floats (auch Doubles genannt)
$float = 1.234;
$float = 1.2e3;
$float = 7E-10;

// Variable löschen
unset($int1);

// Arithmetik
$sum        = 1 + 1; // 2
$difference = 2 - 1; // 1
$product    = 2 * 2; // 4
$quotient   = 2 / 1; // 2

// Kurzschreibweise für Arithmetik
$number = 0;
$number += 1;      // Erhöht $number um 1
echo $number++;    // Gibt 1 aus (erhöht nach der Auswertung)
echo ++$number;    // Gibt 3 aus (erhöht vor der Auswertung)
$number /= $float; // Dividiert und weist den Quotienten $number zu

// Strings sollten in einfache Anführungszeichen eingeschlossen werden;
$sgl_quotes = '$String'; // => '$String'

// Vermeiden Sie doppelte Anführungszeichen außer zum Einbetten anderer Variablen
$dbl_quotes = "This is a $sgl_quotes."; // => 'This is a $String.'

// Sonderzeichen werden nur in doppelten Anführungszeichen escaped
$escaped   = "This contains a \t tab character.";
$unescaped = 'This just contains a slash and a t: \t';

// Schließen Sie eine Variable in geschweifte Klammern ein, falls nötig
$number = 23;
$apples = "I have {$number} apples to eat.";   // => I have 23 apples to eat.
$oranges = "I have ${number} oranges to eat."; // => I have 23 oranges to eat.
$money = "I have $${number} in the bank.";     // => I have $23 in the bank.

// Seit PHP 5.3 können nowdocs für uninterpolierte mehrzeilige Strings verwendet werden
$nowdoc = <<<'END'
Multi line
string
END;

// Heredocs führen String-Interpolation durch
$heredoc = <<<END
Multi line
$sgl_quotes
END;

// String-Verkettung erfolgt mit .
echo 'This string ' . 'is concatenated';  // Returns 'This string is concatenated'

// Strings können als Parameter an echo übergeben werden
echo 'Multiple', 'Parameters', 'Valid';  // Returns 'MultipleParametersValid'


/********************************
 * Konstanten
 */

// Eine Konstante wird mit define() definiert
// und kann niemals zur Laufzeit geändert werden!

// Ein gültiger Konstantenname beginnt mit einem Buchstaben oder Unterstrich,
// gefolgt von beliebig vielen Buchstaben, Zahlen oder Unterstrichen.
define("FOO", "something");

// Zugriff auf eine Konstante ist möglich durch Aufruf des gewählten Namens ohne $
echo FOO; // Returns 'something'
echo 'This outputs ' . FOO;  // Returns 'This outputs something'



/********************************
 * Arrays
 */

// Alle Arrays in PHP sind assoziative Arrays (Hashmaps in einigen Sprachen)

// Funktioniert mit allen PHP-Versionen
$associative = array('One' => 1, 'Two' => 2, 'Three' => 3);

// PHP 5.4 führte eine neue Syntax ein
$associative = ['One' => 1, 'Two' => 2, 'Three' => 3];

echo $associative['One']; // gibt 1 aus

// Element zu einem assoziativen Array hinzufügen
$associative['Four'] = 4;

// Listen-Literale weisen implizit Integer-Schlüssel zu
$array = ['One', 'Two', 'Three'];
echo $array[0]; // => "One"

// Element zum Ende eines Arrays hinzufügen
$array[] = 'Four';
// oder
array_push($array, 'Five');

// Element aus Array entfernen
unset($array[3]);

/********************************
 * Ausgabe
 */

echo('Hello World!');
// Gibt Hello World! an stdout aus.
// Stdout ist die Webseite, wenn in einem Browser ausgeführt.

print('Hello World!'); // Das gleiche wie echo

// echo und print sind auch Sprachkonstrukte, daher können Sie die Klammern weglassen
echo 'Hello World!';
print 'Hello World!';

$paragraph = 'paragraph';

echo 100;        // Gibt skalare Variablen direkt aus
echo $paragraph; // oder Variablen

// Wenn kurze öffnende Tags konfiguriert sind oder Ihre PHP-Version
// 5.4.0 oder höher ist, können Sie die kurze echo-Syntax verwenden
?>
<p><?= $paragraph ?></p>
<?php

$x = 1;
$y = 2;
$x = $y; // $x enthält jetzt den gleichen Wert wie $y
$z = &$y;
// $z enthält jetzt eine Referenz auf $y. Ändern des Wertes von
// $z wird auch den Wert von $y ändern und umgekehrt.
// $x bleibt unverändert als ursprünglicher Wert von $y

echo $x; // => 2
echo $z; // => 2
$y = 0;
echo $x; // => 2
echo $z; // => 0

// Gibt Typ und Wert einer Variable an stdout aus
var_dump($z); // gibt int(0) aus

// Gibt Variable an stdout in menschenlesbarem Format aus
print_r($array); // gibt aus: Array ( [0] => One [1] => Two [2] => Three )

/********************************
 * Logik
 */
$a = 0;
$b = '0';
$c = '1';
$d = '1';

// assert wirft eine Warnung aus, wenn sein Argument nicht true ist

// Diese Vergleiche werden immer true sein, auch wenn die Typen nicht gleich sind.
assert($a == $b); // Gleichheit
assert($c != $a); // Ungleichheit
assert($c <> $a); // alternative Ungleichheit
assert($a < $c);
assert($c > $b);
assert($a <= $b);
assert($c >= $d);

// Das Folgende wird nur true sein, wenn die Werte übereinstimmen und vom gleichen Typ sind.
assert($c === $d);
assert($a !== $d);
assert(1 === '1');
assert(1 !== '1');

// 'Spaceship'-Operator (seit PHP 7)
// Gibt 0 zurück, wenn Werte auf beiden Seiten gleich sind
// Gibt 1 zurück, wenn der Wert links größer ist
// Gibt -1 zurück, wenn der Wert rechts größer ist

$a = 100;
$b = 1000;

echo $a <=> $a; // 0, da sie gleich sind
echo $a <=> $b; // -1, da $a < $b
echo $b <=> $a; // 1, da $b > $a

// Variablen können zwischen Typen konvertiert werden, je nach Verwendung.

$integer = 1;
echo $integer + $integer; // => 2

$string = '1';
echo $string + $string; // => 2 (Strings werden zu Integers gezwungen)

$string = 'one';
echo $string + $string; // => 0
// Gibt 0 aus, weil der +-Operator den String 'one' nicht zu einer Zahl casten kann

// Typecasting kann verwendet werden, um eine Variable als anderen Typ zu behandeln

$boolean = (boolean) 1; // => true

$zero = 0;
$boolean = (boolean) $zero; // => false

// Es gibt auch spezielle Funktionen für das Casten der meisten Typen
$integer = 5;
$string = strval($integer);

$var = null; // Null-Wert


/********************************
 * Kontrollstrukturen
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

// ternärer Operator
print (false ? 'Does not get printed' : 'Does');

// ternärer Kurzoperator seit PHP 5.3
// äquivalent zu "$x ? $x : 'Does'"
$x = false;
print($x ?: 'Does');

// null coalesce Operator seit php 7
$a = null;
$b = 'Does print';
echo $a ?? 'a is not set'; // gibt 'a is not set' aus
echo $b ?? 'b is not set'; // gibt 'Does print' aus


$x = 0;
if ($x === '0') {
    print 'Does not print';
} elseif ($x == '1') {
    print 'Does not print';
} else {
    print 'Does print';
}



// Diese alternative Syntax ist nützlich für Templates:
?>

<?php if ($x): ?>
This is displayed if the test is truthy.
<?php else: ?>
This is displayed otherwise.
<?php endif; ?>

<?php

// Verwenden Sie switch, um etwas Logik zu sparen.
switch ($x) {
    case '0':
        print 'Switch does type coercion';
        break; // Sie müssen ein break einschließen, sonst fallen Sie durch
               // zu den Fällen 'two' und 'three'
    case 'two':
    case 'three':
        // Tun Sie etwas, wenn $variable entweder 'two' oder 'three' ist
        break;
    default:
        // Tun Sie etwas standardmäßig
}

// while-, do...while- und for-Schleifen sind wahrscheinlich bekannt
$i = 0;
while ($i < 5) {
    echo $i++;
} // Gibt "01234" aus

echo "\n";

$i = 0;
do {
    echo $i++;
} while ($i < 5); // Gibt "01234" aus

echo "\n";

for ($x = 0; $x < 10; $x++) {
    echo $x;
} // Gibt "0123456789" aus

echo "\n";

$wheels = ['bicycle' => 2, 'car' => 4];

// foreach-Schleifen können über Arrays iterieren
foreach ($wheels as $wheel_count) {
    echo $wheel_count;
} // Gibt "24" aus

echo "\n";

// Sie können sowohl über die Schlüssel als auch die Werte iterieren
foreach ($wheels as $vehicle => $wheel_count) {
    echo "A $vehicle has $wheel_count wheels";
}

echo "\n";

$i = 0;
while ($i < 5) {
    if ($i === 3) {
        break; // Aus der while-Schleife aussteigen
    }
    echo $i++;
} // Gibt "012" aus

for ($i = 0; $i < 5; $i++) {
    if ($i === 3) {
        continue; // Diese Iteration der Schleife überspringen
    }
    echo $i;
} // Gibt "0124" aus


/********************************
 * Funktionen
 */

// Definieren Sie eine Funktion mit "function":
function my_function () {
    return 'Hello';
}

echo my_function(); // => "Hello"

// Ein gültiger Funktionsname beginnt mit einem Buchstaben oder Unterstrich, gefolgt von beliebig
// vielen Buchstaben, Zahlen oder Unterstrichen.

function add ($x, $y = 1) { // $y ist optional und standardmäßig 1
    $result = $x + $y;
    return $result;
}

echo add(4); // => 5
echo add(4, 2); // => 6

// $result ist außerhalb der Funktion nicht zugänglich
// print $result; // Gibt eine Warnung aus.

// Seit PHP 5.3 können Sie anonyme Funktionen deklarieren;
$inc = function ($x) {
    return $x + 1;
};

echo $inc(2); // => 3

function foo ($x, $y, $z) {
    echo "$x - $y - $z";
}

// Funktionen können Funktionen zurückgeben
function bar ($x, $y) {
    // Verwenden Sie 'use', um externe Variablen einzubringen
    return function ($z) use ($x, $y) {
        foo($x, $y, $z);
    };
}

$bar = bar('A', 'B');
$bar('C'); // Gibt "A - B - C" aus

// Sie können benannte Funktionen mit Strings aufrufen
$function_name = 'add';
echo $function_name(1, 2); // => 3
// Nützlich für die programmatische Bestimmung, welche Funktion ausgeführt werden soll.
// Oder verwenden Sie call_user_func(callable $callback [, $parameter [, ... ]]);


// Sie können alle an eine Funktion übergebenen Parameter erhalten
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

// Seit PHP 5.6 können Sie eine variable Anzahl von Argumenten erhalten
function variable($word, ...$list) {
	echo $word . " || ";
	foreach ($list as $item) {
		echo $item . ' | ';
	}
}

variable("Separate", "Hello", "World"); // Separate || Hello | World |

/********************************
 * Includes
 */

<?php
// PHP innerhalb eingeschlossener Dateien muss auch mit einem PHP-öffnenden Tag beginnen.

include 'my-file.php';
// Der Code in my-file.php ist jetzt im aktuellen Scope verfügbar.
// Wenn die Datei nicht eingeschlossen werden kann (z.B. Datei nicht gefunden), wird eine Warnung ausgegeben.

include_once 'my-file.php';
// Wenn der Code in my-file.php bereits anderswo eingeschlossen wurde, wird er
// nicht erneut eingeschlossen. Dies verhindert mehrfache Klassendeklarationsfehler

require 'my-file.php';
require_once 'my-file.php';
// Das gleiche wie include(), außer dass require() einen fatalen Fehler verursacht, wenn die
// Datei nicht eingeschlossen werden kann.

// Inhalt von my-include.php:
<?php

return 'Anything you like.';
// Dateiende

// Includes und requires können auch einen Wert zurückgeben.
$value = include 'my-include.php';

// Dateien werden basierend auf dem angegebenen Dateipfad eingeschlossen oder, wenn keiner angegeben ist,
// der include_path-Konfigurationsdirektive. Wenn die Datei nicht in
// include_path gefunden wird, prüft include schließlich im eigenen Verzeichnis des aufrufenden Scripts
// und im aktuellen Arbeitsverzeichnis, bevor es fehlschlägt.
/* */

/********************************
 * Klassen
 */

// Klassen werden mit dem class-Schlüsselwort definiert

class MyClass
{
    const MY_CONST      = 'value'; // Eine Konstante

    static $staticVar   = 'static';

    // Statische Variablen und ihre Sichtbarkeit
    public static $publicStaticVar = 'publicStatic';
    // Nur innerhalb der Klasse zugänglich
    private static $privateStaticVar = 'privateStatic';
    // Von der Klasse und Unterklassen zugänglich
    protected static $protectedStaticVar = 'protectedStatic';

    // Eigenschaften müssen ihre Sichtbarkeit deklarieren
    public $property    = 'public';
    public $instanceProp;
    protected $prot = 'protected'; // Von der Klasse und Unterklassen zugänglich
    private $priv   = 'private';   // Nur innerhalb der Klasse zugänglich

    // Erstellen Sie einen Konstruktor mit __construct
    public function __construct($instanceProp)
    {
        // Zugriff auf Instanzvariablen mit $this
        $this->instanceProp = $instanceProp;
    }

    // Methoden werden als Funktionen innerhalb einer Klasse deklariert
    public function myMethod()
    {
        print 'MyClass';
    }

    // Das final-Schlüsselwort würde eine Funktion unüberschreibbar machen
    final function youCannotOverrideMe()
    {
    }

    // Magische Methoden

    // was zu tun ist, wenn ein Objekt als String behandelt wird
    public function __toString()
    {
        return $property;
    }

    // Gegenteil zu __construct()
    // wird aufgerufen, wenn das Objekt nicht mehr referenziert wird
    public function __destruct()
    {
        print "Destroying";
    }

/*
 * Das Deklarieren von Klasseneigenschaften oder -methoden als static macht sie zugänglich ohne
 * eine Instanziierung der Klasse zu benötigen. Eine als static deklarierte Eigenschaft kann nicht
 * mit einem instanziierten Klassenobjekt zugegriffen werden (obwohl eine statische Methode kann).
 */

    public static function myStaticMethod()
    {
        print 'I am static';
    }
}

// Klassenkonstanten können immer statisch zugegriffen werden
echo MyClass::MY_CONST;    // Outputs 'value';

echo MyClass::$staticVar;  // Outputs 'static';
MyClass::myStaticMethod(); // Outputs 'I am static';

// Instanziieren Sie Klassen mit new
$my_class = new MyClass('An instance property');
// Die Klammern sind optional, wenn kein Argument übergeben wird.

// Zugriff auf Klassenmember mit ->
echo $my_class->property;     // => "public"
echo $my_class->instanceProp; // => "An instance property"
$my_class->myMethod();        // => "MyClass"

// Nullsafe-Operatoren seit PHP 8
// Sie können dies verwenden, wenn Sie unsicher sind, ob die Abstraktion von $my_class eine Eigenschaft/Methode enthält
// es kann in Verbindung mit dem nullish coalesce Operator verwendet werden, um den richtigen Wert sicherzustellen
echo $my_class->invalid_property // Ein Fehler wird ausgelöst
echo $my_class?->invalid_property // => NULL
echo $my_class?->invalid_property ?? "public" // => "public"

// Erweitern Sie Klassen mit "extends"
class MyOtherClass extends MyClass
{
    function printProtectedProperty()
    {
        echo $this->prot;
    }

    // Überschreiben Sie eine Methode
    function myMethod()
    {
        parent::myMethod();
        print ' > MyOtherClass';
    }
}

$my_other_class = new MyOtherClass('Instance prop');
$my_other_class->printProtectedProperty(); // => Gibt "protected" aus
$my_other_class->myMethod();               // Gibt "MyClass > MyOtherClass" aus

final class YouCannotExtendMe
{
}

// Sie können "magische Methoden" verwenden, um Getter und Setter zu erstellen
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
echo $x->property; // Wird die __get()-Methode verwenden
$x->property = 'Something'; // Wird die __set()-Methode verwenden

// Klassen können abstrakt sein (mit dem abstract-Schlüsselwort) oder
// Interfaces implementieren (mit dem implements-Schlüsselwort).
// Ein Interface wird mit dem interface-Schlüsselwort deklariert.

interface InterfaceOne
{
    public function doSomething();
}

interface InterfaceTwo
{
    public function doSomethingElse();
}

// Interfaces können erweitert werden
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


// Klassen können mehr als ein Interface implementieren
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
 * Traits
 */

// Traits sind seit PHP 5.4.0 verfügbar und werden mit "trait" deklariert

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
$cls->myTraitMethod(); // Gibt "I have MyTrait" aus


/********************************
 * Namespaces
 */

// Dieser Abschnitt ist getrennt, weil eine Namespace-Deklaration
// die erste Anweisung in einer Datei sein muss. Tun wir so, als wäre das nicht der Fall

<?php

// Standardmäßig existieren Klassen im globalen Namespace und können
// explizit mit einem Backslash aufgerufen werden.

$cls = new \MyClass();



// Setzen Sie den Namespace für eine Datei
namespace My\Namespace;

class MyClass
{
}

// (aus einer anderen Datei)
$cls = new My\Namespace\MyClass;

//Oder aus einem anderen Namespace.
namespace My\Other\Namespace;

use My\Namespace\MyClass;

$cls = new MyClass();

// Oder Sie können den Namespace aliasieren;

namespace My\Other\Namespace;

use My\Namespace as SomeOtherNamespace;

$cls = new SomeOtherNamespace\MyClass();


/**********************
* Late Static Binding
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
        // self bezieht sich auf die Klasse, in der die Methode definiert ist
        self::who();
        // static bezieht sich auf die Klasse, auf der die Methode aufgerufen wurde
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
*  Magische Konstanten
*
*/

// Aktuellen Klassennamen abrufen. Muss innerhalb einer Klassendeklaration verwendet werden.
echo "Current class name is " . __CLASS__;

// Vollständigen Verzeichnispfad einer Datei abrufen
echo "Current directory is " . __DIR__;

    // Typische Verwendung
    require __DIR__ . '/vendor/autoload.php';

// Vollständigen Dateipfad abrufen
echo "Current file path is " . __FILE__;

// Aktuellen Funktionsnamen abrufen
echo "Current function name is " . __FUNCTION__;

// Aktuelle Zeilennummer abrufen
echo "Current line number is " . __LINE__;

// Den Namen der aktuellen Methode abrufen. Gibt nur einen Wert zurück, wenn innerhalb eines Traits oder Objektdeklaration verwendet.
echo "Current method is " . __METHOD__;

// Den Namen des aktuellen Namespaces abrufen
echo "Current namespace is " . __NAMESPACE__;

// Den Namen des aktuellen Traits abrufen. Gibt nur einen Wert zurück, wenn innerhalb eines Traits oder Objektdeklaration verwendet.
echo "Current trait is " . __TRAIT__;

/**********************
*  Fehlerbehandlung
*
*/

// Einfache Fehlerbehandlung kann mit try-catch-Block erfolgen

try {
    // Tun Sie etwas
} catch (Exception $e) {
    // Exception behandeln
}

// Bei der Verwendung von try-catch-Blöcken in einer Namespace-Umgebung ist es wichtig,
// zum globalen Namespace zu escapen, weil Exceptions Klassen sind und die
// Exception-Klasse im globalen Namespace existiert. Dies kann mit einem
// führenden Backslash erfolgen, um die Exception abzufangen.

try {
    // Tun Sie etwas
} catch (\Exception $e) {
    // Exception behandeln
}

// Benutzerdefinierte Exceptions

class MyException extends Exception {}

try {

    $condition = true;

    if ($condition) {
        throw new MyException('Something just happened');
    }

} catch (MyException $e) {
    // Meine Exception behandeln
}
```

## Weitere Informationen

Besuchen Sie die [offizielle PHP-Dokumentation](http://www.php.net/manual/) für Referenz
und Community-Input.

Wenn Sie an aktuellen Best Practices interessiert sind, besuchen Sie
[PHP The Right Way](http://www.phptherightway.com/).

Ein Tutorial, das die Grundlagen der Sprache, das Einrichten der Programmierumgebung und das Erstellen
einiger praktischer Projekte abdeckt bei [Codecourse - PHP Basics](https://www.youtube.com/playlist?list=PLfdtiltiRHWHjTPiFDRdTOPtSyYfz3iLW).

Wenn Sie von einer Sprache mit gutem Paketmanagement kommen, schauen Sie sich
[Composer](http://getcomposer.org/) an.

Für gängige Standards besuchen Sie die PHP Framework Interoperability Group's
[PSR-Standards](https://github.com/php-fig/fig-standards).

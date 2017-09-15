# Чистый код на PHP

## Содержание

  1. [Введение](#Введение)
  2. [Переменные](#Переменные)
     * [Используйте значимые и произносимые имена переменных](#Используйте-значимые-и-произносимые-имена-переменных)
     * [Для одного типа переменных используйте единый словарь](#Для-одного-типа-переменных-используйте-единый-словарь)
     * [Используйте имена, по которым удобно искать (часть 1)](#Используйте-имена-по-которым-удобно-искать-часть-1)
     * [Используйте имена, по которым удобно искать (часть 2)](#Используйте-имена-по-которым-удобно-искать-часть-2)
     * [Используйте пояснительные переменные](#Используйте-пояснительные-переменные)
     * [Избегайте глубоких вложений (часть 1)](#Избегайте-глубоких-вложений-часть-1)
     * [Избегайте глубоких вложений (часть 2)](#Избегайте-глубоких-вложений-часть-2)
     * [Избегайте ментального сопоставления](#Избегайте-ментального-сопоставления)
     * [Не добавляйте ненужный контекст](#Не-добавляйте-ненужный-контекст)
     * [Вместо сокращённых или условных используйте аргументы по умолчанию](#Вместо-сокращённых-или-условных-используйте-аргументы-по-умолчанию)
  3. [Функции](#Функции)
     * [Аргументы функций (в идеале два или меньше)](#Аргументы-функций-в-идеале-два-или-меньше)
     * [Функции должны делать что-то одно](#Функции-должны-делать-что-то-одно)
     * [Имена функций должны быть говорящими](#Имена-функций-должны-быть-говорящими)
     * [Функции должны быть лишь одним уровнем абстракции](#Функции-должны-быть-лишь-одним-уровнем-абстракции)
     * [Не используйте флаги в качестве параметров функций](#Не-используйте-флаги-в-качестве-параметров-функций)
     * [Избегайте побочных эффектов](#Избегайте-побочных-эффектов)
     * [Не пишите в глобальные функции](#Не-пишите-в-глобальные-функции)
     * [Не используйте шаблон Singleton](#Не-используйте-шаблон-singleton)
     * [Инкапсулирование условных выражений](#Инкапсулирование-условных-выражений)
     * [Избегайте негативных условных выражений](#Избегайте-негативных-условных-выражений)
     * [Избегайте условных выражений](#Избегайте-условных-выражений)
     * [Избегайте проверки типов (часть 1))](#Избегайте-проверки-типов-часть-1)
     * [Избегайте проверки типов (часть 2)](#Избегайте-проверки-типов-часть-2)
     * [Убирайте мёртвый код](#Убирайте-мёртвый-код)
  4. [Объекты и структуры данных](#Объекты-и-структуры-данных)
     * [Используйте инкапсуляцию объектов](#Используйте-инкапсуляцию-объектов)
     * [У объектов должны быть private/protected компоненты](#У-объектов-должны-быть-privateprotected-компоненты)
  5. [Классы](#Классы)
     * [Композиция лучше наследования](#Композиция-лучше-наследования)
     * [Избегать Текучий интерфейс](#Избегать-Текучий-интерфейс)
  6. [SOLID](#solid)
     * [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
     * [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
     * [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
     * [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
     * [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
  7. [Don’t repeat yourself (DRY)](#dont-repeat-yourself-dry)
  8. [Переводы](#Переводы)

## Введение

Это принципы разработки ПО, взятые из книги [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) Роберта Мартина и адаптированные для PHP. Это руководство не по стилям программирования, а по созданию читабельного, многократно используемого и пригодного для рефакторинга кода на PHP.

Не каждый из этих принципов должен строго соблюдаться, и ещё с меньшим количеством все будут согласны. Это лишь рекомендации, не более, но все они кодифицированы в многолетнем коллективном опыте автора *Clean Code*.

Вдохновленный [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)

## Переменные

### Используйте значимые и произносимые имена переменных

**Плохо:**

```php
$ymdstr = $moment->format('y-m-d');
```

**Хорошо:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆ вернуться к началу](#Содержание)**

### Для одного типа переменных используйте единый словарь

**Плохо:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**Хорошо:**

```php
getUser();
```

**[⬆ вернуться к началу](#Содержание)**

### Используйте имена, по которым удобно искать (часть 1)

Мы прочитаем больше кода, чем когда-либо напишем. Поэтому важно писать такой код, который будет читабелен и удобен для поиска. Но давая переменным имена, бесполезные для понимания нашей программы, мы мешаем будущим читателям. Используйте такие имена, по которым удобно искать.

**Плохо:**

```php
// What the heck is 448 for?
$result = $serializer->serialize($data, 448);
```

**Хорошо:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### Используйте имена, по которым удобно искать (часть 2)

**Плохо:**

```php
// What the heck is 4 for?
if ($user->access & 4) {
    // ...
}
```

**Хорошо:**

```php
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access & User::ACCESS_UPDATE) {
    // do edit ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Используйте пояснительные переменные

**Плохо:**

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**Лучше:**

Так лучше, но мы всё ещё сильно зависим от регулярного выражения.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

list(, $city, $zipCode) = $matches;
saveCityZipCode($city, $zipCode);
```

**Хорошо:**

С помощью именования подпаттернов снижаем зависимость от регулярного выражения.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(?<city>.+?)\s*(?<zipCode>\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте глубоких вложений (часть 1)

Слишком много `if/else` утверждений может сделать ваш код трудно сопровождаемым. Явное лучше, неявного.

**Плохо:**

```php
function isShopOpen($day)
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            } else {
                return false;
            }
        } else {
            return false;
        }
    } else {
        return false;
    }
}
```

**Хорошо:**

```php
function isShopOpen($day)
{
    if (empty($day) && ! is_string($day)) {
        return false;
    }

    $openingDays = [
        'friday', 'saturday', 'sunday'
    ];

    return in_array(strtolower($day), $openingDays);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте глубоких вложений (часть 2)

**Плохо:**

```php
function fibonacci($n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```

**Хорошо:**

```php
function fibonacci($n)
{
    if ($n === 0) {
        return 0;
    }

    if ($n === 1) {
        return 1;
    }

    if ($n > 50) {
        return 'Not supported';
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте ментального сопоставления

Не заставляйте тех, кто будет читать ваш код, переводить значения переменных. Лучше писать явно, чем неявно.

**Плохо:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```

**Хорошо:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Не добавляйте ненужный контекст

Если имя вашего класса/объекта с чем-то у вас ассоциируется, не проецируйте эту ассоциацию на имя переменной.

**Плохо:**

```php
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```

**Хорошо:**

```php
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Вместо сокращённых или условных используйте аргументы по умолчанию

**Не хорошо:**

Это не хорошо потому, что переменная `$breweryName` может быть `NULL`.

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.')
{
    // ...
}
```

**Лучше:**

Это решение мение понятно, чем предыдущая версия, но лучше контролирует значение переменной.

```php
function createMicrobrewery($name = null)
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**Хорошо:**

Если вы используете только PHP 7+, то вы можете использовать [контроль типов](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) и быть увереным, что переменная `$breweryName` никогда не будет `NULL`.

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.')
{
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

## Функции

### Аргументы функций (в идеале два или меньше)

Крайне важно ограничивать количество параметров функций, потому что это упрощает тестирование. Больше трёх аргументов ведёт к «комбинаторному взрыву», когда вам нужно протестировать кучу разных случаев применительно к каждому аргументу.

Идеальный вариант — вообще без аргументов. Один-два тоже нормально, но трёх нужно избегать. Если их получается больше, то нужно объединять, чтобы уменьшить количество. Обычно если у вас больше двух аргументов, то функция делает слишком много. В тех случаях, когда это не так, чаще всего в качестве аргумента достаточно использовать более высокоуровневый объект.

**Плохо:**

```php
function createMenu($title, $body, $buttonText, $cancellable)
{
    // ...
}
```

**Хорошо:**

```php
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

function createMenu(MenuConfig $config)
{
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Функции должны делать что-то одно

Это, безусловно, самое важное правило в разработке ПО. Когда функции делают больше одной вещи, их труднее составлять, тестировать и обосновывать. А если вы можете наделить функции только какими-то одиночными действиями, то их будет легче рефакторить, а ваш код станет гораздо чище. Даже если вы не будете следовать никакой другой рекомендации, кроме этой, то всё равно опередите многих других разработчиков.

**Плохо:**

```php
function emailClients($clients)
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

**Хорошо:**

```php
function emailClients($clients)
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients($clients)
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive($client)
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```

**[⬆ вернуться к началу](#Содержание)**

### Имена функций должны быть говорящими

**Плохо:**

```php
class Email
{
    //...

    public function handle()
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
$message->handle();
```

**Хорошо:**

```php
class Email 
{
    //...

    public function send()
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Clear and obvious
$message->send();
```

**[⬆ вернуться к началу](#Содержание)**

### Функции должны быть лишь одним уровнем абстракции

Если у вас несколько уровней абстракции, то на функцию возложено слишком много задач. Разбиение функций позволяет многократно использовать код и облегчает тестирование.

**Плохо:**

```php
function parseBetterJSAlternative($code)
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**Тоже плохо:**

Мы выполнили некоторые функции, но функция `parseBetterJSAlternative()` все еще очень сложна и не тестируема.

```php
function tokenize($code)
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer($tokens)
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterJSAlternative($code)
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**Хорошо:**

Лучшим решением является вынесение всех зависимостей из функции `parseBetterJSAlternative()`.

```php
class Tokenizer
{
    public function tokenize($code)
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify($tokens)
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterJSAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse($code)
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Не используйте флаги в качестве параметров функций

Флаги говорят вашим пользователям, что функции делают больше одной вещи. А они должны делать что-то одно. Разделяйте свои функции, если они идут по разным ветвям кода в соответствии с булевой логикой.

**Плохо:**

```php
function createFile($name, $temp = false)
{
    if ($temp) {
        touch('./temp/'.$name);
    } else {
        touch($name);
    }
}
```

**Хорошо:**

```php
function createFile($name)
{
    touch($name);
}

function createTempFile($name)
{
    touch('./temp/'.$name);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте побочных эффектов

Функция может привносить побочные эффекты, если она не только получает значение и возвращает другое значение/значения, но и делает что-то ещё. Побочным эффектом может быть запись в файл, изменение глобальной переменной или случайная отправка всех ваших денег незнакомому человеку.

Но иногда побочные эффекты бывают нужны. Например, та же запись в файл. Лучше делать это централизованно. Не выбирайте несколько функций и классов, которые пишут в какой-то один файл, используйте для этого единый сервис. Единственный.

Главная задача — избежать распространённых ошибок вроде общего состояния для нескольких объектов без какой-либо структуры; использования изменяемых типов данных, которые могут быть чем-то перезаписаны; отсутствия централизованной обработки побочных эффектов. Если вы сможете это сделать, то будете счастливее подавляющего большинства других программистов.

**Плохо:**

```php
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName()
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name); // ['Ryan', 'McDermott'];
```

**Хорошо:**

```php
function splitIntoFirstAndLastName($name)
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name); // 'Ryan McDermott';
var_dump($newName); // ['Ryan', 'McDermott'];
```

**[⬆ вернуться к началу](#Содержание)**

### Не пишите в глобальные функции

Засорение глобалами — дурная привычка в любом языке, потому что вы можете конфликтовать с другой библиотекой, а пользователи вашего API не будут об этом знать, пока не получат исключение в production. Приведу пример: вам нужен конфигурационный массив. Вы пишете глобальную функцию вроде `config()`, но она может конфликтовать с другой библиотекой, пытающейся делать то же самое.

**Плохо:**

```php
function config()
{
    return  [
        'foo' => 'bar',
    ]
}
```

**Хорошо:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get($key)
    {
        return isset($this->configuration[$key]) ? $this->configuration[$key] : null;
    }
}
```

Загрузите конфигурацию и создайте экземпляр класса `Configuration`.

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

И теперь вы должны использовать экземпляр класса `Configuration` в своем приложении.

**[⬆ вернуться к началу](#Содержание)**

### Не используйте шаблон Singleton

Singleton is an [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern). Paraphrased from Brian Button:
 1. They are generally used as a **global instance**, why is that so bad? Because **you hide the dependencies** of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a [code smell](https://en.wikipedia.org/wiki/Code_smell).
 2. They violate the [single responsibility principle](#single-responsibility-principle-srp): by virtue of the fact that **they control their own creation and lifecycle**.
 3. They inherently cause code to be tightly [coupled](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). This makes faking them out under **test rather difficult** in many cases.
 4. They carry state around for the lifetime of the application. Another hit to testing since **you can end up with a situation where tests need to be ordered** which is a big no for unit tests. Why? Because each unit test should be independent from the other.

There is also very good thoughts by [Misko Hevery](http://misko.hevery.com/about/) about the [root of problem](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

**Плохо:**

```php
class DBConnection
{
    private static $instance;

    private function __construct($dsn)
    {
        // ...
    }

    public static function getInstance()
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**Хорошо:**

```php
class DBConnection
{
    public function __construct(array $dsn)
    {
        // ...
    }

     // ...
}
```

Создайте экземпляр класса `DBConnection` и настройте его с помощью [DSN](http://php.net/manual/en/pdo.construct.php#refsect1-pdo.construct-parameters).

```php
$connection = new DBConnection($dsn);
```

И теперь вы должны использовать экземпляр класса `DBConnection` в своем приложении.

**[⬆ вернуться к началу](#Содержание)**

### Инкапсулирование условных выражений

**Плохо:**

```php
if ($article->state === 'published') {
    // ...
}
```

**Хорошо:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте негативных условных выражений

**Плохо:**

```php
function isDOMNodeNotPresent($node)
{
    // ...
}

if (!isDOMNodeNotPresent($node))
{
    // ...
}
```

**Хорошо:**

```php
function isDOMNodePresent($node)
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте условных выражений

Наверно, это кажется невозможным. Впервые это услышав, многие говорят: «Как я смогу что-либо сделать без выражения `if`?» Второй распространённый вопрос: «Ну, это прекрасно, но зачем мне это?» Ответ заключается в рассмотренном выше правиле чистого кода: функция должна делать что-то одно. Если у вас есть классы и функции, содержащие выражение `if`, то тем самым вы говорите своим пользователям, что функция делает больше одной вещи. Не забывайте — нужно оставить что-то одно.

**Плохо:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**Хорошо:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude();
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте проверки типов (часть 1)

PHP не типизирован, т. е. ваши функции могут принимать аргументы любых типов. Иногда такая свобода даже мешает и возникает соблазн выполнять проверку типов в функциях. Но есть много способов этого избежать. Первое, что нужно учитывать, это согласованные API.

**Плохо:**

```php
function travelToTexas($vehicle)
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->peddleTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**Хорошо:**

```php
function travelToTexas(Traveler $vehicle)
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте проверки типов (часть 2)

Если вы работаете с базовыми примитивами (вроде строковых, целочисленных) и массивами, то не можете использовать полиморфизм. Но если кажется, что вам всё ещё нужна проверка типов и вы используете PHP 7+, то примените [объявление типов](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) или строгий режим (strict mode). Это даст вам статичную типизацию поверх стандартного PHP-синтаксиса. Проблема ручной проверки типов в том, что её качественное выполнение подразумевает такое многословие, что полученная искусственная «типобезопасность» не компенсирует потери читабельности кода. Сохраняйте чистоту своего PHP, пишите хорошие тесты и проводите качественные ревизии кода. Или делайте всё это, но со строгим объявлением PHP-типов или в строгом режиме.

**Плохо:**

```php
function combine($val1, $val2)
{
    if (!is_numeric($val1) || !is_numeric($val2)) {
        throw new \Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**Хорошо:**

```php
function combine(int $val1, int $val2)
{
    return $val1 + $val2;
}
```

**[⬆ вернуться к началу](#Содержание)**

### Убирайте мёртвый код

Он плох так же, как и дублирующий код. Не нужно держать его в кодовой базе. Если что-то не вызывается, избавьтесь от этого! Если что, мёртвый код можно будет достать из истории версий.

**Плохо:**

```php
function oldRequestModule($url)
{
    // ...
}

function newRequestModule($url)
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**Хорошо:**

```php
function requestModule($url)
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆ вернуться к началу](#Содержание)**


## Объекты и структуры данных

### Используйте инкапсуляцию объектов

In PHP you can set `public`, `protected` and `private` keywords for methods. 
Using it, you can control properties modification on an object. 

* When you want to do more beyond getting an object property, you don't have
to look up and change every accessor in your codebase.
* Makes adding validation simple when doing a `set`.
* Encapsulates the internal representation.
* Easy to add logging and error handling when getting and setting.
* Inheriting this class, you can override default functionality.
* You can lazy load your object's properties, let's say getting it from a
server.

Additionally, this is part of [Open/Closed](#openclosed-principle-ocp) principle.

**Плохо:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

**Хорошо:**

```php
class BankAccount
{
    private $balance;

    public function __construct($balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdrawBalance($amount)
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function depositBalance($amount)
    {
        $this->balance += $amount;
    }

    public function getBalance()
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->withdrawBalance($shoesPrice);

// Get balance
$balance = $bankAccount->getBalance();
```

**[⬆ вернуться к началу](#Содержание)**

### У объектов должны быть private/protected компоненты

**Плохо:**

```php
class Employee
{
    public $name;

    public function __construct($name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->name; // Employee name: John Doe
```

**Хорошо:**

```php
class Employee
{
    private $name;

    public function __construct($name)
    {
        $this->name = $name;
    }

    public function getName()
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->getName(); // Employee name: John Doe
```

**[⬆ вернуться к началу](#Содержание)**

## Классы

### Композиция лучше наследования

Как говорится в известной книге «[*Шаблоны проектирования*](https://en.wikipedia.org/wiki/Design_Patterns)» Банды четырёх, по мере возможности нужно выбирать композицию, а не наследование. Есть много хороших причин использовать как наследование, так и композицию. Главная цель этой максимы заключается в том, если вы инстинктивно склоняетесь к наследованию, то постарайтесь представить, может ли композиция лучше решить вашу задачу. В каких-то случаях это действительно более подходящий вариант.

Вы спросите: «А когда лучше выбирать наследование?» Всё зависит от конкретной задачи, но можно ориентироваться на этот список ситуаций, когда наследование предпочтительнее композиции:

1. Ваше наследование — это взаимосвязь is-a, а не has-a. Пример: Человек → Животное vs. Пользователь → Детали пользователя (UserDetails).
2. Вы можете повторно использовать код из базовых классов. (Люди могут двигаться, как животные.)
3. Вы хотите внести глобальные изменения в производные классы, изменив базовый класс. (Изменение расхода калорий у животных во время движения.)

**Плохо:**

```php
class Employee 
{
    private $name;
    private $email;

    public function __construct($name, $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// Bad because Employees "have" tax data. 
// EmployeeTaxData is not a type of Employee

class EmployeeTaxData extends Employee 
{
    private $ssn;
    private $salary;
    
    public function __construct($name, $email, $ssn, $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**Хорошо:**

```php
class EmployeeTaxData 
{
    private $ssn;
    private $salary;

    public function __construct($ssn, $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee 
{
    private $name;
    private $email;
    private $taxData;

    public function __construct($name, $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData($ssn, $salary)
    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегать Текучий интерфейс

A [Fluent interface](https://en.wikipedia.org/wiki/Fluent_interface) is an object
oriented API that aims to improve the readability of the source code by using
[Method chaining](https://en.wikipedia.org/wiki/Method_chaining).

While there can be some contexts, frequently builder objects, where this
pattern reduces the verbosity of the code (for example the [PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html)
or the [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)),
more often it comes at some costs:

1. Breaks [Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_%28object-oriented_programming%29)
2. Breaks [Decorators](https://en.wikipedia.org/wiki/Decorator_pattern)
3. Is harder to [mock](https://en.wikipedia.org/wiki/Mock_object) in a test suite
4. Makes diffs of commits harder to read

For more informations you can read the full [blog post](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)
on this topic written by [Marco Pivetta](https://github.com/Ocramius).

**Плохо:**
```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake($make)
    {
        $this->make = $make;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setModel($model)
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setColor($color)
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function dump()
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
  ->setColor('pink')
  ->setMake('Ford')
  ->setModel('F-150')
  ->dump();
```

**Хорошо:**
```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake($make)
    {
        $this->make = $make;
    }

    public function setModel($model)
    {
        $this->model = $model;
    }

    public function setColor($color)
    {
        $this->color = $color;
    }

    public function dump()
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**[⬆ вернуться к началу](#Содержание)**

## SOLID

**SOLID** is the mnemonic acronym introduced by Michael Feathers for the first five principles named by Robert Martin, which meant five basic principles of object-oriented programming and design.

 * [S: Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
 * [O: Open/Closed Principle (OCP)](#openclosed-principle-ocp)
 * [L: Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
 * [I: Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
 * [D: Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

### Single Responsibility Principle (SRP)

As stated in Clean Code, "There should never be more than one reason for a class
to change". It's tempting to jam-pack a class with a lot of functionality, like
when you can only take one suitcase on your flight. The issue with this is
that your class won't be conceptually cohesive and it will give it many reasons
to change. Minimizing the amount of times you need to change a class is important.
It's important because if too much functionality is in one class and you modify a piece of it,
it can be difficult to understand how that will affect other dependent modules in
your codebase.

**Плохо:**

```php
class UserSettings
{
    private $user;

    public function __construct($user)
    {
        $this->user = $user;
    }

    public function changeSettings($settings)
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials()
    {
        // ...
    }
}
```

**Хорошо:**

```php
class UserAuth 
{
    private $user;

    public function __construct($user)
    {
        $this->user = $user;
    }
    
    public function verifyCredentials()
    {
        // ...
    }
}

class UserSettings 
{
    private $user;
    private $auth;

    public function __construct($user) 
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings($settings)
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Open/Closed Principle (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions,
etc.) should be open for extension, but closed for modification." What does that
mean though? This principle basically states that you should allow users to
add new functionalities without changing existing code.

**Плохо:**

```php
abstract class Adapter
{
    protected $name;

    public function getName()
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct($adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch($url)
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall($url)
    {
        // request and return promise
    }

    private function makeHttpCall($url)
    {
        // request and return promise
    }
}
```

**Хорошо:**

```php
interface Adapter
{
    public function request($url);
}

class AjaxAdapter implements Adapter
{
    public function request($url)
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request($url)
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch($url)
    {
        return $this->adapter->request($url);
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Liskov Substitution Principle (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.

**Плохо:**

```php
class Rectangle
{
    protected $width = 0;
    protected $height = 0;

    public function render($area)
    {
        // ...
    }

    public function setWidth($width)
    {
        $this->width = $width;
    }

    public function setHeight($height)
    {
        $this->height = $height;
    }

    public function getArea()
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth($width)
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(height)
    {
        $this->width = $this->height = $height;
    }
}

function renderLargeRectangles($rectangles)
{
    foreach ($rectangles as $rectangle) {
        $rectangle->setWidth(4);
        $rectangle->setHeight(5);
        $area = $rectangle->getArea(); // Плохо: Will return 25 for Square. Should be 20.
        $rectangle->render($area);
    }
}

$rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($rectangles);
```

**Хорошо:**

```php
abstract class Shape
{
    protected $width = 0;
    protected $height = 0;

    abstract public function getArea();

    public function render($area)
    {
        // ...
    }
}

class Rectangle extends Shape
{
    public function setWidth($width)
    {
        $this->width = $width;
    }

    public function setHeight($height)
    {
        $this->height = $height;
    }

    public function getArea()
    {
        return $this->width * $this->height;
    }
}

class Square extends Shape
{
    private $length = 0;

    public function setLength($length)
    {
        $this->length = $length;
    }

    public function getArea()
    {
        return pow($this->length, 2);
    }
}

function renderLargeRectangles($rectangles)
{
    foreach ($rectangles as $rectangle) {
        if ($rectangle instanceof Square) {
            $rectangle->setLength(5);
        } elseif ($rectangle instanceof Rectangle) {
            $rectangle->setWidth(4);
            $rectangle->setHeight(5);
        }

        $area = $rectangle->getArea(); 
        $rectangle->render($area);
    }
}

$shapes = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($shapes);
```

**[⬆ вернуться к началу](#Содержание)**

### Interface Segregation Principle (ISP)

ISP states that "Clients should not be forced to depend upon interfaces that
they do not use." 

A good example to look at that demonstrates this principle is for
classes that require large settings objects. Not requiring clients to setup
huge amounts of options is beneficial, because most of the time they won't need
all of the settings. Making them optional helps prevent having a "fat interface".

**Плохо:**

```php
interface Employee
{
    public function work();

    public function eat();
}

class Human implements Employee
{
    public function work()
    {
        // ....working
    }

    public function eat()
    {
        // ...... eating in lunch break
    }
}

class Robot implements Employee
{
    public function work()
    {
        //.... working much more
    }

    public function eat()
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**Хорошо:**

Not every worker is an employee, but every employee is an worker.

```php
interface Workable
{
    public function work();
}

interface Feedable
{
    public function eat();
}

interface Employee extends Feedable, Workable
{
}

class Human implements Employee
{
    public function work()
    {
        // ....working
    }

    public function eat()
    {
        //.... eating in lunch break
    }
}

// robot can only work
class Robot implements Workable
{
    public function work()
    {
        // ....working
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Dependency Inversion Principle (DIP)

This principle states two essential things:
1. High-level modules should not depend on low-level modules. Both should
depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on
abstractions.

This can be hard to understand at first, but if you've worked with PHP frameworks (like Symfony), you've seen an implementation of this principle in the form of Dependency
Injection (DI). While they are not identical concepts, DIP keeps high-level
modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces
the coupling between modules. Coupling is a very bad development pattern because
it makes your code hard to refactor.

**Плохо:**

```php
class Employee
{
    public function work()
    {
        // ....working
    }
}

class Robot extends Employee
{
    public function work()
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage()
    {
        $this->employee->work();
    }
}
```

**Хорошо:**

```php
interface Employee
{
    public function work();
}

class Human implements Employee
{
    public function work()
    {
        // ....working
    }
}

class Robot implements Employee
{
    public function work()
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage()
    {
        $this->employee->work();
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

## Don’t repeat yourself (DRY)

Постарайтесь соблюдать принцип [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

Старайтесь полностью избавиться от дублирующего кода. Он плох тем, что если вам нужно менять логику, то это придётся делать в нескольких местах.

Представьте, что вы владеете ресторанчиком и отслеживаете, есть ли продукты: помидоры, лук, чеснок, специи и т. д. Если у вас несколько списков с содержимым холодильников, то вам придётся обновлять их все, когда вы готовите какое-то блюдо. А если список один, то и вносить изменения придётся только в него.

Зачастую дублирующий код возникает потому, что вы делаете две и более вещи, у которых много общего. Но небольшая разница между ними заставляет вас писать несколько функций, и те по большей части делают одно и то же. Удаление дублирующего кода означает, что вы создаёте абстракцию, которая может обрабатывать все различия с помощью единственной функции/модуля/класса.

Правильный выбор абстракции критически важен, поэтому нужно следовать принципам SOLID, описанным в разделе «[Классы](#Классы)». Плохие абстракции могут оказаться хуже дублирующего кода, так что будьте осторожны! Но если можете написать хорошие, то делайте это! Не повторяйтесь, иначе окажется, что при каждом изменении вам нужно обновлять код в нескольких местах.

**Плохо:**

```php
function showDeveloperList($developers)
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}

function showManagerList($managers)
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Хорошо:**

```php
function showList($employees)
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Очень хорошо:**

Лучше использовать компактную версию кода.

```php
function showList($employees)
{
    foreach ($employees as $employee) {
        render([
            $employee->calculateExpectedSalary(),
            $employee->getExperience(),
            $employee->getGithubLink()
        ]);
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

## Переводы

На других языках:

 * ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Китайский:**
   * [yangweijie/clean-code-php](https://github.com/yangweijie/clean-code-php)
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
 * ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Русский:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)

**[⬆ вернуться к началу](#Содержание)**

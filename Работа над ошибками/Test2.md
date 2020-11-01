# Работа над ошибка для 2теста

## Оглавление

* [Затенение переменных внутри цикла fori](#question1)
* [Обработка исключений](#question2)
* [Использование переменных интерфейса](#question3)
* [переопределения методов (Overriding)](#question4)
* [Вычисление выражений](#question5)
* [Область видимости выражений](#question6)
* [Недостижимый код](#question7)
* [Классы-обертки](#question8)
  + [Boolean](#quesquestion81)
  + [Byte](#question82)
  + [Short](#question83)
  + [Character](#question84)
  + [Integer](#question85)
  + [Long](#question86)
  + [Float](#question87)
  + [Double](#question88)
* [Правила Switch](#ПравилаSwitch)

## Затенение переменных внутри цикла fori

<a name="question1"></a>

При декларировании цикла for стоит обратить особое внимание на объявление итерируемого значения. Если перед им ененм переменной указан тип, тогда в области видимости цикла ({}) будет выполнено затенение переменной с тем же именем, объявленной до цикла. **т.е. она НЕ будет изменена!**

### Пример

``` java

int j = 0
while (j < 5) {

    for (j = 0; j <= 5;) {
System.out.println("inner J: " +j);
j++;
    }
    System.out.println("outer J: " + j);
    j++;
}
```

В этом случае переменная все изменения j, произошедшие внутри цикла for не повлияют на переменную j, объявленную до цикла for.

## Обработка исключений

<a name="question2"></a>

При проверке возможности перехвата исключений обчзательно нужно обращать внимание на порядок следования блоков catch. Первым должно идти исключение самого узкого типа (child) и далее по мере расширения (от chaild к parent). В противном случае при компиляции будет определена ошибка "Недостижимый код":

 `java: exception testScope.MyException1 has already been caught`

## Использование переменных интерфейса

<a name="question3"></a>

Пееременные интерфейса имеют модификаторы:

 `public static final`

Определение значения в случае с переменной интерфейса (и другими final переменными) происходит на этапе компиляции, а не в рантайме, а тут динамический полиморфизм еще не работает, используется статический, который может определить значение переменной только по типу refType.
Другими словами, если refType

## Правила переопределения методов

<a name="question4"></a>

Есть несколько правил переопределения методов при наследовании.

Общий регламент переопределения:

1. Совпадение сигнатуры (наименование метода, типы и количество параметров)
1. Ковариантность возвращаемых типов. Переопределяемый метод может вернуть не только сам объект, но и его потомков.
1. Ковариантность выбрасываемых исключений. Переопределяемый метод может как не выбрасывать исключение, там и выбросить искллючение parent-метода или его потомков.
1. Последовательность доступа. private метод переопределить нельзя по причине его недоступности.

Пример по правилам:

``` java
class Parent {
    protected ReturnValue ExceptionsThrower() throws MyException {
return new ReturnValue();
    }
}
class Child extends Parent{
    public ChildReturnValue ExceptionsThrower() throws MyException2 {
return new ChildReturnValue();
    }
}

class ReturnValue{}
class ChildReturnValue extends ReturnValue{}

class MyException extends Exception {}
class MyException1 extends MyException {}
class MyException2 extends MyException1 {}
```

## Вычисление выражений

<a name="question5"></a>

Вычисление выражений выполняется слева направо.
т.е. в примере:

``` java
int i = 0;
int[] iA = {10, 20};
iA[i] = i = 30;

```

Последовательность вычислений `iA[i] = i = 30;` будет следующая:

1. `iA[i] = i = 30;`
1. `iA[0] = i = 30;`
1. `iA[0] = 30;`

## Область видимости выражений

<a name="question6"></a>

При решении задач, связанных с вычислением значений первое. на сто стоит обратить внимание наобласть видимости! Она определяется фигурными скобками {}. Несколько правил:

1. Переменные, объявленные внутри области видимости и имеющие такие же наименования как переменные вне - будет затенять внешние.
2. Особое внимание стоит уделять {}

## Недостижимый код

<a name="question7"></a>
При анализе выражений на предмет выявления ошибок компиляции следует искать участки недостижимого кода.
Например, следующее выражение содержит недостижимый код:

``` java
while(false) {
    //
}
```

А этот фрагмент уже будет компилироваться без проблем:

``` java
boolean b = false;
while(b) {
    //
}
```

 В то же время, стоит обратить внимание, что например следующий код будет компилироваться без проблем, т.к. недостижимого кода содержать не будет:

``` java
do {
    // other code
} while(false)
```

## Классы-обертки

<a name="question8"></a>

### Boolean

<a name="quesquestion81"></a>

``` java
 // Constructors
Boolean a = new Boolean("a".equals("a"));
Boolean b = new Boolean("true");
Boolean c = new Boolean("tRue");
// static methods
Boolean d = Boolean.valueOf("trUe");
Boolean e = Boolean.valueOf("a".equals("a"));
boolean f = Boolean.parseBoolean("trUe");
// instance methods
boolean booleanValue = new Boolean(true).booleanValue();
```

### Byte

<a name="quesquestion82"></a>

### Short

<a name="quesquestion83"></a>

``` java
Short a = new Short((short) 12);
Short c = new Short("12");

short r = Short.parseShort("5");
Short j = Short.valueOf((short) 1);
Short p = Short.valueOf("5");
Short s = Short.valueOf("B", 16);

byte b = a.byteValue();
short sh = a.shortValue();
int i = a.intValue();
long l = a.longValue();
float f = a.floatValue();
double d = a.doubleValue();
```

Важное замечание! При арифметических операция все типы, ниже `int` приводятся к `int` ! Т.е. результатом сложения `short + short = int` , а значит выражение:

``` java
short a,b = 5;
short c = a + b;
```

даст ошибку! Необходимо явно привести результат к типу `short` :

``` java
short a,b = 5;
short c = (short) a + b;
```

### Character

<a name="quesquestion84"></a>

``` java
// Constructors
Character a = new Character('f');
// static methods
Character b = Character.valueOf('f');
// instance methods
char y = b.charValue();
```

### Integer

<a name="quesquestion85"></a>

``` java
// constructors
Integer a = new Integer(12);
Integer c = new Integer("12");
// static methods
int r = Integer.parseInt("s");
int h = Integer.parseInt("s", 16);
Integer j = Integer.valueOf(1);
Integer p = Integer.valueOf("1");
Integer v = Integer.valueOf("1", 2);
// instance methods
byte b = a.byteValue();
int i = a.intValue();
long l = a.longValue();
float f = a.floatValue();
double d = a.doubleValue();
```

### Long

<a name="quesquestion86"></a>

``` java
// Constructors
Long a = new Long(12L);
Long c = new Long("12");
// static methods
long r = Long.parseLong("5");
long h = Long.parseLong("5", 16);
Long j = Long.valueOf(1);
Long p = Long.valueOf("5");
Long v = Long.valueOf("5", 10);
Long u = Long.getLong("5");
Long y = Long.getLong("hh", 10L);
Long x = Long.getLong("5", new Long(10L));
// instance methods
byte b = a.byteValue();
short sh = a.shortValue();
int i = a.intValue();
long l = a.longValue();
float f = a.floatValue();
double d = a.doubleValue();
```

### Float

<a name="quesquestion87"></a>

``` java
// Constructors
Float a = new Float(12L);
Float c = new Float("12");
// static methods
float r = Float.parseFloat("5");
Float j = Float.valueOf(1);
Float p = Float.valueOf("5");
// instance methods
byte b = a.byteValue();
short sh = a.shortValue();
int i = a.intValue();
long l = a.longValue();
float f = a.floatValue();
double d = a.doubleValue();
```

### Double

<a name="quesquestion88"></a>

``` java
// Constructors
Double a = new Double(12L);
Double c = new Double("12");
// static methods
double r = Double.parseDouble("5");
Double j = Double.valueOf(1);
Double p = Double.valueOf("5");
// instance methods
byte b = a.byteValue();
short sh = a.shortValue();
int i = a.intValue();
long l = a.longValue();
float f = a.floatValue();
double d = a.doubleValue();
```

## Правила преобразования примитивных типов

Сужающее примитивное преобразование может быть использовано, если выполняются все следующие условия:

1. Выражение является выражением типа int.
2. Тип переменной определяется следующим образом: byte, short, или char.
3. Значение выражения (которое известно во время компиляции, поскольку оно является постоянным выражением) можно представить в виде переменной. Обратите внимание, что сужающее преобразование не применяется к long или double. Таким образом, char ch = 30L; потерпит неудачу, даже если 30 представимо в char.\

Преобразование выполняется в след. порядке:

* byte -> short -> int -> long

* float -> double

При попытке преобразовать int к float или double произойдет потеря точности!

## Правила switch

<a name="ПравилаSwitch"></a>

Вот правила для оператора switch:

1. Только String, byte, char, short, int (и их обертки: Byte, Character, Short, and Integer), и перечисления, может быть использован в качестве типа  (Строка разрешена только начиная с Java 7).
2. В случае константы должны быть переданы переключатель переменной. Например, если переменная switch относится к классу String, то в метках case также должны использоваться строки.
3. переменная переключателя должна быть достаточно большой, чтобы вместить все константы случая. Например, если переменная switch имеет тип char, то ни одна из констант case не может быть больше 65535, поскольку диапазон значений char составляет от 0 до 65535.
4. все метки case должны быть константами времени компиляции.
5. Нет двух константных выражений, связанных с оператор switch может иметь то же значение.
6. Не более одной метки по умолчанию могут быть связаны с тем же операторе switch.

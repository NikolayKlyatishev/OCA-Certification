# Работа над ошибка для 4 теста

## Оглавление

* [Правила декларирование переменныхist](#link1)
* [ArrayList](#link2)

## Правила декларирование переменных <a name="link1"></a>

1. Инициализация переменных выполняется слева направо.
1. Если рпнее переменная не была проинициализирована - мы получим ошибку.

``` java
// Исходное объявление
public class TestClass {
    int i, s, a = 100, b, d;
}

// Результат
public class TestClass {
    int i;
    int s;
    int a = 100;
    int b;
    int d;
}

// Ошибочное объявление
public class TestClass {
    int i, s, a = 100 = b = d;
}
// Результатом будет ошибка компиляции, т.к. переменные b и d еще не инициализированы.
```

## ArrayList <a name="link2"></a>

* Является наследником `AbstractList<E>`

* Реализует интерфейсы `List<E>` ,     `RandomAccess` ,     `Cloneable` ,     `java.io.Serializable`

### Часто используемые методы

* Конструктор, принимающий тип, реализующий `Collection<? extends E>` , где `E` - дженерик `ArrayList`-а.
* `size()` - возвращает размер листа, с 1.
* `isEmpty()` - проверка, является ли ArrayList пустым
* `contains(Object o)` - внутренний вызов `int indexOf(Object o)`. Проверяет весь лист на совпадения. Если передан объект - используется метод `equals()`, если `null` - ищется первый `null`.
* `int indexOf(Object o)` - см. `contains(Object o)`.
* `int lastIndexOf(Object o)` - работает так же как `int indexOf(Object o)`, только поиск начинается с конца списка.
* `Object clone()` - возвращает копию коллекции. При этом внутренние элементы не копируются.
* `Object[] toArray()` - помещает все элементы листа в массив `Object`.
* `<T> T[] toArray(T[] a)` - помещает все элементы листа в массив `T`.
* `E get(int index)` - получает элемент по его индексу
* `E set(int index, E element)` - заменяет элемент по указанному индексу.
* `boolean add(E e)` - добавляет элемент в конец списка.
* `void add(int index, E element)` - вставляет элемент в указанный индекс. элемент в текущей позиции и все последующие сдвигаются на 1.
* `E remove(int index)` - удаляет элемент из списка. Сдвигает все элементы листа после влево на 1.
* `boolean equals(Object o)` - сравнивает все объекты листа меджду собой.
* `void sort(Comparator<? super E> c)` - использует `<T> void sort(T[] a, int fromIndex, int toIndex, Comparator<? super T> c)` для сортировки при помощи компаратора.

# Работа над ошибка для 4 теста

## Оглавление

* [Правила декларирование переменныхist](#link1)

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

# Оглавление
1. [Основы Swift](#основы-swift)
    - [var vs let](#var-vs-let)
    - [Основные типы данных](#основные-типы-данных)
    - [Действия со строками](#действия-со-строками)
2. [Операторы диапазона](#операторы-диапазона)
    - [Оператор замкнутого диапазона](#оператор-замкнутого-диапазона)
    - [Оператор полузамкнутого диапазона](#оператор-полузамкнутого-диапазона)
    - [Односторонние диапазоны](#односторонние-диапазоны)
3. [nil и опциональные типы](#nil-и-опциональные-типы)
    - [Получение значения из Optional](#получение-значения-из-optional)
    - [Неявное получение значений Optional](#неявное-получение-значений-optional)
    - [Проверка Optional на nil](#проверка-optional-на-nil)
    - [Оператор nil-объединения](#оператор-nil-объединения)
4. [Инструкция if](#инструкция-if)
5. [Инструкция switch](#инструкция-switch)
6. [Кортежи (Tuples)](#кортежи-tuples)

## Основы Swift
### `var` vs `let`

- `var`: Для переменных. Значение может быть изменено.
- `let`: Для констант. Значение не может быть изменено после инициализации.
```swift
var variable = "Изменяемая"
let constant = "Неизменяемая"
```

### Основные типы данных
- `Character` - символ
- `String` - текстовая строка
- `Int` - целое число
- `UInt` - беззнаковый тип целого числа
- `Float` - 32-битное число с плавающей точкой
- `Double` - 64-битное число с плавающей точкой
- `Bool` - логическое значение (true/false)

Вы можете добавить обозначение типа, когда объявляете константу или переменную, чтобы иметь четкое представление о типах значений, которые могут хранить константы или переменные, но это необязательно.

> **Примечание**  
>
> В случае с `Character`, `UInt` и `Float` тип данных необходимо задавать явно.

Пример явного обозначения типа:
```swift
// «Объяви переменную с именем welcomeMessage, тип которой будет String»
var welcomeMessage: String
```

Для изменения типа данных переменной в Swift используется процесс, известный как "type casting" (приведение типов):
```swift
let initialNumber = 123
let stringNumber = String(initialNumber) // Преобразование Int в String
```

### Действия со строками
#### Конкатенация
Значения типа `String` могут быть добавлены или конкатенированы с помощью оператора сложения (`+`):
```swift
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome равен "hello there"
```

#### Интерполяция
Способ создать новое значение типа `String` из разных констант:
```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// "3 times 2.5 is 7.5"
```

## Операторы диапазона
В языке Swift есть два оператора диапазона, которые в короткой форме задают диапазон значений

### Оператор замкнутого диапазона
Оператор замкнутого диапазона (`a...b`) задает диапазон от `a` до `b`, включая сами `a` и `b`. При этом значение `a` не должно превышать `b`.

Оператор замкнутого диапазона удобно использовать при последовательном переборе значений из некоторого диапазона, как, например, в цикле `for-in`:
```swift
for index in 1...5 {
    print("\(index) умножить на 5 будет \(index * 5)")
}
// 1 умножить на 5 будет 5
// 2 умножить на 5 будет 10
// 3 умножить на 5 будет 15
// 4 умножить на 5 будет 20
// 5 умножить на 5 будет 25
```

### Оператор полузамкнутого диапазона
Оператор полузамкнутого диапазона (`a..<b`) задает диапазон от `a` до `b`, исключая значение `b`. Такой диапазон называется полузамкнутым, потому что он включает первое значение, но исключает последнее

Операторы полузамкнутого диапазона особенно удобны при работе с массивами и другими последовательностями, пронумерованными с нуля, когда нужно перебрать элементы от первого до последнего:
```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count

for i in 0..<count {
    print("Person \(i + 1) будет \(names[i])")
}
// Person 1 будет Anna
// Person 2 будет Alex
// Person 3 будет Brian
// Person 4 будет Jack
```

### Односторонние диапазоны
Операторы замкнутого диапазона имеют себе альтернативу - это диапазон, который продолжается насколько возможно, но только в одну сторону:
```swift
let names = ["Anna", "Alex", "Brian", "Jack"]

for name in names[2...] {
    print(name)
}
// Brian
// Jack
```

Оператор полузамкнутого диапазона так же имеет одностороннюю форму, которая записывается только с одним конечным значением:
```swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```

Вы так же можете проверить имеет ли односторонний диапазон конкретное значение:
```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```

## nil и опциональные типы
Опциональные типы представляют объекты, которые могут иметь, а могут и не иметь значение. Опциональные типы выступают двойниками базовых типов. Все они имеют в конце вопросительный знак: `Int?`, `String?` и т.д. Вопросительный знак как раз указывает, что это опциональный тип.

По факту, если объект не имеет значения, то ему присваивается специальное значение `nil`. В коде мы также можем установить явным образом это значение:
```swift
var number: Int? = 12
number = nil    // теперь переменная number не имеет значения
```

> Значение `nil` может применяться только к объектам опциональных типов.

Несмотря на то, что в примере выше переменной number присваивается число 12, но фактически переменная будет иметь в качестве значения `Optional(12)`, то есть можно было бы написать следующим образом:
```swift
var number : Optional<Int>= Optional(12)
// или так
var number2 = Optional(12)
```

### Получение значения из Optional
При работе с объектами опциональных типов следует помнить, что они не эквивалентны объектам обычных типов. То есть следующий пример работать не будет:
```swift
var a: Int? = 12
var b: Int = 10
var c = a + b   // ошибка - разные типы
```
Чтобы полноценно работать с объектами опциональных типов, следует извлечь из них значение. Для извлечения значения используется оператор `!` - восклицательный знак после названия объекта опционального типа. Данный оператор еще называют `unwrap operator` или `forced unwrap operator`:
```swift
var a: Int? = 12
var b: Int = 10
var c = a! + b      // с = 22
```

### Неявное получение значений Optional
Swift предоставляет еще один способ получения значения подобных типов, который заключается в использовании типов `Optional` с неявно получаемым значением (`implicitly unwrapped Optional`):
```swift
var b: Int = 10
var a: Int! = Int("123")
b = a + b
print(a)    // 123
print(b)    // 133
```

Здесь переменная a имеет тип `Int!`, а не `Int?`. Фактиччески это тот же самый `Optional`, но теперь нам явным образом не надо применять оператор `!` для получения его значения.

### Проверка Optional на nil
В то же время если переменная `a` в примере выше не будет содержать конкретное значение, то программа опять же выбросит ошибку. Например, в случае `var a: Int! = Int("abc")` или `var a: Int? = Int("abc")`. Поэтому перед использованием объектов опциональных типов желательно проверить, что они имеют какие-либо значение.

Для проверки можно использовать условную конструкцию `if`:
```swift
var str: String = "123"
var b: Int = 10
if var a = Int(str) {
    a += b
    print(a)
} else {
    print(b)
}
```

Но также в данном случае можно и по другому проверить на значение `nil`:
```swift
var str: String = "123"
var b: Int = 10
var a: Int? = Int(str)
if a != nil {
    a += b
    print(a)
} else {
    print(b)
}
```

### Оператор nil-объединения
Оператор `??` позволяет проверить значения объекта `Optional` на `nil`. Этот оператор принимает два операнда `a ?? 10`. Если первый операнд не равен `nil`, то возвращается значение первого операнда. Если первый операнд равен `nil`, то возвращается второй операнд:
```swift
let a = Int("234")
let b = a ?? 10
print(b)    // 234
```

В данном случае поскольку константа a не равна `nil`, то выражение `a ?? 10` возвращает значение этой константы, то есть число 234.

## Инструкция if
Каждый оператор сравнения возвращает значение типа Bool, указывающее, является ли выражение истинным:
```swift
let name = "world"

if name == "world" {
    print("hello, world")
} else if name == "Max" {
    print("hello, Max")
} else {
    print("Мне жаль, \(name), но я тебя не узнаю")
}
// напечатает "hello, world"
```

Так же можно сравнивать кортежи, которые имеют одно и то же количество значений, которые, в свою очередь, должны быть сравниваемыми, что означает, что кортеж типа (`Int`, `String`) может быть сравнен с кортежем такого же типа.

Кортежи сравниваются слева направо, по одному значению за раз до тех пор, пока операция сравнения не найдет отличия между значениями. Если все значения кортежей попарно равны, то и кортежи так же считаются равными
```swift
(1, "zebra") < (2, "apple")   // true, потому что 1 меньше 2, "zebra" и "apple" не сравниваются
(3, "apple") < (3, "bird")    // true , потому что 3 равно 3, а "apple" меньше чем "bird"
(4, "dog") == (4, "dog")      // true , потому что 4 равно 4 и "dog" равен "dog"
```

## Инструкция switch
`Switch` подразумевает наличие какого-то значения, которое сравнивается с несколькими возможными шаблонами. После того как значение совпало с каким-либо шаблоном, выполняется код, соответствующий ответвлению этого шаблона, и больше сравнений уже не происходит. `Switch` представляет собой альтернативу инструкции `if`, отвечающей нескольким потенциальным значениям:
```swift
let fruit = "apple"

switch fruit {
case "apple":
    print("Это яблоко.")
case "banana":
    print("Это банан.")
case "orange":
    print("Это апельсин.")
default:
    print("Неизвестный фрукт.")
}
// Это яблоко.
```

## Кортежи (Tuples)
Кортежи или Tuples представляют набор значений, которые рассматриваются как один объект:
```swift
let props = (22, "age")
var userInfo = (true, 34, "Tom")
```

В данном примере тип данных в кортежах не указан и выводится неявно, но мы можем при определении кортежа также объявить и типы данных его значений:
```swift
let props: (Int, String) = (22, "age")
var userInfo: (Bool, Int, String) = (true, 34, "Tom")
```

Можно присвоить значения из кортежа переменным или константам:
```swift
var userInfo: (Bool, Int, String) = (true, 34, "Tom")
let(isMarried, age, name) = userInfo
print(name)     // "Tom"
```

Также при определении кортежа мы можем именовать его отдельные элементы или обращаться по индексам:
```swift
var userInfo = (married: true, age: 34, name: "Tom")
let age = userInfo.1        // 34
var name = userInfo.name    // Tom
```

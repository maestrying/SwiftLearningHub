# Оглавление
1. [Основы Swift](#основы-swift)
    - [var vs let](#var-vs-let)
    - [Основные типы данных](#основные-типы-данных)
    - [Действия со строками](#действия-со-строками)

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
> В случае с `Character`, `UInt` и `Double` тип данных необходимо задавать явно.

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


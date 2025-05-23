# 🏠 Тест-дизайн: Поле ввода адреса "Откуда"

## 1. **Объект тестирования**
- **Поле:** Адрес отправления
- **Ожидаемый формат:** 
  - Допустимые символы: русские буквы, цифры, пробелы, тире, точка, запятая
  - Максимальная длина: 50 символов
  - Автоматическая проверка адреса через БД

## 2. **Основные проверки**

### 2.1 Валидные значения
| Класс                     | Пример                                  | Результат |
|---------------------------|-----------------------------------------|-----------|
| Русские буквы + цифры     | "3-я Фрунзенская улица, 12"            | ✅ Valid   |
| Пробелы                   | " 3-я Фрунзенская " (с пробелами)      | ✅ Valid*  |
| Тире                      | "ул. Льва-Толстого"                    | ✅ Valid   |
| Точка и запятая           | "М. Пироговская, 25"                   | ✅ Valid   |
| Адрес из БД               | "Комсомольский проспект, 18"           | ✅ Valid   |

_* Пробелы автоматически триммируются_

### 2.2 Невалидные значения
| Класс                     | Пример                                  | Результат |
|---------------------------|-----------------------------------------|-----------|
| Латинские буквы           | "3rd Frunzenskaya Street, 12"          | ❌ Invalid|
| Спецсимволы               | "М. Пироговская, 25$"                  | ❌ Invalid|
| Несуществующий адрес      | "Солнечная аллея д.9"                  | ❌ Invalid|

## 3. **Проверка длины**
### Граничные значения:
| Длина       | Пример                                      | Результат |
|-------------|---------------------------------------------|-----------|
| 1 символ    | "Ф"                                        | ✅ Valid   |
| 49 символов | Адрес длиной 49 символов                   | ✅ Valid   |
| 50 символов | Адрес длиной 50 символов                   | ✅ Valid   |
| 51 символ   | Адрес длиной 51 символа                    | ❌ Invalid|

## 4. **Дополнительные проверки**
### 4.1 Обработка пробелов
| Сценарий                  | Ввод                           | Ожидаемый результат       |
|---------------------------|--------------------------------|---------------------------|
| Пробелы в начале          | "  3-я Фрунзенская"           | "3-я Фрунзенская"         |
| Пробелы в конце           | "3-я Фрунзенская  "           | "3-я Фрунзенская"         |
| Множественные пробелы     | "3-я   Фрунзенская"           | "3-я Фрунзенская"         |

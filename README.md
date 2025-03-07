# Инструмент для анализа текста

**Основная задача**: Создайте инструмент для анализа текста, который обрабатывает текстовые записи (например, отзывы пользователей, статьи или отрывки из книг) и предоставляет некоторые выводы, статистику и преобразования. После этого примените инструмент для анализа текста в соответствии с вашим вариантом и сделайте выводы о характере текста.

## Задача 1: Сбор и предварительная обработка данных

Напишите функцию `preprocess_text`, которая принимает на вход текст и очищает его. Функция должна:
   - Преобразовывать текст в строчные буквы.
   - Удалять ненужные знаки препинания и специальные символы, но сохранять знаки препинания в конце предложения (`.` `!` `?`).
   - Удалить лишние пробелы между словами.
   - Вернуть очищенный текст.

## Задание 2: Анализ частоты слов

Напишите функцию `word_frequency`, которая берет очищенный текст (из задания 1) и возвращает словарь, где ключами являются слова, а значениями - их частота в тексте. Функция должна:
   - Подсчитать, как часто каждое слово встречается в тексте.
   - Игнорировать любые общие стоп-слова. Вы можете использовать предопределенный список, приведенный ниже, или использовать свой собственный. Подумайте о том, чтобы сделать его настраиваемым.

**Предопределённые стоп-слова**:
```python
stop_words = ["and", "the", "is", "in", "it", "you", "that", "to", "of", "a", "with", "for", "on", "this", "at", "by", "an"]
```

## Задача 3: Извлечение информации

**Задача**: Напишите функцию `extract_information`, которая берет неочищенный текст (**не из задания 1**) и извлекает определенные типы информации на основе настраиваемых шаблонов regex, предоставленных в качестве keyword-аргументов. Функция должна возвращать словарь, в котором ключи - это типы совпадений, а значения - списки найденных совпадений.

**Поддерживаемые типы информации**:
1. Адреса электронных почт
2. Телефонные номера
3. Даты
4. Время
5. Цены
6. Дополнительные данные по желанию пользователя

## Задача 4: Анализ настроения

Напишите функцию `analyze_sentiment`, которая берет очищенный текст (из задания 1) и анализирует его настроение на основе заранее определенных положительных и отрицательных слов. Функция должна возвращать оценку настроения текста.

**Предназначенные списки слов**:
- **Положительные слова** (по умолчанию):
```python
positive_words = ["good", "great", "happy", "joy", "excellent", "fantastic", "love", "best"]
```
- **Негативные слова** (по умолчанию):
```python
negative_words = ["bad", "sad", "hate", "terrible", "awful", "poor", "worst"]
```

## Задача 5: Обобщение текста

Напишите функцию `summarize_text`, которая берет очищенный текст (из задания 1) и обобщает его, извлекая наиболее важные предложения на основе их релевантности. Функция должна позволять пользователю указывать в качестве параметра желаемый коэффициент сжатия.

**Инструкции**:
- Функция должна принимать следующие параметры:
  - `text`: Одиночный очищенный текст, который нужно обобщить.
  - `compression_ratio`: Число от 0 до 1, представляющее желаемое сжатие (например, 0,6 для 60-процентного обобщения).
  - `min_threshold`: Целое число, указывающее минимальное количество оставшихся предложений (по умолчанию 2).

- Функция должна:
  - Разделить текст на предложения.
  - Ранжировать предложения на основе их важности (можно использовать простые метрики, такие как длина, частота слов, наличие значимых слов или любые другие метрики, которые вы считаете наиболее подходящими).
  - Используйте рекурсивный подход для динамического отбора предложений с наивысшим рейтингом, удаляя каждое выбранное предложение и заново ранжируя оставшиеся, пока не будет достигнут желаемый коэффициент сжатия.
  - Верните обобщенный текст в виде строки, состоящей из выбранных предложений.

## Задание 6: Визуализация частоты слов

Напишите функцию `visualize_word_frequency`, которая берет словарь частот слов (полученный в задании 2) и визуализирует частоты в текстовом формате.

**Инструкции**:
- Функция должна принимать словарь, в котором ключами являются слова, а значениями - их частоты.
- На выходе должно отображаться каждое слово, за которым следует горизонтальная полоса, представляющая его частоту. Для создания полос используйте простой символ (например, `*`).
- Длину каждой полосы можно масштабировать в зависимости от максимальной частоты, чтобы обеспечить читабельность.
- Функция должна иметь параметр `max_threshold`, чтобы ограничить количество строк в выводе (по умолчанию 20).
- Вывод должен быть отсортирован от наиболее до наименее часто используемых слов

## Задание 7: Функции высшего порядка для анализа текста

Напишите функцию `apply_analysis`, которая принимает список функций анализа и одну текстовую запись. Функция должна применять каждую функцию анализа к текстовой записи и возвращать словарь результатов.

**Инструкции**:
- Функция должна принимать следующие параметры:
  - `text`: Один очищенный текст для анализа.
  - `analysis_functions`: Список функций для применения к тексту. Каждая функция должна принимать на вход один текст и возвращать результат (например, частоту слов, анализ настроения).

- Функция должна:
  - Перебирать список функций анализа, применяя каждую из них к текстовой записи и сохраняя результат в словаре под описательным ключом (например, именем функции).
  - Возвращать словарь, содержащий результаты всех примененных функций анализа.

## Задача 8: Обернуть всё в класс

Создайте класс `TextAnalyzer`, который инкапсулирует всю функциональность из предыдущих задач. Класс должен включать методы для каждого из следующих действий:

1. **Инициализация**:
   - Класс должен принимать один текст при инициализации, хранить исходный текст и автоматически создавать его предобработанную версию.

2. **Методы**:
   - `word_frequency`: Анализирует частоту слов из предварительно обработанного текста.
   - `extract_information`: Извлекает электронные письма, номера телефонов, даты, время и цены из предварительно обработанного текста.
   - `analyze_sentiment`: Выполняет анализ настроения предварительно обработанного текста.
   - `summarize_text`: Обобщает предварительно обработанный текст на основе коэффициента сжатия.
   - `visualize_word_frequency`: Визуализирует данные о частоте слов в тексте.
   - `apply_analysis`: Применяет список функций анализа к предварительно обработанному тексту.

**Инструкции**:
- Класс должен сохранять все необходимые внутренние состояния, такие как исходный и обработанный текст.
- Каждый метод должен вызываться независимо, и класс должен позволять настраивать поведение там, где это возможно (например, передавать пользовательские списки слов или шаблоны regex).
- Убедитесь, что методы хорошо документированы и что класс может быть легко инстанцирован с вводом текста для анализа.

## Задача 9: Анализ текста

Проведите анализ предложенного вам в соответствии с вариантом текста. Воспользуйтесь разработанными инструментами, чтобы:

- Нормализовать текст
- Узнать наиболее часто встречающиеся слова
- Оценить настроение текста
- Определить основную информацию текста

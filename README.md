# Теоретическая часть: Облачные вычисления

## Описание задачи
Современные системы распределенных вычислений требуют эффективных решений для выполнения операций на удаленных узлах кластера. Основная цель проекта — разработка механизма для выполнения удаленных вычислений таким образом, чтобы процесс был максимально прозрачен для пользователя. При этом особое внимание уделяется оптимизации передачи данных, поддержке асинхронного выполнения и транспорту кода.

---

## Основные концепции

### 1. Удаленные вызовы процедур (RPC)
Механизм удаленных вызовов процедур (Remote Procedure Call, RPC) позволяет выполнять функции на удаленных компьютерах так, как будто они вызываются локально. Основные задачи:
- **Прозрачность:** пользователь не должен отличать локальный вызов от удаленного.
- **Маршалинг:** передача кода, данных и возвращаемых значений.
- **Обратная совместимость:** поддержка различных типов данных и форматов.

### 2. Механизм передачи и запуска
Передача данных и кода является ключевой частью системы. Для этого используются следующие подходы:
- **Сериализация данных:** преобразование данных в формат, пригодный для передачи по сети.
- **Передача кода:** компиляция и упаковка функций в виде байт-кода для последующего выполнения на удаленном узле.
- **Загрузка данных:** если данные уже находятся на удаленном узле, они не передаются повторно.

### 3. Балансировка нагрузки
Балансировка нагрузки позволяет равномерно распределять задачи между узлами кластера:
- **Централизованная:** диспетчер принимает все запросы и распределяет их на основе текущей загрузки узлов.
- **Децентрализованная:** узлы сами могут принимать решения о выполнении задач, обмениваясь информацией о состоянии с другими узлами.
- **Критерии оптимизации:** загруженность узлов, местоположение данных и наличие необходимого кода.

---

## Распределенное исполнение

### 1. Декларация удаленно исполняемых функций
Для упрощения создания распределенных задач используются функции/макросы, позволяющие декларативно описывать удаленно исполняемые операции. Пример:
```clojure
@remote
(def compute [data]
  ;; Логика вычислений
  )
## 2. Параллельное исполнение (map-reduce)
Функция `map` расширяется для распределенного исполнения:

- **Разбиение данных:** входные данные разделяются на чанки.
- **Параллельная обработка:** чанки отправляются на разные узлы для обработки.
- **Сбор результатов:** результаты обрабатываются функцией `reduce` на главном узле.

---

## Оптимизация передачи данных

### 1. Локализация вычислений
Для минимизации сетевого трафика и задержек система оптимизирует размещение задач:
- **Кэширование данных:** узлы сохраняют часто используемые данные для повторного использования.
- **Анализ зависимости:** задачи передаются на узлы, где уже развернут код и есть необходимые данные.

### 2. Эффективная сериализация
Clojure поддерживает несколько форматов сериализации, включая EDN, Transit и Fressian, которые обеспечивают компактное представление данных и высокую скорость передачи.

---

## Асинхронное выполнение и мониторинг
Асинхронное выполнение задач реализуется через:
- **Promise/Future:** задачи запускаются в фоновом режиме, возвращая объект для отслеживания их выполнения.
- **Мониторинг прогресса:** главный узел отслеживает выполнение задач и предоставляет данные о статусе, использовании ресурсов и результатах.

Пример асинхронного вызова:
```clojure
(let [result (async-remote compute large-dataset)]
  (println "Task submitted")
  (println "Result:" @result))```

## Поддержка транспорта кода и данных

### 1. Динамическая компиляция и передача кода
В Clojure динамическая природа языка позволяет компилировать код в байт-код JVM на лету и передавать его между узлами. Это достигается через:
- **Функции сериализации:** передача кода в виде строк или байт-кода.
- **Среда выполнения:** узлы принимают код, компилируют его (если требуется) и исполняют.

### 2. Транспорт Java-объектов
Java-объекты могут быть сериализованы и переданы между узлами благодаря JVM-совместимости. Используются стандартные библиотеки (например, Java Serialization или Kryo).

### 3. Поддержка Clojure-кода
Передача Clojure-кода обеспечивается сериализацией форм Clojure или скомпилированного байт-кода. Узлы интерпретируют и выполняют полученный код.

---

## Заключение
Использование языка Clojure для реализации облачных вычислений позволяет:
- Эффективно передавать данные и код благодаря динамической природе языка.
- Упрощать декларацию распределенных задач через макросы и встроенные механизмы.
- Оптимизировать распределение задач и передачу данных с учетом загрузки узлов.
- Реализовать гибкий асинхронный механизм запуска и мониторинга задач.

Этот подход обеспечивает высокую производительность и масштабируемость, делая систему подходящей для широкого спектра вычислительных задач.

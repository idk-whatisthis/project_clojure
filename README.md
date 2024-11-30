
# Облачные вычисления

### Требования
Реализуйте механизм, позволяющий выполнять ряд операций на удаленных компьютерах,
предварительно зарегистрированных в рамках облака (кластера). С точки зрения прикладных
программ вызов кода на удаленном компьютере ничем не должен отличаться от локального.
Не должно также требоваться предварительного развертывания приложения на удаленном
компьютере, т.е. требуется обеспечить маршалинг и передачу не только данных, но и кода.
При оптимизации следует исходить из соображений, что удаленный вызов имеет смысл для
больших объемов вычислений и существенных объемов данных.

### Основные элементы:

1. базовый механизм передачи и запуска (код, данные), а также балансировки загрузки;
2. функция/макрос, обеспечивающая декларацию удаленно исполняемой функции;
3. вариант map с параллельным и распределенным исполнением (учитывайте
многоядерность современных машин).

### Дополнительные требования

Обеспечьте поддержку следующих элементов:
- оптимизация передачи данных по сети: диспетчер заданий будет стараться задачу
отдать тому узлу, на котором уже развернут соответствующий код и есть
соответствующие данные;
- сделайте механизм асинхронного запуска удаленных вычислений с поддержкой
мониторинга прогресса;
- обеспечьте поддержку транспорта Java-объектов;
- обеспечьте поддержку транспорта Clojure- и Java-кода в форме байт-кода.






## Регламент работы
### 1. Формулировка задачи
#### 1.1 Описание проекта
Проект направлен на разработку механизма облачных вычислений, который позволит пользователям выполнять вычислительные операции на удаленных компьютерах (узлах) в рамках облака (кластера). С точки зрения прикладных программ вызов кода на удаленном компьютере должен быть эквивалентен локальному вызову. Пользователям не потребуется предварительно разворачивать приложения на удаленных узлах, так как система должна обеспечивать маршалинг и передачу как данных, так и кода.

#### 1.2 Цели проекта
1. Реализовать механизм передачи и запуска кода и данных на удаленных узлах.
2. Обеспечить балансировку нагрузки между узлами кластера.
3. Разработать функции для декларации удаленно исполняемых функций.
4 Реализовать параллельное и распределенное исполнение с использованием функции map.
5. Оптимизировать передачу данных по сети.
6. Обеспечить асинхронный запуск удаленных вычислений с мониторингом прогресса.
7. Поддерживать транспорт Java-объектов и Clojure/Java-кода в форме байт-кода.

#### 1.3 Подход к решению
Для реализации проекта будут использованы следующие подходы:

- Сетевое взаимодействие: Для передачи данных и кода между клиентом и удаленными узлами будет использоваться протокол HTTP/REST или сокеты.
- Маршалинг: Будет реализован механизм сериализации объектов и кода для передачи по сети.
- Балансировка нагрузки: Диспетчер заданий будет использовать алгоритмы для оптимального распределения задач между узлами.
- Асинхронность: Реализация асинхронных вызовов с использованием Future или Promise для мониторинга выполнения задач.



  
### 2. Табличное описание (календарный план)

# График выполнения проекта

| **Этап**                               | **Описание**                                                                                              | **Результат**                                                                                   | **Длительность** | **Ответственный**      |
|---------------------------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|------------------|-----------------------|
| **1. Анализ требований и проектирование** | Определение архитектуры, форматов передачи данных и механизмов загрузки Java и Clojure-кода.            | Минимально необходимый дизайн, покрывающий оба языка.                                            | 3 дня            | Шелковникова Светлана            |
| **2. Реализация базового механизма**   | Создание транспортного уровня, передачи данных, выполнения задач, упрощенная поддержка Java и Clojure.    | Рабочий прототип для выполнения задач и передачи данных.                                         | 7 дней           | Грехова Анастасия           |
| **3. Балансировка нагрузки и параллельное выполнение** | Реализация базового алгоритма распределения задач и многопоточности.                                    | Round Robin или Data Locality, многопоточная обработка задач на узлах.                           | 4 дня            | Грехова Анастасия |
| **4. Асинхронное выполнение и транспорт кода (Java + Clojure)** | Поддержка асинхронного API и механизм динамической загрузки байт-кода для Java и Clojure.               | Асинхронный запуск задач, поддержка передачи и выполнения байт-кода для двух языков.            | 6 дней           | Грехова Анастасия   |
| **5. Оптимизация и тестирование**      | Тестирование функциональности, производительности и базовая оптимизация передачи данных.                  | Протестированная система с минимальными задержками и кэшированием кода и данных.                | 5 дней           | Шелковникова Светлана           |


## Сокращенный график

| **Неделя**  | **День 1–3 (25.11 - 27.11)**       | **День 4–10 (28.11 - 4.12)**          | **День 11–14 (5.12 - 8.12)**       | **День 15–20 (9.12 - 14.12)**        | **День 21–25 (15.12 - 19.12)**        | **День 26–30 (20.12 - 23.12)**       |
|-------------|---------------------|------------------------|----------------------|-----------------------|-----------------------|----------------------|
| **1. Анализ и проектирование** | ███████████            |                      |                      |                       |                       |                      |
| **2. Реализация механизма**    |                       | ██████████████████   |                      |                       |                       |                      |
| **3. Балансировка и параллельность** |                     |                      | ██████████           |                       |                       |                      |
| **4. Асинхронность и код**     |                       |                      |                      | ██████████████████    |                       |                      |
| **5. Оптимизация и тестирование** |                     |                      |                      |                       | ███████████████      | ███████████         |

---

## Контрольные точки (Milestones)

1. **День 10**: Реализован базовый механизм передачи данных и выполнения задач (Java + Clojure).  
2. **День 14**: Готова балансировка нагрузки и поддержка многопоточности.  
3. **День 20**: Реализована поддержка асинхронного выполнения и динамической загрузки кода.  
4. **День 30**: Проведены оптимизация, тестирование, устранены критические баги.


### 3. Реализация базовой функциональности

Реализация базового функционала включает в себя создание ключевых механизмов для распределенных вычислений в облачной среде. Основное внимание уделяется оптимизации передачи данных, поддержке асинхронного выполнения, а также транспортировке данных и кода для выполнения задач на удаленных узлах.

#### 3.1 Основные элементы 

##### **1. Оптимизация передачи данных**
- **Локализация задач:** Диспетчер заданий анализирует текущее состояние узлов (наличие кода, данных, свободных ресурсов) и старается минимизировать передачу данных по сети.  
- **Кэширование:** Коды и данные, переданные на узел однажды, сохраняются в локальном кэше для повторного использования. Это снижает сетевые задержки при выполнении похожих задач.  
- **Сжатие данных:** Использование алгоритмов сжатия (например, GZIP или Snappy) для уменьшения объема передаваемой информации.  

##### **2. Асинхронный запуск удаленных вычислений**
- **API для асинхронного выполнения:** Предоставляется интерфейс для постановки задач в очередь и выполнения их в асинхронном режиме.  
- **Мониторинг прогресса:** Возможность отслеживания состояния выполнения задач (например, _"в очереди"_, _"в процессе"_, _"завершено"_).  
- **Управление зависимостями:** Задачи могут зависеть друг от друга, и механизм должен корректно организовать их выполнение (например, через граф зависимостей).  
- **Обработка результатов:** Асинхронные задачи возвращают _future_-объекты, которые содержат либо результат выполнения, либо информацию об ошибке.  

##### **3. Поддержка транспорта Java-объектов**
- **Сериализация и десериализация:** Java-объекты преобразуются в поток данных с использованием стандартных инструментов (например, `ObjectOutputStream`) или более производительных библиотек (Kryo, Protocol Buffers).  
- **Универсальность:** Поддержка передачи объектов произвольных классов (при условии, что они сериализуемы).  
- **Обеспечение безопасности:** Использование механизма верификации передаваемых объектов для предотвращения атак на основе передачи вредоносного кода.  

##### **4. Поддержка транспорта Clojure- и Java-кода**
- **Передача байт-кода:** Код передается в виде готового для выполнения Java-байт-кода, что устраняет необходимость компиляции на удаленном узле.  
- **Динамическая загрузка:** Использование `ClassLoader` для загрузки Java-классов и `clojure.lang.Compiler` для выполнения кода Clojure на лету.  
- **Унификация:** Код как Java, так и Clojure, обрабатывается с использованием общего механизма, что упрощает поддержку и развитие системы.  
- **Совместимость:** Поддерживается передача кода, содержащего замыкания, лямбда-функции и ссылки на внешние библиотеки.  


### 4. Расширенная функциональность

#### 4.1 Дополнительные требования

- Оптимизация передачи данных:
Диспетчер заданий будет учитывать наличие развернутого кода и данных на узлах при распределении задач.

- Асинхронный запуск удаленных вычислений:
Реализация механизма асинхронного выполнения задач с возможностью мониторинга их прогресса.

- Поддержка транспорта Java-объектов:
Обеспечение возможности передачи Java-объектов через сетевой интерфейс.

- Поддержка транспорта Clojure- и Java-кода:
Реализация механизма передачи кода в виде байт-кода, который может быть выполнен на удаленных узлах.

### 5. Артефакты

По завершении этапов реализации будут получены следующие артефакты:

- Программный код со сборочными файлами: Код будет организован и собран с использованием инструментов сборки (например, Maven, Gradle, Leiningen).
- Покрытие компонентными тестами: Реализация тестов для проверки функциональности и производительности системы.
- Автоматически генерируемая документация: Документация на программный интерфейс, генерируемая с использованием инструментов, таких как Javadoc или ClojureDoc.
- Примеры использования: Модельные примеры, демонстрирующие функциональность разработанной библиотеки и ее применение в различных сценариях.

#### Заключение
Проект по разработке механизма облачных вычислений нацелен на создание эффективной и удобной системы для выполнения вычислений на удаленных узлах. Он будет включать в себя все необходимые элементы для обеспечения простоты использования и высокой производительности.

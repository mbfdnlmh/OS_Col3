# OS_Col3
Харченко Анастасия 2 курс 9 группа
Третий коллоквиум нечетный вариант

# Классические поведенческие шаблоны проектирования и архитектура ПО

## 1. Поведенческие шаблоны проектирования

### 1.1. Шаблон "Команда" (Command)

**Определение:**
Инкапсулирует запрос в виде объекта, позволяя параметризовать клиентов с различными запросами, ставить операции в очередь, логировать их и поддерживать отмену.

**Проблема/Решение:**
| Проблема | Решение |
|----------|---------|
| Жесткая связанность между инициатором и исполнителем операции | Инкапсуляция запроса в объект Command |
| Необходимость реализации undo/redo функциональности | Хранение истории команд |

**Примеры использования:**
1. Графический редактор:
   - Кнопки инструментов создают команды (DrawCommand, EraseCommand)
   - Поддержка отмены последнего действия

2. Очередь задач:
   - Команды ставятся в очередь и выполняются последовательно
   - Возможность приоритезации задач

3. Транзакционные системы:
   - Команды для финансовых операций
   - Возможность отката транзакции

**Принципы:**
- Инкапсуляция: запрос скрыт внутри объекта
- Разделение: инициатор не знает деталей выполнения
- Ортогональность: новые команды не влияют на существующие

**Многопоточность:**
- Очередь команд должна быть потокобезопасной
- Команды могут выполняться в пуле потоков

### 1.2. Шаблон "Стратегия" (Strategy)

**Определение:**
Определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми.

**Проблема/Решение:**
| Проблема | Решение |
|----------|---------|
| Множество вариантов одного алгоритма | Выделение интерфейса стратегии |
| Жесткая привязка к конкретной реализации | Динамическая замена стратегии |

**Примеры использования:**
1. Система оплаты:
   - Стратегии: CreditCardPayment, PayPalPayment, CryptoPayment
   - Возможность добавления новых способов оплаты

2. Сортировка данных:
   - QuickSortStrategy, MergeSortStrategy, BubbleSortStrategy
   - Выбор алгоритма в runtime

3. Кэширование:
   - LRUStrategy, FIFOStrategy, LFUStrategy
   - Замена стратегии без изменения клиентского кода

**Принципы:**
- Инкапсуляция: алгоритмы скрыты за интерфейсом
- Разделение: клиентский код не зависит от реализации
- Ортогональность: стратегии независимы друг от друга

**Многопоточность:**
- Каждая стратегия должна быть потокобезопасной
- Возможность параллельного выполнения разных стратегий

### 1.3. Шаблон "Шаблонный метод" (Template Method)

**Определение:**
Определяет скелет алгоритма, перекладывая ответственность за некоторые его шаги на подклассы.

**Проблема/Решение:**
| Проблема | Решение |
|----------|---------|
| Повторяющаяся структура алгоритма | Вынесение общего алгоритма в базовый класс |
| Необходимость вариативности отдельных шагов | Выделение абстрактных методов |

**Примеры использования:**
1. Игровой движок:
   - Базовый класс Game с методом play()
   - Подклассы реализуют initGame(), processInput(), render()

2. Обработка документов:
   - Общий процесс: открыть → обработать → сохранить
   - Подклассы определяют форматы обработки

3. Тестирование:
   - Шаблон: setUp() → test() → tearDown()
   - Конкретные тесты реализуют свои шаги

**Принципы:**
- Инкапсуляция: алгоритм скрыт в базовом классе
- Разделение: вариативные части вынесены в подклассы
- Ортогональность: изменения в шагах не влияют на структуру

**Многопоточность:**
- Весь шаблонный метод должен быть потокобезопасным
- Возможность синхронизации на уровне отдельных шагов

## 2. Архитектура ПО

### 2.1. Определение архитектуры ПО

Архитектура программного обеспечения - это:
- Фундаментальная организация системы
- Набор значимых решений о:
  * Структуре компонентов
  * Взаимодействии между ними
  * Принципах принятия проектных решений

**Ключевые характеристики:**
1. Модульность
2. Масштабируемость
3. Поддерживаемость
4. Тестируемость

### 2.2. Влияние многопоточности на архитектуру

**Основные аспекты:**
1. Синхронизация:
   - Мьютексы, семафоры, атомарные операции
   - Очереди сообщений

2. Распределение ресурсов:
   - Пулы потоков
   - Асинхронные вызовы

3. Модели параллелизма:
   - Акторная модель
   - Реактивное программирование


**Проблемы и решения:**
| Проблема | Решение |
|----------|---------|
| Состояние гонки | Синхронизация доступа |
| Взаимные блокировки | Иерархия блокировок |
| Голодание потоков | Приоритеты и fair-очереди |

### 2.3. Ортогональные стратегии в архитектуре

**Принципы:**
1. Разделение ответственности:
   - MVC, Clean Architecture
   - Микросервисы

2. Независимость компонентов:
   - Слабая связанность
   - Четкие интерфейсы

3. Гибкость изменений:
   - Подмена реализации
   - Минимальное воздействие изменений

**Примеры:**
1. СУБД:
   - Изменение хранилища (SQL → NoSQL)
   - Без изменения бизнес-логики

2. UI:
   - Замена интерфейса (Desktop → Web)
   - Без изменения backend

3. Сетевой протокол:
   - HTTP → WebSockets
   - Без изменения обработчиков

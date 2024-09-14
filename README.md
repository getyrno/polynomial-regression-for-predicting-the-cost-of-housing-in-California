# Полиномиальная Регрессия: Теория и Практика

Добро пожаловать в мой проект по реализации полиномиальной регрессии для предсказания стоимости жилья в Калифорнии. В этом проекте я рассмотрел два подхода к созданию модели полиномиальной регрессии:

1. **Использование готовых инструментов** из библиотеки `scikit-learn`.
2. **Реализация модели "с нуля"** без использования готовых решений, используя только библиотеки `numpy` и `pandas`.

## Оглавление

- [Обзор Проекта](#обзор-проекта)
- [Датасет](#датасет)
- [Скрипты](#скрипты)
  - [model.py](#modelpy)
  - [model_without_libs.py](#model_without_libspy)
- [Результаты](#результаты)
- [Анализ](#анализ)
- [Выводы и Рекомендации](#выводы-и-рекомендации)
- [Установка и Запуск](#установка-и-запуск)
- [Глоссарий](#глоссарий)
- [Лицензия](#лицензия)

## Обзор Проекта

Цель этого проекта — понять, как работает полиномиальная регрессия, и научиться реализовывать её как с использованием готовых инструментов, так и самостоятельно. Я использовал Калифорнийский датасет о жилье, который содержит различные характеристики домов и их стоимость.

Реализация полиномиальной регрессии "с нуля" помогла мне глубже понять процесс обучения модели, вычисление градиентов и обновление весов, что важно для подготовки к собеседованиям и углубленного понимания машинного обучения.

## Датасет

Я использовал **Калифорнийский датасет о жилье (California Housing Dataset)**, доступный в библиотеке `scikit-learn`. Этот датасет включает в себя:

- **Признаки (Features):**
  - `MedInc`: Средний доход.
  - `HouseAge`: Возраст дома.
  - `AveRooms`: Среднее количество комнат.
  - `AveBedrms`: Среднее количество спален.
  - `Population`: Население района.
  - `AveOccup`: Среднее количество жителей на дом.
  - `Latitude`: Широта.
  - `Longitude`: Долгота.
  
- **Целевая переменная (Target):**
  - `MedHouseVal`: Средняя стоимость дома в 100 тысячах долларов.

Датасет содержит данные 20,640 домов.

## Скрипты

### model.py

Этот скрипт использует готовую модель полиномиальной регрессии из библиотеки `scikit-learn` для предсказания стоимости жилья.

**Описание:**

1. **Загрузка и подготовка данных:** Я загружаю датасет, преобразую его в DataFrame и разделяю на признаки и целевую переменную.
2. **Разделение данных:** Данные разделяются на обучающую и тестовую выборки в соотношении 80/20.
3. **Подготовка полиномиальных признаков:** Генерирую полиномиальные признаки степени 2.
4. **Обучение модели:** Создаётся и обучается модель полиномиальной регрессии.
5. **Оценка модели:** Предсказываются значения на тестовых данных и вычисляются метрики RMSE и MAE.
6. **Визуализация:** Создаётся график, сравнивающий истинные и предсказанные значения.

### model_without_libs.py

Этот скрипт реализует полиномиальную регрессию **с нуля**, используя только библиотеки `numpy` и `pandas`. Здесь я самостоятельно вычисляю градиенты и обновляю веса модели с помощью метода градиентного спуска.

**Описание:**

1. **Загрузка и подготовка данных:** Я загружаю датасет, нормализрую признаки и добавляю столбцы для полиномиальных признаков (например, \( x^2 \) для степени 2).
2. **Разделение данных:** Данные разделяются на обучающую и тестовую выборки в соотношении 80/20.
3. **Реализация модели:**
   - **Инициализация весов:** Веса модели инициализируются случайными значениями.
   - **Гипотеза:** Вычисляю предсказанные значения как скалярное произведение признаков и весов.
   - **Функция потерь:** Использую среднеквадратичную ошибку (MSE) для оценки качества предсказаний.
   - **Градиент:** Вычисляю градиент функции потерь по весам.
   - **Обновление весов:** Обновляю веса модели с использованием градиентного спуска.
   - **Условие остановки:** Останавливаю обучение, если изменение потерь становится меньше заданного порога.
4. **Оценка модели:** Предсказываю значения на тестовых данных и вычисляю метрики RMSE и MAE.
5. **Визуализация:** Создаю графики для отображения процесса обучения и сравнения истинных и предсказанных значений.

## Результаты

### Размеры обучающей и тестовой выборок

- **Размер обучающей выборки:** (16,512, 3)  
  *(Включает bias и полиномиальные признаки: [1, x, x²])*
  
- **Размер тестовой выборки:** (4,128, 3)

### model.py (С использованием scikit-learn)

- **RMSE на тестовом наборе:** 0.84
- **MAE на тестовом наборе:** 0.63

### model_without_libs.py (Реализация с нуля)

| Запуск | RMSE на тестовом наборе | MAE на тестовом наборе | Количество эпох |
|-------|-------------------------|------------------------|------------------|
| 1     | 0.91                    | 0.70                   | 99               |
| 2     | 0.83                    | 0.64                   | 299              |
| 3     | 0.83                    | 0.64                   | 304              |

## Анализ

### Сравнение Подходов

1. **Использование scikit-learn (model.py):**
   - **Преимущества:**
     - Быстрая и простая реализация.
     - Оптимизированные алгоритмы для обучения модели.
     - Автоматическое разделение данных и вычисление метрик.
   - **Недостатки:**
     - Меньше контроля над процессом обучения.
     - Ограниченная возможность для обучения алгоритму самому.

2. **Реализация с нуля (model_without_libs.py):**
   - **Преимущества:**
     - Глубокое понимание процесса обучения модели полиномиальной регрессии.
     - Полный контроль над параметрами и процессом оптимизации.
     - Возможность модификации алгоритма под специфические задачи.
   - **Недостатки:**
     - Более длительное время разработки.
     - Возможность ошибок в реализации алгоритма.
     - Отсутствие оптимизаций, реализованных в специализированных библиотеках.

### Причины Различий в Результатах

- **Инициализация весов:** В модели с нуля веса инициализируются случайными значениями, что может влиять на скорость и качество сходимости.
- **Метод оптимизации:** Реализованный градиентный спуск может отличаться от оптимизированных методов, используемых в `scikit-learn`.
- **Количество эпох:** В зависимости от числа эпох и скорости обучения модель может либо переобучаться, либо недообучаться.
- **Нормализация данных:** В обоих скриптах применялась нормализация признаков, что важно для стабильности градиентного спуска.
- **Степень полинома:** Использование полинома степени 2 в обоих подходах обеспечило схожие результаты, однако scikit-learn может использовать более эффективные методы для обучения.

### Проблемы и Решения

- **Предупреждение в scikit-learn:**
  - **Проблема:** В одном из запусков появился warning о том, что параметр `squared` устарел.
  - **Решение:** Перейти на использование новой функции `mean_squared_error` с `squared=False` для вычисления RMSE вручную, как было сделано в скрипте.

- **Неустойчивость результатов в реализации с нуля:**
  - **Проблема:** Разные запуски модели "с нуля" давали разные результаты и количество эпох для остановки обучения.
  - **Решение:** Установить фиксированное количество эпох или более точные условия остановки. Также можно экспериментировать с параметрами градиентного спуска, такими как скорость обучения и порог остановки.

## Выводы и Рекомендации

1. **Использование готовых библиотек** значительно упрощает процесс разработки и обеспечивает высокую производительность моделей.
2. **Реализация алгоритмов самостоятельно** помогает лучше понять их внутреннюю работу, что важно для углубленного изучения машинного обучения и подготовки к собеседованиям.
3. **Градиентный спуск:** Важно правильно выбрать скорость обучения и условия остановки, чтобы обеспечить сходимость модели.
4. **Нормализация данных:** Приведение признаков к одному масштабу улучшает эффективность обучения.
5. **Визуализация:** Графики потерь и сравнения истинных и предсказанных значений помогают оценить качество модели.

### Рекомендации для Дальнейшего Обучения

- **Множественная полиномиальная регрессия:** Изучить использование нескольких признаков для предсказания.
- **Регуляризация:** Ознакомиться с методами Ridge и Lasso для предотвращения переобучения.
- **Полиномиальная регрессия более высокой степени:** Экспериментировать со степенями полинома, но с осторожностью, чтобы избежать переобучения.
- **Методы оптимизации:** Изучить различные методы градиентного спуска, такие как стохастический градиентный спуск (SGD), моментум и адаптивные методы.
- **Кросс-валидация:** Использовать k-fold кросс-валидацию для более надежной оценки модели.
- **Расширение набора признаков:** Включить дополнительные признаки для улучшения качества модели.

## Установка и Запуск

### Требования

- Python 3.6+
- Библиотеки:
  - `numpy`
  - `pandas`
  - `scikit-learn`
  - `matplotlib`

### Установка

1. **Клонируйте репозиторий:**

   ```bash
   git clone https://github.com/getyrno/polynomial-regression-for-predicting-the-cost-of-housing-in-California.git
   cd polynomial-regression-for-predicting-the-cost-of-housing-in-California
   ```

2. **Установите необходимые библиотеки:**

   ```bash
   pip install numpy pandas scikit-learn matplotlib
   ```

### Запуск Скриптов

1. **Запуск модели с использованием scikit-learn:**

   ```bash
   python model.py
   ```

2. **Запуск модели, реализованной с нуля:**

   ```bash
   python model_without_libs.py
   ```

## Результаты Запусков

### model.py (С использованием scikit-learn)

- **RMSE на тестовом наборе:** 0.84
- **MAE на тестовом наборе:** 0.63

### model_without_libs.py (Реализация с нуля)

| Запуск | RMSE на тестовом наборе | MAE на тестовом наборе | Количество эпох |
|-------|-------------------------|------------------------|------------------|
| 1     | 0.91                    | 0.70                   | 99               |
| 2     | 0.83                    | 0.64                   | 299              |
| 3     | 0.83                    | 0.64                   | 304              |

**Примечания:**

- В последних запусках модель достигла стабильных значений RMSE и MAE с количеством эпох около 300, что указывает на хорошую сходимость.
- Реализация с нуля показала сопоставимые результаты с использованием scikit-learn, демонстрируя эффективность вручную реализованного градиентного спуска.

## Лицензия

Этот проект лицензирован под [MIT License](LICENSE).

---

Если у вас есть вопросы или предложения по улучшению проекта, не стесняйтесь открывать issue или отправлять pull request. Удачи в изучении машинного обучения!#   p o l y n o m i a l - r e g r e s s i o n - f o r - p r e d i c t i n g - t h e - c o s t - o f - h o u s i n g - i n - C a l i f o r n i a 
 
 
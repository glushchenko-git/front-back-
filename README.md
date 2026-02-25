ОТЧЁТ ПО ПРАКТИЧЕСКОМУ ЗАНЯТИЮ №1

CSS-препроцессоры (SASS/LESS)

Дисциплина: Фронтенд и бэкенд разработка
Семестр: 4 семестр, 2025/2026 уч. год
Преподаватели: Загородних Николай Анатольевич, Краснослободцева Дарья Борисовна
Выполнил: Студент группы ___________

1. Цель работы

Изучить возможности CSS-препроцессоров (SASS/LESS), научиться использовать переменные, миксины и вложенную структуру селекторов для стилизации веб-приложений. Практически реализовать карточку товара с применением указанных возможностей.

2. Теоретическая часть

2.1. Что такое CSS-препроцессор?

Препроцессор — это программа, принимающая на вход код, написанный на языке препроцессора, и возвращающая на выходе готовый CSS-код, который понимает браузер.

2.2. Основные возможности препроцессоров

Переменные — позволяют хранить часто используемые значения (цвета, размеры, отступы) и переиспользовать их по всему проекту.
Вложенность — даёт возможность создавать иерархические селекторы, повторяющие структуру HTML.
Миксины — блоки стилей, которые можно переиспользовать в разных местах с возможностью передачи параметров.
Функции — математические операции и манипуляции со значениями.
Модульность — разделение стилей на отдельные файлы с возможностью импорта.
2.3. Сравнение SASS и LESS

Функциональность	SASS	LESS
Переменные	$variable	@variable
Миксины	@mixin name() {...}	.name() {...}
Наследование	@extend .class;	.class;
Вложенность	Да	Да
Условные выражения	@if, @else	when, and, not
Циклы	@for, @each, @while	Только рекурсией
Для выполнения работы был выбран препроцессор SASS как более функциональный и распространённый.

3. Ход выполнения работы

3.1. Установка SASS

SASS был установлен через npm (менеджер пакетов Node.js):

bash
# Проверка наличия Node.js и npm
node -v
npm -v

# Установка SASS глобально
npm install -g sass

# Проверка установки
sass --version
Результат: установлена версия 1.86.3 (или актуальная на момент выполнения).

3.2. Создание структуры проекта

Была создана следующая структура папок и файлов:

text
product-card/
│
├── index.html          # HTML-разметка карточки товара
├── scss/
│   └── styles.scss     # Исходный код на SASS
├── css/
│   └── styles.css      # Скомпилированный CSS (создаётся автоматически)
└── README.md           # Инструкция по установке и запуску
3.3. Написание HTML-кода

Был создан файл index.html с разметкой карточки товара:

html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Карточка товара</title>
    <link rel="stylesheet" href="css/styles.css">
</head>
<body>
    <div class="card">
        <img src="https://avatars.mds.yandex.net/get-marketpic/9048107/pic1d31ac74dde055ba63b633659615dc22/orig" alt="https://avatars.mds.yandex.net/get-marketpic/9048107/pic1d31ac74dde055ba63b633659615dc22/orig" class="card__image">
        <h2 class="card__title">POCO MOCO</h2>
        <p class="card__description">Современный смартфон с отличной камерой и мощным процессором.</p>
        <a href="#" class="card__btn">Купить</a>
    </div>
</body>
</html>
3.4. Написание SASS-кода с использованием препроцессора

В файле scss/styles.scss были реализованы следующие возможности препроцессора:

3.4.1. Переменные (минимум 2)

Были созданы переменные для основного цвета и радиуса скругления:

scss
// Переменные
$primary-color: #3498db;   // Основной цвет (синий)
$border-radius: 12px;      // Радиус скругления углов
3.4.2. Миксин (минимум 1)

Был создан миксин для добавления тени карточке. Миксин принимает цвет в качестве параметра:

scss
// Миксин для тени карточки
@mixin card-shadow($color) {
    box-shadow: 0 4px 12px rgba($color, 0.2);
    border: 1px solid lighten($color, 30%);
}
3.4.3. Вложенная структура селекторов

Была применена вложенность для организации стилей по методологии БЭМ:

scss
// Вложенная структура
.card {
    max-width: 320px;
    margin: 20px auto;
    padding: 16px;
    border-radius: $border-radius;
    background-color: #fff;
    @include card-shadow($primary-color);  // Подключение миксина

    &__image {
        width: 100%;
        border-radius: $border-radius;
    }

    &__title {
        font-size: 1.5rem;
        color: $primary-color;
        margin: 12px 0 8px;
    }

    &__description {
        font-size: 1rem;
        color: #555;
        margin-bottom: 16px;
    }

    &__btn {
        display: inline-block;
        padding: 10px 18px;
        background-color: $primary-color;
        color: #fff;
        text-decoration: none;
        border-radius: 6px;
        transition: background-color 0.3s;

        // Вложенный псевдокласс
        &:hover {
            background-color: darken($primary-color, 10%);
        }
    }
}
3.5. Компиляция SASS в CSS

Для компиляции SASS-кода в обычный CSS была использована команда:

bash
# Однократная компиляция
sass scss/styles.scss css/styles.css

# Или режим автоматического слежения за изменениями
sass --watch scss/styles.scss:css/styles.css
3.6. Результат компиляции

После компиляции был получен следующий CSS-код (css/styles.css):

css
.card {
  max-width: 320px;
  margin: 20px auto;
  padding: 16px;
  border-radius: 12px;
  background-color: #fff;
  box-shadow: 0 4px 12px rgba(52, 152, 219, 0.2);
  border: 1px solid #b6daf2;
}

.card__image {
  width: 100%;
  border-radius: 12px;
}

.card__title {
  font-size: 1.5rem;
  color: #3498db;
  margin: 12px 0 8px;
}

.card__description {
  font-size: 1rem;
  color: #555;
  margin-bottom: 16px;
}

.card__btn {
  display: inline-block;
  padding: 10px 18px;
  background-color: #3498db;
  color: #fff;
  text-decoration: none;
  border-radius: 6px;
  transition: background-color 0.3s;
}

.card__btn:hover {
  background-color: #217dbb;
}
4. Результат работы

4.1. Скриншот выполненной карточки товара

<img src="Снимок экрана 2026-02-25 в 18.27.21.png" alt="Снимок экрана 2026-02-25 в 18.27.21.png">
5. Выводы

В ходе выполнения практического занятия были изучены возможности CSS-препроцессора SASS:

Переменные позволяют централизованно хранить значения цветов, размеров и других параметров, что упрощает поддержку и изменение стилей.
Миксины помогают избежать дублирования кода и позволяют создавать переиспользуемые блоки стилей с параметрами.
Вложенная структура делает код более читаемым и организованным, особенно при использовании методологии БЭМ.
Автоматическая компиляция SASS в CSS экономит время и исключает человеческие ошибки при написании валидного CSS.
SASS значительно упрощает процесс стилизации веб-приложений по сравнению с обычным CSS, делая код более модульным, поддерживаемым и организованным. Полученные навыки будут полезны при разработке реальных веб-проектов.

6. Ссылка на репозиторий

https://github.com/tvthietkeweb/product-card-sass

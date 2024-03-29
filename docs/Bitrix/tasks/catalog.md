# План выполнения задания “Каталог товаров”

# Структура страницы 📄

## Условие: нет `SECTION_CODE`

- Выводите списка разделов
- `require_once 'sections.php'`
- `/catalog/`

## Условие: есть `SECTION_CODE`, но нет `CODE`

- Выводите список элементов
- `require_once 'elements.php'`
- `/catalog/код раздела/` - все для мороженого 🍦
- `/catalog/код раздела 2 уровня/` - подраздел

## Условие: есть `CODE`

- Выводите детальную товара
- `require_once 'detail.php'`

# Страница списка элементов 📋

## Цепочка навигации

- Компонент цепочка навигации
    - Строится по разделам (добавить название разделов в физические папки)
    - Шаблон приводим к виду верстки

## Заголовок страницы

- Формируем в шаблоне компонента список новостей

## Меню разделов

- Создаем инфоблок `Каталог`
- Создаем разделы в нем
- Настраиваем ЧПУ
    - Инфоблок
        - Раздел
            - Символьный код обязательное
            - Символьный транслитируется из названия
            - Страница раздела `/catalog/#SECTION_CODE#/`
        - Элемента
            - Символьный код обязательное
            - Символьный транслитируется из названия
            - Страница элемента `/catalog/#SECTION_CODE#/#CODE#/`
    - Обработка адресов
        - Правило для разделов
            - `#^/catalog/{}/`
            - `/catalog/index.php`
            - `SECTION_CODE=$1`
        - Правило для элементов
            - `#^/catalog/{}/{}/`
            - `/catalog/index.php`
            - `SECTION_CODE=$1&CODE=$1`
- В компоненте список новостей
    - Список разделов
        - В `result_modifier`
            - `CIBlockSection::GetList` (в документации)
                - Фильтрация
                    - ID инфоблока = `$arResult['ID']`
                    - `GLOBAL_ACTIVE = Y`
                    - `SECTION_ID = $arResult['MAIN_SECTION']['ID']`
                    - `DEPTH_LEVEL = 2`
                - Сортировка
                    - `SORT = по возрастанию`
        - Записать данные в `$arResult['SECTIONS']`
        - Выделение `$arResult['SECTIONS'] => $section['ID'] = $arResult['SECTION']['ID']`
    - Все -> `/catalog/` - это просто ссылка вне разделов
        - Выделение `$arResult['MAIN_SECTION']['ID'] = $arResult['SECTION']['ID']`
    - Текущий раздел
        - В `result_modifier`
            - `CIBlockSection::GetList` (в документации)
                - Фильтрация
                    - ID инфоблока = `$arResult['ID']`
                    - `GLOBAL_ACTIVE = Y`
                    - `CODE = $arParams['SECTION_CODE'] = $_REQUEST['SECTION_CODE']`
                - Сортировка
                    - `срать`
                - if
                - Записать данные в `$arResult['SECTION']`
            - if (`$arResult['SECTION']['IBLOCK_SECTION_ID']`) {
                - `CIBlockSection::GetList` (в документации)
                - Фильтрация
                    - ID инфоблока = `$arResult['ID']`
                    - `GLOBAL_ACTIVE = Y`
                    - `ID = $arResult['SECTION']['IBLOCK_SECTION_ID']`
                - Сортировка
                    - `срать`
                - if
                - Записать данные в `$arResult['MAIN_SECTION']`
                } else {
                `$arResult['MAIN_SECTION'] = $arResult['SECTION']`
                }
    - Родитель раздел
        - `$arResult['MAIN_SECTION']`

## Фильтр

- Источник
    - Из компонента список новостей

## Элементы каталога 📚

- **Источник**: из компонента список новостей
    - **Фильтрация**:
        - `FILTER_NAME` - в документации
            - Имя глобальной переменной: `global $arrFilter; $arrFilter = [];`
            - Если установлен `$_REQUEST['SECTION_CODE']`, то `$arrFilter['=SECTION_CODE'] = $_REQUEST['SECTION_CODE'];`
            - `$arParams['FILTER_NAME'] => 'arrFilter'`

### Инфоблок

- Картинка анонса + ресайз
- Множественный список / 2 отдельных свойства типа список (настройка флажок) = `Y`
- Название
- Символьный код - обязательный/уникальный/транслитится из названия
- Текст анонса
- Свойство вес (число целое) = значение + описание значения
- Свойство кол-во в коробке (число целое) = значение + описание значения
- Свойство кол-во на паллете (число целое) = значение + описание значения

# Страница детальная 📖

- **Цепочка навигации**: смотрим выше + настройка компонента новость детальная - вставляем над компонентом

### Инфоблок

- Свойство галерея (файл) + множественное
    - Ресайз
    - Вывод в слайдер
- `new/top` - со страницы списка
- Свойство бренд - привязка к элементу другого инфоблока
    - Создаем инфоблок `Бренды`
        - Название
    - Вывод
- Название
- Текст анонса
- Свойство рекомандации по выпеканию (тип файл)
    - Ссылка открывается в новом окне
- Фасовка - со страница списка
- Свойство условие хранения (строка) множественное + описание
    - Вывод
- Свойство состав (текст)
- Пищевая ценность (строка) множественное + описание
    - Вывод
- Свойство следующий продукт (привязка к элементу инфоблока)
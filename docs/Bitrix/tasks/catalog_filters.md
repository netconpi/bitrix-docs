# Задание на фильтрацию

```
Фильтр
    формирование
        визуал
            обернуть в тег form (или заменить верхний div)
            проверяем что у всех значимых элементах стоит name|value (input, select)
        значения
            топ продаж
                да/нет (top=y || top=null)       
            бренд - тип привязка к элементу
                ciblockelement:getlist
                    Фильтр
                        текущий раздел
                        активность
                    GroupBy
                        PROPERTY_brand
                            $item['PROPERTY_BRAND_VALUE'] = null
                            $item['PROPERTY_BRAND_VALUE'] = значение 3
                            $item['PROPERTY_BRAND_VALUE'] = значение 1
                            $item['PROPERTY_BRAND_VALUE'] = значение 4
                            $item['PROPERTY_BRAND_VALUE'] = значение 2
                        $brandIds = [] = записываем уникальные не пустые значения
                        if (!$brandIds) {
                            $brandIds = ['xxx'];
                        }

                        $filterList = [];
                        $filterList['brand'] = ciblockelement:getlist
                            Фильтр
                                ID = $brandIds
                                активность
            жирность - тип строка
                ciblockelement:getlist
                    Фильтр
                        текущий раздел
                        активность
                    GroupBy
                        PROPERTY_brand
                            $item['PROPERTY_FAT_VALUE'] = null
                            $item['PROPERTY_FAT_VALUE'] = значение 3
                            $item['PROPERTY_FAT_VALUE'] = значение 1
                            $item['PROPERTY_FAT_VALUE'] = значение 4
                            $item['PROPERTY_FAT_VALUE'] = значение 2
                        $filterList['fat'] = [] = записываем уникальные не пустые значения
        выделение
            топ продаж
                ($_REQUEST['top'] == #VALUE#) checked
            бренд - тип привязка к элементу
                ($_REQUEST['brand'] == $item['ID']) selected
            жирность - тип строка
                ($_REQUEST['fat'] == $item) selected
        результат
            /ссылка/?
            + параметры name=value
            top=y
            brand=ID бренда
            fat=строка
    фильтрация
        ciblockelement:getlist - отсюда
            типам свойств
                ($_REQUEST['top'] == #VALUE#)
                    $arrFilter['PROPERTY_TOP_VALUE'] = 'y';

Сортировка
    https://dev.1c-bitrix.ru/api_d7/bitrix/main/web/cookie/index.php?ysclid=lto53h97sf643692616

```
# Bitrix Cheatsheet

**`CMain::` == $APPLICATION**

| Docs Location | Path  | Command  | Usage example | Пояснение  |
| --- | --- | --- | --- | --- |
| Главный модуль > Page > Asset (с версии 14.9.4) (D7) | use Bitrix\Main\Page\Asset; |  addJS  addCSS  addString   | Asset::getInstance()->addJs(SITE_TEMPLATE_PATH . "/js/fix.js"); | Добавление стилей по API |
| Главный модуль > Классы > CMain (для разработчиков) | CMain:: | GetCurPage() | $APPLICATION->GetCurPage() | Поучение в template.php ссылку на текущую страницу  |
| Главный модуль > Классы > CMain | CMain:: | GetDirProperty | GetDirProperty("<Наименование переменной>", "<Ссылка на страницу с переменной >") | Поучение информации о странице по ее адресу  |
| D7 Diag/Debug | use Bitrix\Main\Diag\Debug; | writeToFile | Debug::writeToFile($_SERVER); | запись результата в файл, что бы Debug был в файле.  |
| Главный модуль Классы CFile ResizeImageGet | /** @global CFile $CFile */ | ResizeImageGet | CFile::ResizeImageGet($picture['ID'], array("width" => 40, "height" => 40), BX_RESIZE_IMAGE_PROPORTIONAL); | Изменение размера изображения  |
| Главный модуль Классы CUtil GetAdditionalFileURL | /** @global CUtil $CUtil */ | GetAdditionalFileURL | CUtil::GetAdditionalFileURL($image_resize['src'], true); | Получение ссылки на файл  |
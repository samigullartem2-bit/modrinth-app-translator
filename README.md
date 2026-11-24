# Modrinth App Translator

Автоперевод описаний модов в лаунчере **Modrinth App** (Windows) через Google Translate.
Auto-translates mod descriptions inside the **Modrinth App** launcher (Windows) using Google Translate.

> Неофициальный проект, не связан с Modrinth. / Unofficial, not affiliated with Modrinth.

## Как это работает

Лаунчер рисует интерфейс через WebView2. Скрипт запускает лаунчер с включённым портом отладки
(`--remote-debugging-port=9222`), подключается к нему по Chrome DevTools Protocol и внедряет JS,
который переводит текст описания, не трогая картинки, ссылки и код. Сами запросы к переводчику
делает Python, поэтому ограничения лаунчера на сетевые запросы не мешают.

## Установка

1. Установи [Python](https://www.python.org/downloads/) (на первом экране отметь **Add Python to PATH**).
   Заглушка Python из Microsoft Store не подойдёт.
2. Скачай репозиторий и положи в постоянную папку (потом её нельзя удалять и переносить).
3. Открой `launch_modrinth.vbs` в блокноте и, если лаунчер стоит не в стандартной папке,
   впиши путь в `CUSTOM_EXE`, например `Const CUSTOM_EXE = "E:\Modrinth App\Modrinth App.exe"`.
   Язык меняется в `LANG_CODE` (`ru`, `uk`, `de`, `pl`...).
4. Запусти `install.bat` (поставит `websocket-client` и создаст ярлык на рабочем столе).
   Если ярлык не появился: правая кнопка на `launch_modrinth.vbs` -> Отправить -> Рабочий стол.
5. Полностью закрой Modrinth App (и в трее) и запускай его через этот ярлык.

Иконку ярлыка можно сменить в его свойствах, указав `Modrinth App.exe`.

## Использование

Открой страницу мода: описание переведётся само. Кнопка справа внизу переключает оригинал и перевод.

## Ограничения

- Только Windows (WebView2). На Linux и macOS не работает.
- Лаунчер нужно запускать через `launch_modrinth.vbs`, обычный запуск перевода не включает.
- Используется бесплатный неофициальный эндпоинт Google Translate. При очень большом числе
  запросов Google может временно ограничить доступ.
- После обновления лаунчера вёрстка может измениться, тогда придётся поправить селекторы
  в `modrinth_app_translator.py` (переменная `SEL` и функция `findContainers`).

## Для сайта modrinth.com

В `browser-userscript/` лежит юзерскрипт для Tampermonkey/Violentmonkey, который делает то же самое на сайте.

## Лицензия

MIT

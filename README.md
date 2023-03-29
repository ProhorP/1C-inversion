# 1C-inversion

За основу взята обработка с GitHub:
https://github.com/EvilBeaver/v8asm

Автор этой обработки описывает работу 1С на уровне байт-кода здесь:
https://habr.com/ru/post/489392/

В учебных целях, а не для принесения ущерба была доработана обработка, для преобразования байт-кода обратно в код на языке 1С.

Для открытия запароленных/закрытых модулей нужно выполнить такой алгоритм:
1. Сделать копию базы
2. Открыть конфигуратор. В конфигураторе "Конфигурация" - "Выгрузить конфигурацию в файлы"
3. Выбрать модуль чего вы хотите открыть: "Общий модуль"/"Модуль обработки". От выбранного значения будет зависеть имя конечного сохраняемоего файла после декомпиляции.
3. Открыть в режиме 1С:Предприятия эту обработку и нажать кнопку "Прочитать закрытый модуль".
Нужно в папке, куда выгрузили конфигурацию выбрать файл закрытого модуля, он будет называться "Module.bin" для общего модуля, и "ObjectModule.bin" для обработки.
Далее сработает стандартный механизм обработки, который срабатывает при нажатии на кнопку "Открыть" - файл будет детально проанализирован и разобран по таблицам с процедурами/константами/параметрами и т.д.
4. Нажать на кнопку "Декомпиляция". Будет проанализированы таблицы обработки и сформирован код 1С. Код будет показан в обработке и автоматически сохранен в том же каталоге, где и закрытый модуль под правильным названием, которое было выбрано в пункте 3.
5. Удалить в папке с закрытым модулем все файлы, кроме файла с расширением "bsl"(это и есть открытый модуль)
6. Открыть конфигуратор. В конфигураторе "Конфигурация" - "Загрузить конфигурацию из файлов".
Если при загрузке будут ошибки - нужно будет снимать конфигурацию с поддержки.

Внимание: когда модули закрывают - из них удаляется форматирование и комментарии, поэтому при обратном преобразовании их не будет. Обфускатор/деобфускатор 1с отсутствует.

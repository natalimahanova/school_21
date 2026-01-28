Exercise 00. First shell script
Turn-in directory: ex00/.
Files to turn in: hh.sh, hh.json.
Allowed functions: curl, jq.
For this exercise, you will interact with the HeadHunter API to parse information about vacancies. To do so, you must understand how both curl and the HeadHunter API work.

Write a shell script that:

gets the name of a vacancy, "data scientist", as an argument (some later exercises will be based on this);
downloads information about the first 20 vacancies that correspond to the search parameters;
stores it in a file named hh.json.
The result in the file must be formatted so that each field is on a different line. See the example in the ex00_sample.json file.

Your script must be executable. The interpreter to use is /bin/sh.

Place your script and the parsing results in the ex00 folder in the src directory of your repository.

## Заметки

Утилиты curl и jq часто используются вместе в скриптах и терминале для работы с данными из интернета: первая загружает данные, а вторая помогает их прочитать и обработать.

### Функция curl (Client URL)
Это «швейцарский нож» для передачи данных по сети. Она позволяет взаимодействовать с серверами по множеству протоколов (HTTP, FTP, SMTP и др.) без использования браузера.

Загрузка данных: Позволяет скачивать файлы или просматривать содержимое веб-страниц прямо в консоли.

Работа с API: Незаменима для тестирования REST API (отправка GET, POST и других запросов с заголовками и токенами).

Отладка: Помогает проверять доступность сайтов, смотреть HTTP-заголовки ответов и тестировать редиректы.

Пример: curl https://api.example.com/data просто выведет текст ответа на экран.

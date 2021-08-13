Создать Ansible-playbook, обеспечивающий установку и запуск простого тестового приложения на Node.js

Базовой системой является CentOS7, установленная в минимальной конфигурации.

В plaubook необходимо предусмотреть следующие шаги:

Убедится, что все пакеты в системе обновлены до последней версии
Установить EPEL-репозиторий
Установить Remi-репозиторий (https://rpms.remirepo.net/enterprise/remi-release-7.rpm), GPG-ключ (https://rpms.remirepo.net/RPM-GPG-KEY-remi)
Создать пользователя для удаленного администрирования, добавить ему RSA-ключ для авторизации и дать ему права sudo
Настроить OpenSSH-сервер (авторизация по паролю отключена, вход пользователю root запрещён)
Установить Node.js и npm
Установить и запустить тестовое Node.js приложение
Проверить его доступность
Состав развернутого сервера:

После работы Ansible-playbook, сервер должен содержать следующие компоненты:

Node.js (самая свежая версия, доступная в EPEL репозитории)
Модуль Express версии 4.x
Простое демонстрационное Node.js приложение (исходный код ниже)
Тестовое приложение:

исходный код тестового приложения app.js
`<
// Load the express module.
var express = require('express');
var app = express();
 
// Respond to requests for / with 'Hello World'.
app.get('/', function(req, res){
res.send('<h1>Hello World!</h1>');
});
 
// Listen on port 80 (like a serious web server).
app.listen(80);
console.log('Express server started successfully.');
Файл с зависимостями:

Файл с описанием зависимостей приложение (Express) с именем package.json должен располагаться в одном каталоге с файлом приложения app.js

{
"name": "examplenodejsapp",
"description": "Example Express Node.js app.",
"dependencies": {
"express": "4.x"
},
"engine": "node >= 0.10.6"
}
>`

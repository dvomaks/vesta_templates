# vesta_templates

### What is this
This repository contains useful config templates for [Vesta CP](https://vestacp.com)

Work with vesta 0.9.8

### Templates list

* Drupal 7
* Redmine
* Laravel 5.1

### Installation
To install thoose templates just:

```sh
cd /usr/local/vesta/data/templates/web
git clone https://github.com/errogaht/vesta_templates.git
cp -R vesta_templates/apache2 .
cp -R vesta_templates/nginx .
rm -R vesta_templates
```
### Для NodeJs

После применения шаблона для nginx будут автоматически сгенерированы конфигурационные файлы по пути /home/{имя пользователя}/conf/web. Давайте подробнее разберем содержимое шаблона, а именно нас интересует строчка:

include /home/vasya/conf/web/nginx.example.com.conf*;

Так как файлы конфигурации nginx - динамические, мы не можем изменять их содержимое, иначе мы потеряем изменения после перегенерации шаблона. Но мы можем создать файл nginx.example.com.conf*, который будет извлечен. Стоить отметить что мы имеем доступ только к блоку server конфигурационного файла, так как include производится именно там. Это сделано так, потому что блок server должен быть сгенерирован автоматически и иметь базовые настройки.

Создайте файлы:

snginx.example.com.conf*
```
location / {
  proxy_pass http://localhost:3000;
}
```
nginx.example.com.conf*
```
location / {
  proxy_pass http://localhost:3000;
}
```

где example.com - Ваш домен.

Это правило гласит - при открытии url / текущего домена произвести перенаправление запроса на http://localhost:3000. Более подробную информацию Вы можете получить тут: https://nginx.ru/ru/docs/http/ngx_http_proxy_module.html. Важно заметить что если Ваш сайт работает с сертификатом, вам не придется указывать его в своем приложение NodeJS, так как nginx будет проксировать все запросы к приложению.

После создания файлов Вам необходимо перезапустить nginx и запустить приложение. После перезапуска при открытии домена, на нем будут отображаться данные с http://localost:3000.
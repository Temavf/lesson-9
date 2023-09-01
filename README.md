
## Задание

1. Написать service, который будет раз в 30 секунд мониторить лог на предмет наличия ключевого слова (файл лога и ключевое слово должны задаваться в /etc/sysconfig).
2. Из репозитория epel установить spawn-fcgi и переписать init-скрипт на unit-файл (имя service должно называться так же: spawn-fcgi).
3. Дополнить unit-файл httpd (он же apache) возможностью запустить несколько инстансов сервера с разными конфигурационными файлами.

## Методичка

https://docs.google.com/document/d/1wXZLFDG7NSsrmeSmL0qqec6H9CFAYIolDfiFbDa2WBU/edit

## Script

```bash
scriptreplay --timing=timing.log --divisor=5 script.log
```

### Мониторинг лога

Выполняем всё по методическе с учетом следующих моментов:
* файл сервиса */etc/systemd/system/watchlog.service* (не указан в методичке);
* файл таймера */etc/systemd/system/watchlog.timer* (не указан в методичке);
* для того, чтобы таймер запустился, необходимо один раз запустить сервис watchlog:
```bash
systemctl start watchlog
```    
В противном случае, сервис таймера сразу переходит в состояние `active (elapsed)`
и не дергает watchlog.
Нормальная работа таймера наблюдается в статусе `active (wating)`.

### spawn-fcgi / apache httpd

Делаем всё по методичке, ошибок не обнаружено.

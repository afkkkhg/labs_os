1.На прошлой паре я установила Ansible.
2.На сегодняшей паре я подготавливала стенд на Vagrant, настраивала ansimble для доступа к стенду, написала плейбук, который устанавливает NGINX в конфигурации по умолчанию, с применением модуля yum, подготовила шаблон jinja2 новой конфигурации для nginx, чтобы сервис слушал на стандартном порту 8080, добавила в плейбук копирование новой конфигурации сервиса на стенд, использовала механизм notify для рестарта nginx после установки или изменения конфигурации и вводила на проверку, полученный айпишник.
3.Проверяем версии python и ansible.
4.Далее подготавливаем стенд, создаем каталог ansible, в этом же каталоге копируем присланные файлы и за одно проверяю вагрант на ошибки.
5.Подключаем к хосту, чтобы к нему подключиться мы используем команду vagrant ssh-config (узнаем параметры).
6.Создаем файл inventory, который поможет ansible управлять нашим хостом, добиваясь результата SUCCESS
7.Создаем файл конфигурации ansible.cfg, чтобы каждый раз не указывать инвентори файл в командной строке.
8.Из инвентори убираем информацию о пользователе и убеждаемся, что управляемый хост доступен.
9.Далее пользуемся командами Ad-Hoc; тоесть просматриваем ядро, установленное на хосте; проверка статуса сервиса firewalld; установка пакета epel-release.
10.Написали простой Playbook; создали файл epel.yml, далее проверили правильность и дееспособность данного файла, после вводили команду ansible nginx -m yum -a "name=epel-release state=absent" -b - чтобы посмотреть разницу в выводе.
11.Теперь нам надо написать Playbook-а для установки NGINX, делаем все по-шагово.
12.За основу взяли уже созданный нами плейбук epel.yml, теперь его будем дополнят, так же добавляем tags, вводим их все поочередно в консоль.
13.Создаем файл nginx.conf.j2 для конфига NGINX, и добляем в Playbook задачу, которая копирует подготовленный шаблон на хост (используем модуль template).
14.Для конечной работоспособности Playbook мы добавили секции handler и notify для рестарта nginx (применяется модуль systemd).
15.Далее мы занимались исправлением ошибок в Playbook, после поправки вводим команду ansible-playbook nginx.yml - просмотр работы Playbook.
16.Проверяем работу NGINX на нестандартном порту, выясняем IP адрес по команде vagrant ssh -c "ip addr show".
17.Выбираем 3 IP адрес т к он являемся публичным и кнему можно обращаться.
18.Вводим в поисковую строку и готово.

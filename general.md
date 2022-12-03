##### BASIC SETTINGS UBUNTU

```
sudo ap-get update  
sudo apt-get upgrade  
sudo apt install ubuntu-restricted-extras libavcodec-extra libdvd-pkg  
sudo dpkg-reconfigure libdvd-pkg  
sudo apt install adobe-flashplugin  
sudo apt install chrome-gnome-shel wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb  
sudo apt install ./google-chrome-stable_current_amd64.deb  
sudo snap remove firefox  
lsb_release -a // можно узнать релиз ОС  
uname -a //   
gnome-shell --version // версия gnome   
sudo snap install code --classic // установка vscode
```

```
sudo apt install mysql-server mysql-client // пакет для mysql
sudo update-alternatives --config php // меняем версию php
```

```
lscpu // оперативка  
free -m // место на диске  
cat /proc/cpuinfo | grep processor // чтобы определить сколько ядер имеет процессор  
su - // переключения на root  
cat /etc/passwd // список пользователей  
cat /etc/group // список групп  
id // инфо о пользователи
```

##### DOWNLOAD COMPOSER
`sudo apt install composer`

##### CHANGE PASSWORD
```
vim /etc/pam.d/common-password  
password     [success=1 default=ignore]    pam_unix.so obscure sha512  => chnage => password     [success=1 default=ignore]    pam_unix.so sha512 minlen=L
```

##### DATABASE INSTALL AND BASIC SETTINGS & LAMP
```
sudo tasksel install lamp-sever  
sudo systemctl enable --now mysql // автозапуск базы  
sudo systemctl enable --now apache2 // автозапуск apache  
sudo mysql_secure_installation  
sudo apt install phpmyadmin
```

```
sudo mysql -u root  
SELECT User, Host, plugin FROM mysql.user;  
show variables like 'validate_password%';  
SET GLOBAL validate_password_length=4;  
FLUSH PRIVILEGES;  
exit  
sudo service mysql restart  
  
CREATE DATABASE test;  
SHOW DATABASES LIKE '%';
```

##### CHANGE PRIVILEGE:
```
chmod 777 name_file // 4 - read(право на чтение); 2 - write(право на запись); 1 - execute(право на выполнение)
```

##### DOCKER

```
sudo apt install docker.io // установка docker  
sudo systemctl status docker // статус docker  
sudo groupadd docker // группа, для доступа по команде docker  
sudo usermod -aG docker $USER // добавляю текущего пользователя  
sudo usermod -aG docker ${USER}  // добавляю текущего пользователя  
ctrl+c // exit  
apt update  
apt install mc
```

```bash
sudo systemctl enable docker.service  
sudo systemctl enable containerd.service  
sudo systemctl enable docker  
  
sudo docker run -it ubuntu bash  
docker // вывод запущенных контейнеров  
docker ps -a // вывод всех контейнеров  
docker start container_name // запуск контейнера  
docker rename old_name new_name  
docker stop container_name // остановка контейнера  
docker run -h alisher02 --name containerName -it ubuntu bash // создание контейнера   
docker logs containerName // история контейнера  
docker rm $(docker ps -aq) // удаление всех контейнеров  
docker rmi $(docker images -q) // удвлвние всех образов  
  
docker run -d bitnami/apache  
docker run -it --name container_name --hostname alisher02 ubuntu bash // создание контейнера с название => container_name, и с хостом => alisher02, images => ubuntu, command => bash  
#apt update  
#apt install cowsay  
#ln -s /usr/games/cowsay /usr/bin/cowsay  
#cowsay "test"  
  
docker commit test user_name/repository_name  
docker images  
docker run alish02/test cowsay "TEST"  
docker push alish02/test  
  
docker stop container_name  
docker run -d -p 8000:8080 bitnami/apache // образ  
docker images // список всех образов  
docker attach container_name //  подключение к контейнеру  
  
docker-compose build // собирает контейнер  
docker-compose up -d // запуск + собирает контейнер  
  
chmod -R guo+w storage // права  


docker run -d -p 80:80 --name nginx nginx:latest  
docker swarm leave --force  
docker exec -it container_name bash // запуск в bash  
docker-compose down // удаление  
docker exec container_name service_name(nginx) -s reload // обновление сервиса  
docker rm -f container_name // удаляет запущенный контейнер  
docker exec // для того чтобы зайти в контейнер (выполняет команду в контейнере)  
docker exec -it (для того чтобы интерактивно и выделяет terminal) container_name bash
```

##### PORT LIST
```
21 – ftp;  
22 – ssh;  
23 – telnet;  
25 – smtp;  
43 – whois;  
53 – dns;  
80 – http;  
115 – sftp;  
443 – https;  
3306 – mysql;  
8080 – http (альтернативный)
```

##### ВЗАИМОДЕЙСТВИЕ КЛИЕНТА И СЕРВЕРА
>Сперва у сервера открывается server socket и у клиента(браузер) открывается socket (socket состоит из ip и порт:127.0.0.1:8080). Клиент отдает свой socket запрос, например открой ка мне google.com и сервер отрабатывает этот запрос и также отдает ответ с кодом(js, php, html, css картинки). У клиента всегда порт > 1000, и ip тоже разные. В компьютере 65535 портов.  
Прокси сервер - это компьютер выполняющий роль посредника между пользователем и целевым сервером.

##### NVIDIA
```bash
nvidia.com/Download/index.aspx // по этой ссылке можно узнать какой драйвер установить   
sudo nvidia-smi // проверяем драйвера (если нету устанавливаем)  
sudo apt install nvidia-driver-510 (510 - версия драйвера)  
sudo prime-select nvidia // (применяем + перезагрузка)
```

##### NGINX
```bash
systemctl enable nginx// разрешение на автозапуск  
systemctl is-enabled nginx // проверка  
nginx -T // выведет конфиги nginx  
service nginx -s reload  
systemctl nginx restart
sudo ln -s /etc/nginx/sites-available/domain_name.conf /etc/nginx/sites-enabled/ // symbol link for nginx
service php7.4-fpm stop
ls /run/php
```

##### APACHE2
```apacheconf
sudo service mysql status // статус  
hotname -i  
sudo chown $USER:$USER /var/ww/domain_name  
sudo nano /etc/apache2/sites-available/domain_name.conf  
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName test
    ServerAlias www.test
    DocumentRoot /var/www/test
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    <Directory /var/www/test>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
sudo a2ensite domain_name  
sudo apache2ctl configtest
sudo a2enmod php8  
sudo apt-get install php7.4-mbstring  
sudo apt-get install libapache2-mod-php7.4  
sudo apt-get install php7.2-mysql  
sudo apt-get install php7.4-gd  
sudo apt policy phpmyadmin
systemctl reload apache2  
a2enmod rewrite // for .htaccess
```

##### GIT
```bash
git pull merge master // для своей ветки  
git push origin import_excel --force  
git reset --hard HEAD~ // удаляет последний коммит в локальной ветке  
git push -f // как только вернули коммит, надо удаленно еще сделать push чтобы и там исчезла  
git cherry-pick 63ec2ae3 // можно получить один коммит  
git rm -r --cached bitrix/managed_cache // удаляет из локального репозиторий  
git stash branch [branch-name] [stash]  
git show -s —pretty=raw commit_number // отобразить то что мы изменили  
  
git ls-tree tree_number // дерево изменений  
git show commit_kesh // коммит то что мы изменили  
git reset HEAD file_name // для того чтобы убрать из индекса  
git reset HEAD ~1 // для того чтобы убрать с commit (указываю количество коммитов)  
git reset --merge HEAD~1
git reflog

git reset --soft HEAD^


git revert commit_kesh // обратно вернуть с удаленного репозиторий (если сделал push коммит)  
  
git merge --abort // отмена merge  
git diff // интерфейс  
  
git stash save "description" // добавляю в stash  
git stash list // список stash  
git stash apply "stash@{0}" // возвращает с stash не удаляет stash  
git stash pop "stash@{0}" // возвращает с stash и удаляет stash  
git stash drop // delete all stash or (git stash drop "stash@{0}")  
  
git remote -v // можно узнать откуда и куда отправляю  
git remote remove origin // remove origin in locale  
git remote add origin https://gitlab.com/alish02/test2.git // add new origin for locale  
git push --set-upstream origin dev // for add new origin after =>  git remote add origin https://gitlab.com/alish02/test2.git  
git blame file_name // who edit file  
git log --pretty=format:"%h %s" --graph // for view log pretty
```

##### РЕГУЛЯРКА
```
.   => любой один символ  
[]  => любой один указанный символ  
[^] => отрицание  
*   => пред. символ может встречаться или нет  
^   => вначале строки  
$   => в конце строки
```

##### ТЕОРИЯ
```
- Виртуализация - технология, которая позволяет запускать несколько ОС на одном физическом сервере. 

- Docker - программное обеспечение для автоматизации развертывания и управления приложениями в средах с поддержкой контейнеризации, контейнеризатор приложений  
- Виртуальный хостинг - это когда ресурс одного сервера делят между многими сайтами. У этих сайтов все одинаковые ip, если у одного сайта будет бамбит то все сайты будет тормозить  

- Виртуальный сервер - это когда физический сервер делят на несколько виртуальных, также его называют VDS (виртуальный выделенный сервер). У каждого сайта есть свой ресурс и они не зависят друг от друга

- Выделенный сервер - это когда весь сервер отдают на аренду, клиентам дается полный доступ к аппаратному и программному обеспечению, они могут самостоятельно устанавливать нужные операционные системы, менять конфигурацию и совершать любые технические работы

- Облачные сервисы — это сеть мощных компьютеров — серверов, которые позволяют клиентам пользоваться своими ресурсами через интернет: хранить файлы и обмениваться ими, работать в онлайн-офисах, производить вычисления.

- CMS - готовая система, которой воспользоваться может **не программист**.  
Ее можно программировать, но обычно предпочитают не заморачиваться с этим, а искать уже готовые (созданные программистами) модуля CMS под ту или иную задачу  
  
- Фреймворк - это сырая заготовка **для программиста.**  
Без приложения более-менее значительных программистких усилий вы воооооооооообще ничего не получите, никакого результата.
```
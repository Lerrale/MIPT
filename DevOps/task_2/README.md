#### Решение задания расположено по ссылке [ссылке](https://gitlab.com/ledneva.valeriya/hw2_continuous_integration.git)

**Цель задания**

Научиться собирать docker-compose сборку из предыдущего задания и разворачивать в автоматическом режиме на сайте.

**Часть 1 (сборка образов)**

Соберите Job, в котором будет собираться образ из предыдущего задания и заливаться в Container Registry на сайте https://gitlab.com. Для этого необходимо сделать следующие шаги:

- Создайте репозиторий на сайте gitlab.com, в котором необходимо будет настроить CI.
- Для настройки задания в Gitlab создайте файл .gitlab-ci.yml, в котором будет настроен pipeline для сборки.
- Создайте файл docker-compose.yml, который соединяет в одну конфигурацию образы из предыдущего задания. Образы называем nginx-customized, postgres-customized.
- Создайте job build_images, который соберет образы nginx-customized и postgres-customized. После сборки образа необходимо будет залить образы (docker push) в Registry сайта gitlab.com (вкладка в проекте Deploy → → Container Registry). Для job используйте тег gitlab-org-docker для runner-а внутри job, который позволяет использовать команду docker для runner-ов на сайте gitlab.com.
- Создайте файл docker-compose-deploy.yaml из файла docker-compose.yaml, в котором замените опции build внутри services на опцию image с собранными названиями образов в Docker Registry из шага 4.
  
**Часть 2 (Deploy)**

Создайте job deploy_compose, который будет делать следующие шаги:

- Настроит SSH-соединение на сервер в пользователя studentXX по адресу master.hadoop.akhcheck.ru (46.XXX.XXX.XXX) (“виртуалка”).
- По scp копирует файл docker-compose-deploy.yaml в файл docker-compose.yaml
- Для каждого пользователя будет выделен порт 350XX для nginx. Для тестов дополнительно будет выделен порт 450XX для postgres.
- Запустит команду docker-compose up -d. После корректного запуска команды по адресу http://master.hadoop.akhcheck.ru:350XX будет доступна страница nginx.

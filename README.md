# ECサイトのインフラ

## 仕様

### 前提

以下がサーバー(ホスト)にインストール済み

- git
- Docker
- docker-compose

## 設定方法

### サーバー起動（Docker）

```bash
cd /path/to/ec-infra
git submodule update --init --recursive
docker-compose up -d
```

### 設定

composerを設定

```
$ docker-compose exec app bash

# php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# php -r "if (hash_file('sha384', 'composer-setup.php') === 'c31c1e292ad7be5f49291169c0ac8f683499edddcfd4e42232982d0fd193004208a58ff6f353fde0012d35fdd72bc394') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
# php composer-setup.php
# php -r "unlink('composer-setup.php');"
# mv ./composer.phar /usr/bin/composer
```

初期設定

```
$ docker-compose exec app bash

# cd /var/www/html/cms
# cp ./.env.docker .env
# php artisan key:generate
# php artisan migrate
# composer install
# chmod -R 777 public/
# chmod -R 777 storage/

# cd /var/www/html/cms
# cp ./.env.docker .env
# php artisan key:generate
# composer install
# chmod -R 777 public/
# chmod -R 777 storage/

```


### 動作確認

80番・8080番ポートからアクセスできることを確認する

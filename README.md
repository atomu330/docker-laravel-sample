# DockerでLaravelを動かすときのひな型フォルダ群

## 本リポジトリを使用したLaravelの起動方法

### 1.本リポジトリをローカルにクローンする

git clone https://github.com/atomu330/docker-laravel-sample.git

### 2.使用したい環境に併せて適宜ファイルを更新する

 - app/000-default.confのDocumentRoot
 - docker-compose.ymlのcontainer_name（3つとも）
 - その他は環境に応じて変える

### 3.コンテナを立ち上げる

docker-compose up -d --build


### 4.Laravel資産をインストールする
// コンテナに入る
docker-compose exec php-apache /bin/bash

// 資産のインストール
cd /var/www/html
git clone [Laravel資産リポジトリ]

// パーミッションエラー対応
chmod 777 /var/www/html/laravelapp/storage/logs/laravel.log
chmod 775 /var/www/html/laravelapp/storage/logs/
chmod -R gu+w /var/www/html/laravelapp/storage
chmod -R guo+w /var/www/html/laravelapp/storage

// .envの作成
cp -p .env.copy .env

// Laravelセットアップ
composer install
php artisan key:generate
php artisan config:cache
php artisan migrate

### 5.アクセスできること確認する
http://localhost


## Dockerコマンド

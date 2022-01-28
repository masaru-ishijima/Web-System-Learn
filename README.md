# 構築手順：
## 1.	下記環境をインストールする。
- Git
- Docker
- Docker Compose
## 2.	[コマンドプロンプト]または[ターミナル]でソースコードをcloneし、そのディレクトリに移る
(cloneする場所はデスクトップ推奨)
```sh
git clone https://github.com/masaru-ishijima/Web-System-Learn.git
cd Web-System-Learn
```
## 3.	Docker Composeを立ち上げる
```sh
docker-compose build
docker-compose up
```
## 4.	起動中にmysqlのcliクライアントを起動する
```sh
docker exec -it mysql mysql techc
```
## 5.	ソースコード内のinit.sqlの内容を入力し、テーブルを作成する
```sql
CREATE TABLE `users` (
    `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `name` TEXT NOT NULL,
    `email` TEXT NOT NULL,
    `password` TEXT NOT NULL,
    `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);

ALTER TABLE `users` ADD COLUMN icon_filename TEXT DEFAULT NULL;

ALTER TABLE `users` ADD COLUMN introduction TEXT DEFAULT NULL;

ALTER TABLE `users` ADD COLUMN cover_filename TEXT DEFAULT NULL;

ALTER TABLE `users` ADD COLUMN birthday DATE DEFAULT NULL;

CREATE TABLE `user_relationships` (
    `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `follower_user_id` INT UNSIGNED NOT NULL,
    `followee_user_id` INT UNSIGNED NOT NULL,
    `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE `bbs_entries` (
    `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `user_id` INT UNSIGNED NOT NULL,
    `body` TEXT NOT NULL,
    `image_filename` TEXT DEFAULT NULL,
    `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
);
```
## 6.	動作確認
`http://サーバーアドレス/timeline.php` からサービスの動作を確認する

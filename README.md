# LaratterTuter

Laravel で構築した Twitter 風の SNS アプリケーションです。

## 主な機能

- ユーザー登録・ログイン（Laravel Breeze）
- ツイートの CRUD（作成・閲覧・編集・削除）
- いいね（お気に入り）機能
- マイページ（自分のツイート一覧）

## 技術スタック

- PHP 8.1+
- Laravel 10
- MySQL 8.0
- Tailwind CSS / Alpine.js
- Vite
- Docker（Laravel Sail）

## セットアップ

### 前提条件

- Docker Desktop がインストールされていること
- Git がインストールされていること

### 1. リポジトリのクローン

```bash
git clone <repository-url>
cd LaratterTuter
```

### 2. 環境変数の設定

```bash
cp .env.example .env
```

`.env` を開き、DB 接続情報を Sail 用に編集します。

```
DB_HOST=mysql
DB_DATABASE=larattertuter
DB_USERNAME=sail
DB_PASSWORD=password
```

### 3. Composer 依存パッケージのインストール

Docker 環境を使って Composer をインストールします。

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php81-composer:latest \
    composer install --ignore-platform-reqs
```

### 4. Laravel Sail の起動

```bash
./vendor/bin/sail up -d
```

以下のサービスが起動します。

| サービス     | URL / ポート              |
| ------------ | ------------------------- |
| アプリ       | http://localhost          |
| phpMyAdmin   | http://localhost:8080     |
| Mailpit      | http://localhost:8025     |
| MySQL        | localhost:3306            |
| Redis        | localhost:6379            |
| Vite (HMR)  | localhost:5173            |

### 5. アプリケーションキーの生成

```bash
./vendor/bin/sail artisan key:generate
```

### 6. データベースのマイグレーション

```bash
./vendor/bin/sail artisan migrate
```

### 7. フロントエンドのビルド

```bash
./vendor/bin/sail npm install
./vendor/bin/sail npm run dev
```

本番用ビルドの場合:

```bash
./vendor/bin/sail npm run build
```

### 8. 動作確認

ブラウザで http://localhost にアクセスし、アプリケーションが表示されれば完了です。

## よく使うコマンド

```bash
# Sail の起動 / 停止
./vendor/bin/sail up -d
./vendor/bin/sail down

# Artisan コマンド
./vendor/bin/sail artisan migrate
./vendor/bin/sail artisan migrate:fresh   # DB を再作成
./vendor/bin/sail artisan tinker          # REPL

# テスト
./vendor/bin/sail test
```

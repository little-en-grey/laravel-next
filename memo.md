## Docker立ち上げ
1. rootディレクトリで`docker-compose up -d --build`を実行 

## バックエンド
### Laravel Project作成
1. apiコンテナに入る
2. `/app`　配下で `composer create-project laravel/laravel .` を実行
### .envの編集
> TZなど
```ini
APP_TIMEZONE=UTC
APP_URL=http://localhost

APP_LOCALE=en
APP_FALLBACK_LOCALE=en
```
↓
```ini
APP_TIMEZONE=Asia/Tokyo
APP_URL=http://localhost:8000

APP_LOCALE=ja
APP_FALLBACK_LOCALE=ja
```
> DB設定など
```ini
DB_CONNECTION=sqlite
# DB_HOST=127.0.0.1
# DB_PORT=3306
# DB_DATABASE=laravel
# DB_USERNAME=root
# DB_PASSWORD=

SESSION_DRIVER=database
```
↓
```ini
DB_CONNECTION=mysql
DB_PORT=3306            # dockerで設定したports
DB_DATABASE=database    # dockerで設定したMYSQL_DATABASE
DB_USERNAME=user        # dockerで設定したMYSQL_USER
DB_PASSWORD=password    # dockerで設定したMYSQL_PASSWORD
DB_HOST=gl_db           # コンテナ名

SESSION_DRIVER=file
```

> ログ出力
```ini
LOG_CHANNEL=stack
```
↓
```ini
LOG_CHANNEL=daily
```
### Laravel Sanctumインストール
```shell
php artisan install:api
```

### マイグレーションファイルの作成
```shell
php artisan make:model [モデル名] -a
```

### マイグレーションファイルの適用
```shell
php artisan migrate
```

### シーダーの適用
```shell
php artisan db:seed
```


## フロントエンド
### Nuxt Project(仮)作成
1. webコンテナに入る
2. `/app` 配下で `npx nuxi@latest init ./` (仮)を実行


## 参考
- [LaravelとVueのプロジェクトを分離してDocker上にローカル環境を構築する](https://qiita.com/Sxun0325/items/d4515a69d5fe32c9e3af)
- [【Laravel11 Sanctum】SPA認証](https://macocci7.net/blog/2024/05/02/%E3%80%90laravel11-sanctum%E3%80%91spa%E8%AA%8D%E8%A8%BC/)
- [【Laravel】SanctumでAPIトークン認証の使い方とSPA認証との比較](https://qiita.com/104dev/items/0787a81f7dda892ce86a)
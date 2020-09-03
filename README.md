# 参考記事

https://qiita.com/kyhei_0727/items/e0eb4cfa46d71258f1be

※最新バージョンに対応するためいくつかコマンド内容を修正

# getting started

# Django＋Gunicorn用のベースイメージ作成

Gitから本レポジトリを取得し、カレントディレクトリを本レポジトリに移動する。

その後、dockerfileをビルドする。

参考記事ではdjango2.1だが、ここではdjango3.0とする。

```
$ docker build -t django3.0 -f ./django/Dockerfile.base ./django
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
django2.1           latest              c391e4c70e98        6 minutes ago       960MB
python              3.7                 825141134528        4 weeks ago         923MB
```

## Djangoプロジェクトのローカルへの作成

```
$ cd django
$ docker run --rm \
--mount type=bind,src=(pwd),dst=/opt/apps \
django3.0 \
django-admin startproject my_docker_project .
```

## Docker Composeでupする

```
docker-compose up --build
```

各コンテナが立ち上がった後、http://localhost:80にアクセスする。

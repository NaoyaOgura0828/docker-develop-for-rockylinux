# docker-develop-for-rockylinux
[Docker](https://www.docker.com/)で[RockyLinux](https://rockylinux.org/ja/)開発環境を構築する。

<br>

# Requirement
[Fedora](https://fedoraproject.org/ja/)38ローカル環境で実行確認済。
<br>
[VSCode](https://code.visualstudio.com/Download)と以下のVSCode拡張機能をInstallする。
- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
- [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)

<br>

# Installation
git cloneコマンドで本Repositoryを任意のディレクトリ配下にcloneする。

<br>

## 実行ユーザー名の設定
[.env](./.env)内の`USER_NAME`にコンテナ起動後の実行ユーザーを設定する。

```
USER_NAME = ${実行ユーザー名}
```

<br>

## コンテナイメージ名の設定
[.env](./.env)内の`IMAGE_NAME`を任意のコンテナイメージ名に変更する。

```
IMAGE_NAME = ${コンテナイメージ名}
```

<br>

> **Warning**<br>
> コンテナイメージは以下の命名規則に従うこと。<br>
> `^[a-z0-9][a-z0-9_.-]{1,}$`

<br>

> **Note**<br>
> [DockerHub](https://hub.docker.com/)へコンテナイメージのPUSHを想定する場合は以下の命名規則に従うこと。
> ```
> IMAGE_NAME = ${DockerHubユーザー名}/${コンテナイメージ名}:${タグ名}
> ```

<br>

## コンテナ名の設定(Optional)
[.env](./.env)内の`CONTAINER_NAME`を任意のコンテナ名に変更する。
<br>
コンテナ名が起動中のコンテナと重複しないように留意する。

```
CONTAINER_NAME = ${コンテナ名}
```

<br>

## ボリューム名の設定(Optional)
[.env](./.env)内の`VOLUME_NAME`を任意のボリューム名に変更する。
<br>
ボリューム名が起動中のコンテナと重複しないように留意する。

```
VOLUME_NAME = ${ボリューム名}
```

<br>

## ネットワーク名の設定(Optional)
[.env](./.env)内の`NETWORK_NAME`を任意のネットワーク名に変更する。
<br>
ネットワーク名が起動中のコンテナと重複しないように留意する。

```
NETWORK_NAME = ${ネットワーク名}
```

<br>

## HostがLinux以外の場合(Optional)
HostがLinux以外の場合は、[docker-compose.yml](./docker-compose.yml)内の`Valid only if the host OS is Linux`とコメントされている行をコメントアウトする。

```yml
    volumes:
      - /etc/passwd:/etc/passwd:ro # Valid only if the host OS is Linux
      - /etc/group:/etc/group:ro # Valid only if the host OS is Linux
```

<br>

# Usage

## コンテナ実行
本Repository直下([docker-compose.yml](./docker-compose.yml)が存在するディレクトリ)で以下のコマンドを実行する。

```bash
docker compose up -d --build
```

<br>

## コンテナ環境へのアクセス
1. VSCodeの拡張機能左メニューから拡張機能`リモートエクスプローラー`を押下する。

<img src='images/RemoteDevelopment_RemoteExplorer.png'>

<br>

2. プルダウンを`開発コンテナー`に変更し、コンテナ一覧から本リポジトリ名にマウスオーバーする。

<img src='images/RemoteDevelopment_DevContainer.png'>

<br>

3. 右側に表示される`新しいウィンドウでアタッチする`を押下する。

<img src='images/RemoteDevelopment_AttachNewWindow.png'>

<br>

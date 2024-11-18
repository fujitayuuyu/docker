# 1 kaliへのdockerのインストール
## (1) 必要なもののインストール
まずcurlやgnupg2などの事前に必要となるものをインストールします（docker-composeのインストールは後半で）。
```
sudo apt -y install curl gnupg2 apt-transport-https software-properties-common ca-certificates
```

## (2) DockerのGPGキーをインポート：
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-archive-keyring.gpg
```
（gpgキーはセキュリティ関連のものです）

## (3) DockerのリポジトリをKaliに追加
```
echo "deb [arch=amd64] https://download.docker.com/linux/debian buster stable" | sudo tee  /etc/apt/sources.list.d/docker.list
```
このコマンドでリポジトリのURLをKali中の/etc/apt/sources.list.d/docker.listに追加してくれる。

## (4) 一旦アップデート(Dockerのリポジトリの追加の適用)
```
sudo apt update
```

## (5) dockerのインストール
```
sudo apt install docker-ce docker-ce-cli containerd.io
```
（Do you want to continue?はYesと答える。）

## (6) これらのインストールにより、”docker”というグループが新しく作られるから、自身のユーザーアカウントをそのグループに追加しておく：
```
sudo usermod -aG docker $USER
newgrp docker
```
こうすることでDockerを実行する際に一々sudoをつける必要がなくなる。

## (7) docker versionと打ち込んでインストールされてるはずのDocker情報が出るか確認。
```
docker-compose
```

## (8) docker-composeをKaliに入れる
次のコマンドを一気に、そのままターミナル上にコピペして実行する：
```
curl -s https://api.github.com/repos/docker/compose/releases/latest | grep browser_download_url  | grep docker-compose-linux-x86_64 | cut -d '"' -f 4 | wget -qi -
```

## (9) 取得された実行ファイルに実行権限を与える
```
chmod +x docker-compose-linux-x86_64
```
## (7) PATHに追加する：
```
sudo mv docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
```
docker-composeのバージョンを確認して完了：
```
docker-compose version
```
# 2 参考資料
https://qiita.com/Hashibirokou/items/c9104f2da834000cfe2a

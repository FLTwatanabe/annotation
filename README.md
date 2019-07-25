# vatic_annotation
Generate annotation data using Vatic
## Installation
Vatic is installed into docker container.
### docker installation
https://qiita.com/n-yamanaka/items/ddb18943f5e43ca5ac2e
### vatic installation
https://qiita.com/wakaba130/items/b0db5c5af4d1ecdaf985
## Operation
### Directory structure
```
~/vatic/data/labels.txt
~/vatic/data/videos_in/<your_video>
$ cd vatic/
```
### docker operation
```
# initial
# local volume is mounted on the container
$ docker pull npsvisionlab/vatic-docker
$ docker run -it -p 8111:80 -v $PWD/data:/root/vatic/data npsvisionlab/vatic-docker /bin/bash

# 起動中コンテナ表示
$ docker container ls
# 停止中コンテナも含めて表示
$ docker container ls -a
# コンテナ停止
$ docker contaier stop <conateir_id>
# コンテナ再起動
$ docker contaier start <container_id>
# コンテナ入る
$ docker exec -it <contaier_id> /bin/bash
```

### ファイル修正
```
# cd root/vatic/
# vi cli.py

Line No.933, 934
file.write("<height>{0}</height>".format(video.width))
file.write("<width>{0}</width>".format(video.height))
>>
file.write("<height>{0}</height>".format(video.height))
file.write("<width>{0}</width>".format(video.width))
```
### １動画終わったら
* Webアプリにおいて save ボタン
* コマンドラインに戻って、docker環境上で以下のコマンド
```
# --pascal-skip 1 オプションをつけることにより、全てのフレームのデータを出力できます。
~/vatic# turkic dump currentvideo -o /root/vatic/data/VOC/ --pascal --pascal-skip 1
```
* 生成されたVOCを退避
* データベースの初期化
```
~/vatic# turkic setup --database --reset
> y
```
* 先の工程と同様に、dataディレクトリに必要なファイルを用意した上で
```
~/vatic# sh example.sh
```
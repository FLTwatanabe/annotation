# vatic_annotation
## Installation
### docker
```
$ 
```
### まとめサイトに従う
https://qiita.com/wakaba130/items/b0db5c5af4d1ecdaf985
## Operation
### ディレクトリ構成
```
~/vatic/data/labels.txt
~/vatic/data/videos_in/<your_video>
$ cd vatic/
```
### docker operation
````
# 初回のみ
# ローカルのボリュームがコンテナにマウントされる.
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
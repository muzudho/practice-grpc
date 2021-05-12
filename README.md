# practice-grpc

gRPCの練習（＾～＾）  

```shell
# もうやった（＾～＾）
go mod init
```

うーん、Dockerで環境作った方がいいのかだぜ（＾～＾）？  

[gRPC Web - Quick start](https://grpc.io/docs/platforms/web/quickstart/)  

```shell
git clone https://github.com/grpc/grpc-web
```

`grpc-web` というでかいフォルダーがでけたぜ（＾～＾）  

```shell
cd grpc-web

docker-compose pull

docker-compose up -d node-server envoy commonjs-client
```

![20210512shogi19.png](./doc/img/20210512shogi19.png)  

もしかして、Windowsにダウンロードしたときにテキストファイルの改行が `\r\n` になってしまって  
DockerのLinuxにファイルを置いたときに `\r` が邪魔になったのかだぜ（＾～＾）？  
`CRLF` を `LF` に変えたろ（＾～＾）  

![20210512shogi20.png](./doc/img/20210512shogi20.png)  

つら（＾～＾）  

```shell
cd ..
git submodule init
git submodule update
cd grpc-web
docker-compose pull

# WARNING: Some service image(s) must be built from source by running:
#     docker-compose build interop-client closure-client node-interop-server echo-server binary-client protoc-plugin prereqs grpcwebproxy java-interop-server ts-client

docker-compose build interop-client closure-client node-interop-server echo-server binary-client protoc-plugin prereqs grpcwebproxy java-interop-server ts-client

# docker-compose up -d node-server envoy commonjs-client
```

同じエラー（＾～＾）  
じゃあ Visual Studio Code を使っていることによる カレント・ディレクトリ の違いか（＾～＾）？  

```shell
# これでトップ・ディレクトリを grpc-web にしたれ（＾～＾）
code .

docker-compose up -d node-server envoy commonjs-client
```

同じエラー（＾～＾）  
まず `third_party/protobuf` ディレクトリーに移動したいんだが、なぜ無いのか（＾～＾）？  

![20210513shogi21a1.png](./doc/img/20210513shogi21a1.png)  

👆 このディレクトリーが空なんだが、何か入れるのかだぜ（＾～＾）？  

[grpc-web example don't work #1064](https://github.com/grpc/grpc-web/issues/1064)  

```shell
# ダメ（＾～＾）
docker-compose build common prereqs

# grpc-web ディレクトリで（＾～＾）
git submodule init
git submodule update
# よっしゃ（＾～＾） third_party ディレクトリの中に何かがダウンロードされたぜ（＾～＾）

# ダメ（＾～＾）
docker-compose build common prereqs

docker-compose up -d node-server envoy commonjs-client
```

![20210513shogi22.png](./doc/img/20210513shogi22.png)  

👆 エラーの箇所が変わったので進んでいるのかも（＾～＾）  

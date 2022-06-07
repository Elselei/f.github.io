- 获取最新快照指向 

```shell
#curl -I https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_latest.car
HTTP/1.1 200 OK
x-amz-id-2: biqOuwSCmzombG+QJpHFjbEE0O0kTFhv1MhZzNHNdDFct6Xm2lPjS+H2Fn+YW0pLPfIjpB/r+M8=
x-amz-request-id: G6SYTWMHBZGY6XWX
Date: Tue, 07 Jun 2022 08:55:16 GMT
Last-Modified: Tue, 07 Jun 2022 08:13:07 GMT
ETag: "7cf0cc7eb466b4a83a4136d3e0be3e37-9136"
x-amz-website-redirect-location: https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_1875840_2022-06-07_06-00-00.car
Accept-Ranges: bytes
Content-Type: binary/octet-stream
Server: AmazonS3
Content-Length: 76630435539

```

- 下载快照
```
aria2c -x10 https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_1875840_2022-06-07_06-00-00.car
```

- 停止lotus-deamon服务
```
#systemctl stop lotus-deamon.service
```

- 获取lotus-deamon PATH
```
#cat /etc/systemd/system/lotus-daemon.service |grep PATH
Environment=LOTUS_PATH=/test/.lotus
```

- 备份chain数据
```
#mv /test/.lotus/datastore/chain /test/.lotus/datastore/chain_backup

#mkdir /test/.lotus/datastore/chain

```
- 导入快照,直到完成为止

```
#lotus daemon --import-snapshot minimal_finality_stateroots_1875840_2022-06-07_06-00-00.car --halt-after-import

```

- 启动lotus-deamon服务
```
#systemctl start lotus-deamon.service
```

- 检查sync状态,直到diff为0即可

```
#lotus sync wait
Worker: 0; Base: 0; Target: 0 (diff: 0)
State: idle; Current Epoch: 0; Todo: 0

Done!
```
- 获取最新快照指向 

```shell
#curl -I https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_latest.car 
x-amz-website-redirect-location: https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_1875840_2022-06-07_06-00-00.car
```

- 下载快照 
```shell
#aria2c -x10 https://fil-chain-snapshots-fallback.s3.amazonaws.com/mainnet/minimal_finality_stateroots_1875840_2022-06-07_06-00-00.car 
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

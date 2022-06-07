DBMotion MySQL安装：
```bash
docker network create dts-network && docker pull mysql:latest && docker pull squids/squids-dbmotion-tool:1.0.0 && docker pull squids/squids-dbmotion:1.0.0 && docker run --name dts-mysql --network dts-network -e MYSQL_ROOT_PASSWORD=dbmotion -d mysql && docker run --network dts-network -d -p 30000:3000 --name squids-dbmotion -v /var/run/docker.sock:/var/run/docker.sock -v /tmp/dbmotion:/tmp/dbmotion squids/squids-dbmotion:1.0.0
```

DBMotion MongoDB命令行安装使用
```
# run mysql in docker container:
docker run -d --name mysql4dbmotion -e MYSQL_ROOT_PASSWORD=dbmotion mysql 

# run dbmotion in docker container:
docker run -it --name dbmotion-mongo --link mysql4dbmotion --pull always woqutech/dbmotion-mongo

# 全量
dbmotion --dbtype=mongo  --source='root/dbmotion@10.10.108.75:27017/?connect=direct' --target='root/dbmotion@10.10.108.75:27017/?connect=direct' --result-storage=mysql --connection-string='root/dbmotion@mysql4dbmotion:dbmotion' --schemas=orderdb,saledb --move-model=all --exists-handle=drop --do-truncate=y --work-threads=4 --commit-batchsize=512

# 增量
dbmotion --dbtype=mongo --source='root/dbmotion@10.10.108.75:27017/?connect=direct' --target='root/dbmotion@10.10.108.75:27017/?connect=direct' --result-storage=mysql --connection-string='root/dbmotion@mysql4dbmotion:dbmotion' --schemas=orderdb,saledb  --move-model=onlychanged --work-threads=4

# 日志放在执行命令的当前目录dbmotion.log
```


[1.产品简介](https://github.com/squids-io/dts-doc/wiki/1.%E4%BA%A7%E5%93%81%E7%AE%80%E4%BB%8B)

[2.快速上手](https://github.com/squids-io/dts-doc/wiki/2.%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B)

[3.命令行使用说明](https://github.com/squids-io/dts-doc/wiki/3.%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F%E8%AF%B4%E6%98%8E)

- [MySQL命令行使用说明](https://github.com/squids-io/dts-doc/wiki/3.%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F%E8%AF%B4%E6%98%8E#mysql%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F%E8%AF%B4%E6%98%8E)

- [MongoDB命令行使用说明](https://github.com/squids-io/dts-doc/wiki/3.%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F%E8%AF%B4%E6%98%8E#mongodb%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F%E8%AF%B4%E6%98%8E)

[4.命令行参数说明](https://github.com/squids-io/dts-doc/wiki/4.%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E)

[5.常见问题](https://github.com/squids-io/dts-doc/wiki/5.%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)

[6.故障排除](https://github.com/squids-io/dts-doc/wiki/6.%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4)

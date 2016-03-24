#### pkapazooesst
#####1
######installing:
```
tar -C /usr/share -zxf zookeeper-3.5.1.tar.gz
export ZK_HOME=/usr/share/zookeeper-3.5.1
export PATH=$PATH:/usr/share/zookeeper-3.5.1/bin
cd bin 
./zkServer.sh start
```

using java shell
```
zkCli.sh -server localhost:2181
```

create node:
```
create /NodeName ""
ls /
delete /NodeName
```

config:
```
conf/zoo.cfg
```

for multiple instance, the format is
```
server.2=zoo2:1000:2000  //  id:peertopeerip:peertoleaderip
```





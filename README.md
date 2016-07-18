#### pkapazooesst
#####1
######installing:
```
wget http://apache.mirrors.tds.net/zookeeper/zookeeper-3.4.8/zookeeper-3.4.8.tar.gz && tar -C /usr/share -zxf zookeeper-3.4.8.tar.gz
export ZK_HOME=/usr/share/zookeeper-3.4.8 && export PATH=$PATH:/usr/share/zookeeper-3.4.8/bin
cd /usr/share/zookeeper-3.4.8/bin/
./zkServer.sh start
```

check ps:
```
ps –ef | grep zookeeper | grep –v grep | awk '{print $2}'
```
jps command
```
which jps
jps
```

using java shell
```
zkCli.sh -server localhost:2181
```

create node with empty data:
```
create /NodeName ""
ls /
```
delete node:
```
delete /NodeName
```

config:
```
vim /usr/share/zookeeper-3.4.8/conf/zoo.cfg
```

for multiple instance, the format is
```
tickTime=2000
dataDir=/var/lib/zookeeper
clientPort=2181
initLimit=5
syncLimit=2
server.1=zoo1:2888:3888
server.2=zoo2:2888:3888
server.3=zoo3:2888:3888  //  id:peertopeerip:peertoleaderip
```
set myid file(must)
```
echo 1 > /var/lib/zookeeper/myid //machine1
echo 2 > /var/lib/zookeeper/myid //machine2
echo 3 > /var/lib/zookeeper/myid //machine3
```
if failed to connect, stop previous connection
```
netstat -ltnp
```
```
kill -9 pid
```
Or use zkCli
```
./zkCli.sh -server zoo1:2181,zoo2:2181,zoo3:2181
```
on single machine:(different ports)
```
tickTime=2000
initLimit=5
syncLimit=2
dataDir=/var/lib/zookeeper/zoo1
clientPort=2181
server.1=localhost:2666:3666
server.2=localhost:2667:3667
server.3=localhost:2668:3668
```
The second instance:
```
tickTime=2000
initLimit=5
syncLimit=2
dataDir=/var/lib/zookeeper/zoo2
clientPort=2182
server.1=localhost:2666:3666
server.2=localhost:2667:3667
server.3=localhost:2668:3668
```
The third:
```
tickTime=2000
initLimit=5
syncLimit=2
dataDir=/var/lib/zookeeper/zoo3
clientPort=2183
server.1=localhost:2666:3666
server.2=localhost:2667:3667
server.3=localhost:2668:3668
```
add myid:
```
echo 1 > /var/lib/zookeeper/zoo1/myid
echo 2 > /var/lib/zookeeper/zoo2/myid
echo 3 > /var/lib/zookeeper/zoo3/myid
```
start by appoint cfg file
```
$ ${ZK_HOME}/bin/zkServer.sh start ${ZK_HOME}/conf/zoo1.cfg
$ ${ZK_HOME}/bin/zkServer.sh start ${ZK_HOME}/conf/zoo2.cfg
$ ${ZK_HOME}/bin/zkServer.sh start ${ZK_HOME}/conf/zoo3.cfg
```
connect cluster
```
$ ${ZK_HOME}/bin/zkCli.sh –server localhost:2181, localhost:2182, localhost:2183
```




# -linux-
常用linux命令

超融合常用，有：

1.生成war包：
    文件目录下即可
    mvn clean install

    生成static：gulpfile.js相同目录下
    gulp addLibs
    build.bat,生成后查看有无datepicker.js,如无，手动添加

    最好先打后台的war包，快

2.替换147war包：ssh node2,centos 
    大致过程：停掉cvm下的tomcat，删掉其文件。上传war包到node1，从node1复制到node2、node3。
    从node复制到cvm上，重启。

    进入147环境，
     1.node1下，进入cvm1   ssh 189.0.0.1,root
     2.kill掉cvm的tomcat：ps -ef|grep tomcat，kill -9 XXX
     3.cvm文件目录cd /opt/apache-tomcat-8.5.15/webapps/
    ll
    rm -rf 文件名（移除文件）
     4.exit(cvm1->node1) 
    上传文件到node1（/root目录下）
    scp console.war root@node2:/root
    scp console.war root@node3:/root

     5.将node目录下文件复制到cvm
    scp console.war root@189.0.0.1:/opt/apache-tomcat-8.5.15/webapps/
     6.进入cvm1  ssh 189.0.0.1,root查看
    cd /opt/apache-tomcat-8.5.15/webapps/bin
    ./startup

  
3.lhv环境开启
    1,ssh 10.10.10.23 密码：root
    2,cat /root/lhvreadme.md 
    3,cd /root/ft-dispatch
    4,执行2的第一条语句（打开lhv的server）./build/lhv -c ./build/ -s server
    5,新打开窗口进入23环境 cd /root/ft-dispatch
    6,执行2的第二条语句（打开lhv的agent）./build/lhv -c ./build/ -s agent
    7,新打开窗口进入23环境 cd /root/monitor
    8,cat readme.md
    9,执行8的语句（打开监控数据推送）

    开启watch环境
    10,进入10.100.2.197环境
    11,开启/home/apache-cassandra-2.1.8/bin/cassandra
    12,开启vega服务 /home/vega_watch/bin/start.sh

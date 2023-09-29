# cloud_computing

<h2>네트워크 설정</h2>

sudo nano /etc/network/interfaces

1.내 ip및 네트워크 설정
2.만약 회사나 교육용 컴퓨터일 시 -> gateway로 작성
3.내 개인 노트북이면 -> boradcast로 작성
4.dns-nameserver 8.8.8.8 8.8.4.4 
이 dns는 구글의 무료 dns주소로 기관에서 따로 지정해주지 않으면이 dns로 설정
    
 
  
<h4>DNS설정</h4>

sudo nano /etc/resolv.conf(nameserver는 위와 동일하게 작성)
   

 

   <li> dns 동작 확인</li>

    ping www.google.co.kr

   ->안될경우 설정에 문제가 있음

   <li> ssh 설치</li>

     sudo apt-get install ssh


   <li>내 ip로 xshell과 연동가능</li>

![xshell 연동성공](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/972e7324-1711-4a29-b6d0-3e750ab4303b)



   <h4>java 설치</h4>

    sudo apt-get update
    sudo apt-get install default-jdk -y
    readlink -f /usr/bin/java11-openjdk-amd64/bin/java
    sudo nano /etc/profile(export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 파일 밑에 설정)
    source /etc/profile


   <h4>hadoop 설치</h4>

    wget http://apache.mirror.cdnetworks.com/hadoop/common/hadoop-2.9.2/hadoop-2.9.2.tar.gz
    tar zxvf hadoop-2.9.2.tar.gz
    sudo cp -rf hadoop-2.9.2 /usr/local/hadoop
    rm -rf hadoop-2.9.2(용량을 위해 지움)


   <h4>하둡 사용자 등록 및 하둡 소유권 변경</h4>


    sudo add grouop hadoop
    sudo adduser --ingroup hadoop manager(manager란 이름으로 사용자 등록)
    sudo adduser manager sudo(사용자를 sudo 그룹에 추가)

    sudo chown -R manager:hadoop /usr/local/hadoop (소유가가 하위 디렉토리 읽기 권한 부여)
    ls -l /usr/local(파일 목록 확인)


   <h4>하둡 환경 설정</h4>
   
    sudo su - manager(manager 사용자로 root변경)
![manager변경](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/7965704e-c41e-4536-bde4-f63bf220270d)

    nano /.bashrc(여기서 하둡에 대한 환경변수들을 설정)
            
    export HADOOP_HOME=/usr/local/hadoop
    export PATH=$PATH:$HADOOP_HOME/bin
    export PATH=$PATH:$HADOOP_HOME/sbin
    export HADOOP_MAPRED_HOME=$HADOOP_HOME
    export HADOOP_COMMON_HOME=$HADOOP_HOME
    export HADOOP_HDFS_HOME=$HADOOP_HOME
            
    source ~/.bashrc(내용을 업데이트 했다고 알려주는 명령어)


  <h4>core-site 설정</h4>

   sudo chwon -R manager:hadoop /usr/local/hadoop/tmp/ (이 경로에 있는 파일들을 읽을 수 있는 권한 부여)

   sudo nano /usr/local/hadoop/etc/hadoop/core-site.xml(분산 컴퓨팅을 구현하기 위한 manager의 ip와 port를 설정)

![core-site설정](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/718ad199-343f-4857-82a4-bdf6d1b5240e)


  <h4>mapred-site 설정</h4>

   sudo nano /usr/local/hadoop/etc/hadoop/mapred-site.xml(core-site와 동일)

![mapred-site 설정](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/c57651c4-e1af-479c-8074-e036eaa4e377)

   <h4>hdfs-site 설정</h4>

    $ sudo mkdir -p /usr/local/hadoop/hdfs/namenode
    $ sudo mkdir -p /usr/local/hadoop/hdfs/datanode
    $ sudo chown -R manager:hadoop /usr/local/hadoop/hdfs
    $ sudo nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml

![hdfs-site 설정](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/a5229142-bea5-480e-8daf-bae13c8ef27d)
<li>dfs.repication의 1의 값은 싱글보드 3은 분산모드 </li>


  <h4>hadoop start</h4>

    hadoop namenode –format
    start-dfs.sh(hadoop 실행 , 멈춤은 stop-all.sh)
![하둡실행](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/2d2e35ea-68a2-4913-af36-ab1034ae0038)

    jps(실행상태 출력)
![프로세스 상태 확인](https://github.com/HANYONUJUN/cloud_computing/assets/104452243/efd6667a-4506-4212-a6a2-2781a4de592f)
<li>여기 실행 상태 중 jps를 제외한 나머지가 하나라도 실행을 안할 시 설정이 잘못된 것으로 반드시 수정해줘야 함(hdfs-site 부분으로 생각)</li>
<li>왜냐하면 hadoop이 정상 실행이 되지 않는 것으로 hadoop명령어를 사용할 시 연결이 거부됨</li>
         
          

    
            

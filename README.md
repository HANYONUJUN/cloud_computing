# cloud_computing

<h2>네트워크 설정</h2>

    sudo nano /etc/network/interfaces

     <li>내 ip및 네트워크 설정</li> <br>
     <li>만약 회사나 교육용 컴퓨터일 시 -> gateway로 작성</li> <br>
     <li>내 개인 노트북이면 -> boradcast로 작성</li> <br>
     <li>dns-nameserver 8.8.8.8 8.8.4.4 <br> 
      이 dns는 구글의 무료 dns주소로 기관에서 따로 지정해주지 않으면이 dns로 설정
     </li>
 
  
<h4>DNS설정</h4>

    sudo nano /etc/resolv.conf
   

 <li>nameserver 위 내용이랑 똑같이 작성</li>

   <li> dns 동작 확인</li>

    ping www.google.co.kr

   ->안될경우 설정에 문제가 있음

   <li> ssh 설치</li>

     sudo apt-get install ssh


   <li>내 ip로 xshell과 연동가능</li>


   <h4>java 설치</h4>

       sudo apt-get update
       sudo apt-get install default-jdk -y
       readlink -f /usr/bin/java11-openjdk-amd64/bin/java
       sudo nano /etc/profile(export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 파일 밑에 설정)
       source /etc/profile

    
   

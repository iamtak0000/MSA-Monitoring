# MSA-Monitoring

사전에 할 일.
  OS : Ubuntu 18
  
  sudo apt-get install openjdk-11-jdk
  
  git, wget command
  
  git clone https://github.com/iamtak0000/MSA-Monitoring.git

1. SpringBoot로 Monolithic 기반 Application 시작하기

  git pull https://github.com/iamtak0000/MSA-Monitoring.git
  
  #압축 풀기
  
	tar xvf example01.tar
  
  #실행 하기
  
	./mvnw spring-boot:run
  
  #확인하기
  
	http://인스턴스IP:8080/hello

2. Application를 APM으로 모니터링 하기

  #스카우터 다운로드
  
	wget https://github.com/scouter-project/scouter/releases/download/v2.12.0.1.SNAPSHOT/scouter-all-2.12.0.1.SNAPSHOT.tar.gz
  
  #압축 풀기
  
	tar -zxvf scouter-all-2.12.0.1.SNAPSHOT.tar.gz
  
  #Application에 설정하기
  
	  <artifactId>spring-boot-maven-plugin</artifactId>
	  <configuration>
	    <jvmArguments>
	      -javaagent:/home/ubuntu/scouter/agent.java/scouter.agent.jar
	      -Dscouter.config=/home/ubuntu/scouter/agent.java/conf/scouter.conf
	      -Dobj_name=WAS-01
	    </jvmArguments>
	  </configuration>
  
  #스카우터 시작하기(스카우터 서버)
  
	/home/ubuntu/scouter/server/startup.sh
  
  #Application 시작하기
  
	./mvnw spring-boot:run
  
  #스카우터 클라이언트 설치(윈도우 기준)
  
	https://github.com/scouter-project/scouter/releases/scouter.client.product-win32.win32.x86_64.zip
  
  ##스카우터 클라이언트 시작(윈도우 기준)
  
	  server Address : 스카우터를 설치한 서버 아이피와 포트(127.0.0.1:6100)
	  ID : 초기에는 admin으로 설정되어있다.
	  Password : 패스워드 또한 아이디와 동일하게 기본값으로 admin으로 설정되어있다.
  

3. ab로 Application에 부하 주기
  
  #ab 설치하기
  
  	sudo apt-get install apache2-utils
  
  #ab 실행하기
  
  	ab -n 500 -c 10 http://133.186.223.100:8080/hello

4. Application를 Prometheus로 모니터링 하기

5. SpringBoot로 MSA 기반 Application 시작하기

6. Application를 Jaeger로 모니터링 하기

7. Application를 ELK로 모니터링 하기

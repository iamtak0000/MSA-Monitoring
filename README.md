# MSA-Monitoring

사전에 할 일.

  OS : Ubuntu 18
  
  sudo apt-get install openjdk-11-jdk
  
  #JAVA_HOME settings
  	
	cd
	vi .profile
	
	export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
	export PATH=$PATH:$JAVA_HOME/bin
  
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
  	  
	  vi /home/ubuntu/MSA-Monitoring/example01/pom.xml
	  
	  i
	  
	  <artifactId>spring-boot-maven-plugin</artifactId>
	  <configuration>
	    <jvmArguments>
	      -javaagent:/home/ubuntu/scouter/agent.java/scouter.agent.jar
	      -Dscouter.config=/home/ubuntu/scouter/agent.java/conf/scouter.conf
	      -Dobj_name=WAS-01
	    </jvmArguments>
	  </configuration>
  	  
	  wq!
	  
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

   #Prometheus 설치하기
   
   	wget https://github.com/prometheus/prometheus/releases/download/v2.17.1/prometheus-2.17.1.linux-amd64.tar.gz
	tar -xzf prometheus-2.17.1.linux-amd64.tar.gz
	cd prometheus-2.17.1.linux-amd64
   
   #Application 설정 : pom.xml, application.yml
   
   	pom.xml
	
		<dependency>  
     		  <groupId>org.springframework.boot</groupId>  
     		  <artifactId>spring-boot-starter-actuator</artifactId>  
		</dependency>  
		<dependency>  
     		  <groupId>io.micrometer</groupId>  
     		  <artifactId>micrometer-registry-prometheus</artifactId>  
		</dependency>	

	application.yml
	
		spring:
  		  application:
    		    name: my_spring_boot_app
		management:
  		  endpoints:  
    		    web:
      		      exposure:
        		include: "prometheus"
  		  metrics:
    		      tags:
      			application: ${spring.application.name}
	
	#Configuration prometheus.yml
	
	targets에 모니터링할 Spring Boot 애플리케이션 IP:Port 추가
	
		global:
  		  scrape_interval: "15s"
  		  evaluation_interval: "15s"
		scrape_configs:
		- job_name: "springboot"
  		  metrics_path: "/actuator/prometheus"
  		  static_configs:
  		  - targets:
    		    - "<my_spring_boot_app_ip>:<port>"
		- job_name: "prometheus"
  		  static_configs:
  		  - targets:
    	 	    - "localhost:9090"
	#Run
	
		./prometheus
	
	#Grafana 설치
	
		wget https://dl.grafana.com/oss/release/grafana-6.7.2.linux-amd64.tar.gz
		tar -zxvf grafana-6.7.2.linux-amd64.tar.gz
		cd grafana-6.7.2
		./bin/grafana-server
	
5. SpringBoot로 MSA 기반 Application 시작하기

6. Application를 Jaeger로 모니터링 하기

7. Application를 ELK로 모니터링 하기

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

3. ab로 Application에 부하 주기

4. Application를 Prometheus로 모니터링 하기

5. SpringBoot로 MSA 기반 Application 시작하기

6. Application를 Jaeger로 모니터링 하기

7. Application를 ELK로 모니터링 하기

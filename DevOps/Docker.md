# Docker?
__컨테이너 기반의 오픈소스 가상화 플랫폼__   
도커 엔진을 통해 컨테이너를 관리한다. 컨테이너는 도커 이미지가 실행된 인스턴스로 격리된 공간에서 프로세스가 동작하는 기술이다.
![docker](https://user-images.githubusercontent.com/64389378/113676002-ea2ef800-96f6-11eb-9664-91c2fb06d61e.png)    
과거엔 OS를 가상화 하여 사용하였으나 무겁고 느리다는 단점이 있음.    
이를 개선하기 위해 프로세스를 격리하는 방식이 등장하였고, 이를 컨테이너라고 한다.    
하나의 서버에 여러개의 컨테이너를 띄워 서로에게 영향을 미치지 않고, 독립적으로 실행된다.    
하나의 리눅스 커널을 여러개의 컨테이너에서 공유하는 것.
![docker](https://user-images.githubusercontent.com/64389378/113681537-0897f200-96fd-11eb-8357-ca37adba06b7.png)

## 도커를 사용하는 이유
- 애플리케이션의 운영 표준화
- 지속적 배포 / 전달 및 안정적 서비스 제공 속도
- 서비스 제공을 위한 노력 감소, 자원 사용률 증대
- **비용절감**   
![도커의 구조](https://user-images.githubusercontent.com/64389378/113681757-4f85e780-96fd-11eb-9009-1cb2d2e7f8fa.png)

## 도커의 기반기술 (작동구조)
- namespace : 컨테이너를 구획화 하는 장치.
	- PID(Process ID) : 프로세스 격리. 고유ID
	- NET(Networking) : 네트워크 인터페이스 관리(디바이스,ip주소,포트번호,라우팅데이블 등)
	- IPC(InterProcess Communication) : 공유 통신 자원 관리
	- MNT(Mount) : 파일시스템 마운트 포인트 관리
	- UTS(Unix Time Sharing) : 호스트명, 도메인명 관리
	- UID 
- cgroups(control groups) 
	- 릴리즈 관리 장치
	- 자원의 할당관리.
	- 프로세스 그룹 별로 자원의 사용을 제한함.
	- 계층구조를 사용하여 프로세스를 그룹화 해 관리할 수 있음.
- Union file system
	- 가볍고 빠른 읽기전용 레이어 사용.

## 도커허브
[도커 공식 레파지토리 서비스](https://hub.docker.com)

## 도커 이미지
- 애플리케이션의 실행에 필요한 파일이 저장된 디렉토리.
- Dockerfile을 통해 이미지를 만들고 설정함

## 도커 레이어
![docker layer](https://user-images.githubusercontent.com/64389378/113799116-6bd26480-978f-11eb-8d0e-89b93fc0c74a.png)
- 도커이미지는 컨테이너를 실행하기 위한 모든 정보를 가지고 있어 용량이 수백MB에 이른다.
- 기존 이미지에 파일이 추가 될 때, 수백메가를 다시 다운받는다면 비효율적이다.
- 이런 문제를 해결하기 위해 **레이어**라는 개념을 사용했다.
- 여러개의 레이어를 하나의 파일시스템으로 사용한다.

## 이미지경로
![이미지 경로](https://user-images.githubusercontent.com/64389378/113799486-206c8600-9790-11eb-9f71-415fd8d40753.png)
- 이미지는 url방식으로 관리하며 태그를 붙일 수 있다.
- 태그기능을 잘 이용하면 테스트나 롤백도 쉽게 할 수 있다.

## Dockerfile
![image](https://user-images.githubusercontent.com/64389378/113800034-2f076d00-9791-11eb-9328-97c8a35927be.png)
- 이미지를 만들기 위해 Dockerfile에 이미지 생성에 관한 설정을 기록함
- 텍스트파일, 명령어는 주로 대문자로 작성.
### Dockerfile 명령어
|명령어|내용|
|--|--|
|FROM|베이스 이미지 지정|
|MAINTAINER|작성자|
|RUN|명령실행|
|CMD|데몬 실행|
|EXPOSE|호스트와 연결할 포트설정|
|WORKDIR|작업 위치 설정|
|ENV|환경 변수 설정|
|ADD|파일추가|
|COPY|파일복사|
|ENTRYPOINT|데몬실행|
|USER|사용자 계정 설정|
|VOLUME|볼륨마운트|

## 사용
### ps
- 컨테이너 목록확인
```
docker ps [OPTIONS]
```
### stop
- 컨테이너 중지
```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```
### rm
- 컨테이너 제거
```
docker rm[OPTIONS] CONTAINER [CONTAINER...]
```
- - -
### run
- 이미지를 컨테이너로 생성한 뒤 실행
```
docker run --name [이미지 이름] [실행할 파일]
docker run --name javaweb ubuntu
```
### run -dit
- 컨테이너는 데몬으로 띄운다. 그렇지 앟으면 생상과 동시 종료된다.

### images
- 이미지 목록 확인
```
docker images [OPTIONS] [REPOSITORY[:TAG]]
```
### rmi
- 이미지 삭제. 컨테이너가 실행중인 이미지는 삭제되지 않는다. 
```
docker rmi [OPTIONS] IMAGE [IMAGE...]
```
### exec
- 실행중인 컨테이너에 들어가거나, 컨테이너이 파일을 실행하고 싶을 때
```
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```



- - -
참고
- https://cultivo-hy.github.io/docker/image/usage/2019/03/14/Docker%EC%A0%95%EB%A6%AC/
- https://jjeongil.tistory.com/866
- https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
- https://tech.weperson.com/wedev/devops/docker/#docker%E1%84%8B%E1%85%B4-%E1%84%89%E1%85%B5%E1%86%AF%E1%84%86%E1%85%AE-%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC
- https://www.itworld.co.kr/news/87971

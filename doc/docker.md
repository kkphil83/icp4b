# Dockerfile 작성 

```Docker
FROM mycluster.icp:8500/cicd/openjdk:8-jdk-alpine3.9

ADD target/samstore-0.0.1-SNAPSHOT.jar app.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Dspring.profiles.active=prd","-jar","/app.jar"]
```


## 샘플 yaml 파일 4개를 보내드립니다.

```
Git Url 과 Docker 이미지 이름을 알려주시면 Docker 이미지를 만들고 쪽지 드리겠습니다.

yaml 파일에서 대괄호 부분은 각자 id 에 맞게 수정하여 사용하시면 됩니다.

예시)
apiVersion: v1
kind: Service
metadata:
  name: [samstore-icppoc03]
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: tomcat
  selector:
    app: [samstore-icppoc03]

```


---

# Docker 이미지 빌드/태그/푸시 방법


## 도커 이미지 빌드

```shell
docker build [option]  [Tag-Image URI] [Dockerfile]
예) docker build -t mycluster.icp:8500/red/samstore-icppoc03:1.0.0 .
```


## 도커 이미지에 태그 작업

```
docker tag mycluster.icp:8500/red/samstore-icppoc03:1.0.0 mycluster.icp:8500/red/samstore-icppoc03:latest
```


## 도커 이미지 푸시
```
docker push mycluster.icp:8500/red/samstore-icppoc03:1.0.0
docker push mycluster.icp:8500/red/samstore-icppoc03:latest
```


## 도커 이미지 확인
```
docker images | grep samstore
```




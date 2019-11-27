# 개발 가이드

## springboot
> springboot는 spring framework을 cloud native 특성에 맞춰 tomcat/jetty 등을 embedded하여
> msa에 적합하도록 bundling 하였으며, datasource, log 등 기타 application에 필요한 설정등을
> propery 파일로서 environment와 분리되어 처리할 수 있도록 제공함.

## Template Project 설명

- [maven을 통한 빌드](doc/maven.md)
- [data base 연결](doc/jdbc.md)
- [cache 처리](doc/cache.md)
- [http client](doc/http.md)
- [Docker 사용법](doc/docker.md)
- [kubernetes Yaml](doc/yaml.md)
- [kubernetes 사용법](doc/kubectl.md)


cf) mvn install:install-file -DgroupId=com.oracle -DartifactId=ojdbc6 -Dversion=12.1.0.2 -Dpackaging=jar -Dfile=ojdbc6.jar


# 스프링 부트 프로젝트 구조 (Spring Boot Project Structure) 

스프링 부트의 프로젝트 구조는 다음과 같습니다.
```
|   pom.xml
        +---src
        |   +---main
        |   |   +---java
        |   |   |   \---com
        |   |   |       \---tutorial
        |   |   |           \---springboot
        |   |   |                   Application.java
        |   |   |
        |   |   \---resources
        |   |       |   application.properties
        |   |       |
        |   |       +---static
|   |       \---template
        |   \---test
        |       \---java
```

> src/main/java

 자바 소스 파일들이 있는 곳입니다.

> src/test/java 

 자바 테스트 파일들이 있는 곳입니다.

> src/resources/application.properties

 스프링 부트 프로퍼티 값들을 모아놓은 파일입니다.

> src/static 

 html, css 같은 정적 파일을 모아놓은 디렉터리입니다.

> src/template

 JSP같은 동적으로 값이 변환되는 파일을 모아놓은 디렉터리 입니다.


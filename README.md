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

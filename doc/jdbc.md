# jdbc(oracle) 이용한 개발
> mybatis를 기준으로 설명함

## Overview
> Mybatis는 sql을 **mapper**란 기능을 통해 sql 구문과 java method로 연결하여 사용할 수 있도록 제공함.  
> mapper interface를 작성하고, 해당 method의 이름으로 sql 구문을 xml 파일로 작성


### pom 구성
```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>1.3.2</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
<!-- https://mvnrepository.com/artifact/com.oracle/ojdbc7 -->
<dependency>
    <groupId>com.oracle</groupId>
    <artifactId>ojdbc6</artifactId>
    <version>12.1.0.2</version>
</dependency>
```

### Java : Mapper Interface 작성

``` java
@Mapper
public interface CityMapper {

    // [resulttype] [sql id](String [parameter-name]);

    List<City> findByName(String name);
    List<City> getCities();
}
```
### SQL 작성
> application.properties 파일에 mapper xml 위치 지정  
> 예) mybatis.mapper-locations=mybatis/**/*.xml

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="io.nogada.petstore.city.repository.CityMapper">
    <select id="findById" resultType="io.nogada.petstore.city.model.City">
        SELECT idCity
              ,name
              ,population
          FROM CITY
         WHERE idCity = #{id}
    </select>

    <select id="findByName" resultType="io.nogada.petstore.city.model.City">
        SELECT idCity
              ,name
              ,population
          FROM CITY
         WHERE idCity like concat("%",#{name},"%")
    </select>

    <select id="getCities" resultType="io.nogada.petstore.city.model.City"> 
        select idCity
            ,name
            ,population 
        from city
    </select>
</mapper>
```

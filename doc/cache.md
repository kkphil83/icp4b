# cache 적용 방법
> redis를 활용한 cache 처리

## Overview
> 최초 요청시에는 datasource에 접근하여 응답하지만, 무효화 할 때 까지  
> redis 메모리 데이터를 이용하여 응답함.

### pom 구성
``` xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

### application properties
```
#spring properties
spring.cache.type=redis
spring.redis.host=<service ip or service name>
spring.redis.port=<port>
spring.redis.password=<password>
```

### Java
> @Cacheable 값과 parameter:code 가 index됨

``` java
@Service
@CacheConfig(cacheNames = "message")
public class MetaService {

    @Cacheable("metadata")
	public Message getMessageByCode(String code) {
		try {
			Thread.sleep(1000*5);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		return new Message(code,"dummy message");
		
	}
}
```
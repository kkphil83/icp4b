# http client 개발 
> restful api를 사용하기 위한 개발 방법

## Overview
> spring의 httpclient를 사용하며, client pool 등의 기능을 사용하기 위해서는  
> resttemplate을 customize해야함

### pom 구성
> web start에 기본 내장되어 있음

``` xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

### Java 개발

### endpoint 선언
> application.properties에 endpoint 값을 설정하고  
> 객체내에서는 해당 값을 멤버 형태로 사용함.

```
api.comm.svc=comm-svc
```

### RestTemplate 객체를 spring Bean 설정 방법을 이용하여 생성함.
> 임의의 class에서 함수 선언

``` java
@Bean
public RestTemplate getRestTemplate() {
    logger.info("initialize resttemplate");
    return new RestTemplate();
}
```

### RestTemplate  변수 선언 및 호출

``` java
@Service
public class PetRemoteService {

    private static final Logger logger = LoggerFactory.getLogger(PetRemoteService.class);
		
	@Autowired
    RestTemplate restClient;
    
    @Value("${api.comm.svc}")
    String apiEndpoint;
	
	public String search(String q) throws Exception{
		HttpHeaders headers = new HttpHeaders();
		headers.setAccept(Arrays.asList(MediaType.APPLICATION_JSON));
		HttpEntity <String> entity = new HttpEntity<String>(headers);
		
		String str= restClient.exchange("http://".concat(apiEndpoint).concat("/pet"), HttpMethod.GET, entity, String.class).getBody();
		return str;

	}
}
```
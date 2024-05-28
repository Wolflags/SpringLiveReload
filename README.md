# Spring Boot Enable Live Reload For Thymeleaf Templates

## 1. Add dev tools dependency

### Gradle:
#### Add the following lines to your build.gradle file
```java
dependencies {

    implementation 'org.springframework.boot:spring-boot-devtools'

}
```

### Maven:
#### Add the following lines to your pom.xml file
```java
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

## 2. Add the following properties in application.properties

```java
spring.thymeleaf.cache=false
spring.thymeleaf.enabled=true
spring.thymeleaf.templates_root=src/main/resources/templates/
spring.devtools.livereload.enabled=true
spring.devtools.restart.enabled=true
```

## 3. Add the following lines in your main class

```java

    @Autowired
    private ThymeleafProperties properties;

    @Value("${spring.thymeleaf.templates_root:}")
    private String templatesRoot;

    @Bean
    public ITemplateResolver defaultTemplateResolver() {
        FileTemplateResolver resolver = new FileTemplateResolver();
        resolver.setSuffix(properties.getSuffix());
        resolver.setPrefix(templatesRoot);
        resolver.setTemplateMode(properties.getMode());
        resolver.setCacheable(properties.isCache());
        resolver.setCharacterEncoding("UTF-8");
        return resolver;
    }

```

### Example:

```java
@SpringBootApplication
public class YouMainClassName {

    public static void main(String[] args) {
      // TODO Auto-generated method stub
    }

    @Autowired
    private ThymeleafProperties properties;

    @Value("${spring.thymeleaf.templates_root:}")
    private String templatesRoot;

    @Bean
    public ITemplateResolver defaultTemplateResolver() {
        FileTemplateResolver resolver = new FileTemplateResolver();
        resolver.setSuffix(properties.getSuffix());
        resolver.setPrefix(templatesRoot);
        resolver.setTemplateMode(properties.getMode());
        resolver.setCacheable(properties.isCache());
        resolver.setCharacterEncoding("UTF-8");
        return resolver;
    }

}
```

## 4. Enable the following settings in IntelliJ IDEA

### 4.1 Build project automatically

#### Go to File -> Settings -> Build, Execution, Deployment -> Compiler -> Build project automatically

![image](https://github.com/Wolflags/SpringLiveReload/assets/61167302/43219558-4986-4470-a42a-cac995c8aa09)

### 4.2 Allow auto-make to start

#### Go to File -> Settings -> Advanced Settings -> Allow auto-make to start even if developed application is currently running

![image](https://github.com/Wolflags/SpringLiveReload/assets/61167302/0c181294-e870-4e39-85b6-4ddca61aa38d)

## 5. Run the application


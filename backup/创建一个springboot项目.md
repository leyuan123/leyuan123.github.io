### 创建一个空项目


![CreateNullPoject](https://github.com/leyuan123/leyuan123.github.io/assets/126044735/ceaebe04-ea0c-4b6a-be3c-58d02044a451)



### 上一步的基础上创建一个springboot项目

- 选择java11 ，用Maven管理项目


![CreateSpringboot1](https://github.com/leyuan123/leyuan123.github.io/assets/126044735/aed538a7-8752-4390-92a1-8e205de42874)

- 选择springboot版本（此处我选择2.7.6）
- 选择依赖
  - Lombok
    - 日志功能
    - @Date生成get，set方法
    - 等等
  - Spring Web
  - MySQL Driver
  - MyBatis Framework


![CreateSpringboot2](https://github.com/leyuan123/leyuan123.github.io/assets/126044735/9f943d77-c8dc-41db-b31c-4c52134d8112)

### 完善项目结构

- 建立controller软件包//控制层
- 建立service软件包//服务层
- 建立mapper软件包//与数据库交换层
- 建立pojo软件包//实体层
- 建立utils软件包//工具层


![struct](https://github.com/leyuan123/leyuan123.github.io/assets/126044735/3e26a8e3-67c1-4bdb-a038-9f7d363f5b91)

### 完善配置文件

- 在resources目录下建立application.yml文件
- 配置好数据库，Lombok输出等

![](C:\Users\86183\Desktop\建立spring boot项目\img\application.png)
![application](https://github.com/leyuan123/leyuan123.github.io/assets/126044735/274cf996-6a0f-4926-b029-ee71319eda96)

~~~yml
spring:
  #数据库连接信息
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/webpoject
    username: root
    password: 123456
    #文件上传配置
  servlet:
    multipart:
      max-file-size: 10MB
      max-request-size: 100MB
#mybatis配置
mybatis:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
    map-underscore-to-camel-case: true

#spring事务管理日志
logging:
  level:
    org.springframework.jdbc.support.JdbcTransactionManager: debug
~~~






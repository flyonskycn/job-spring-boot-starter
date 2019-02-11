# job-spring-boot-starter

## 简介
> 基于xxl-job,为项目中快速引入xxl-job执行器功能。
## 项目依赖
job-spring-boot-starter依赖于[autoconfigure项目](https://github.com/flyonskycn/autoconfigure)

## 使用步骤
### 引入依赖
```xml
<dependency>
    <groupId>org.flyonsky.boot</groupId>
    <artifactId>job-spring-boot-starter</artifactId>
</dependency>
```
### 基本配置
1. 设置xxl.job.admin.addresses:调度中心URL,可以是多个调度中心,多个地址之间用","分隔;
2. 设置xxl.job.executor.appname:执行器的Appname,通常设置为${spring.application.name}；
3. 设置xxl.job.executor.ip:执行器的地址,在本存在多个IP地址时需要设置。调度器通过此IP与端口访问执行器;
4. 设置xxl.job.executor.port:执行器的端口;
5. 设置xxl.job.executor.logpath:执行器日志存储位置；
6. 设置xxl.job.executor.logretentiondays:执行器Log文件定期清理功能，指定日志保存天数，日志文件过期自动删除。限制至少保持3天，否则功能不生效,默认为-1；
7. 设置xxl.job.enabled:设置为true，开启xxl执行器自动注册功能;
### 编写job
```java
@Component
@JobHandler("helloJob")
public class HelloJobHandler extends IJobHandler{
	
	private static final Logger LOG = LoggerFactory.getLogger(HelloJobHandler.class);

	@Override
	public ReturnT<String> execute(String param) throws Exception {
		LOG.info("hello job");
		return ReturnT.SUCCESS;
	}

}
```
**注意:job代码所在的包，需要能够被spring 自动扫描到。**

## 样例
[样例参见](https://github.com/flyonskycn/micro-service-study/tree/master/jobdemo)

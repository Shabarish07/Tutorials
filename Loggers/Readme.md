# **LOGGERS**
________________________

## **Welcome to Loggers Tutorial** <br>

### We will discuus about LOGGERS and its uses and different Logging type. <br>

SOURCE : 
[LoggerPdf](Logger.pdf)

_____


## Table of Contents
____

 * [Chapter 01 - Loggers Introduction](#Chapter-01)
 * [Chapter 02 - Loggers Components n Types of loggers](#Chapter-02)
 * [Chapter 03 -  Logback](#Chapter-03) 
 * [Chapter 04 - LOG4J ](#Chapter-04)
 * [Chapter 05 - log4j2](#Chapter-05)

_____
## Chapter 01
##  **Loggers Introduction -**
____

- BUG/Problem:- After Application is developed then it will be handover to End Client/Customer.
At the time of Running Application some problems may occur while processing a request. In
programming concept it is called as Exception.

- These problems try to identify at the time of development to avoid few. Some will be
handled once they are occurred. Those are analyzed and solved by developer. Give priority to
Avoid problems if not handle the problems.

> To avoid problems concepts are : 1. Validations 2. Standard Coding
> To handle the problems concepts are: 1. Error pages 2.Log4J


-  A Logger object is used to log messages for a specific system or application component. Loggers are normally named, using a hierarchical dot-separated namespace. Logger names can be arbitrary strings, but they should normally be based on the package name or class name of the logged component, such as java.net or javax

-  loggers are similar to system.out.println, but loggers is standard way to print status of the application.

_________________________________________________________________________________________________________________________________________

## Chapter 02
## **Loggers Components n Types of loggers -** 
__________________________________________________________________________________________________________

> By default Spring provides the Logging, i.e. 

```xml
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-logging</artifactId>
```

- Loggers has has 3 components: __Layout, Appender, Logger.__

## Logger-
+ This object must be created inside the class as a instance variable. It is used to enable Log4J service to current   class. If this object is not created in the class then Log4J concpet will not applicable(will not work)for that class.

 It has 5 priority methods with names (along with order):

1. debug(msg) : It prints a message with data. It is used to print a final result of process. Like EmpId after saved is : 2362.
2. info(msg) : It is used to print a simple message. Like process state-I done, if block end. Email sent etc..
3. warn(msg): It is used to print warning messages. Like Collection is not with Generic, local variable not used, resource not closed etc...
4. error(msg): It is used to print Exceptions like NullPointer, ArrayIndex, SQLException etc..
5. fatal(mgs) : It indicates very high level problem. Like Server/DB Down, Connection timeout, Network broken, Class Not Found etc...


## Appenders-
- It will provide details for "Where to print Message?". Means in what type of memories, messages must be stored. To write Logger Statements to

1. File use FileAppender
2. Database use JdbcAppender
3. Email use SmtpAppender
4. Console use ConsoleAppender
5. Network use Ftp(Telnet)Appender

In one Application we can use more than one appender also.

## Layout-
- It provide the format of message to be printed. Possible layouts are:

1. Simple Layout : Print message as it is
2. HTML Layout : Print message in HTML format(<html><body>....)
3. XML Layout: Print message in XML format (<Errors><Type>..<Message>..)
4. Pattern Layout : Prints messages in given pattern. example pattern: Date-Time / LineNumber : Class-method :- Message

In development mostly used Appender is FileAppender and Layout is Pattern Layout.

## Pattern Layout- 
- PatternLayout : This class provides output pattern for a message that contains date, time,
class, method, line number, thread name, message etc..

> Date&Time pattern
  - %d = date and time

examples:
a) %d
b) %d {dd-MMM-yy hh:mm:ss SSS}
c) %d {dd-MM-yy hh:mm:ss SSS}
d) %d {HH:mm:ss}
e) Here meaning of every word used
f) in date pattern is,
g) dd = date
h) MMM = Month Name
i) MM = Month number
j) yy = Year last two digitis
k) yyy = Year in 4 digits
l) hh = Hours in 12 format
m) HH = Hours in 24 format
n) mm = Minutes
o) ss = Secs
p) SSS = MillSecs

- %C = Class Name
- %M = Method Name
- %m = Message
- %p = Priority method name(DEBUG,INFO..)
- %L = Line Number
- %l = Line number with Link
- %n = New Line(next line)
- %r = time in milli sec.
- %% = To print one '%' symbol.
- we can also use symbols like - [] , /

```One Example Pattern with all matching``` " %d-%C[%M] : {%p}=%m<%L> %n " 

```Example:```

```java

import org.apache.log4j.Logger;

public class Product {
private static Logger log=Logger.getLogger(Product.class);
public static void main(String[] s) throws Exception {

log.debug("Hello");
log.info("Hello");
log.warn("Hello");
log.error("Hello");
log.fatal("Hello");
}
}
```

> Mainly there are 4 types-
 - Logback
 - Log4j
 - log4j2
 - Log4j Using Slf4j

____
## Chapter 03

## **Logback-**
___

- Logback is provided out of the box with Spring Boot when you use one of the Spring Boot starter dependencies, as they include spring-boot-starter-logging — providing logging without any configuration that can be altered to work differently if required. There are two ways of providing your own configuration. 

- If you only need simpler alterations, they can be added to a properties file, such as application.properties or for more complex needs, you can use XML or Groovy to specify your settings. In this tutorial, we will focus on using XML to define a custom logging configuration and look at some of the basics of doing so, as well as a brief look at using property files to specify simple alterations to the standard setup provided by Spring Boot.

- Logback was written by the same developer who implemented Log4j with the goal to become its successor. It follows the same concepts as Log4j but was rewritten to improve the performance, to support SLF4J natively, and to implement several other improvements like advanced filtering options and automatic reloading of logging configurations.

- The framework consists of 3 parts:
  - logback-core
  - logback-classic
  - logback-access

+ Logback-core provides the core functionality of the logging framework. Logback-classic adds more features to the core functionality, e.g., native support for SLF4J. And logback-access integrates it with servlet containers so that you can use it to write HTTP-access logs.

- we can define the config file i.e. logback.xml to define the configuration of the logback logger.

> Dependency
 ```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
</dependency>
 ``` 

+ The dependency spring-boot-starter to pull in spring-boot-starter-logging , which can be found below. 

```xml
<dependencies>
  <dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
  </dependency>
  <dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>jul-to-slf4j</artifactId>
  </dependency>
  <dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>log4j-over-slf4j</artifactId>
  </dependency>
</dependencies>
```

```Example: logback.xml```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    
    <property resource="application.properties" />

    <property name="LOGS" value="${app.logfile}" />
    
    <property name="DEV_LEVEL" value="${dev.profile.level}" />
    
    <property name="PROD_LEVEL" value="${prod.profile.level}" />
    
       <appender name="Console"
	        class="ch.qos.logback.core.ConsoleAppender">
	        <layout class="ch.qos.logback.classic.PatternLayout">
	            <Pattern>
	                %black(%d{ISO8601}) %highlight(%-5level) [%blue(%t)] %yellow(%C{1.}): %msg%n%throwable
	            </Pattern>
	        </layout>
	    </appender>
	 
	    <appender name="RollingFile"
	        class="ch.qos.logback.core.rolling.RollingFileAppender">
	        <file>${LOGS}/app.log</file>
	        <encoder
	            class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
	            <Pattern>%d %p %C{1.} [%t] %m%n</Pattern>
	        </encoder>
	 
	        <rollingPolicy
	            class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
	            <!-- rollover daily and when the file reaches 10 MegaBytes -->
	            <fileNamePattern>${LOGS}/archived/spring-boot-logger-%d{yyyy-MM-dd}.%i.log
	            </fileNamePattern>
	            <timeBasedFileNamingAndTriggeringPolicy
	                class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
	                <maxFileSize>10MB</maxFileSize>
	            </timeBasedFileNamingAndTriggeringPolicy>
	        </rollingPolicy>
	    </appender>
	    
	    <appender name="ASYNC_CONSOLE"
			class="ch.qos.logback.classic.AsyncAppender">
			<discardingThreshold>0</discardingThreshold> <!-- default 20, means drop lower event when has 20% capacity remaining -->
			<appender-ref ref="Console" />
			<appender-ref ref="RollingFile" />
			<queueSize>1</queueSize> <!-- default 256 -->
			<includeCallerData>false</includeCallerData><!-- default false -->
			<neverBlock>true</neverBlock><!-- default false, set to true to cause the 
				Appender not block the application and just drop the messages -->
		</appender>
    
	    <springProfile name="dev" source="spring.profiles.active">
		      <logger name="com.navietm.ms" level="DEBUG" additivity="false">
		        <appender-ref ref="Console" />
		    </logger>
		  
		 <!-- <root level="${DEV_LEVEL}">
		      <appender-ref ref="Console" />
		      <appender-ref ref="RollingFile" /> 
		  </root> -->
		    
		</springProfile>
 
	  <springProfile name="prod" source="spring.profiles.active">
	    <root level="${PROD_LEVEL}">
	      <appender-ref ref="RollingFile" />
	    </root>
	  </springProfile>
    
 
</configuration>

```
- Here the details like path, logging level, active_profile like dev,QA,prod are defined in application.properties .
- hence we define the <property resource="application.properties" />

```Example: Application.properties```
```log
app.logfile = logs

dev.profile.level = debug

prod.profile.level = info

#======if no active profile, default is 'default'=======
spring.profiles.active = dev
#spring.profiles.active = prod
```

```Example: Class```

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class SpringLoggingHelper {
    private final Logger logger = LoggerFactory.getLogger(this.getClass());
    public void helpMethod(){
        logger.debug("This is a debug message");
        logger.info("This is an info message");
        logger.warn("This is a warn message");
        logger.error("This is an error message");

    }
}
```
- we should slf4j as inertface for logback.

- why we use slf4j for logback..?
- [solution1](https://stackoverflow.com/questions/13949899/should-i-use-slf4j-as-wrapper-for-logback) 
- [solution2](https://stackoverflow.com/questions/9920336/how-to-use-logback-directly-without-going-through-slf4j/20713891)


Now lets disccus about Log4j ->
___________________
## Chapter 04-

## **LOG4J-**
-----
1. It is a Tracing or Logging Tool used in Specially in Production Environment. It is used to
find success messages, information, warnings, errors in application while using it.

2. By Default any Message/Error will be printed on Console, which is temporary location, it
can show only few lines like last 100 lines.

3. To see all problems from beginning to till date use Log4j concept.

4. Log4J can write problems/error to File(.log), Database, Email, Network etc..

5. Log4J provides Error Details like Exception type, class and method with line number it
occured, Date and time also other information ..

6. Log4J also supports writing errors to Console also.

7. Using System.out.println prints only on console, but not to file or any other memory.

> Dependency:

```xml
<dependency>
<groupId>log4j</groupId>
<artifactId>log4j</artifactId>
<version>1.2.17</version>
</dependency>
```
- must excelude spring-logging dependency

```xml
<dependency>
		   <groupId>org.springframework.boot</groupId>
		   <artifactId>spring-boot-starter</artifactId>
		   <exclusions>
		      <exclusion>
		         <groupId>org.springframework.boot</groupId>
		         <artifactId>spring-boot-starter-logging</artifactId>
		      </exclusion>
		   </exclusions>
		</dependency>
```



> we can create a log4j.properties files to specify the configuration of log4j
________
### Log4j.properties -
______

- log4j is highly configurable through external configuration files at runtime. It views the logging process in terms of levels of priorities and offers mechanisms to direct logging information to a great variety of destinations, such as a database, file, console, UNIX Syslog, etc.

- Mainly we can configure the log4j in 2 type- .xml file and .properties file

- In log4j we define a log4j.proprties file in src/main/resource folder in classpath, where we can configure the log4j properties.

-  This file is used to specify all the configuration details of Log4J. Especially
like Appender Details and Layout Details with Patterns and also root Logger details. This File
contains details in key=value format (.properties). 

> Data will be shown in below order like
1. rootLogger
2. appenders
3. layouts

- In this file (log4j.properties) use symbol '#' to indicates comments.

- We can specify multiple appenders in log4j.properties file Like 2 File Appenders, one JdbcAppender, One SmtpAppender etc..

- Every Appender must be connected with layout

- Appender name must be define before use at rootLogger level.

- Appender name can be anything ex: abc,hello,sysout,file,db,email etc..

- log4j.properties file must be created under src folder (normal project) or src/main/resource folder (maven project).

- Make rootLogger = OFF to disable Log4J completely without deleting code in any class or properties file

- log4j.properties file will be auto detected by Log4J tool. No special coding is required.

```Example:```

```log
#ROOT
log4j.rootLogger=DEBUG,stout,file

#CONSOLE
log4j.appender.stout=org.apache.log4j.ConsoleAppender
log4j.appender.stout.Target=System.out
log4j.appender.stout.layout=org.apache.log4j.PatternLayout
log4j.appender.stout.layout.ConversionPattern=%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n

#FILE
log4j.appender.file=org.apache.log4j.FileAppender
log4j.appender.file.File=./logs/Filemanager.log
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n
```
```OUTPUT```
```2017-09-21 21:47:59 DEBUG com.app.Product:6 - Hello
2017-09-21 21:47:59 INFO com.app.Product:7 - Hello
2017-09-21 21:47:59 WARN com.app.Product:8 - Hello
2017-09-21 21:47:59 ERROR com.app.Product:9 - Hello
2017-09-21 21:47:59 FATAL com.app.Product:10 - Hello
```

## Note-
1. If we use console appender it print the log in console.
2. If we use file appender it print the lon in file.
3. If we use both we get both console n file appender.

## Disadvantage-
1. Its complicted to create the config file in log4j i.e. log4j.xml.

> To overcome this we can use logback logging.
_____
## Chapter 05
## **log4j2 -**
____

- Log4j2 is similar to log4j, log4j2 is successor of log4j.
- Here we can specify the .xml config file.
- Log4j2 is more advanced form of logging but here we cant use spring.active.profile i.e. dev/prod directly.
- we need to specify respective config file and place it in classpath and specify in application.properties

>Dependecy:

```xml
<dependency>
	<groupId>org.apache.logging.log4j</groupId>
	<artifactId>log4j-api</artifactId>
	<version>2.13.1</version>
</dependency>
<dependency>
	<groupId>org.apache.logging.log4j</groupId>
	<artifactId>log4j-core</artifactId>
	<version>2.13.1</version>
</dependency>

```

```Example: Simple log4j2.xml```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
	<Appenders>
		<Console name="Console" target="SYSTEM_OUT">
			<PatternLayout
				pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
		</Console>
		<File name="File-Appender" fileName="logs/projectslogfile.log">
			<PatternLayout
				pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
		</File>
	</Appenders>
	<Loggers>
	<!--  
		<AsyncLogger name="org.springframework" level="all" additivity="false">
			<AppenderRef ref="Console" />
			<AppenderRef ref="File-Appender" />
		</AsyncLogger>
	-->
	
		<AsyncLogger name="com.navietm.ms" level="INFO" additivity="false">
			<AppenderRef ref="Console" />
			<AppenderRef ref="File-Appender" />
		</AsyncLogger>
		
		<Root level="DEBUG">
			<AppenderRef ref="Console" />
			<AppenderRef ref="File-Appender" />
		</Root>
	</Loggers>
</Configuration>
```

```Example: Appliaction.properties```
```java
log.file.path=logs

dev.profile.level = debug

prod.profile.level = info

log.pattern=%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n

#logging.level.org.springframework.web=DEBUG
#spring.http.log-request-details=true

## if no active profile, default is 'default'

##dev
logging.config=classpath:log4j2-dev.xml

##prod
#logging.config=classpath:log4j2-file.xml
```

```Example: log4j2-dev.xml where values are configured in application.properties ```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
    <Properties>
        <property name="basePath">${bundle:application:log.file.path}</property> 
        <property name="level">${bundle:application:dev.profile.level}</property> 
        <property name="logpattern">${bundle:application:log.pattern}</property> 
    </Properties>
 
    <Appenders>
        <RollingFile name="fileLogger" fileName="${basePath}/project.log" filePattern="${basePath}/archive/project-%d{yyyy-MM-dd}.log">
            <PatternLayout   pattern="${logpattern}"/>
            <Policies>
                 <Policies>
		        <OnStartupTriggeringPolicy />
		        <SizeBasedTriggeringPolicy size="10 MB" />
		        <TimeBasedTriggeringPolicy />
		    </Policies>
		    <DefaultRolloverStrategy max="5" />
            </Policies>
        </RollingFile>
        
         <RollingFile name="rootfileLogger" fileName="${basePath}/root.log" filePattern="${basePath}/root-%d{yyyy-MM-dd}.log">
            <PatternLayout   pattern="${logpattern}"/>
            <Policies>
                 <Policies>
		        <OnStartupTriggeringPolicy />
		        <SizeBasedTriggeringPolicy size="10 MB" />
		        <TimeBasedTriggeringPolicy />
		    </Policies>
		    <DefaultRolloverStrategy max="5" />
            </Policies>
        </RollingFile>
 
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout   pattern="${logpattern}"/>
        </Console>
    </Appenders>
    
    <Loggers>
        <AsyncLogger name="com.navietm.ms" level="debug" additivity="true">
            <appender-ref ref="fileLogger" level="debug" />
        </AsyncLogger> 
        
        <Root level="debug" additivity="false">
            <appender-ref ref="console" />
            <appender-ref ref="rootfileLogger"  />
        </Root>
    </Loggers>
</Configuration>
```

```Example: log4j2-file.xml  ```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
    <Properties>
        <property name="basePath">${bundle:application:log.file.path}</property> 
        <property name="level">${bundle:application:prod.profile.level}</property> 
        <property name="logpattern">${bundle:application:log.pattern}</property> 
    </Properties>
 
    <Appenders>
        <RollingFile name="fileLogger" fileName="${basePath}/project.log" filePattern="${basePath}/project-%d{yyyy-MM-dd}.log">
            <PatternLayout>
                <pattern>%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n</pattern>
            </PatternLayout>
             <Policies>
		        <OnStartupTriggeringPolicy />
		        <SizeBasedTriggeringPolicy size="10 MB" />
		        <TimeBasedTriggeringPolicy />
		    </Policies>
		    <DefaultRolloverStrategy max="5" />
        </RollingFile>
        
        <RollingFile name="rootfileLogger" fileName="${basePath}/root.log" filePattern="${basePath}/root-%d{yyyy-MM-dd}.log">
            <PatternLayout>
                <pattern>%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n</pattern>
            </PatternLayout>
            <Policies>
                <TimeBasedTriggeringPolicy interval="1" modulate="true" />
            </Policies>
        </RollingFile>
 
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout   pattern="${logpattern}"/>
        </Console>
    </Appenders>
    
    <Loggers>
        <AsyncLogger name="com.navietm.ms" level="${level}" additivity="true">
            <appender-ref ref="fileLogger" level="${level}" />
        </AsyncLogger>
        
        <!-- <AsyncLogger name="org.springframework" level="info" additivity="true">
            <appender-ref ref="fileLogger" level="info" />
        </AsyncLogger> -->
        
        <Root level="debug" additivity="false">
            <appender-ref ref="console" />
            <appender-ref ref="rootfileLogger"  />
        </Root>
    </Loggers>
</Configuration>
```
____
# Using slf4j -
____

- Using SLF4j for logging is the most Efficient way for logging.
- Slf4j is used as interface to loggers.
- we can use any loggers like log4j,logback,log4j2.
- If we use direct log4j/2,logback in code then if we want to change to other logger then we need to change whole code, there will be many classes and its diffcult to do so.
- **Best practise is to use slf4j as interface and use any logger for logging.**  

> Dependecy 
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter</artifactId>
		<exclusions>
		    <exclusion>
		        <groupId>org.springframework.boot</groupId>
		        <artifactId>spring-boot-starter-logging</artifactId>
		    </exclusion>
	</exclusions>
</dependency>

<!-- SLf4j -->
	<dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.30</version>
    </dependency>

    <!-- Binding for Log4J -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-slf4j-impl</artifactId>
        </dependency>

   <!-- Log4j2 -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        </dependency>

    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
     </dependency>
     
     <dependency>
		<groupId>com.lmax</groupId>
		<artifactId>disruptor</artifactId>
		<version>3.3.4</version>
	</dependency>
```
> NOTE:
- Exclude the spring-logging
- we need to define slf4j first 
- Define log4j dependecy
- Define the Binding for log4j and slf4j

```application.properties```
```log
log.file.path=logs

dev.profile.level = debug

prod.profile.level = info

log.pattern=%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n

##=====if no active profile, default is 'default'=====

##dev
logging.config=classpath:log4j2-dev.xml

##prod
#logging.config=classpath:log4j2-file.xml
```

> NOTE:
- log.file.path define the folder where log files should be stored.
- dev.profile.level define which log lvl we need in dev
- prod.profile.level define which log lvl we need in prod
- logging.config=classpath:log4j2-dev.xml define which logging file to be considered.
- there will be 2 Config file for 2 environment dev and prod, if environment is dev consider dev.xml or else prod.xml that is specified in logging.config

```log4j2-dev.xml```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
    <Properties>
        <property name="basePath">${bundle:application:log.file.path}</property> 
        <property name="level">${bundle:application:dev.profile.level}</property> 
        <property name="logpattern">${bundle:application:log.pattern}</property> 
    </Properties>
 
    <Appenders>
        <RollingFile name="fileLogger" fileName="${basePath}/project.log" filePattern="${basePath}/archive/project-%d{yyyy-MM-dd}.log">
            <PatternLayout   pattern="${logpattern}"/>
            <Policies>
                 <Policies>
		        <OnStartupTriggeringPolicy />
		        <SizeBasedTriggeringPolicy size="10 MB" />
		        <TimeBasedTriggeringPolicy interval="1" modulate="true"/>
		    </Policies>
		    <DefaultRolloverStrategy max="5" />
            </Policies>
        </RollingFile>
        
         <RollingFile name="rootfileLogger" fileName="${basePath}/root.log" filePattern="${basePath}/root-%d{yyyy-MM-dd}.log">
            <PatternLayout   pattern="${logpattern}"/>
            <Policies>
                 <Policies>
		        <OnStartupTriggeringPolicy />
		        <SizeBasedTriggeringPolicy size="10 MB" />
		        <TimeBasedTriggeringPolicy />
		    </Policies>
		    <DefaultRolloverStrategy max="5" />
            </Policies>
        </RollingFile>
 
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout   pattern="${logpattern}"/>
        </Console>
    </Appenders>
    
    <Loggers>
        <AsyncLogger name="com.navietm.ms" level="debug" additivity="true">
            <appender-ref ref="fileLogger" level="debug" />
        </AsyncLogger> 
        
        <Root level="debug" additivity="false">
            <appender-ref ref="console" />
            <appender-ref ref="rootfileLogger"  />
        </Root>
    </Loggers>
</Configuration>
```

```log4j2-file.xml```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
    <Properties>
        <property name="basePath">${bundle:application:log.file.path}</property> 
        <property name="level">${bundle:application:prod.profile.level}</property> 
        <property name="logpattern">${bundle:application:log.pattern}</property> 
    </Properties>
 
    <Appenders>
        <RollingFile name="fileLogger" fileName="${basePath}/project.log" filePattern="${basePath}/project-%d{yyyy-MM-dd}.log">
            <PatternLayout>
                <pattern>%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n</pattern>
            </PatternLayout>
             <Policies>
		        <OnStartupTriggeringPolicy />
		        <SizeBasedTriggeringPolicy size="10 MB" />
		        <TimeBasedTriggeringPolicy />
		    </Policies>
		    <DefaultRolloverStrategy max="5" />
        </RollingFile>
        
        <RollingFile name="rootfileLogger" fileName="${basePath}/root.log" filePattern="${basePath}/root-%d{yyyy-MM-dd}.log">
            <PatternLayout>
                <pattern>%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n</pattern>
            </PatternLayout>
            <Policies>
                <TimeBasedTriggeringPolicy interval="1" modulate="true" />
            </Policies>
        </RollingFile>
 
        <Console name="console" target="SYSTEM_OUT">
            <PatternLayout   pattern="${logpattern}"/>
        </Console>
    </Appenders>
    
    <Loggers>
        <AsyncLogger name="com.navietm.ms" level="${level}" additivity="true">
            <appender-ref ref="fileLogger" level="${level}" />
        </AsyncLogger>
        
        <!-- <AsyncLogger name="org.springframework" level="info" additivity="true">
            <appender-ref ref="fileLogger" level="info" />
        </AsyncLogger> -->
        
        <Root level="debug" additivity="false">
            <appender-ref ref="console" />
            <appender-ref ref="rootfileLogger"  />
        </Root>
    </Loggers>
</Configuration>
```
> NOTE:

- ```<Configuration status="warn">``` is for Log4j internal events only.
- In ```<Properties>``` we define the property using <property name="basePath">${bundle:application:log.file.path}</property> where these are defined in application.properties file.

- ```<property name="logpattern">${bundle:application:log.pattern}</property>``` Here the pattern is defined in application.porperties "%d{dd--MM-yyyy hh:mm} %p --- [%M] : %C %L %m %n" <br>
**The pattern will be "date loggerlevel --- [Methodname] : ClassName Linenumber Message nextline**

- ```<Appenders>``` are used to define the appenders like cosole,file etc...
- for file we use <RollingFile> and for console <Console> n there we define the pattern in which we want to print the loggers
- ```<Root level="error">``` is configuration for the root logger, it will apply the error log level for all logs except the ones configured in separate Loggers (which you don't have in the above configuration).
- In ```<Loggers>``` we define the loggers/AsyncLogger which contain the package name and level and also specify the appender-ref that is where want to print the loggers. [AsyncLogger is used because the time to print logging is very less, there will be no delay between the execution and logging.
- ```<Root>``` is the highest level where we get all the log details including org.springframework,sql,hibernate etc..

---
title: 用quartz+spring 实现定时任务   
author: wuche  
layout: post  
permalink:  /quartz-spring/  
tags:  
  - java 
  - quartz
  - spring
  
--- 
定时任务，是个很常用的功能。在日常开发，经常要用定时任务来分析每天的数据，产生报表。  
如果是简单的定时任务，可以调用java原生态的timer。但是我在使用timer的过程中，非常初始化接口，决定还是用quartz+spring来实现。  

<!--more-->  
1. pom.xml中引入quartz的依赖  


        <dependency>
            <groupId>org.quartz-scheduler</groupId>
            <artifactId>quartz</artifactId>
            <version>1.8.6</version>
        </dependency>

2.定义job类，定义几个方法，用来执行任务。

```java
public class LwJob {  
    @Autowired
    private LwFlowService lwFlowService;  

    public void syncYesterdayData(){
       // System.out.println("hello!!");
        for (int i=0,size=LwConstant.VERSIONS.size();i<size;i++){
            String appId = LwConstant.VERSIONS.get(i);
            String appIds[] = appId.split("@");
            String appKey = LwConstant.APP_KEY_MAP.get(appIds[0]);
            String appVersion = appIds[1];
            String pt = DateUtils.getYesterday();
            LwFlowQuery lwFlowQuery = lwFlowService.getFlowByPt(appKey, appVersion, pt);
            System.out.println(lwFlowQuery);
        }
    }

    public void syncLiveData(){
        System.out.println("test!");

    }
}
``` 
 
3.在spring的bean配置文件中，定义这个类。  
 
      <bean id="exampleBusinessObject" class="com.laiwang.perf.util.LwJob"/> 
      <!--定义MethodInvokingJobDetailFactoryBean，可以定义多个-->
      <bean id="jobDetail" class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean">
       <!--对象-->  
        <property name="targetObject" ref="exampleBusinessObject" />
        <!--方法-->  
        <property name="targetMethod" value="syncYesterdayData" />
    </bean>
    <!--第二个-->  
    <bean id="syncLiveData" class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean">
        <property name="targetObject" ref="exampleBusinessObject" />
        <property name="targetMethod" value="syncLiveData" />
    </bean>  

4.配置trigger，触发器。常见的有两种，一种是周期性的。另一种是在某个时间点,我这里定义了启动1分钟后触发，每隔1小时重复任务。另一种是每天早上6点定时触发。 
  
    <bean id="liveTrigger" class="org.springframework.scheduling.quartz.SimpleTriggerBean">
        <!-- see the example of method invoking job above -->
        <property name="jobDetail" ref="syncLiveData" />
        <!-- 60 seconds -->
        <property name="startDelay" value="60000" />
        <!-- repeat every 1 hour -->
        <property name="repeatInterval" value="3600000" />
    </bean>

    <bean id="cronTrigger" class="org.springframework.scheduling.quartz.CronTriggerBean">
        <property name="jobDetail" ref="jobDetail" />
        <!-- run every morning at 6 AM -->
        <property name="cronExpression" value="0 0 6 * * ?" />
    </bean>  
  
5.定义完触发器，加上触发器的schedule,schedule的list里可以增加多个trigger，不同类型的trigger。  
  
    <bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean">
        <property name="triggers">
            <list>
                <ref bean="cronTrigger" />
                <!--<ref bean="liveTrigger" />-->
            </list>
        </property>
    </bean>  
 
6.这样用quartz+spring的定时任务就实现了，非常简单，也很强大。google了一下午，原来发现最有用的还是官方的文档。哎！    
[参考文献](http://docs.spring.io/spring/docs/3.0.x/spring-framework-reference/html/scheduling.html) 

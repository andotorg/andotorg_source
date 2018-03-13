---
title: SpringBoot dao层中Final方法注入jdbcTempate为空的问题
date: 2018-03-13 10:59:59
tags: springboot,final,method,problem
---

### 项目从Spring+SpringMVC中移植到SpringBoot中数据库操作的时候发现了一个问题

#### 代码示例
```bash 
    public class DemoDaoImpl(){
        @Autowrit
        private JdbcTemplate jdbcTempate;
        
        public final void addDemoInfo(Demo demo){
            jdbcTemplate.query(){   //加入断点后发现jdbcTemplate为空
                ......
            }
        }
    }
```

### 刚开始发现是否为数据库没有连接或者注入没有成功

> 后来发现其他的方法是可以的，其他类中jdbcTempleta不为空

> 这就证实了一个问题：已经注入进来了，然后进行了方法的比较，唯一一个不一样的地方就是方法中加入了Final关键字，导致这个方法成为了不可变的方法了

### 解决方案

> 去掉Finel 关键字，问题解决了

### 遗留问题

> 为什么SpringMVC中可以，SpringBoot不可以呢？


# j2crawler

#### 一、简介
j2crawler是一个通用的、最小化依赖第三方组件、灵活扩展组件、开箱即用，简单易用性、支持目前主流的通用的解析语法、灵活多变的实时/离线抓取方式、遵循Springboot规范、并且支持分布式部署的Java爬虫引擎，能够最大程度的提高一个爬虫新手构建一个高可用性、高性能的爬虫应用的门槛，并且提升开发爬虫系统的开发效率，只需要具备一些简单的网页解析语法同时遵循j2crawler少量开发约束即可。

#### 二、爬虫引擎特性：

* 最小化依赖第三方组件；
* 灵活扩展各个内部组件；
* 开箱即用，简单易用性；
* 支持目前主流的通用的解析语法；
* 灵活多变的实时/离线抓取方式；
* 遵循Springboot规范；
* 只需要遵循引擎极少约束即可应用应用至生产环境；
* 整个引擎需要环境和依赖已完成镜像打包；
* 支持简单静态抓取；
* 复杂的动态渲染（浏览器级别）抓取；
* web自动化测试；

#### 三、引擎架构

J2crawler爬虫引擎架构图：

![J2crawler爬虫引擎架构图](http://image.jplogic.cn/img/J2crawler-archecture.png "J2crawler爬虫引擎架构图")

J2crawler爬虫引擎内部组件架构图：

![J2crawler爬虫引擎内部组件架构图](http://image.jplogic.cn/img/jplogiccloud-j2crawler-engine.png "J2crawler爬虫引擎内部组件架构图")


#### 四、Quik Start

1.  添加starter依赖
```javascript
  <dependency>
      <groupId>com.saas.jplogiccloud</groupId>
      <artifactId>jplogiccloud-starter-j2crawler</artifactId>
  </dependency>
```

2.  在springboot应用配置实例demo

按照引擎的规范创建FetchJob即可（具体原理详见以上架构图），引擎启动时自动添加Job到引擎上下文中并按照自己的定制调度该FetchJob;

```java
package com.saas.jplogiccloud.crawler.jobs;

import com.saas.jplogiccloud.starter.j2crawler.annotation.FetchJob;
import com.saas.jplogiccloud.starter.j2crawler.core.*;
import lombok.extern.slf4j.Slf4j;

import java.util.ArrayList;
import java.util.List;

@FetchJob(fetchTimeOut = 60000, jobName = "demoFetchJob")
@Slf4j
public class DemoFetchJob extends BaseFetchJob {

    @Override
    public List<FetchReq> initFetchReqs() {
        List<FetchReq> fetchReqs = new ArrayList<>();
        FetchReq fetchReq = FetchReq.builder()
                .reqUrl("http://www.ip3366.net/?stype=1&page=1")
                .onFetchBack("onFetch")
                .fetcherType(FetcherType.WEBDRIVER)
                .build();
        fetchReqs.add(fetchReq);
        return fetchReqs;
    }

    @Override
    public String[] initFetchUrls() {
        return null;
    }

    @Override
    public void onFetch(FetchResp resp) {
        try {

        } catch (Exception e) {
            log.info(">>>> demoFetchJob-> 抓取数据异常:{}", e.getMessage());
            e.printStackTrace();
        }
    }

    
    private void getCloudProxyIp(FetchResp resp, JXDocument doc) {
    }
}

```
3.  配置springboot引擎配置application.yml

```java
j2crawler:
  application:
    enabled: true
    jobnames: "poxyIpFetchJob"
    threadunit: 2
    driver:
      driverKey: "webdriver.chrome.driver"
      driverPath: "C://Users//Administrator//AppData//Local//Google//Chrome//Application//chromedriver.exe"

```

剩下的就是springboot应用的其他配置了，在这里省略；

#### 五、爬虫实例Demo

1、PoxyIpFetchJob ===> 免费代理IP抓取；
![免费代理IP抓取](http://image.jplogic.cn/img/poxyIp.png "免费代理IP抓取")
![免费代理IP抓取](http://image.jplogic.cn/img/PoxiIpfetchJob.png "免费代理IP抓取")
2、NCoVFetchJob ===> 2019NCov新型冠状疫情信息实时抓取；
![2019NCov新型冠状疫情信息实时抓取](http://image.jplogic.cn/img/nCoV1.png "2019NCov新型冠状疫情信息实时抓取")
![2019NCov新型冠状疫情信息实时抓取](http://image.jplogic.cn/img/nCoV2.png "2019NCov新型冠状疫情信息实时抓取")
![2019NCov新型冠状疫情信息实时抓取](http://image.jplogic.cn/img/nCoV3.png "2019NCov新型冠状疫情信息实时抓取")
![2019NCov新型冠状疫情信息实时抓取](http://image.jplogic.cn/img/nCoV4.png "2019NCov新型冠状疫情信息实时抓取")

#### 五、技术群交流

![jplogiccloud群二维码](http://image.jplogic.cn/img/Jplogiccloud-qcode2.png "jplogiccloud群二维码")

#### 六、其他交流

我的csdn博客地址:https://blog.csdn.net/romantichjwhjwhjw/；
我的gitee地址：https://gitee.com/romantichjw;


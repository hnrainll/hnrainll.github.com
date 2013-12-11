---
title: '一口气读完了&lt;&lt;兄弟&gt;&gt;'
author: wenhao
layout: post
permalink:  /first-post/
tags:
  - 学校生活
  - 心情日记
  - 全部
  - 读书随笔
---
# 

     那天在博客上看了余华的小说《兄弟》的片断，突然想看看这本书。今天下午正好在朋友的那儿发现了这本书的下部，抱起来就看了起来。结果一看就收不住了，不  
管后天考试，笔记还一页未看，也不管旁边有多少人，就傻瓜似的笑着，别人的责怪也无动于衷。两年了，看过的也就一堆电脑编程方面的书，其他的书基本没有看  
过。两年了，没有这种投入读书的感觉，感觉自己一会成了宋刚，一会成了李光头，自己的心随着书中的人物的命运而波动。

        
前面看着只是笑，后面看着看着就笑不出来了，想哭的冲动。余华文字很少有修饰，基本上就宋刚自杀前的那段景色描写的很凄美，别的都是白描加夸张，但没有一  
点做作。夸张的一看就知道是夸张，但想一想，又真实得自己都能感觉到。余华将整个中国的变化都浓缩在一个小镇里，将多少人的经历命运都浓缩在兄弟两人的身  
上，所以有这夸张又真实的感觉。对宋刚的感觉深刻一些，或许是作者描写宋刚的心理状况的情况多一些，或许是宋刚那种敏感又固执的性格和自己有点相似。

       
心理过于细腻敏感的人适合于倒弄点文字，或者研究什么的，但命运单单不给宋刚这么个机会，而浮躁经济下的市场需要的是刘作者那样的贩卖文字的人，于是宋刚  
注定的悲剧命运。这也就是为什么在残酷的环境下，这样的人往往无法生存，为什么文革时候那么多作家自杀。这样的人对精神上的支柱过于依赖，而这种精神支柱  
往往是最容易被击碎的，无论这种精神支柱是爱情，理想，还是事业。这种人对事业的追求也偏重于感觉，很少用世俗所追求的金钱或名声衡量，所以这种事业无论  
成功还是失败，都带有悲剧性色彩。

       看完了小说，写了这么篇博客，终于深深喘一口气。最近一段时间的郁闷和彷徨也豁然消散。人有的时候感情不能过于敏感。

### Twitter Search is Now 3x Faster

In the spring of 2010, the search team at Twitter started to rewrite our search engine in order to serve our ever-growing traffic, improve the end-user latency and availability of our service, and enable rapid development of new search features. As part of the effort, we launched a new [real-time search engine][1], changing our back-end from MySQL to a real-time version of [Lucene][2]. Last week, we launched a replacement for our Ruby-on-Rails front-end: a Java server we call Blender. We are pleased to announce that this change has produced a 3x drop in search latencies and will enable us to rapidly iterate on search features in the coming months.

## PERFORMANCE GAINS

Twitter search is one of the most heavily-trafficked search engines in the world, serving over one billion queries per day. The week before we deployed Blender, the [#tsunami][3] in Japan contributed to a significant increase in query load and a related spike in search latencies. Following the launch of Blender, our 95th percentile latencies were reduced by 3x from 800ms to 250ms and CPU load on our front-end servers was cut in half. We now have the capacity to serve 10x the number of requests per machine. This means we can support the same number of requests with fewer servers, reducing our front-end service costs.

[![][5]][5]

[][5]*95th Percentile Search API Latencies Before and After Blender Launch*

## TWITTER’S IMPROVED SEARCH ARCHITECTURE

In order to understand the performance gains, you must first understand the inefficiencies of our former Ruby-on-Rails front-end servers. The front ends ran a fixed number of single-threaded rails worker processes, each of which did the following:

 

*   parsed queries
*   queried index servers synchronously
*   aggregated and rendered results

 

We have long known that the model of synchronous request processing uses our CPUs inefficiently. Over time, we had also accrued significant technical debt in our Ruby code base, making it hard to add features and improve the reliability of our search engine. Blender addresses these issues by:

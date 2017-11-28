title: Python爬虫之Scrapy上手指南
date: 2017-11-28
tages:
- Python
- Scrapy
- 爬虫
-----

## 介绍

目前学习了2周机器学习+数据分析方面的知识，但是一直没有实践。网上有一些测试数据可供练习Pandas和可视化，但是还是觉得很假，造出来的数据。于是我想写个爬虫，在网上抓抓数据，实战一下。

现在机器学习和数据方向的工作很热门，但是作为我来说还是不太了解职场的行情，于是我萌生了抓抓招聘网站的数据想法。因为提到招聘网站，我第一个想到就是猎聘网，所以我就选取它作为抓取的对象。

抓取工具方面，之前有使用过原生requests + beautifulSoup + 正则的方式抓取过链家网的房价数据。纯练手还是可以，但是我们的目的是获取数据，因此最快抓取到数据才是我们的目的。
于是乎，选择了Scrapy，作为我的抓取工具，本文也是对我建立工程的介绍以及Scrapy快速上手的指南。

## Scrapy 快速上手

我使用了 Anaconda 2的Python环境，安装 Scrapy是一件很轻松的事：

```
pip install scrapy
```
此外 [scrapy-cookbook中文版](http://scrapy-cookbook.readthedocs.io/zh_CN/latest/scrapy-01.html)也是很好的阅读材料，可以帮我们快速上手。

接下来可以使用 Scrapy 了，这部分内容部分来自截取[教程](http://scrapy-cookbook.readthedocs.io/zh_CN/latest/scrapy-02.html)：

- 创建一个新的Scrapy工程
- 定义你所需要要抽取的Item对象
- 编写一个spider来爬取某个网站并提取出所有的Item对象
- 编写一个Item Pipline来存储提取出来的Item对象

在开始之前,我首先访问了猎聘网,并设计了我需要的数据字段:
```
工作编号	工作名称	薪资水平	地点	学历要求	工作经验	工作描述	公司编号	公司名称	公司详情
job_id	job_title	salary	address	education	experience	job_description	company_id	company_name	company_detail

```
可以看出，数据是包括工作信息和公司信息的。

当我在猎聘搜索职位时，URL是这样的：
```
https://www.liepin.com/zhaopin/?pubTime=&ckid=1332aa8f01903528&fromSearchBtn=2&compkind=&isAnalysis=true&init=-1&searchType=1&flushckid=1&dqs=020&industryType=&jobKind=&sortFlag=15&industries=&salary=20$30&compscale=&key=%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90+%E6%8C%96%E6%8E%98&clean_condition=&headckid=1332aa8f01903528&d_pageSize=40&siTag=QO8nKG85cnMdx-KPcDMiNQ~r3i1HcfrfE3VRWBaGW6LoA&d_headId=bbf230b06ecffc26c174201bc44f6c50&d_ckId=bbf230b06ecffc26c174201bc44f6c50&d_sfrom=search_unknown&d_curPage=0
```
<img src="/assets/20171128/liepin.png"> </img>

可以看到搜索条件可以包含：薪水范围，工作名关键字，行业，分页信息。

可以说相当完善了，于是我选择如下url作为我起始抓取的URL，并将工作关键词设置为“数据分析  挖掘”

```
https://www.liepin.com/zhaopin/?d_pageSize=40&industries=040&dqs=020&key=%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90++%E6%8C%96%E6%8E%98&d_curPage=1
```

## 创建工程和设定item

采集的数据模型建好以后，可以使用scrapy 创建工程采集数据了。

```
scrapy startproject data_analyzer_jd
cd data_analyzer_jd
```

其中`data_analyzer_jd`可以改成你的工程的名称。

根据我的模型，我在 `items.py`中如下定义：
```python
import scrapy


class JobDetailItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    job_id = scrapy.Field()
    job_title = scrapy.Field()
    salary = scrapy.Field()
    salary_min = scrapy.Field()
    salary_max = scrapy.Field()
    job_req = scrapy.Field()
    address = scrapy.Field()
    education = scrapy.Field()
    experience = scrapy.Field()
    job_desp = scrapy.Field()
    comp_id = scrapy.Field()
    comp_name = scrapy.Field()
    comp_detail = scrapy.Field()

```

## 分析网页提取信息

接下来，需要定义我们的`spider`来抓取页面信息了，`spider`需要定义在 spiders 目录下。

```python

class JobDetailSpider(scrapy.Spider):
    name = 'jb'
    allowed_domains = ['liepin.com']

    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.143 Safari/537.36',
    }

    def start_requests(self):
        url = 'https://www.liepin.com/zhaopin/?d_pageSize=40&industries=040&dqs=020&key=%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90++%E6%8C%96%E6%8E%98&d_curPage=1'
        yield Request(url, headers=self.headers)

    def parse(self, response):
        pass
```

这里我定义了一个名为`JobDetailSpider`的spider, 一个spider可以看成是一类抓取任务，我们需要不断的生成抓取的URL、实现抓取内容的逻辑。

抓取的内容分为2步：
- 首先，我在首页获取、解析一个页面中40条工作信息的详情URL，解析下一页的URL并放入放入待抓取的队列中
- 解析每一个工作的详情页，使用XPath解析得到具体的item

下图是第一步，可以看到链接的具体URL。
<img src="/assets/20171128/s1.png"> </img>

下图是第二步，可以看到我们需要采集的具体内容。

<img src="/assets/20171128/s1.png"> </img>

这2步的逻辑都写在 `parse(self, response)`这个方法中。

### XPath的介绍

其实逻辑比较简单，就是 XPath语法的使用，这里简单提一下XPath。

如下一个文档结构：

```html
<html>
<body>
    <div class="hehe">
        <ul class="lalal">
            content
        </ul>
        <span>
            some words
            <a href="http://xxx/">Link</a>
        </span>
    </div>
</body>
</html>
```
想要获取到ul的内容，可以这样写：
```
//ul[@class="lalal"]/text()
```
`//`表示从文件根开始查找，不管中间节点，一直找到就行。
`ul[@class="lalal"]`表示找到css属性为lalal的ul标签。
`/text()`表示取该标签的文本，不包括格式。

我如果想要 `<a>`的地址如何写呢，如下：
```
//span/a/@href
```
更多的请自行谷歌了

## 启动爬虫

运行命令：
```
scrapy crawl jb -o items.csv
```
这样，抓取的数据就保存到items.csv中了，开心~

## 其他

我还写了2个Pipeline用于处理抓取到的item，比如去除html标签，和用正则提取薪水的上限和下限。
写了一个run.py，可以按照日期命名保存的数据。

接下来的，我利用采集的数据，简单分析了一下，使用jieba中文分词，统计了工作要求的高频词汇，并制作了图云，先放一波图。

工具的要求
<img src="/assets/20171128/r1.png"> </img>

工作内容的要求
<img src="/assets/20171128/r2.png"> </img>

## 小结

以上就是对Scrapy工具快速上手的介绍，所有的代码放在这里[https://github.com/lxyangfan/job_analyser](https://github.com/lxyangfan/job_analyser)
接下来，可以再介绍词云的生成，以及探究一下工作年限、掌握的技能跟薪水之间的关系，目测可以使用贝叶斯回归来做（因为不久前才学，想试试...)
学习使用scikit机器学习包，玩玩这个数据。


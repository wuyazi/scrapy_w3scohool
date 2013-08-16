from scrapy.selector import HtmlXPathSelector
from scrapy.contrib.linkextractors.sgml import SgmlLinkExtractor
from scrapy.contrib.spiders import CrawlSpider
from scrapy.http import Request
from w3school.items import W3SchoolItem

class ContentSpiderSpider(CrawlSpider):
    name = 'content_spider'
    allowed_domains = ['w3school.com.cn']
    start_urls = ['http://www.w3school.com.cn',]

    def parse(self,response):
        """from start_urls select a url"""
        hxs = HtmlXPathSelector(response)
        second_urls = hxs.select('/html/body/div/div[@id="navsecond"]//ul/li/a[text()="HTML5"]/@href').extract()
        urls = [self.start_urls[0]+second_urls[0],]
        try:
            yield Request(urls[0],callback=self.parse_second)
        except Exception,e:
            print "--------------------------------\n--",e

    def parse_second(self,response):
        """from the url select second_urls"""
        hxs = HtmlXPathSelector(response)
        third_urls = hxs.select('/html/body/div/div[@id="navsecond"]/div[@id="course"]/ul//li/a/@href').extract()
        urls = [self.start_urls[0]+url for url in third_urls]
        for url in urls:
            try:
                yield Request(url,callback=self.parse_third)
            except Exception,e:
                print "--------------------------------\n--",e

    def parse_third(self,response):
        """from second_urls select content"""
        hxs = HtmlXPathSelector(response)
        site = hxs.select('/html/body/div/div[@id="maincontent"]')
        item = W3SchoolItem()
        item['title'] = site.select('h1/text()').extract()[0]
        item['content'] = ''
        for site_line in site.select('div/descendant::*/text()').extract():
            item['content'] = item['content'] + site_line
        yield item

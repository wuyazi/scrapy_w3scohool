# Scrapy settings for w3school project
#
# For simplicity, this file contains only the most important settings by
# default. All the other settings are documented here:
#
#     http://doc.scrapy.org/topics/settings.html
#

BOT_NAME = 'w3school'
BOT_VERSION = '1.0'

SPIDER_MODULES = ['w3school.spiders']
NEWSPIDER_MODULE = 'w3school.spiders'
USER_AGENT = '%s/%s' % (BOT_NAME, BOT_VERSION)

DOWNLOAD_DELAY = 2
RANDOMIZE_DOWNLOAD_DELAY = True

ITEM_PIPELINES = ['w3school.pipelines.JsonWriterPipeline']

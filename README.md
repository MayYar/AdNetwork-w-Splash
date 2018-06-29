# AdNetwork-w-Splash

- Pulling from scrapinghub/splash
  
  ```
  docker pull scrapinghub/splash
  ```

- Run docker and visit Splash on port 8050(http)
  
  ```
  docker run -p 8050:8050 scrapinghub/splash
  ```
  
## Configuration

- In  ```setting.py ```

  To activate a downloader middleware component, add it to the ```DOWNLOADER_MIDDLEWARES``` and ```SPIDER_MIDDLEWARES``` setting

  ```
  DOWNLOADER_MIDDLEWARES = {
  'scrapy_splash.SplashCookiesMiddleware': 723,
  'scrapy_splash.SplashMiddleware': 725,
  'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware': 810,
  'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
  }
  ```

  ```
  SPIDER_MIDDLEWARES = {
      'scrapy_splash.SplashDeduplicateArgsMiddleware': 100,
  }
  ```
  The class used to detect and filter duplicate requests. <br />
  (need to set the ```dont_filter``` parameter to ```True``` on the specific Request)
  ```
  DUPEFILTER_CLASS = 'scrapy_splash.SplashAwareDupeFilter'
  ```
  change the HTTP cache storage backend with the ```HTTPCACHE_STORAGE``` setting
  ```
  HTTPCACHE_STORAGE = 'scrapy_splash.SplashAwareFSCacheStorage'
  ```
  If you want to process response codes outside 200-300 (successful responses), you can specify which response codes the spider is able to handle using the ```HTTPERROR_ALLOWED_CODES``` setting.
  ```
  HTTPERROR_ALLOWED_CODES = [400] (# error code)
  ```
Links
-----

- Reference from [scrapy-cookbook](http://scrapy-cookbook.readthedocs.io/zh_CN/latest/scrapy-12.html)

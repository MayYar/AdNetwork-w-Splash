# AdNetwork-w-Splash

- Pulling from scrapinghub/splash
  
  ```
  docker pull scrapinghub/splash
  ```

- Run docker and visit Splash on port 8050(http)
  
  ```
  docker run -p 8050:8050 scrapinghub/splash
  ```
  Open browser an enter ```localhost:8050``` then you can see below:

  ![](https://github.com/MayYar/AdNetwork-w-Splash/blob/master/pic.png?raw=true)
  
  You can put any URL in the editbox and click "Render me !" to see the result.
  
## Configuration

In  ```settings.py ```

  1. To activate a downloader middleware component, add it to the ```DOWNLOADER_MIDDLEWARES``` and setting

  ```
  DOWNLOADER_MIDDLEWARES = {
  'scrapy_splash.SplashCookiesMiddleware': 723,
  'scrapy_splash.SplashMiddleware': 725,
  'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware': 810,
  'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
  }
  ```
  2. Enable ```SplashDeduplicateArgsMiddleware``` by adding it to ```SPIDER_MIDDLEWARES```:
  ```
  SPIDER_MIDDLEWARES = {
      'scrapy_splash.SplashDeduplicateArgsMiddleware': 100,
  }
  ```
  3. Set a custom ```DUPEFILTER_CLASS```:
  (need to set the ```dont_filter``` parameter to ```True``` on the specific Request)
  ```
  DUPEFILTER_CLASS = 'scrapy_splash.SplashAwareDupeFilter'
  ```
  4. If you use Scrapy HTTP cache then a custom cache storage backend is required:
  ```
  HTTPCACHE_STORAGE = 'scrapy_splash.SplashAwareFSCacheStorage'
  ```
  5. If you want to process response codes outside 200-300 (successful responses), you can specify which response codes the spider is able to handle using the ```HTTPERROR_ALLOWED_CODES``` setting:
  ```
  HTTPERROR_ALLOWED_CODES = [400] (# error code)
  ```

## Requirements
- [scrapy](https://scrapy.org)
- Install [scrapy-splash](https://github.com/scrapy-plugins/scrapy-splash) using pip:
```
$ pip install scrapy-splash
```
- [bs4](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) for pulling data out of HTML files

## Usage
- pass 2 argument (format: '%Y-%m-%d')
- Spider: ClickForce_login, VMFive_login

**Example**:
```
$ scrapy crawl ClickForce_login -a start_time=2018-06-15 -a end_time=2018-06-20
```
- default (last 14 days)
```
$ scrapy crawl ClickForce_login
```
## Contact
Feel free to [contact me](jyunyan.lu@gmail.com) if there's any problem.

## Links


- Reference from [scrapy-cookbook](http://scrapy-cookbook.readthedocs.io/zh_CN/latest/scrapy-12.html)



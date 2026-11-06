There are lots of web crawlers, each with their own strengths and weaknesses.
### Popular Web Crawlers
1. `Burp Suite Spider`: Burp Suite, a widely used web application testing platform, includes a powerful active crawler called Spider. Spider excels at mapping out web applications, identifying hidden content and uncovering potential vulnerabilities 
2. `OWASP ZAP (Zed Attack Proxy)`: ZAP is a free, open-source web application security scanner. It can be used in automated and manual modes and includes a spider component to crawl web applications and identify potential vulnerabilities
3. `Scrapy (Python Framework)`: Scrapy isa  versatile scalable Python framework for building custom web crawlers. It provides rich features for extracting structured data from websites, handling complex crawling scenarios, and automating data processing. Its flexibility makes it ideal for tailored reconnaissance tasks. 
4. `Apache Nutch (Scalable Crawler)`: Nutch is a highly extensible and scalable open-source web crawler written in Java. It's designed to handle massive crawls across the entire web or focus on specific domains. While it requires more technical expertise to set up and configure, its power and flexibility make it a valuable asset for large-scale reconnaissance projects.

When web crawling always be responsible and get permission especially if performing extensive or intrusive scans. Don't overload some poor soul's server
### Scrapy
#### Installing Scrapy
install using pip3
```
n00blyfe@htb$ pip3 install scrapy
```
remember nowadays you typically need to make a python environment for this first : P 
#### ReconSpider
in the example shown they used reconSpider
#### Relust.json
After running the crawler, data was saved in a JSON file
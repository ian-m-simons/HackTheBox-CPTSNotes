robots.txt is a text file telling bots which areas of a website they are allowed or not allowed to access
### What is robots.txt
ultimately, just a text file at the root directory of a website. 
### How it works
you'll have a big long list of directives suchas 
```
User-agent: * 
Disallow: /admin/
Disallow: /private/
```
this tells any user-agents that URLs starting with /private/ or /admin/ are not allowed to be accessed. 

each record has two main components a User-agent which specifies who the directive applies to, and a directive, common directives include

| Directive     | Description                                                                                                       | Example                                                      |
| ------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `Disallow`    | Specifies paths or patterns that the bot should not crawl                                                         | `Disallow: /admin/` (disallow access to the admin directory) |
| `Allow`       | Explicitly permits the bot to crawl specific paths or patterns, even if they fall under a broader `Disallow` rule | `Allow: /public/` (Allow access to the public directory)     |
| `Crawl-delay` | Sets a delay (in secords) between successive requests from the bot to avoid overloading the server                | `Crawl-delay:10` (10-second delay between requests)          |
| `Sitemap`     | Provides the URL to an XML sitemap for more efficient crawling                                                    | `Sitemap: https://www.example.com/sitemap.xml`               |
### Why Respect robots.txt
most legit crawlers and search engines will respect it because
- `avoids overburdening Servers`: limiting crawler access to certain areas, website owners can prevent excessive traffic that could slow down or crash their servers
- `Protecting Sensitive Information`: Robots.txt can shield private or confidential information from being indexed by search engines
- `Legal and Ethical compliance`: In some cases, ignoring robots.txt directives could be considered a violation of a website's terms of service or even a legal issues, especially if copyright comes into play

### Robots.txt in web recon
great place to find intelligence 
- find hidden directories
- Map website structure
- Detecting crawler traps (honeypots to lure malicious bots)
- 
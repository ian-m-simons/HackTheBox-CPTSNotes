Crawling is the automated process of systematically browsing the world wide web. 
### How Web Crawlers work
you give a web page, it will fetch the page, parse the content, and extract all links, it then adds these links to a queue and crawls them, repeating iteratively. 
### Breadth first crawling,
prioritizes exploring a websites width before going deep, ie finds all links on home page before going down a level etc great for a broad overview

### Depth-first crawling
prioritizes following a single path of links as far as possible before backtracking and exploring other paths, good for specific content or reaching deep into a website's structure

### Extracting Valuable Information
crawlers can extract a diverse array of data, each serving a specific purpose in the reconnaissance process
- `Links (Internal and External)` allows you to map out a website's structure, and discover hidden pages and identify relationships with external resources
- `Comments`: Comments sections on blogs, forums, or other interactive pages can be a goldmine of information. Users often inadvertently reveal sensitive details, internal processes, or hints of vulnerabilities in their comments
- `metadata`: refers to data about data. things like page titles, descriptions, keywords, author names, and dates
- `Sensitive files`: can configure crawlers to look for sensitive files that may be inadvertently exposed including thinks like backups, config files, log files, and API keys, sometimes even database credentials, encryption keys, or code snippets
### The Importance of Context
the real value here is in connecting the dots, ie a comment on a post + a discovered config file. 
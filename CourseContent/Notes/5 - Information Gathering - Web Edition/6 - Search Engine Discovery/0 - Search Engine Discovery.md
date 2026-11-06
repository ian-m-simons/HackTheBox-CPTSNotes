You can find a ton of information using search engines. doing so, is called OSINT (open source intelligence) gathering. if you know how to look you can find all sorts of things.

### Why Search Engine Discovery Matters
- `Open Source`: The information gathered is publicly accessible, making it a legal and 'ethical' way to gain insights into a target
- `Breadth of information`: Search engines index a vast portion of the web, offering a wide range of potential information sources.
- `Ease of Use`: Search engines are user friendly and require no specialized tech skills
- `Cost-effective`: free and easily available
This information can be used for all sorts of things, but some information may be deliberately hidden or protected.

### Search Operators
special commands and modifiers that give you extra precision and control when searching, it lets you pinpoint specific types of information (think google dorking)

there may be some difference between search engines, but view the following

| Operator                | Operator Description                                        | Example                                             | Example Description                                                                    |
| ----------------------- | ----------------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `site:`                 | Limits results to a specific website or domain              | `site:example.com`                                  | Find all publicly accessible pages on example.com                                      |
| `inurl:`                | finds pages with a specific term in the URL                 | `inurl:login`                                       | search for login pages on any website                                                  |
| `filetype:`             | Searches for files of a particular type                     | `filetype:pdf`                                      | Find downloadable PDF documents                                                        |
| `intitle:`              | Finds pages with a specific term in the title               | `intitle:"confidential report"`                     | Look for documents titled "confidential report" or similar variations                  |
| `intext:`or `inbody:`   | searches for a term within the body text of pages           | `intext:"password reset"`                           | Identify webpages containing the term "Password reset"                                 |
| `cache:`                | Displays the cached version of a webpage (if available)     | `cache:example.com`                                 | view the cached version of example.com to see its previous content                     |
| `link:`                 | Finds pages that link to a specific webpage                 | `link:example.com`                                  | Identify websites linking to example.com                                               |
| `related:`              | Finds websites related to a specific webpage                | `related:example.com`                               | Discover websites similar to example.com                                               |
| `info:`                 | provides a summary of information about a webpage           | `info:example.com`                                  | Get basic details about example.com such as its title and description                  |
| `define:`               | provides definitions of a word or phrase                    | `define:phishing`                                   | Get a definition of "phishing" from various sources                                    |
| `numrange:`             | searches for numbers within a specific range                | `site:example.com numrange:1000-2000`               | finds pages on example.com containing numbers between 1000-2000                        |
| `allintext:`            | finds pages containing all specified words in the body text | `allintext:admin password reset`                    | searches for pages contaning both "admin" and "password reset" in the body text        |
| `allinurl:`             | Finds pages containing all specified words in the URL       | `allinurl:admin panel`                              | Look for pages with Admin and Panel in the url                                         |
| `allintitle:`           | Finds pages containing all specified words in the title     | `allintitle:conffidential report 2023`              | Search for pages with "Confidential" "Report", and "2023" in the title                 |
| `AND`                   | Narrows results by requiring all terms to be present        | `site:example.com AND (inurl:admin OR inurl:login)` | Find admin or login pages specifically on example.com                                  |
| `OR`                    | Broadens results by including pages with any of the terms   | `inbody:"linux" OR "ubuntu" OR "debian`             | search for webpages mentioning linux, ubuntu, or debian in the body                    |
| `NOT`                   | excludes results contaning the specified term               | `site:bank.com NOT inurl:login`                     | Find pages on bank.com excluding login pages                                           |
| `*` (wildecard)         | Represents any character or word                            | `site:secialnetwork.com filetype: pdf user* manual` | search for user manuals (userguide, user handbook) in pdf format on social network.com |
| `..` (range search)     | finds results within a specified numerical range            | `site:ecommerce.com "price" 100..500`               | look for products priced between 100-500 on an ecommerce website                       |
| `" "` (quotation marks) | Searches for exact phrases                                  | `"information security policy"`                     | Find documents mentioning the exact phrase "information security policy"               |
| `-` (minus sign)        | excludes terms from the search results                      | `site:news.com -inurl:sports`                       | Search for news articles on news.com excluding sports-related content                  |
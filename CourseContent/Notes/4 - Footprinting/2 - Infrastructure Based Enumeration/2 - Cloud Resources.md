Cloud has changed the game, notably we need to be familiar with AWS Azure and GCP. Even though cloud providers secure their infrastructure, that doesn't mean that their clients secure the products they pay for. Usually this starts with storage (AWS = S3, Azure = blobs) which can be accessed without authentication if configured incorrectly.
Usually cloud storage is added to the DNS list to make it easier for employees to reach and manage them. Another easy way to find cloud storge is google dorks. see the below table

| Dork                                                 | Target          |
| ---------------------------------------------------- | --------------- |
| `intext: <company-name> inurl:amazonaws.com`         | AWS resources   |
| `intext: <company-name> inurl:blob.core.windows.net` | Azure resources |
be able to recognize links to aws and azure resources you may see them in html source code from time to time. you can also find a lot from third party providers see the table below

| provider                                         | Description                                               |
| ------------------------------------------------ | --------------------------------------------------------- |
| [domain.glass](https://domain.glass)             | grab infrastructure details (using primarily DNS I think) |
| [grayhatwarfare.com](https://grayhatwarfare.com) | find cloud storage                                        |
ensure that you learn enough about your target to find common name abbreviations, then search those as those are also commonly used to name things. You never know what you'll find but sometimes you'll get extremely lucky and find an ssh key.
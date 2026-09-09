### Different Formats
always save your results either raw (`-oN`) greppable (`-oG`), or XML (`-oX`) can also use `-oA` for all

### Style sheets
to convert the xml document to an html document use xsltproc
```
n00blyfe@htb$ xsltproc target.xml -o target.html
```
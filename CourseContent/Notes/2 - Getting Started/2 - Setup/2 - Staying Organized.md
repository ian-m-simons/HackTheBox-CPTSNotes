Staying organized is critical to success. This is true regardless of if you are studying, playing CTF's, or on a legitimate pentesting engagement. 
### Folder Structure 
ensure that we have a clear folder structure to save data such as 
- scoping information
- enumeration data
- evidence of exploitation attempts
- sensitive data such as credentials
- other data obtained during recon, exploitation, and post-exploitation
below is a sample folder structure
```shell
n00blyfe@htb[/htb]$ tree Projects/ 

Projects/ 
└── Acme Company
	├── EPT 
	│   ├── evidence 
	│   │    ├── credentials 
	│   │    ├── data 
	│   │    └── screenshots 
	│   ├── logs 
	│   ├── scans 
	│   ├── scope 
	│   └── tools 
	└── IPT 
		├── evidence 
		│    ├── credentials 
		│    ├── data 
		│    └── screenshots 
		├── logs 
		├── scans 
		├── scope 
		└── tools
```
in the above example we have an internal and external penetration test (IPT and EPT). Each has its own folder and and subfolders. A lot of this will come down to personal preference and figuring out what works best for you. Spend the time and figure out a system, it will pay dividends. 
### Note Taking Tools
Some popular options include 
- Cherrytree
- VSCode
- Evernote
- Notion
- GitBook
- Sublime Text 
- Notepad++
We will use the tool blessed by God himself Obsidian.
>pro tip from both Hack the Box and John Hammond, learn to use markdown to take notes
### Other Tools and Tips
Maintain your own professional knowledge base. Include quick reference guides for common setup tasks, and cheat sheets for common commands. As we complete modules, aggregate everything into your knowledge base. HTB will often include cheat sheets which you should integrate into your knowledge base. Additionally create checklists, report templates, and a findings/vulnerability database which includes: a finding title, description, impact, remediation advice, and references. this will save you a ton of time and energy when writing your reports. 
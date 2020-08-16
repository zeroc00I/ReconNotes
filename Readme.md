[Shortcut to Extract Subdomains and running services]
---
| Website | Comment |
|--- | --- |
http://zoomeye.org | Powerfull. Search automatically for exploits on running services<br> Allows only 20 requests on free tier
http://netograph.io | Useless. Low data<br>
https://www.nerdydata.com/ | Useless/Marketing stuff<br>
http://intelx.io | Very impressive. There are many emails with passwords extracted of many databases leaked. Very helpfull to Redteams Companies which have to see whats is going on with your employes email<br>
http://fofa.so | Limited. You must have an API key to see more than one page<br>
http://onyphe.io | Useless, Single target<br>
http://app.binaryedge.io | Powerfull. Can filter by iot, ports, products, ASN. Allows 250 requests per month<br>
http://shodan.io | Top tool. Expensive. You should buy when it is on chinese blackfriday. Also, recommend you to monitor shodan's twitter for new update or promotions<br>
http://viz.greynoise.io | Few contents, although makes automatically exploits on running services, e.g: Its seems exploitable to eternal blue<br>
http://ivre.rocks | Use Zeek (formerly known as Bro), Argus and Nfdump/ Isnt Website tool<br>
https://spyse.com/search/subdomain | Amazing table view. No search limits, although doesn't make advanced things. It's make like a research about service or product<br>
https://community.riskiq.com/search/ | There are a lot of contents, but seems useless. I cant see anything sensitive<br>

# Process/Methodology:
## 1. Attacks(Test on Subdomains first if Target has no subdomains or not juicy subdomains then go for main Domain.)
	
	All Subdomains:-
	1) XSS
	2) Host Header Injection
	3) Open Redirection through WaybackURLS
	4) Improper Access Control & Parameter Tampering(Forgot password,price etc)
	5) HTML Injection(like xss,reflect back our HTML code)
	6) File Inclusion(upload malicious file using LFI,RFI(search in burp for file://,url,redirect etc.) , path traversal(var/www/html),run with url)
	7) SPF(no valid SPF Records)-Sender Policy Framework
	8) CORS -Cross Origin Resource Sharing(Change Origin by curl or burp search:Access control.. and get XML code)
	9) SSRF- Server Side Request Forgery(../etc/passwd)(Read Unrestrted file,Scn intrnl network,Rfi(Execute Own Code))
	10) Critical file Search (use wordlist and on main domain)
	11) Sorce Code Disclosure(use burp search file://login.php,try to find sql code,site:domain.com index.of.backup)
	12) CSRF-GET ,POST(html file)
	13) API search using grep(Use tool for that)
	14) Authentication Bypass(use my writeup)
	15) SSTI-Server Side Template Injection (use Portswigger for help)
	16) Unicode Injection in Mail address param and use burp collborator for receiving mails. 
	17) for business logic error(use fuzzdb github)
	18) Sub Domain Takeover(HostileSubbruteforcer, sub404)
	19) Email Header Injection On Reset password Function
	20) SMTP and Host Header Injection
	21) Iframe (for Clickjacking)
	22) Check Burp History,Arjun,Hakcrawler for finding Endpoint
	23) Check Cryptography in Reset Password Token
	24) Bypassing Rate Limit
	25) Check Headers:
		X-Originating-IP:IP
		X-Remote-IP:IP
		X-Remote-Addr:IP
		X-Client-IP:IP
		X-Forwarded-Host:IP
		X-Forwarded-For:IP
	26) Directory Bruteforce
	27) Http Request Smuggling
	28) Check for Social Signon Bypass
	29) File Upload CSRF, SSRF, RCE, LFI, XXE
	30) Buffer Overflow
	31) SQL Injection(use SQLmap) https://medium.com/@hninja049/sql-injection-using-sqlmap-9d14182005a0


## 2. RECON
	Find Subdomains(use Amass,Subfinder,Sublister,Nahamsec repo,crtsh,virustotal,)
		ex: 1. amass enum -brute -d twitch.tv -src
			2. amass enum -brute -d twitch.tv -rf resolvers.txt -w bruteforce.list

			Auxiliary-
			DNSSEC
				LDNSUTILS,NSEC3WALKER,NSEC3MAP
			Github Recon
				Search for Goodies
			Dorking
				ADS key,Priv pol,TOS,AWS,S3

		-Use Directory Finder Tool(massdns,Dirbuster,GoBuster,dns-parallel-prober,blacksheepwall) also for subdomain brute force.
			commonspeak for wordlist- subdomain & url data(Not Recommended).
			Nahamsec Wordlist- Sec-list
## 3. ENUMERATE
	Port Scanning
		Massscan     ex: masscan -p1-65535 -iL $ipFile --max-rate 1800 -oG $outPutFile.log
		Nmap
	Credential Bruteforcing
		Brutespray
	Use Eyewitness for Screenshots
		webscreenshot
		Aquatone
	WayBackurl -get API's
		-to see previous version of URLs
	Xmind Organisation
		-to track the Enum process.
	Burp Vuln Scanner
		-Platform Identification CVE Searching
	Parsing javascript(Links parsing,or extracting Links from js files),Coverage for Heavy javascript sites
		ZAP AJAX SPIDER
		JSParser
		Link finder
			burp>>Engagement tools>>Find Scripts>>Copy Selected URLs and pass this to these tools
	Platform Identification
		Builtwith
		WappAlyzer
	Content Discovery/Directory Bruting
		TBHMV1
			Seclists
			Raft
			Digger Wordlists
			WPScan
			CMSMAP
		Gobuster
		Burp Content Discovery
		Robots Disallowed
		git/jhaddix/content_discoveryall.txt
	Parameter Bruting
		Parameth
		Burp Analyze Target
	Param Spider(find urls which have parameters)

------------------------------------------------------

### Blind XSS Frameworks
	LewisArdern/bXSS
  
	ssl/ezXSS
  
### SSRF
	git/jhaddix/cloud_metadata.txt
  
### IDOR-MFLAC(Insecure Direct Object Reference)
	Id's
	Hashes
	Emails
### Subdomain Takever
	git/Edoverflow/can-i-take-over-xyz
  
	s3scanner
  
	Hostilesubbruteforcer
  
### WAF
	Cloudfare/Akamai
  
	Security testing against Akamai?look for origin-sub.domain.com,origin.sub.domain.com bypass the filtering by going to the source.

### Other Useful Tools-
	Eyewitness- for Screenshots
  
	webscreenshot -for screenshots
  
	Aquatone -for screenshots
  
	HTTPSscreenshot -for screenshots
  
	Openlist Chrome Extension- open tabs with specified urls 
 	
### ASN Lookup,net,
  http://bgp.he.net,Crunchbase      for Aquistions(Other Organisations)

  Whoxy.com,
  
  DOMLink,
 
  https://builtwith.com/relationships/twitch.tv,
  Google Fu,
  
  Shodan API,
  
  and juicy Subdomains

	### tips to crawl
	webpaste
  
	meg -path find
  
	ffuf -path ''
  
	concurl -path ''
  
	comm -compares sorted files
  
	gau -fetch js files
  
	find -to list directory
  
	Arjun - Find parameters on a specific endpoint

---
### Advance Payloads:-
#### for XSS

	1. <marquee loop=1 width=0 onfinish=pr\u006fmpt(document.cookie)>Y000</marquee>  

			'">><marquee><img src=x onerror=confirm(1)></marquee>"
      
			></plaintext\></|\><plaintext/onmouseover=prompt(1)
      
			><script>prompt(1)</script>@gmail.com<isindex
      
			formaction=javascript:alert(/XSS/) type=submit>'-->"
      
			></script><script>alert(1)</script>"><img/id="confirm&lpar;
      
			1)"/alt="/"src="/"onerror=eval(id&%23x29;>'"><img src="http://i.imgur.com/P8mL8.jpg">
      ';alert(String.fromCharCode(88,83,83))//';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//--
			></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))
			</SCRIPT>

			“ onclick=alert(1)//<button ‘ onclick=alert(1)//> */ alert(1)//
#### for SQL injection used URL encode
	2. /*!50000%75%6e%69on*/%73%65%6cect 1,2,3,4,...                                     

---
### Personal Recommended tools(Left to Right Priority):-

#### for subdomains

	1. Subfinderv2,Amass,Sublister,crtsh   

#### for Finding Parameters 

	2. Arjun,ParamSpider,Parameth 
	ex: for paramspider:- python3 paramspider.py --domain healthifyme.com --exclude woff,css,js,png,svg,php,jpg --output healthifyme.txt
  
#### for Separating https & http
	3. httpx(With Title),httprobe
  
#### for Subdomains,cloud Services subdomains in js files,Use the Shannon Entropy
  4. SubDomainizer
	5.Link Discovery by GoSpider|Hakrawler|Burp Suite Pro & use advance scope as keyword 'Twitch'
  
#### Juicy Domains by Google,Crtsh,WayBackMachine
	6. SubDomain Scraping
		ex:- site:domain.com -maindomain.com -otherdomain.com (subtract main domain)
    
#### by shodan scraped subdomains
	7. Shosubgo 

#### for Subdomain Bruting
	8. Amass,ShuffleDNS,commonspeak2

####  Service Scanning 
	9. brutespray                            

####  Screenshotting 
	10. Eyewitness, Aquatone, httpscreenshot	
  
#### Subdomain takeover 
	11. (can i take over xyz),SubOver & nuclei                    

#### Automation
	12. Interlace,Pwnkey,Lazyrecon,Spiderfoot(GUI)   

#### for links,endpoints
	13. Linkfinder 

#### for API and different Payloads
	14. PayloadsAllTheThings 

---
### Automation Tools by different Hunters:-

C-Tier: automation built around scripting up other tools in bash or python. Step based, no workflow.

Few techniques. Little extensibility.

B-Tier: automation writing a few of their own modules. Some GUI or advanced workflow. Medium

techniques. Runs point-in-time. Flat files.

A-Tier: automation writing all their own modules. Has GUI. Runs iterativley. Manages data via db.

S-Tier: automation writing their own modules. Has GUI. Runs iterativley. Manages data via db. Scales

across multiple boxes. Sends alerts to user. Uses novel techniques and iterates quickly. ML + AI.

	Frameworks (C-Tier)
  
		https://github.com/AdmiralGaust/bountyRecon
    
		https://github.com/offhourscoding/recon
    
		https://github.com/Sambal0x/Recon-tools
    
		https://github.com/JoshuaMart/AutoRecon
    
		https://github.com/yourbuddy25/Hunter
    
		https://github.com/venom26/recon/blob/master/ultimate_recon.sh
    
		https://gist.github.com/dwisiswant0/5f647e3d406b5e984e6d69d3538968cd

	Frameworks (B-Tier)
		https://github.com/capt-meelo/LazyRecon https://github.com/Screetsec/Sudomy
    
		https://github.com/phspade/Automated-Scanner
    
    https://github.com/devanshbatham/Gorecon
    
		https://github.com/shmilylty/OneForAll https://github.com/LordNeoStark/tugarecon
    
		https://github.com/SolomonSklash/chomp-scan
    
		https://github.com/TypeError/domainedLazyRecon    (A-Tier)
    
		https://github.com/Edu4rdSHL/findomain
    
		https://github.com/SilverPoision/Rock-ON
    
		https://github.com/epi052/recon-pipeline

---

Tips:

	1. wc -l   ---for word count
  
	2. grep -v ".tmi"
  
	3. amass enum -brute -d twitch.tv -src
  
	4. echo $PATH -----To show all the paths where apps are installed 
  
		use export PATH=$PATH:/pathtofolder   --for path set(Temp) and add in bash.rc(for permanent)
    
		ln -s /opt/hackerEnv/hackerEnv /usr/local/bin/ --another command to create a link like shortcut
    
		https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/
    
	5. /.config/amass/config.ini -----to config api of amass
  
	6. shodan init 61TvA2dNwxNxmWziZxKzR5aO9tFD00Nj7.bYD);n%?Le984)xg2Ye3n^3Eb)9(8*g
  
	8. https://www.wolframalpha.com/input/?i=target.com       to analyze Target
  
	9. https://www.nmmapper.com/                              online subdomain finder
  
	10. https://chaos.projectdiscovery.io/#/                  Great tools for Analysis and subdoamin finder in secs.
  
	11. https://owasp.org/www-community/xss-filter-evasion-cheatsheet           XSS Cheat Sheet
  
	12. https://medium.com/@ehsahil/bash-cookbook-for-everyone-part-2-b70d40610025          Bash For Eyeryone
  
	13. https://httpstatus.io/                                Bulk url Status Checker
  
	14. https://tools.w3cub.com/                              Free Collection of Tools
  
	15.https://pentester.land/list-of-bug-bounty-writeups.html                 List of Bug Bounty Writeups

---

Tools to Install:-

	DNS Validator
  
	Bug Bounty Dorks\
  
	waybackurl

---

BUG BOUNTY PLATFORMS

	Bugcrowd
  
	Hackerone
  
	Hackenproof
  
	Bugbountyjp
  
	Intigriti
  
	Open Bug Bounty
  
	Yogosha
  
---

Best Books

	Web Application Haackers Handbook
  
	Web hacking 101
  
	Mastering Modern Web Pen Testing
  
	Bug Bounty Playbook
  
	Real World Bug Hunting
  
	Owasp Testing Guide
  
	Mobie Application Hackers Handbook
  

---

Burp Extensions
	iprotate

---

Github Repositories
	https://github.com/vishal9066/AwesomeXSS
	https://github.com/vishal9066/RegExAPI                       For API findings on Targets

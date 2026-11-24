# Burp Suite Stuff

<details>
<summary>Plugins</summary>

<dl>
<dd>

<details>
<summary>https://github.com/Co0nan/ParamsExtractor</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Best pro Extension</summary>

<dl>
<dd>

https://twitter.com/sachin_pandey98/status/1435878156062257153?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Burp Project saving</summary>

<dl>
<dd>

If you save a copy of your project, you can choose whether to include data from your Target, Proxy, Dashboard, and Repeater in your new project file.

You can find this option by going to "Project > Save copy" in Burp.

</dd>
</dl>

</details>

<details>
<summary>Burp (Match & Replace) regexes</summary>

<dl>
<dd>

https://github.com/daffainfo/match-replace-burp

<details>
<summary>Tip :</summary>

<dl>
<dd>

match and replace false to true lol

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

https://twitter.com/payloadartist/status/1422247377516122114?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Search regex</summary>

<dl>
<dd>

https://twitter.com/t1nd19d/status/1522102300990398466?s=20&t=DTRsTBz4tWFuwxorT\_khoQ

https://t.co/LKUYvLbWBr

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Pro tip: when testing for authorization issues using different profiles/browsers going through the same proxy, set a unique canary in the user agent property of one of them. Then in Burp -> Search for that canary -> Highlight all

</dd>
</dl>

</details>

<details>
<summary>Burp Sharpener</summary>

<dl>
<dd>

https://github.com/mdsecresearch/BurpSuiteSharpener

</dd>
</dl>

</details>

<details>
<summary>JSdir extension</summary>

<dl>
<dd>

<details>
<summary>Instruction</summary>

<dl>
<dd>

Jsdir is an Burp Suite extension that extract hidden url paths from js files, beautify it and save for futher/better reading. The extracted paths are printed on Burp Suite.

</dd>
</dl>

</details>

<details>
<summary>https://github.com/Lopseg/Jsdir</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>BurpJSLinkFinder</summary>



</details>

<details>
<summary>Install Jython</summary>

<dl>
<dd>

Here’s how to install Jython in Burp:

1. Download latest Jython Installer from here and install it:`java -jar jython-installer-2.7.2.jar`

2. Provide paths to Burp:Go to Extender tab -> Options sub-tab
   - In Java Environment sectionFolder for loading library JAR files (optional): `/home/user/burp/addons`
   - In Python Environment sectionLocation of Jython standalone JAR file: `/home/user/jython2.7.2/jython.jar`Folder for loading modules (optional): `/home/user/burp/addons`

</dd>
</dl>

</details>

<details>
<summary>Usefull Extensions</summary>

<dl>
<dd>

https://twitter.com/harshbothra_/status/1299720306777415680

</dd>
</dl>

</details>

<details>
<summary>Burp Repeater Tricks</summary>

<dl>
<dd>

https://twitter.com/tabaahi_/status/1507405006621884420?s=20&t=89qxXEQoSLSAbcu7JdhQDA

</dd>
</dl>

</details>

<details>
<summary>https://github.com/Elsfa7-110/GoldenNuggets-1 extension</summary>



</details>

<details>
<summary>https://github.com/wagiro/BurpBounty extension</summary>



</details>

<details>
<summary>https://github.com/xsuperbug/BurpParamFlagger extension</summary>



</details>

<details>
<summary>Highlight requests that have never appeared in Burp history</summary>

<dl>
<dd>

extensions :

1. Scope Monitor

2. Progress Tracker

</dd>
</dl>

</details>

<details>
<summary>Shortcuts</summary>

<dl>
<dd>

https://twitter.com/rez0__/status/1562118093412995073?s=20&t=_831qCX4RPyKiAIP8NhfMQ

</dd>
</dl>

</details>

<details>
<summary>Adding scopes in Burp</summary>

<dl>
<dd>

1) Go to target-> Scope-> Use advance scope control-> add  
2) Add Host regex: .\*\.facebook\.com$  
3) go to Site map-> Show only in-scope items  
4) All subdomains of http://facebook.com added :)

</dd>
</dl>

</details>

<details>
<summary>Blacklist useless scopes interfering through proxy</summary>

<dl>
<dd>

Burp Suite > Proxy > Options > TLS Pass Through.  
Add these:  
.*\.google\.com  
.*\.gstatic\.com  
.*\.mozilla\.com  
.*\.googleapis\.com  
.\*\.pki\.goog  
No more noise in your logs!

</dd>
</dl>

</details>

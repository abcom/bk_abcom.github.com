---
layout: post
title: "Django Security Checklist"
description: ""
categories: Django python XSS CSRF security checklist 
tags: [django, XSS, CSRF, security]
---
{% include JB/setup %}

People tend to finish projects as quickly as possible and deploy in production environment, sometimes forgetting about security aspect of the project. You have already spent amount of time for developing, testing your application and got hacked right after the deploying into production, then what?! Thus, you should always spend some time to review your configurations and settings from security perspective. 

I know most of us are very busy and don't have time to check all of those settings, so this is where a basic security checklist becomes a handy. This post mainly addresses major security concerns with respect to [Django framework](http://djangoframework.com) and lists down common security settings specific to Django. 

You don't have to follow all of these, but it's strongly recommended.

**Django security checklist**


1.	**Secret Key:** 
	Set your secret key to a big random unique value and keep it always secret.  Do not hardcode it, source it from the environment variables. 
2.	**Database passwords:**
	Follow point #1 for Database passwords.
3.	**Debug Mode:** 
	You must never enable DEBUG in production environment. `DEBUG = False` 
4.	**Use HTTPS:** 
	Always use site-wide HTTPS (if possible) and route HTTP traffic to HTTPS. Assuming you have enabled HTTPS, set the following in `settings.py`:

	- `SESSION_COOKIE_SECURE = True` - To transfer session cookies only from HTTPS 
	
	- `CSRF_COOKIE_SECURE = True` - To avoid <a href="https://en.wikipedia.org/wiki/Cross-site_request_forgery" >CSRF cookie</a> transfers over HTTP. More on CSRF protection in Django can be found here <a href="https://docs.djangoproject.com/en/dev/ref/contrib/csrf/">here</a>.
	- `SESSION_EXPIRE_AT_BROWSER_CLOSE = True`  - This is recommended, but not must. If you set this variable to True, it will force the users to login every time they re-open the browser. This setting may not work for some users who use browser's <i>"continue to work after re-open"</i> type of settings.  Keep in mind, one browser can be used by different people, so it's up to you to choose between more comfortable or secure user experience.
5.	**Python in root directory:**
	Don't put any Python code in your Webserver's root directory so that you won't serve your code as a plain text (unless it's an open source).
6.	**Upload file size:**
	Set a reasonable file size limit if you serve user file uploads. This will help to hinder DoS attacks.
7.	**Restricted Access:**
	Don't forget to put ` @login_required ` decorator wherever you require the restricted access, be it entire views or specific actions.
8.	**Raw SQL:**
	Don't bypass Django's ORM layer to avoid SQL injection. Don't use raw SQL queries like `raw()` and don't execute custom SQL directly.
9.	**Quote attributes:**
	Quote all attributes in your HTMLs where dynamic data is inserted. For instance,{% capture text %}<img... alt=variable...>{% endcapture %}{% include JB/liquid_raw %}is not good, but{% capture text %}<img... alt="variable"...>{% endcapture %}{% include JB/liquid_raw %} is good. This will help you to avoid XSS attack.<br>
10.	**Security updates:**
	Keep track of Django and Python core team blogs for the latest security updates. 
	Also, checkout [django-secure](http://django-secure.readthedocs.org/en/latest/index.html) to help you with basic Django security steps.

**Please let me know if you have any suggestions or additions, would be glad to update the post.**

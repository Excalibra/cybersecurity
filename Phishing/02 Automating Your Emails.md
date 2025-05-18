# Social Engineer's Toolkit (SET)

## What is SET?
The social engineer's toolkit is everything you need to perform a variety of social engineering attacks. You can perform everything from spearfishing, copying websites, mass mailers, and even powerful attacks. There are a couple of ways to launch it. You can launch it from the GUI (graphical user interface) by clicking Application → Social Engineering Tools → Social Engineer's Toolkit, or from the command line with the command `setoolkit`.

## lab
![image](https://github.com/user-attachments/assets/a8ce7c34-7cb3-45bb-8f87-6085b42d25ad)

# Attacking With SET
## Attacking with SET
- In this video we’re going to perform an actual phishing attack using SET.
- Remember! This course and lab are for learning purposes only. What I’m about to show you is intended to expand your knowledge and skills, to make you a better penetration tester and cyber security expert. I am not responsible if you decide to break the law.

## Attack Prep
1. Clone the website.
   - Target: http://testphp.vulnweb.com/login.php
   - Use SET credential harvester to clone the website.

2. Prepare your email.
   - Remember the keys to a good phishing email.
   - Sender, subject, email address, email details, emotional buy-in.

3. Send the email.

## Cloning Websites

- One of the best ways to capture credentials is by cloning a website.
- You can use SET to do this and capture any input!
- After launching SET, you’ll need to select 2) Website Attack Vectors.

## Lab
1.`setoolkit`
2. `1) Social-Engineering Attacks` / `2) Website Attack Vectors`
3. We want to capture credentials, so we sellect `3) Credential Harvester Attack Method`
4. We would like to clone a website, so `2) Site Cloner`

## Sending your email
- Now that we've cloned our website, we're going to send our phishing email to the target, directing them to our login page.

set> `5) Mass Mailer Attack` set> `1) E-Mail Attack Single Email Address`

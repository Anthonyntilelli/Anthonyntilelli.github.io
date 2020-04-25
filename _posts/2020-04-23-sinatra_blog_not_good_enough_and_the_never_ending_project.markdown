---
layout: post
title:      "Sinatra Blog: Working with Emails."
date:       2020-04-23 22:50:39 -0400
permalink:  sinatra_blog_not_good_enough_and_the_never_ending_project
---


The email has become one of the de facto ways a user is identified on a system (at least in the USA).  This is due to their uniqueness, and popularity, and end-user simplicity.  If a user needs to verify their email ownership or reset their password, simply send an email with a link for the user to for them to click on.  However, while email is simple for the end-user, there are important considerations for application authors. Email is not secure and should not contain sensitive information. Anti-Spam and anti-virus efforts have made working with email more complex. Comprise of an email account can lead to compromise of your application's account.

Classic email communication is similar to sending a postcard, any service in that transits the email can read its contents.  There is some effort to [secure email in transit](https://starttls-everywhere.org/) or [secure message body](https://en.wikipedia.org/wiki/GNU_Privacy_Guard), however, adoption is limited for both. Adding message-level encryption confused most users and, at the moment, there is little value in adding a message encryption option to your application. You should not send sensitive information by email, such as [personally identifiable information](https://en.wikipedia.org/wiki/Personal_data). Different applications will be affected by this, to some extent depending on the industry, it's used in.  Special care should be taken when dealing with financial or healthcare-related data as information leaks can lead to fines or worse for you or your organization. 

Email technology was designed as a very simple and robust protocol it was one of the preferred ways to alert and communicate. Many classic Unix tools, such as Cron, would email the root user when needed. However, due to email spam/spoofing, email usage has become significantly more restricted, and no longer could any application generate an email. Several anti-spam solutions were devised to filter spam and prevent spoofing, which is again at various levels of adoption. There are several hurdles and gatekeepers now preventing emails from being delivered. The first major hurdle is that you must be authorized to send an email for the desired domain via [dns records](https://www.godaddy.com/garage/configuring-dns-for-email-a-quick-beginners-guide/). Even if you are authorized you will still not be able to send the email from many locations, most ISPs and major cloud providers block the [port](https://cloud.google.com/compute/docs/tutorials/sending-mail/) email is sent on and third party anti-spam companies will have an ever-rotating [email black list](https://mxtoolbox.com/blacklists.aspx), which you will need to appeal. It is not unheard of for a service such as Gmail to occasionally get a few IP blacklisted. The final hurdle is the heuristic anti-spam solution use by those receiving email. A popular solution is a tool called Spam Assasin, if you are getting several dropped emails, it can be helpfull to evaluate sample email again it. Most bounce backed email will an error message on the error. 

TODO: Danger of reset links 

TODO: solution managed  provider




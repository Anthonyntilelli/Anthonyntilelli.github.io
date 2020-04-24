---
layout: post
title:      "Sinatra Blog: Working with Emails."
date:       2020-04-23 22:50:39 -0400
permalink:  sinatra_blog_not_good_enough_and_the_never_ending_project
---


The email has become one of the de facto ways a user is identified on a system (at least in the USA).  This is due to their uniqueness, and popularity, and end-user simplicity.  If a user needs to verify their email ownership or reset their password, simply send an email with a link for the user to for them to click on.  However, while email is simple for the end-user, there are important considerations for application authors. Email is not secure and should not contain sensitive information. Anti-Spam and anti-virus efforts have made working with email more complex. Comprise of an email account can lead to compromise of your application's account.

Classic email communication is similar to sending a postcard, any service in that transits the email can read its contents.  There is some effort to [secure email in transit](https://starttls-everywhere.org/), however, adoption is not limited   You should not send sensitive information by email, such as [personally identifiable information](https://en.wikipedia.org/wiki/Personal_data). Depending on the nature of the application this may be an issue, such as banking and healthcare-related applications, and sending some information can lead to fines. Most companies will send email alerts when the users have a message and the actual message content is in the application.

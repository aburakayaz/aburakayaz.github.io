---
layout: post
title: How to install Discourse on Google Cloud
tags: 
   - discourse
   - google cloud
   - compute engine
   - installation
   - tutorial
---

For a hobby project of mine and [my friend](https://github.com/bekorn)'s, I recently installed a Discourse forum into Google Cloud. I ran into some problems and couldn't find a tutorial that covers all the issues I faced. While I was dealing with the difficulties, I decided to create a tutorial that, hopefully, will help some other people who may be dealing with these issues as well.

## Why not Bitnami?

We first tried to install Discourse using Bitnami. To be honest, installation with Bitnami was quite easy; it was just one click. But the problem started when we tried to update the Discourse version. Surely, Bitnami documentations were there, but it didn't cover all the possible issues. While I was trying to find a solution, I've read some other people's Bitnami related questions in the official Discourse forum. I saw that the developers didn't like what Bitnami is doing with their software and suggested seeking help from the Bitnami documentation. At some point, I gave up trying to solve the problems and decided to install it from scratch, without Bitnami.

## Disclaimer

This tutorial is not going to cover all the steps of the installation. I will be referring to other tutorials and try to guide you through the issues I had while following them in case you also come across them.

## Installation

### Step One: Creating a Compute VM Instance

Start by following [Google's documentation](https://cloud.google.com/compute/docs/instances/create-start-instance). 

* First, read hardware [Hardware Requirements part](https://github.com/discourse/discourse/blob/master/docs/INSTALL.md#hardware-requirements) of the Discourse's documentation.
* Unless you are familiar with command line interfaces, it's simpler to follow these steps from the console (the web application interface).
* I left most of the options as it is, but I strongly suggest you increase the storage size to at least 15 GB (10 GB by default). That is because when you need to run commands like `./launcher rebuild app`, you will need to have twice the amount of space that is required to install Discourse. Simply put, these commands create another version of your Discourse installation, it doesn't directly apply changes to the current version.

### Step Two: Installing Discourse
We will use Discourse's abovementioned documentation [here](https://github.com/discourse/discourse/blob/master/docs/INSTALL-cloud.md#create-new-cloud-server).

* It is essential to have an e-mail service before the installation. We used [SendGrid](https://sendgrid.com/) since it provides some increased limits for students by [GitHub's student developer pack](https://education.github.com/pack).
* Whatever e-mail service you're using, you need to keep in mind that Google blocks outgoing TCP 587 port. Hence, you should use 2525 instead. 
* If you're using SendGrid you need to use the smtp address `smtp.sendgrid.net` instead of `smtp.sendgrid.com`.

This is how it will look like if you use SendGrid:
```
DISCOURSE_DEVELOPER_EMAILS: 'name@example.com'
DISCOURSE_SMTP_ADDRESS: smtp.sendgrid.net
DISCOURSE_SMTP_PORT: 2525
DISCOURSE_SMTP_USER_NAME: YOUR_SENDGRID_USERNAME
DISCOURSE_SMTP_PASSWORD: YOUR_SENDGRID_PASSWORD
```

## Conclusion
If I didn't miss anything, this covers all the issues I had, I've got it to work like this. In case you have some other issues, you can check the helpful links that I provided.

## Helpful links
* <https://meta.discourse.org/t/troubleshooting-email-on-a-new-discourse-install/16326/2>
* <https://meta.discourse.org/t/how-do-i-change-my-smtp-settings-discourse-docker-install/20067>
* <https://community.bitnami.com/t/google-cloud-bitnami-nginx-stack-postfix-smtp-email-relay-failure/49184/4>





# Project 7 - WordPress Pen Testing

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pen Testing Report

### 1. Vulnerability Name or ID: CVE-2017-6817 YouTube URL XSS

- [ ] Summary: This part of the testing involved exploiting the option to embed alert messages in a post with a YouTube URL. Authenticated users are able to create a post that contains a cross site scripting attack hidden in the YouTube URL. So anyone who is visiting the site can scroll through and click on the different post. Clicking on the other post works as intended and takes you to the post, but when you click on the post that exploits this vulnerability there is a different response. As  soon as you click on the post with the exploit, you are returned with an alert message that the hacker set in the url. You can set the attack to start once a user simply moves their mouse over or clicks on the post.
  - Tested in version:WordPress version 4.2
- [ ] GIF Walkthrough: In this gif I first show the url with the embedded alert on the create a post page to show what had to be typed to exploit this vulnerability. Next I show what the page would look like for every user that visits the website. From there you can see the recent post and I interact with a normal post to show a noraml repsonse. Then I interact with the exploit to show that the message will pop up when clicked on. 
- [ ] Steps to recreate: To exploit this vulnerability I first had to make sure I had access to an authenticated users account that has contributor privileges, so I used the admin account. From there I went to create a post and set it to text editor. The post was named YouTube that appeared to contain a legit YouTube link, but it was actually not legit and contained an alert message for anyone that ended up clicking on the link. This message was able to go undetected because of a flaw with embedding in the YouTube URL. Any user who clicks the link on that page now gets a message informing them that XSS has just occurred.
- [ ] Affected source code: wpdistillery.vm/wp-content/post.php

  
### 2. (Required) Vulnerability Name or ID  CVE-2015-5623 XSS with Post

- [ ] Summary: This part of testing again involved cross site scripting with creating a post, but this time we used HTML that contained javascript to conduct the attack. Again you needed to be an authenticated user that has the ability to post, and you would insert HTML that is meant to trick users and look like a legit link that will take you to another resource. The post will show ‘link’ with an option to click it and anything you set as the title. This can be used to encourage users to click the link because they think they are going to a resource of the site, but actually they are victim of the XSS attack.
  - Tested in version:WordPress version 4.2
- [ ] GIF Walkthrough: In this gif I show the post from the admin point of view to show the HTML that was used to execute this attack. Next I show the webpage and interact with the post again. The site has numerous post that have been made, and first I interact with a normal post to show a normal response. Next I intereact with the post that has html and a link to clink on. In this exploit the user actually has to click on the link that is in the post to get the alert message to pop up. 
- [ ] Steps to recreate: To exploit this vulnerability we first have to login to an account that has the ability to create post on the site, I used the admin account. From there we went to create a post and set the editor option to text. In the actual post text box I inserted the HTML that contained javascript and set it to look like a link that the user could click on. That is why I set the code to execute once a user clicked on the link. The code contains an alert message that will popup once any user decides to click on the link. Similar to the XSS with the url, this post will show up with all the other post on the main page and won’t execute until interacted with. 
- [ ] Affected source code: wpdistillery.vm/wp-content/post.php
 

### 3. (Required) Vulnerability Name or ID CVE-2015-3440 XSS

- [ ] Summary: In this part of the testing, we found that when replying to a comment on WordPress a hacker could inject javascript and execute a XSS attack. Whatever code the hacker inserts in the reply will be executed once the main comment is clicked on. In this exploit the size of the reply is crucial because for this exploit to work the reply must be larger than the maximum size of MySQL text box and get truncated. Leaving a reply can be done by unauthenticated users, so these replies must be confirmed by the admin of the website before the reply can publicly be seen.
  - Tested in version: WordPress version 4.2 
- [ ] GIF Walkthrough: In this gif I show a portion of the long message that has to be used in the reply to be able to get the reply truncated and be able to execute the attack. Then I go to the front page of the site again to show the comments that any user can see. From there I click on the thread that contains the malicous reply and see that the script is executed and an alert message pops up. 
- [ ] Steps to recreate: To exploit this vulnerability I went to the comments on the Wordpress website, and replied to the first one. I was not logged in and I had to enter some information about myself so the site can know who is adding to their content. After putting in information about who is replying, I left my reply that contained the XSS attack. The reply is made up of the javascript that will trigger an alert message and a lot of random content too make sure my response is truncated because it is too long. Then I send the reply and wait for an authenticated user with privileges to say the reply is okay to be displayed publicly. So I validate the reply from the admin account and visit the comments of the website. As soon as a user clicks the threat that includes the response with the script, they are given an alert message that tells them XSS has occurred
- [ ] Affected source code:wpdistillery.vm/wp-content/comments.php
  

### 4. (Optional) Vulnerability Name or ID User Enumeration 

- [ ] Summary: Part of the testing involved attempting to login with some default usernames and passwords, I found that the website would return some valuable  information when the correct username was entered with the wrong password. The website would tell users if the username they are trying to login with was correct, allowing anyone to test a bunch of usernames to find valid usernames.
  - Tested in version:WordPress version 4.2
- [ ] GIF Walkthrough: In this gif I show an attacker attempting to login with default credentials to see if they can get lucky or learn some valuable information. And after entering a correct default username, the site returned some valuable infomation for the attacker. The system would tell users when they have entered the correct username, which allows attackers to enumerate users and gain info. 
- [ ] Steps to recreate: I used the admin account to create some new and random accounts with very basic usernames and passwords. Then when an attacker tries to attack the site they can continue to try common login names until the website tells the attacker that they have got a correct username. The website should only return that the login credentials were wrong and that the user needs to try again. Confirming that the user has entered the correct username makes conducting attacks easier for hackers and leaves your site more vulnerable.
- [ ] Affected source code:  http://wpdistillery.vm-login.php


### 5. (Optional) Vulnerability Name or ID CVE-2015-4133 Reflex Gallery Plugin

- [ ] Summary: This part of the testing involved installing a specific version of a plugin called Reflex Gallery. This plugin is popular for being like a photo gallery on WordPress, however this plugin also allows for file upload and remote code execution because it does not correctly sanitize user input. Allowing attackers to execute code and access files remotely gives numerous options to attackers and raises endless problems for the website owners. 
  - Tested in version:WordPress version 4.2
- [ ] GIF Walkthrough: I included two gifs related to this exploit, one is a before and after and the other is me accessing and interacting with the files and directories of the website from my kali machine. With this exploit I was able to make see the content of this webpage and delete or add files, so I removed the images that had been added with the reflex gallery plugin. I have a gif with a before and after of the site to show that the picture was deleted. And the other gif shows me interacting with the files to show I had access from my kalli machine and was able to remove files through shell. 
- [ ] Steps to recreate: I used the metasploit framework to look up known exploits that may be able to attack the website with the reflex gallery plugin. Next I specify the target website and myself as the local host, this is so I am sure I get a shell that allows me to access the website. The tool then does all the heavy lifting and returns a shell that is linked to the target site. Once the exploit has been taken advantage of, I was able to see the files and directories for the web server. I was also able to change directories and views the content in each file in the directories. Lastly I was able to use the ‘rm’  command to remove the images I added with the reflex gallery plugin that creates this exploit.
- [ ] Affected source code:http://wpdistillery.vm/wp-content/plugins/reflex-gallery/admin/scripts/FileUploader/php.php
 


## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [Kap](https://getkap.co/) for macOS


## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

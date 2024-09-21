
## **general information**

You are going to create a tutorial using markdown and hosted on GitHub or GitLab that takes a user through the steps of creating a remote server using DigitalOcean.  
- create ssh keys and add them to your DigitalOcean account  
- Add a custom Arch Linux image  
- Create a droplet running Arch Linux  
- connect to your droplet from your local machine using SSH

The tutorial should provide information on each stage so that a reader is not only able to complete the tasks but understands what they are doing and why. For example the reader should know what SSH keys are and why you are using them instead of password authentication.

Roughly aim the tutorial at the skill level and technical understanding of a 2nd term CIT student in week 1.

You don't have to include instructions on creating a DigitalOcean account. Assume that the reader can create an account without assistance.

Your tutorial should guide the reader through the stages in a clear and concise manor. Include images where appropriate to aide the reader.

The tutorial should also demonstrate your understanding of the material. This provides you with opportunity to not just complete a task, but to demonstrate that you understand the content.

This assignment has three possible levels, pick 1 of the levels and work towards that. Levels 1 and 2 were covered in class. Level 3 requires that you learn how to use `doctl` on your own.

**Level overview:**

- **Level 1 (Max grade 60%):**  
    - Create SSH keys on your local machine.  
    - Add a custom Arch Linux image using the web console  
    - Create a new Droplet running Arch Linux using the DigitalOcean web console.  
    - Connect to your server using your SSH keys.  
- **Level 2 (Max grade 85%):**  
    - Create SSH keys on your local machine.  
    - Add a custom Arch Linux image using the web console  
    - Create a Droplet running Arch Linux using the DigitalOcean web console.  
    - Use a cloud-init configuration file to automate initial setup tasks (e.g., user creation).  
    - Connect to your server using your SSH keys.  
- **Level 3 (Max grade 100%) This one is significantly more difficult than 1 and 2:**  
    - Create SSH keys on your local machine  
    - Create a Droplet running Arch Linux using the `doctl` command-line tool.  
    - Use `doctl` and cloud-init for every stage of setting up an Arch Linux droplet

## **instructions details**

**cloud-init (level 2 and 3)**  
Use a cloud-init configuration file to:  
- create a new regular user  
- install some initial packages  
- add a public ssh key to the authorized_keys file in your new users home directory  
- disable root access via ssh  
          
**markdown**  
Use clear correct markdown. Use markdown for links, images, footnotes...

Any code or commands should be in code blocks, so that they can be easily copied by a reader.

You can either test your markdown directly in GitHub/GitLab or using a third party markdown preview utility from your editor. I recommend just testing in GitHub or GitLab.

**Git**  
Make regular thoughtful commits. e.g. If you add an image, make a commit with a clear commit message. 

**citations and external resources**  
I am not going to impose a specific style guide for this assignment. Pick one and stick to it. APA is a good choice.

Any facts, or words and images that are not your own should be referenced from an appropriate source. Official documentation, peer-reviewed academic material such as a textbook. Random blogs, ChatGPT, wikipedia and stackoverflow are [https://www.markdownguide.org/)](https://www.markdownguide.org/)**not** good sources.

**level 3 only**

Install and configure `doctl` in an existing droplet and use it to create a new droplet. The `doctl` command line tool is in the Arch package repositories, so you can install it with Pacman.

Your tutorial should include instructions on installing and configuring `doctl`.

--- 
# Getting started with doctl and cloud-init

---
# Table of contents:
- [Introduction](#Introduction)
- [doctl Installation and Setup](#Second-Table)

--- 
# Introduction

This tutorial will walk you through the process of using the tools `doctl`[^1], and `cloud-init`[^2] to set up an Arch Linux droplet on Digital Ocean. 

**Things we'll need:**
- A local machine running the cloud version of Arch Linux
- A Digital Ocean account
- The `doctl` program

[^1]: doctl is a tool that allows you to utilize the DigitalOcean API using the command line(reference).

--- 

# Something




# something






# something






# Something









# Second Table



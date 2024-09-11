## Learning outcomes and topics

This week:
- Introductions
- Pro tips
- Linux: what, where and why
- Tools that we will be using this term

Next week:
- Create an SSH key pair and add to your DigitalOcean account
- Create a Droplet (Linux VM)
- Introduction to working in the terminal

### Course overview

#### Course notes

The course notes are available as [markdown](https://www.markdownguide.org/) on GitLab. I use [Obsidian](https://obsidian.md/) to view the notes in class. While you can use any markdown tool to the view the notes, you will probably get better results using Obsidian as well.  

More on class notes and taking notes later.

#### Course Breakdown
| Criteria                    | %   | Comments                     |
| --------------------------- | --- | ---------------------------- |
| Midterm exam                | 20  |                              |
| Final exam                  | 30  |                              |
| Assignments                 | 30  | 3 assignments each worth 10% |
| Quizzes and reading reviews | 10  | To be done in class          |
| In-class exercises          | 10  | To be done in class          |

#### Making recordings in class

Most of the time anything on screen in class I will share with you. So you don't need to take pictures of the screen. If for some reason you would like to make any kind of recording in class such as taking pictures of the screen, please ask first.

https://www.bcit.ca/files/pdf/policies/5201.pdf
## Pro tips (or how to succeed in school)

### Stay on top of the flipped material

Set aside regular times to do to the flipped material and review your notes on the flipped material. You should always have the flipped material done before class. Quizzes and in-class exercises will be based on the flipped material. 

### Taking notes

Taking good notes is a really valuable skill to have in general, not just in school. 

Any careers related to the content that you learn in this program will require you to continue to learn new things, taking notes can help you do this.

Writing documentation for software is essential, taking notes can help you write good documentation. 

**Note taking tools:**

Note taking tools, and PKM have been hot topics for the past few years, as such there are a lot of awesome note taking tools out there. This is just a small selection of some that I think have benefits for students.

- [Logseq](https://logseq.com/) (free)
    - Logseq includes a great [flashcard](https://docs.logseq.com/#/page/flashcards) feature, that uses spaced repetition to help you study.
    - Good youtube integration for taking time stamped notes on a youtube video.
    - Good PDF integration, for taking notes from a PDF.
- [Obsidian](https://obsidian.md/) (free)
- [Heptabase](https://heptabase.com/)
- [Remnote](https://www.remnote.com/)
- [Tana](https://tana.inc/)

All of the above have three important features

1. daily notes
2. bi-directional links
3. Are great tools for creating atomic notes

#### A simple note taking strategy

**Class notes**

Don't try to write down everything I say. Treat class notes like a todo list, or a bullet point list. Write down important concepts and questions that you have. You can later search for the answers on your own or ask me for more info.

Write your class notes in your daily notes. Use tags and or links

**Reading notes**

Take notes on all of the flipped material.

- Copy and paste material that you think is important.
- Write more questions, things you don't fully understand

You could write these in your daily notes as well or create individual pages and tag them as something like reading notes. 

**Atomic notes**

Review your class and reading notes and paraphrase the material in them into your own "atomic" notes.

By atomic I mean break down concepts into small chunks. For example you could have a note that is just on creating variables in JavaScript. This would be a single document. 

Use tags and links to associate it with other notes on related content.

You might have a MOC (map of content) for types in one document with links to individual notes on each type.

Writing the notes yourself and paraphrasing will help you learn the material. Inter-linked atomic notes will make it easier for you to find your material when you are studying.

**flash cards**

Create flash cards on the material in your atomic notes and try to review these cards a few times a week. Logseq has a great feature for this, but you can do this in any note taking tool, or use pen and paper or a stand alone flash card tool.

Writing your own questions will help you learn the material far more than simply reviewing example questions provided in class.

If you have difficulty coming up with questions on your own, this might be a good use of AI, or better yet start a study group with other people in the class.

### AI

The short version, you can use AI to help you study, you ==**cannot**== use AI to do your assignments.

Examples of _acceptable_ use:

- Ask an AI tool to generate questions, based on flipped content, to use as flash cards to help you study.
- Use AI to help you understand concepts in the flipped material. For example a reading in class mentions "containerisation" and you don't know what that is. 
	- It is a good idea to double check that AI information is correct.

Examples of _unacceptable_ use:

- Use AI to write a portion of your shell scripts in assignment 2. This includes using tools like Copilot. Using tools like this will hinder your learning and will result in academic integrity issues.
- Use AI as a source of information in a bibliography.

> [!note] There is a short video on AI in the flipped learning material section, watch the entire video. Particularly the section on learning methods and the benefits of hard work.

## Linux: what, where and why

> [!question] What do you think Linux is?

> [!question] Where do you think Linux is used?

#### What is Linux?

Linux is a family of operating systems that use the Linux kernel.

The Linux kernel was created by Linus Torvalds in 1991 when Linus was an undergraduate student. 

Linus also created Git. Linus created Git to work on the Linux kernel.  

Today the Linux kernel is maintained by thousands of people and organisations. These organisations include: Microsoft, Amazon and Google.

A Linux operating system will include other software like the GNU of busybox utils, an init system (like systemd) and any number of applications specific to that OS' intended purpose, desktop, web server...

A Linux OS is generally referred to as a distribution or more commonly a "_distro_".  [Ubuntu](https://ubuntu.com/) for example is a Linux distro, which an operating system that uses the Linux kernel.

##### The Linux kernel

![[kernel.webp]]

> The Linux kernel is the main component of a Linux operating system (OS) and is the core interface between a computer’s hardware and its processes. It communicates between the 2, managing resources as efficiently as possible.
>
>The kernel has 4 jobs:
> 
> 1. **Memory management:** Keep track of how much memory is used to store what, and where
> 2. **Process management:** Determine which processes can use the central processing unit (CPU), when, and for how long
> 3. **Device drivers:** Act as mediator/interpreter between the hardware and processes
> 4. **System calls and security:** Receive requests for service from the processes
> 
> - Red Hat

reference:
- [Red Hat, What is the Linux kernel](https://www.redhat.com/en/topics/linux/what-is-the-linux-kernel)
##### Linux distros

The image below shows how new operating systems are forked from other existing operating systems over time. There are a lot of Linux operating systems!

![[Linux_Distribution_Timeline.svg]]

##### Server vs desktop

Many Linux based OS' have a Server edition and Desktop edition. In this class we are going to focus on Servers. Generally the only difference between the Server and Desktop editions is the software installed on each. The obvious one is that it doesn't make a lot of sense to have a desktop environment running on a server. Many of the commands that we will use in class in a server environment I use regularly in my desktop environment.

Focusing on the server means that we are going to do most of our work in a text based environment, in a terminal.

At first working in the terminal may seem difficult, but as you get more familiar with working in the terminal you will start to appreciate just how powerful it is. It is an essential skill for anyone interested in development.

My advice on getting more comfortable with it is to practice, and accept that it is different. Try to use the terminal to do things you currently do in a GUI. For example the next time you create a directory, use the terminal instead of the file explorer.

Unfortunately we probably won't have time to look at working in a Linux GUI or at any Linux desktop environments this term. That said I have been using a Linux OS as my daily driver for a long time and am mostly happy with the experience. Playing with Linux related things is fun for me. So; if you have any questions about something related to Linux that we don't have time for in the class I am happy to talk about it. 
## Tools that we will be using this term

### A terminal emulator

**Installing a terminal:**

Chances are you already have a terminal emulator installed on your system.
- Linux OS' will usually come with _Gnome terminal_ (Gnome) or _Konsole_ (KDE).
- MacOS comes with _terminal_ (most mac users install one of the terminals listed below).
- As of Windows 11 windows comes with the _Windows Terminal_.

This is the primary tool that we will use to interact with our Linux environment. It is also an essential tool for developers, system admins... So it is worth getting familiar with.

> [!note] Note for Windows users
> The Windows terminal is not the same as PowerShell. When you open the terminal on Windows make sure that you are opening the program called [Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/). If you are running Windows 10 you will need to install this first

**Here are a few cross platform terminals you may want to consider:**

- [Alacritty](https://alacritty.org/) (Linux, MacOS and Windows)
- [Kitty](https://sw.kovidgoyal.net/kitty/) (Linux and MacOS)
- [Wezterm](https://wezfurlong.org/wezterm/index.html) (Linux, MacOS and Windows)

[Configuration examples to help you get started.](https://gitlab.com/nathan-climbs/example-terminal-configs)

#### Terminal vs shell

Something new developers are often confused by is the distinction between the *terminal* and *shell*.
- _The terminal_ is an interface, the GUI that you interact with.
- _The shell_ is software that runs the commands you enter in the terminal.

For example in Windows you might open up the Windows Terminal and use PowerShell to run commands on your system. I am using Kitty(terminal) and Bash(shell).

We are going to be using the **Bash** shell in Linux. In MacOS you are probably using **zsh**. 

In a Linux environment it is really easy to use a different shell. A lot of people running a Linux OS use [Fish](https://fishshell.com/) or [Zsh](https://www.zsh.org/). Bash is the most common Linux shell, the default in many Linux operating systems, so we are going to use Bash.

> [!warning] Local vs Remote environments
> Throughout the term we will be running commands on both a remote Linux OS and your local machine. Make sure you pay attention to which environment you are working in!

### DigitalOcean

[DigitalOcean](https://www.digitalocean.com/) is a developer focused cloud service provider. Similar to AWS of Azure. 

We are going to use digitalocean "droplets" as our Linux environment for the term. These are remote Linux virtual machines running on servers owned by digitalocean.

### Git and a remote repository

We are going to be using Git and a remote repository for some of the work in class. You can use GitHub, GitLab, BitBucket... The remote repository doesn't matter. You will need to use Git from the command line. 

Make sure you have Git installed on your machine and have an account with a remote Git repository tool, like GitLab.

### Arch Linux

[Arch Linux](https://archlinux.org/) is the Linux distro that we are going to be using in class. Arch has fantastic documentation via the [Arch Wiki](https://wiki.archlinux.org/title/Main_page). 


### Vim

Vim is the text editor that we are going to use in class. It is a terminal text editor, you run it in the terminal instead of it having a separate GUI(although there are a bunch of GUI versions of Vim). Vim has been around for a long time and is still a very popular text editor used by millions of developers. It is also often the only text editor you have access to when you are working on a remote server, so it is important to know the basics.
## Before next weeks class

- Download the appropriate [Arch Linux](https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/) image.  You want the most recent "cloudimg". The ".qcow2" like in the image below, the date may be different. Download the most recent image.

![[Screenshot from 2024-08-30 16-55-08.png]]

- Create a [DigitalOcean](https://www.digitalocean.com/) account. 
	- We will create a VM (Droplet) in class next week. You just need to create an account for now. DigitalOcean accounts are free, you only pay for resources that you use. You do need a credit card or PayPal account to create a DigitalOcean account. 
	- You can use the referral link below to get a $200 credit for 60 days. Generally monthly DigitalOcean expenses for this class are about as much as 1 cup of coffee, so it is quite affordable. 
		- referral link: https://m.do.co/c/14533c62ea62

### Flipped learning material

==This should all be completed before next weeks class.==

- [AI can do your homework. Now what?](https://www.youtube.com/watch?v=bEJ0_TVXh-I)
- [What is SSH?](https://www.cloudflare.com/learning/access-management/what-is-ssh/)
- [CH 2. The Shell and Its Commands](https://learning.oreilly.com/library/view/linux-for-system/9781803247946/B18575_02.xhtml), Linux for System Administrators
	- O'Reilly Online Learning is available to you via the [BCIT library](https://www.bcit.ca/library/)
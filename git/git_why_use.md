## Why use GIT?

* It is a "distributed" version control system not a centralized version control system like the ones it preceeded.

* A system that records changes to our files over  time. 

* It can recall specific version of a file at any given point in time.

* It saves you time and disk space.

* Many people can easily collaborate on a project and have their own version of project files on their computer.

When I first started doing web development, clients would send me a website design and asked me to code it for them. I created a simple project directory on my PC with all the code for the website. After uploading the files to the web server, I gave the link to the customer to take a look at my web design. During this phase of the project, the customer kept making small changes to the design. All changes were made to files in the original project directory. After each revision, the website files were re-uploaded by FTP to the web server and the customer was asked to review the update. The client kept asking for more design changes which were done using files in the original project folder. At which point the customer gets back to me a couple of days later and apologetically asks me to revert some of his recent design requests. At this point I am getting very frustrated but I make the changes to make the website more like the original design. In this case, there was no version control. There was no way to simply revert to a prior point in the web design. In fact, I had to code the site over and over again to satisfy the client. It wasted a lot of time and effort. Coding software without version control is not an efficient work flow. There has to be a better way. 

To avoid this situation on my next project, I started copying the project directory and suffixing the folder name with a version number. Thus making a new folder for each round of editing which contained a copy of all files from the previous editing round. 

As each customer requested a new round of editing, the current project folder was duplicated. Therefore, when a client wants to revert the design to a prior point in time, just change directories and make changes in the appropriate project folder.

This process becomes unmanageable when clients request numerous revisions and your PC's disk space is low. And at this point you will discover that git is the solution to the problem. Git is a better method of version control. Git is an absolute game changer. It benefits are listed below.  

* Stores all revisions in a project history in just one directory

* Can rewind to any revision in the project I wanted too

* Work on new features without messing up the main codebase; called branching.

* Easily collaborate with other programmers, developers and designers when working on a team 

Git can easily synch our projects with GitHub website. 

GitHub is an free online service that hosts our projects.

It allows us to share our code with other developers.

Developers can donwload our projects, called forking, and work on them independently. 

They can also re-upload their edits and merge them with main codebase, called pulling. 
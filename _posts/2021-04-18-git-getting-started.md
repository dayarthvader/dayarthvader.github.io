---
layout: post
title: git_getting_started
---

[git_getting_started](https://github.com/dayarthvader/git_getting_started)

## Concering version control systems
Today, a considerable part of the workforce, be it in any field, uses computers to create digital artifacts. It could be for the purpose of purely storing away some information/events(Ledgers, account statements etc ...) for the record or for saving away a version/form/iteration(code, wireframes etc ...) of an artifact for future references. In effect we all still do the old school filing for the same old reasons but have to using the computers.

Let's explore some options below to acheive an effective filing solution using computers. The key consideration of the effectiveness being the ease of access and reliability of the solution.

### Named files/folders
This could be the simplest method, to map the workflow of the physical files/folder structure in the real world to files/folder structure in the digital form. Just as labelling each folder and files in the records would help with the ease of access, developing a naming convention to name each files and folders will help. Adding a time stamp to the names is considered a good practice when such a method is used. This method has limitations of scaling and extremely error prone (accidental overwrite of the files etc ...) when we have to have multiple iterations of artifacts. Perhaps suitable for a small project.

### Local version control system
A natural graduation for solutions that suffer because of human errors is to try and automate the solution with the help of a well designed and well tested software/hardware. And so comes the local version control system. Which, in a simple form is a persistent database wrapped around with algorithms that deal with naming, saving and retrieving the information with ease and high degree of reliability. This works really well, as long as the workflow is localised and there is no need to collaborate with other creators/colleagues. As sharing the information accross the bounds of the user's computer would still need to be manually handled.

### Centralised version control system
A centralised version control system addresses the information sharing aspect of the local version control system. It does so by hosting the information on a centralised server and letting all the users access the information with the help clients. Clients checkout a view/version of the information and enable all the users with each of their workflows. Users can check-in the updated information back to the server in a controlled manner to preserve the most meaningful version of the information. However, this system suffers with a drawback of having a single point of failure. Any duration of downtime in one server will cause disruption across.

### Distributed version control system
A distributed version control system combines the best parts of all of other version control systems discussed. In that, it enables the workflow by making each client get a copy/snapshot of the full repository including the history, this way, when one the server is unavailable, any of the cients can be copied back to bring up the server.

## About Git
Git is distributed version control system initially designed to maintain Linux Kernel source code, now pretty ubiquitos.
A few very notable features of Git being:

### Snapshots against Deltas
Delta-based version control systems track the changes to the files. Each version of the information holding the patch/diff from the previous version. Most of the VCSs have such a design. Git on the otherhand treats each version as a snapshot of information. Each version holding references to the snapshots of files, this design choice enables a very powerful feature of Git called Git Branching. (Seperate streams of snapshots running independently until merged)

### Flexible offline/local-online/remote options
Since each client in itself a complete repository, there is no need for the user to be online to perform version control operations. This too is a great convenience for I have personally worked with svn, clearcase and perforce. I find the convenience of working offline means a very sleek workflow.

### Built-in error detection
Everthing in Git is checksummed before it's stored and is then referred to by that checksum. Any corruption of the file, in the transit can be detected by the system.

### Git moves only forward
With each commit to the repository, things are pretty much written in stone and there to stay forever. That is, a snapshot of changes keep geting stored, deleting the history is mostly not possible which makes reverting to any past historical versions is very easy.

### The three states
Each of the files when tracked/controlled with git have three possible states assigned to it in the git context.
modified, staged, committed.

modified  - file has been changed/edited (dirtied), but it is not considered to be committed to the repository yet.   
staged    - A modified file in it's form is a candidate for committing into the repository.   
committed - In this stage the file is guarenteed to have been saved in the repo as a snapshot.   

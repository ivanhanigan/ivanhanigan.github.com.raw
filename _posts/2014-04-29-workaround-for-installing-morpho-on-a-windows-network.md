---
name: workaround-for-installing-morpho-on-a-windows-network
layout: post
title: workaround-for-installing-morpho-on-a-windows-network
date: 2014-04-29
categories:
- Data Documentation
tags:
- morpho
---

### Introduction

Morpho is an open source piece of software designed to host all kinds of ecological data.  It is used to describe data collections. We publish to Metacat using Morpho.  For technical reasons, we have our own server running an older version of the Metacat software so have to run an old version of Morpho (v1.8).
  
### Installation and configuration

TERN specific instructions are replicated across:

- [http://www.tern-supersites.net.au/index.php/data/repository-tutorial](http://www.tern-supersites.net.au/index.php/data/repository-tutorial)
- [http://www.ltern.org.au/index.php/data/guides-and-tutorial](http://www.ltern.org.au/index.php/data/guides-and-tutorial)

### Morpho issue on Windows in our network environment

The ANU Fenner School came across this issue. Our local IT department have discovered with Morpho (v1.8) Installation on Windows in our network environment, Morpho installs a hidden directory called ".morpho" and this is written to a PATH next to the User Desktop. This is actually on a network share with a very small quota.

Therefore as Morpho writes data there it can easily exceed the quota causing the software to stop working.  All users of Morpho on such a network should check for the location of the ".morpho" directory and if it is located with such a restricted quota then alternative arrangements need to be made.

At the ANU Fenner School we opted to set up local user accounts (the ".morpho" file is then on the C drive) and this user is accessible from the main User's account.  The Morpho files are therefore stored on the C drive which is of course a danger for hard disk failure and data loss.

We feel that as long as the draft packages are saved to the networked Metacat (with the maximum access restrictions in force for draft work) then if the local hard disk dies then the draft data package is not lost but can be accessed again from a new Morpho install and the Metacat server.

Issues remain about the long term solution to this problem but this will work in the short-term.

We think you can also create a junction (symlink) so that .morpho/ can point to a different location (perhaps another network storage with bigger capacity and automated backup).

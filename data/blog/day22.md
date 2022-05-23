---
title: Day 22
date: '2022-05-17'
tags: ['internship', 'journal']
draft: false
summary: ''
---

First of all, I am well aware that this is not day 22. "What about last Friday and this Monday mate!?"🤔

These two days were not that interesting. I was transferring bits from the original blog onto the new one. Fixing errors and broken links, etc.

But today... I have managed to deploy my "new look" site.
I would be lying if I say that it was easy.

Maybe some of you who are much better than me would finish it a long time ago. Well done! Good luck!

There were moments of struggle but I succeeded at last!! Some bits still not working, like comments, but everything in time will work as expected🤞.

Something funny (in retrospect) happened today. I was getting errors when I was running my

    npm run build

My "new look" website is running locally already despite these errors.

So, after some reading, I decided to check if maybe packages need some updating and if you want to find something to fit your theory then you will😉.

I installed the **npm-check-updates** which is for updating a new and major version of the packages and then I run the command:

    ncu

which will list all the global packages which have new releases.

And what would you know, it found 49😁.

Like a good boy, I run this👇

    ncu -u

for upgrading all the version hints in the package.json file, so npm will install the major version.

After that

    npm update
    npm install

And... The website stopped working 👀.

Eventually, I gave up and asked my mentor for help.

I explained what happened. He was very complimentary regarding my approach but then he helped me to understand that:

- read your errors a bit better(turned out that my errors were just warnings and my updating packages created errors 🤦‍♂️😂). Beginner's mistake🤷‍♂️.
- when updating packages, do it one by one, test it and then repeat the process if necessary.

Eventually, we fixed all errors and now you are reading this journal entry on my new website🥳🎉.

The very rewarding feeling was when the website was successfully deployed.

Tomorrow I will fix the comments section 🗣️.

---
title: How to use GitHub Pages and Markdown to host a website.
date: '2022-04-11'
tags: ['github','blogging','beginner','tutorial']
draft: false
summary: ''
---
> _GitHub Pages is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub,optionally runs the files through a build process, and publishes a website._

---

If you are a seasoned programmer or tech guru then this post may not be for you. Although you are still welcome to read it as you may find some issues with this tutorial and I am open to corrections.
 
I will try to write it as simple (like myself) as possible so even people who are not tech-savvy will be able to follow and start blogging or just publish a website.

Here is the summary of what you will find in this post:

- [<a name="start"></a>What you need](#what-you-need)
- [<a name="new-repo"></a>Creating a new repository](#creating-a-new-repository)
- [<a name="page"></a>Setting up your website](#setting-up-your-website)
- [<a name="work"></a>Working on your website/blog](#working-on-your-websiteblog)
- [<a name="skills"></a>Hone your Git, GitHub and Markdown skills](#hone-your-git-github-and-markdown-skills)

---

### <a name="start"></a>What you need

Most important. Before you start you need to have a GitHub account.

**What is GitHub?**

Briefly, it is a platform offering internet hosting for software development and version control. You are going to store your code here and you will be able to collaborate with whoever you wish and track and control changes.

I will not cover here how to open a GitHub account. There are many tutorials available on YouTube or just search on Google.
I would recommend just diving right in as the process is not that complicated. Just go to [GitHub](https://github.com) click "Sign up for GitHub" and follow the instructions. They are straightforward.

I am assuming that you already have an account and you are logged in.

---

### <a name="new-repo"></a>Creating a new repository

1️⃣ On the top right-hand side click on your avatar and then click _"Your repositories"_. 

Depending if you are just starting fresh, you may see just info that "_your profile name_ doesn’t have any public repositories yet." or the list of your existing repositories. 
2️⃣ Most important is that you need to click on _"New"_. 

Now you should see this 👇

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u8t1kchg8yn8bkutz41n.png)

Your repository name should be the same as the owner followed by github.io so like **m1ner79** is an owner so the repository is **m1ner79.github.io**.

A description is optional so you can leave it blank, also leave the selection at Public.

3️⃣ Next, you need to tick _"Add a README file"_ - here is where you will be creating your website content.

_"Add .gitignore"_ is not required at this stage because .gitignore creates a list of files that do not need to be tracked. This can be added at any moment and depending on how complicated your blog is, might not be necessary at all.

4️⃣ Tick _"Choose a license"_ because it will help future collaborators what they can and can't do with your code. You can't go wrong with "MIT License" so select it and click _"Create repository"_ **(Before you are going to follow my advice, please have a look 👉 [here](https://dev.to/kbeirne/comment/1ngbp) where Kevin makes a valid observation)**. 

You should see this 👇

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sd1ezuqxl7047ntv73qk.png)

We are almost there. I know, it is **THAT** easy.

---

### <a name="page"></a>Setting up your website

1️⃣ Now, as you can see on the screenshot below, click _"Settings"_ and then on the left select _"Pages"_ (highlighted in green).

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qumso5c39u31frzx1dhq.png)

After you do that you will be advised where is your website "Your site is published at...".

2️⃣ Source(red highlight) should be set to _"main"_ and _"/root"_.

3️⃣ Now the best part. Click on _"Choose a theme"_ (on my screenshot, it says _"Change theme"_ because I already selected the theme).

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/00byw5en2mp0lf211l2m.png)

On the top each square represents a theme and below you will see what your website will look like when you select it.

4️⃣ Once you are happy with your theme, click on _"Select theme"_ and that's it. You will be presented with a page full of markdown language like this 👇

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yuabs1zxtui1xpo5iv69.png)

5️⃣ Don't worry, just scroll to the bottom and click _"Commit new file"_.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0f1p3v4zaw94a2d6l7wt.png)

Now you should see an extra file in your repository.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vizs5n8ty2ypg1wnzhno.png)

Yours might be different because you may selected another theme.

Now starts the best part. 

---

### <a name="work"></a>Working on your website/blog

Depending on your needs there are two ways to write your blog. 

**Option one:** 

1️⃣ Click on README.md file and then on the pencil, like on the highlighted picture below.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pxh20ifmvb9liwvfbtpf.png)

2️⃣ All you need to do now is remove everything and start writing your blog. In the end, make sure to commit your changes.That will amend your file and new content will appear on your website.

Option one has also another way of editing your code ("another way" is marked with*️⃣). 

*️⃣1️⃣ If you have your repository open and you are on your laptop /desktop(it will work with other devices too), all you need to do is just hit "."

This will open Visual Studio Code in your browser and you can start editing right away.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6mopon1135t300j0kx7a.png)

*️⃣2️⃣ After you will make your changes, you will notice that the source control icon indicates a number of changes. Click on it and then on the top you will see a space where you will enter a message.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uplpmtof1nd1hfake29l.png)

*️⃣3️⃣ This message needs to make sense. Just assume that there might be someone else reading that comment so give them a chance to understand what you did i.e. "add a folder for images" or "update xyz file".

*️⃣4️⃣ Now click the tick and your changes are pushed to your repository. 

Give it a few seconds and your changes should be visible when clicking on your GitHub Pages address.

**Option two:**

A bit more complex and I am doing that(because I like a challenge 😉).

1️⃣ You need to create a folder on your local machine where you are going to keep all files required for your blog. Open a terminal. 

2️⃣ Now, in your repository, click _"Code"_ and copy that highlighted link.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lhz8ujbwqs7wbofc2vxc.png)
  
3️⃣ Go back to your terminal and type in "git clone _your link goes here_"

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3xn60g47u5oc9i1bwn0y.png)

This will download all files into your folder. You can now use your favourite editor to work on your blog.

4️⃣ After you have done all changes you need to push these to your repository. 

I will not cover how to do it here, instead, I will share some links to the tutorials I have used myself to get better with Git and GitHub.

---

### <a name="skills"></a>Hone your Git, GitHub and Markdown skills

This is a very good tutorial from well known freecodecamp.com 👉 [How to Start and Create your First Repository](https://www.freecodecamp.org/news/a-beginners-guide-to-git-how-to-create-your-first-github-project-c3ff53f56861/).

If you prefer YouTube then try this one 👉 [Git and GitHub explained for beginners](https://youtu.be/8Dd7KRpKeaE).

Also, I know that I said it is easy to start writing your blog but you need to get some of the basics for the markdown language so your website will render the way you wanted.
 
Here is a great source 👉 [Markdown Guide](https://www.markdownguide.org/basic-syntax/) and if you like emojis then this is a must 👉 [Emojipedia](https://emojipedia.org).

That would be all. Please let me know what you think about this post.

Oh, and if you wish to check my internship journal (shameless plug) then click here 👉 [Internship Journal](https://m1ner79.github.io/).

Thank you for your time, bye!

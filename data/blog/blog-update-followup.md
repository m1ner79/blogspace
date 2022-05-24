---
title: How to configure Next.js, Tailwind CSS starter blog.
date: '2022-05-24'
tags: ['beginners', 'tutorial', 'webdev', 'blog']
draft: false
summary: ''
---

After I wrote my article on [How to make your blog feature-rich with Next.js, Tailwind CSS and Vercel](https://michals-corner.vercel.app/blog/blog-update) I realised that some beginners might have troubles with configuration.

In this article, I will explain the changes which I made when I created my new website.

---

This is what I changed so far:

- [data/siteMetadata.js](#site)
- [data/authors/default.md](#author)

- [data/projectsData.js](#project)
- [components/comments/Giscus.js](#giscus)
- [data/blog](#blog)
- [public/static](#images)

---

### <a name="site"></a>data/siteMetadata.js

Information about the site that should be modified to meet your needs. In this file I have only changed:

- _title:_ - this is the title of your page, it is what you will see in the tab

![title](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6xb74aarfyt9kjghau2g.png)

- _author:_ - put in your name
- _headerTitle:_ - your page name

![name](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xaspxwwfi3x183vwckfd.png)

- _description:_ - describe your website, put in something "catchy"😎

![description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/chnyxn35cyibwy21hyrf.png)

- _siteUrl:_ - your website address
- _siteRepo:_ - update the link to this project's repository on GitHub
- _siteLogo:_ - if you have a logo, update it here
- _image:_ - update the link to your picture here
- _email:_ - update your email (I don't have the newsletter switched on yet)
- _github:_ - showcase all of your GitHub repositories
- _linkedin:_ - put in the link to your LinkedIn profile page

I commented out other social media links but you do whatever you think is the best for you.

---

### <a name="author"></a>data/authors/default.md

This is your "About" page so it is important to change it.

![about](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/m5eadr1fqpn29cpdea7k.png)

---

### <a name="projects"></a>data/projectsData.js

Styled cards are generated using data from the projectsData file.

![projects](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u4k54f8ri0kbfbt3lt31.png)

---

### <a name="giscus"></a>components/comments/Giscus.js

Before you can activate the comments system on your website, you need to generate a script with your specific information.

1️⃣ Go to the giscus [website](https://giscus.app/) then click on **giscus app**.

![website](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3wt2x1j3m29kxbiq73g6.png)

You should see this 👇

![install](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qf31aczs87yzpmcn8ezd.png)

2️⃣ Click _Install_ then select **Only select repositories** and pick your project repo.

![config install](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/29hpt87t25w8fmou9xs4.png)

3️⃣ Again, click _Install_. This should add giscus to your account.

![giscus installed](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lpw98mfqlegysl86kf7e.png)

4️⃣ Now you need to activate discussions. Go to _Settings_ in your repository.

![settings](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rokt3xcht3dpu8ekcgf5.png)

Scroll to _Features_ and tick the box for **Discussions**.

![discussions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yxxpzzr2rka45ndl7n7s.png)

5️⃣ Go back to https://giscus.app/ and scroll to _Configuration_. Here are some things you need to do:

1. Choose the language giscus will be displayed in.
2. Test if your repository meets all three highlighted criteria ( I would recommend to type in the details of your repository because Copy/Paste creates an error).
3. In _Page ↔️ Discussions Mapping_ I selected **Discussion title contains page URL** but you select whatever you think is the best option for you.
4. In _Discussion Category_ select from the drop-down menu a category where the new discussions will be created. If you want your own custom category then you need to:

   - Go back to your project repository and click on **Dicussions** and then the pen icon.

![custom category](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v96cg7nzy770xvsj2o8d.png)

- Now you should be able to add your custom category name, select discussion format and then click **Create**.

![create category](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5g47kqf77j9sh5e0cfig.png)

- Go back to giscus main page, scroll to _Discussion Category_
  and your custom category should be there for you to select.

5. I did not change anything in section _Features_ and _Theme_.
6. In _Enable giscus_ you can see there was a script generated.

6️⃣ Now, go to your project folder, open your favourite editor and go to `components/comments/Giscus.js`.

7️⃣ Update all the data in that file (mine starts on line 33) with the data from the generated script.

![giscus config](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/76zx6naj739u6jm0ybmg.png)

8️⃣ Now, save that file, push it to your repository and voila - you have comments on your website.

---

### <a name="blog"></a>data/blog

- _title:_ - here goes the name of your post, it is required.
- _date:_ - it is self-explanatory, also required.
- _tags:_- this is a required field. If you don't want to use tags then you can leave it as an empty array, like this 👉 `['']`)
- _draft:_ - this is an optional but handy feature. Let's say that you are in the middle of writing a post but you don't want it to appear on your website. All you need to do is to type in `draft: true` and this post will remain invisible. Type in `false` if you want the blog to be visible.
- _summary:_ - another optional feature. You will use it to give brief information on what is the blog about.

---

### <a name="images"></a>public/static

Here you will store your images and favicons.

If you already have a logo but don't have the favicons, here is what I did.

First, I [removed background](https://www.remove.bg/) from my logo.

Next, I used the updated logo to [generate favicons](https://realfavicongenerator.net/).

Now all you need to do is to replace existing favicons with your design.

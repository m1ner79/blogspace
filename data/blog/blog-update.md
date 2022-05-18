---
title: How to make your blog feature-rich with Next.js, Tailwind CSS and Vercel.
date: '2022-05-18'
tags: ['beginners', 'tutorial', 'webdev', 'blog']
draft: false
summary: ''
---

A few weeks ago I set up my first blog with the use of [GitHub Pages and Markdown](https://dev.to/m1ner/how-to-use-github-pages-to-host-a-blog-4ofd).

It was not that complicated and did not require any coding knowledge.

Today I decided to "pimp my blog"😀. I want it to look a bit better than it already looks but also add more features and maybe separate articles from the internship journal and also maybe add a bit about myself.

‼️*First of all. This blog transformation would not be possible without Timothy who created this amazing starter blog 👏. It comes pre-configured with the latest technologies (Next.js, Tailwind CSS), it is highly customizable and not very difficult to configure. The original repository is available [here](https://github.com/timlrx/tailwind-nextjs-starter-blog).* ‼️

This is not going to be as easy as last time but I will try to create a simple tutorial so you will be able to do it yourself.

Just to let you know, I am using Pop!\_OS so if you are using MacOS or Windows then you may have to look for another tutorial 🤷‍♂️. If you are using other Linux distributions then you should be fine(there might be some differences in the command line but I am not expecting anything major).

Also, you need to run these commands:

> `sudo apt install build-essential` > `sudo apt install libssl-dev`

We don't need to get into details now but these packages may be required at some stage during this or future projects.

## Last but not least, you need a GitHub account. It is essential.

### Here are the steps I did to complete my website transformation:

- [Downloading and installing Node.js](#start)

- [Starting my "new look" site](#new-look)

- [Push everything to GitHub](#GitHub)

- [Deploying to Vercel](#vercel)

---

### <a name="start"></a>Downloading and installing Node.js

What is [Node.js](https://nodejs.org/en/)? It is the back-end JavaScript runtime environment. We will also need **npm** which is the world's largest software registry and the default package manager for JavaScript. More information about npm is available [here](https://docs.npmjs.com/about-npm).

1️⃣First of all check if you need to install Node.js. Open your terminal and type:

> `node -v`

If you have it then you will see this(you may have a different version number)👇

![node version](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nt36ow3te86fco98ns1r.png)

If you don't have it then you will see

> `command 'node' not found...`

After reading a few articles it looks like the best way to install Node.js is through nvm (node version manager) because it allows to quickly install and use different node versions for different projects.

2️⃣Open your terminal and type👇

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

If you don't have curl, install the utility by running the command:

> `sudo apt install curl`

(curl is used in command lines or scripts to transfer data).

Close your terminal and open, then type this `nvm --v`. If everything worked ok then you should see something like this👇

![nvm install](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b17bl2yt416wvlu3202r.png)

Let's install the latest long term support Node.js with the following command👇

```
nvm install --lts
```

Now, verify if everything is installed. Type these commands:

> `node -v` > `npm -v`

![verifying installation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1havnv4cuz7wi6rvmmoy.png)

If you run into any issues, please check this 👉 [very detailed source](https://github.com/nvm-sh/nvm).

---

### <a name="new-look"></a>Starting my "new look" site.

1️⃣You need to create a new empty folder(name it whatever you like). If you will try to run the command from step2️⃣ in the directory where you have an existing git project then you will see this message

> `! destination directory is not empty, aborting. Use --force to override`

2️⃣Open console in your new folder and type 👉`npx degit https://github.com/timlrx/tailwind-nextjs-starter-blog.git`.

More likely you will see this message👇

![degit installation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qjv983rsgsuzvwmusycy.png)

Don't worry, just hit "y" and it will install it. **degit** makes copies of git repositories, it is like a clone in GitHub.

![GitHub](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gzh4s822lz7q1q6eu15z.png)

Once you successfully installed degit, run the step2️⃣ command once again and you should see 👉 `> cloned timlrx/tailwind-nextjs-starter-blog#HEAD`

3️⃣Open your favourite editor (I am using Visual Studio Code) and access the cloned folder.

Here are some files that you need to edit:

- `data/siteMetadata.js` - here you personalize your site related information.

- `next.config.js` - here you modify the content security policy if you want to use any analytics provider or a commenting solution other than giscus (visitors leave comments and reactions on your website via GitHub).

If you are a beginner like myself, I would recommend staying away from that one for a time being. Just leave it be 😉.

- `data/authors/default.md` -here you put your info, this will be your "About" page.

- `projectsData.js` - if you have any projects completed that you would like to show then you need to edit this file as well.

- `headerNavLinks.js` - here you customize the navigation links.

- `data/blog` - here you put in your blog posts.

- `public/static` - here you keep your images and favicons.

4️⃣Once you are happy with your changes then you need to run this command 👉 `npm install`.

5️⃣Now enter `npm run dev`. This will create a build directory with a production build of your app and also will highlight any issues which may potentially cause your app to break.

I had to resolve the chaining issue in file `components/comments/Giscus.js` and on line 31 I removed all "?"(no, I am not that advanced, I managed to fix it with help of my mentor👏).

6️⃣After you are happy that all issues were resolved🤞, you need to open this address http://localhost:3000 in your browser to see if the website looks like you wished.

This is mine at the moment👇
![new look](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ysa8a9nuvulwkqbjhpz7.png)

---

### <a name="GitHub"></a> Push everything to GitHub.

So far everything happened locally, on my laptop. Now it is the time to send everything to my GitHub.

This is the first time where I created a project before having the repository.

I usually clone repositories with HTTPS and then I need to create a token to securely communicate with GitHub but this time I decided to try SSH(Secure Shell). Not only because it is considered more secure but entering the secure token before each push was getting on my nerves.

1️⃣First, open a terminal and generate a new SSH key. Follow these instructions 👉 [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key)

⚠️*You need to remember the password that you created in step 1️⃣ because you will need it in the future(each time PC reboots you will need to enter it).*⚠️

To copy that key, go to your **Home** directory and in settings, tick the box to show hidden files.

![hidden files](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h3mumk4tnz4g7kssnwt6.png)

Locate your .ssh folder and then open .pub file and copy your key.

2️⃣Next, you need to add your key to your GitHub account as per instructions in this 👉 [document](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

3️⃣Go to the folder where you keep your project and open the terminal. Add your SSH key to the ssh-agent. This is explained 👉[here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent).

4️⃣Now, please follow this great tutorial on [How to Push an Existing Project to GitHub](https://www.digitalocean.com/community/tutorials/how-to-push-an-existing-project-to-github). To push your repository to GitHub, you will need these commands👇.

```
git init
git add .
git commit -m 'some comment'
git remote add origin git@github.com:your-GitHub-name/new-project.git
git push --set-upstream origin main
```

I really recommend going through the tutorial first(unless you know what you are doing).

5️⃣All files should be now uploaded to your GitHub repository.

---

### <a name="vercel"></a> Deploying to Vercel.

Vercel is another company offering website hosting, and it is maybe even easier to deploy your website than with GitHub Pages. Again, personal opinion.

1️⃣Go to their [website](https://vercel.com/) and click "Start Deploying" and then pick the option to sign in with your GitHub.

2️⃣After successful sign in you should see this 👇

![vercel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t8cr2wxs5mr5wdbd09mh.png)

3️⃣Click on "Select a Git Namespace" and then "Add GitHub Account".

Select your account and then tick "Only select repositories" which will allow you to pick the one with the project.

![vercel setup](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j46jg1984d9pnclf1urm.png)

Now click "Install"(you will need to enter your GitHub password).

4️⃣Once successful, you should see this 👇

![import to vercel](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d7r8wju0kudeoputbo7o.png)

Click "Import".

![almost done](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dubulac22eoahpy5obj6.png)

Change "Project Name" to the name of your website. This is important because it will become a part of your domain name i.e. _"your-website-name.vercel.app"_.

Now, click "Deploy".

It will take a minute which (if you are lucky😉) should finish with your website deployed.

![deployed website](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lu539dn3my56pmbfs21p.png)

Clicking on the image will take you to your website.

That's... The best luck scenario. If you managed it without any issues then go and get yourself some Lotto tickets😉.

More likely you will encounter some errors or issues. That's ok. Investigating these problems will increase your knowledge because you will need to read more material/documentation.

I understand that this might be frustrating. Believe me, **I KNOW**.

Once you pass this stage where you want to smash your laptop with the hammer and you will make this project work, I can guarantee you that you will feel amazing.

If after deployment some things don't work yet, don't worry. It is your ongoing project. Who knows, maybe with time, you will select a different blog to clone or you will build your own from scratch.

Keep your chin up and don't give up 💪.

As always, please share your comments👇. I am still learning so if you notice something wrong with the article, please let me know and together we will improve it🤝.

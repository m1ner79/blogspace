---
title: Website rendering for beginners.
date: '2022-06-16'
tags: ['beginners', 'tutorial', 'webdev', 'blog']
draft: false
summary: ''
---

I decided to write an article about website rendering because this topic is not as easy as it may seem.

For all the people who have worked in this environment for some time, this subject may be as easy as pie, but if you are a beginner, it may be confusing or intimidating even.

I will try to explain everything as simple as possible. I will not dive too deep because the sole purpose behind this post is to give you a general idea of how rendering works.

If after reading you feel that this was interesting, and you wish to go into more details, then I will provide some extra links at the [bottom](#extra) 👇

---

What are the rendering types:

- [<a name="ssr"></a>Server-side Rendering (SSR)](#server-side-rendering-ssr)
- [<a name="csr"></a>Client-side Rendering (CSR)](#client-side-rendering-csr)
- [<a name="blr"></a>Build-level Rendering(BLR)](#build-level-renderingblr)
- [<a name="dssr"></a>Dynamic SSR](#dynamic-ssr)

---

First, let me explain what the rendering is.

![diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kh4ynzt9c6eu1qchvu7i.png)

As you can see, a browser requests an HTML document from a server. Then a server returns a formatted HTML text file.

Within that file, there is the whole information about the elements (CSS, JavaScript, images, videos, etc.) required to create a visual representation with which you can interact in the browser.

Rendering is combining all that information to create a website. The way you are rendering the website means what way are all these elements fetched.

Website rendering affects how a page is indexed, which impacts Search Engine Optimization (SEO).

I will not cover indexing or SEO in great detail here. As I mentioned, I will add links at the end of the article.

---

### <a name="ssr"></a>Server-side Rendering (SSR)

Server-side rendering means that when you are visiting a website, all the website's content is processed and rendered on the server.

1️⃣ First, through your browser, you are sending a request to access a website.

2️⃣ Next, all necessary files (HTML, CSS, JavaScript) are prepared and compiled.

3️⃣ A fully rendered webpage is delivered to your browser.

Something like that 👇

![Server-side rendering diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ewzg1qx04st930roc2w3.png)

**When would you use SSR?**

If your website doesn't have many users, it has a simple User Interface (UI), maybe a few pages, small dynamic data, and minor interactivity.

**SSR pros:**

- It is Search Engine Optimization friendly, which means that a search engine such as Google can crawl each page on a website successfully, analyse the content efficiently, and index it in their databases. All this has then an impact on how high your website will appear on the search engine results page (we all want that **#️1** page 🤑😉).

- Faster initial page load time, which also impacts your SEO because Google prioritizes the ones that load faster.

**SSR cons:**

- It can be very expensive. When your website increases the number of visitors, with each user accessing a new page, it has to send a server request every time. As a result, the server must deal with high memory usage and high processing power, which will have an impact on the hosting price 🤷‍♂️.

---

### <a name="csr"></a>Client-side Rendering (CSR)

Client-side rendering means that when you are visiting a website, all the website content is downloaded, compiled and rendered in your browser.

1️⃣ First step is the same as in SSR, through your browser, you are sending a request to access a website.

2️⃣ Then, the server sends an HTML text file.

3️⃣ After that, the browser will download all static content required by the HTML file and JavaScript.

4️⃣ The JavaScript framework of choice (React, Angular or Vue.js) takes control and starts fetching and processing data within the browser.

5️⃣ Lastly, you can view a website of your choice in your browser.

Take a look here 👇

![Client-side Rendering diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/74168e5bl1t5dlf7wk4e.png)

**When would you use CSR?**

If SEO is not a priority, your website has many visitors and depends on dynamic content and complex UI (or both).

**CSR pros:**

- allows creating a website with complex user interactions.

- although the initial load can be slow, but after that, we can see fast website rendering.

**CSR cons:**

- as mentioned above, it can be slow when loading for the first time. It depends on many variables like a visitor's internet connection speed, or is the device used to access that website is an old computer or tablet (old machines might not be powerful enough to handle it).

- if Search Engine Optimization is important to you, then you probably need to stay away. SEO for the website will be negatively affected because the content is not rendered until the browser is loaded. I know that they are ways around it, but apparently, these are complicated(hence expensive).

---

### <a name="blr"></a>Build-level Rendering(BLR)

Before I can explain how Build-level Rendering works, I need to address what is CI/CD.

CI/CD stands for Continuous Integration, Continuous Delivery and Continuous Deployment; it is often referred to as a "CI/CD pipeline".

"How it works?" - you may ask. Most simply, this is a modern approach to product development. It is continuous automation of integration, testing, delivery and deployment phases in the life cycle of a website/application.

1️⃣ A developer works on a local environment. Code some changes to a website and run some tests (`npm run dev`). Once everything went ok, the code is pushed onto a shared branch.

2️⃣ At the Continuous Integration stage, a code is validated by automatically **building** an application and running different automated **tests**. If these changes break the app, then CI makes it easier to locate and fix these bugs. If all unit and integration tests were successful, then the code is merged into the release branch.

3️⃣ The Continuous Delivery is the part that interests us from the perspective of the Build-level Rendering. In the cloned production environment (an environment imitating your end product) all components are automatically tested and once everything is good, the code changes are deployed to production. The release branch can be deleted once it merges with the production.

4️⃣ Here is the last stage of CI/CD pipeline. During the Continuous Deployment stage, if all automated tests are completed, then all changes are applied to a website/application.

Some would say that Build-level Rendering takes place now, but I think that the whole "hard work" is done at the previous step. If any tests fail now, that would be more likely down to the development environment not being set up correctly (if you think of other reasons, please let me know in the comments below 👇).

In short, the CI/CD pipeline (steps 2-4) is very good and necessary because it allows you as a developer to get continuous feedback across all stages. This is an agile way of developing an application (Chris, my lecturer, would be very proud 😉).

5️⃣ Unlike in SSR where everything is compiled on the severer (once a user requests a website), BLR delivers a ready product to a server where it waits for a user to request it.

It looks like that 👇

![Build-level Rendering](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3y8mfak7xwtzfgg7tokx.png)

**When would you use BLR?**

It would have this same application as Server-side Rendering.

Pros and Cons would be similar to SSR. I would add another potential con - if you decide to go with this way of building an application, just make sure that your CI/CD pipeline is set up correctly. It requires creating a high level of automation and continuous monitoring which can be costly at the beginning, but once it is set up correctly then it should work like a charm.

---

### <a name="dssr"></a>Dynamic SSR

Dynamic SSR is trying to combine SSR and CSR together. The goal is to provide solutions which would allow the creation of SEO-friendly, fast-loading, dynamic websites with loads of visitors with minimal performance impact.

> _"In a nutshell, dynamic rendering is the principle of sending normal, Client-side Rendered content to users, and sending fully Server-side Rendered content to search engines and to other crawlers that need it."_ (John Mueller at Google I/O 2018 event)

1️⃣ Just like on other occasions, through your browser, you are sending a request to access a website.

2️⃣ Next, initial HTML load and minimal JavaScript is sent to your browser and separate one to a renderer. This allows you to see the website in your browser (the website is not yet interactive).

3️⃣ Initial load sent to the renderer is now compiled into a formatted HTML text file.

4️⃣ Web crawlers (like Googlebot, Bingbot, DuckDuckBot) "digest" the website's content and then index it. This is what helps to improve Search Engine Optimization and user experience. Crawler focuses on the information best known to it, and you as a user can see a website on your screen.

5️⃣ Lastly, JavaScript downloads and runs all necessary code to make a website fully interactive.

Obviously, all the above steps take seconds to complete.

Here is a visual representation 👇

![Dynamic SSR](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0vycenrwyrcs7j997j30.png)

**When would you use Dynamic SSR?**

A large website with very demanding, dynamic JavaScript content.

**Dynamic SSR pros:**

- it enables crawling and indexing of content without executing JavaScript.

- SEO-friendly website with all interactive components that need JavaScript.

**Dynamic SSR cons:**

- like with the SSR, it can be expensive. Now the website not only has to handle every visitor's traffic but crawl bots as well, and we know that this will put an extra burden on the server, hence the hosting price hike.

---

## <a name="extra"></a>Something extra

The idea behind my article was to simplify website rendering for beginners, but if you feel that you need to dive deep into the nitty-gritty, then here are some other sources:

- ["deep dive into DOM and CSSOM to understand how the browser renders a webpage"](https://medium.com/jspoint/how-the-browser-renders-a-web-page-dom-cssom-and-rendering-df10531c9969)

- [The Beginner's Guide to SEO](https://moz.com/beginners-guide-to-seo)

- an interesting clip on how to [deliver search-friendly JavaScript-powered websites](https://www.youtube.com/watch?v=PFwUbgvpdaQ&t=1255s)

- [web crawlers](https://www.keycdn.com/blog/web-crawlers)

I hope that you have enjoyed this article and I managed to make the website rendering a little less overwhelming.

If you notice any mistakes on my part, please let me know in the comments section below 👇 then I will address them, and together we can make this article even better.

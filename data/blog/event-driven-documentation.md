---
title: Event driven API documentation made simple (Client-Side Rendering).
date: '2022-07-27'
tags: ['eventdriven', 'asyncapi', 'documentation', 'guide']
draft: false
summary: ''
---

This post is a bit different from the other articles.

In my previous posts, I have written for absolute beginners, but this one is for developers looking to automate and formalize documentation generation for event-driven projects.

This guide is directed toward folks looking for instructions on how to generate documentation using their AsyncAPI files. Event-driven APIs are not the same as the synchronous APIs you usually document with OpenAPI or GraphQL. Many people use AsyncAPI now, and it is time to provide the community with a guide that shows what options the community has to render documentation on the client-side.

Oh, if you are still not sure about Client-Side Rendering or Server-Side Rendering, then you can read all about it here 👉 [Website rendering for beginners](https://michals-corner.vercel.app/blog/website-rendering-for-beginners) (shameless plug 😉).

I will cover the usage for:

- [<a name="react"></a>React](#react)
- [<a name="vue"></a>Vue](#vue)
- [<a name="wc"></a>Web Components](#web-components)
- [<a name="sb"></a>Standalone Bundle](#standalone-bundle)

All examples will use this same AsyncAPI sample file 👇

```
{
  "asyncapi": "2.2.0",
  "info": {
    "title": "Account Service",
    "version": "1.0.0",
    "description": "This service is in charge of processing user signups"
  },
  "channels": {
    "user/signedup": {
      "subscribe": {
        "message": {
          "$ref": "#/components/messages/UserSignedUp"
        }
      }
    }
  },
  "components": {
    "messages": {
      "UserSignedUp": {
        "payload": {
          "type": "object",
          "properties": {
            "displayName": {
              "type": "string",
              "description": "Name of the user"
            },
            "email": {
              "type": "string",
              "format": "email",
              "description": "Email of the user"
            }
          }
        }
      }
    }
  }
}
```

This is the expected look of the generated document 👇

![document-template](/public/static/images/document-template.png)

All usage examples from this article are available to check on [asyncapi-docs-rendering-examples](https://github.com/m1ner79/asyncapi-docs-rendering-examples) repository.

---

### <a name="react"></a>React

If you wish to render documentation from your AsyncAPI file in React application, then you need to use [AsyncAPI React component](https://github.com/asyncapi/asyncapi-react).

1️⃣ To install the **React AsyncAPI component** run the command `npm install --save @asyncapi/react-component@next`.

2️⃣ Now, create **index.js** file and type in:

```
import React from "react";
import ReactDOM from "react-dom";

import AsyncApiComponent from "@asyncapi/react-component";
import "@asyncapi/react-component/styles/default.min.css";

import { specMock } from "./testDoc";

const rootElement = document.getElementById("root");
ReactDOM.render(<AsyncApiComponent schema={specMock} />, rootElement);
```

**React AsyncAPI component** is imported on the **line 4**.

If you are happy with AsyncAPI styling then you need to import their CSS pattern with `import "@asyncapi/react-component/styles/default.min.css";`

On the **line 7** is where AsyncAPI sample file is imported.

---

### <a name="vue"></a>Vue

If you wish to generate documentation from your AsyncAPI file in Vue application, then you need to use [AsyncApiStandalone bundle](https://github.com/asyncapi/asyncapi-react/blob/next/docs/usage/vue.md).

1️⃣ React AsyncAPI component is required here as well, so again you need to run `npm install --save @asyncapi/react-component@next` command.

2️⃣ In your **App.vue** just add this code:

```
<template>
  <div ref="asyncapi"></div>
</template>

<script>
import AsyncApiStandalone from '@asyncapi/react-component/browser/standalone';

// AsyncAPI specification, fetched or pasted.
const schema =
'{"asyncapi":"2.4.0","info":{"title":"Account Service","version":"1.0.0","description":"This service is in charge of processing user signups"},"channels":{"user/signedup":{"subscribe":{"message":{"$ref":"#/components/messages/UserSignedUp"}}}},"components":{"messages":{"UserSignedUp":{"payload":{"type":"object","properties":{"displayName":{"type":"string","description":"Name of the user"},"email":{"type":"string","format":"email","description":"Email of the user"}}}}}}}';

const config = {}; // Configuration for component. This same as for normal React component.

export default {
  name: 'AsyncApiComponent',
  props: {
    msg: String
  },
  mounted() {
    const container = this.$refs.asyncapi;
    AsyncApiStandalone.render({ schema, config }, container);
  }
}
</script>

<style scope src="@/assets/asyncapi.min.css"></style>
```

As you can see on **line 6**, you need to import **AsyncApiStandalone** bundle with `import AsyncApiStandalone from '@asyncapi/react-component/browser/standalone';` command.

3️⃣ There is one more thing to do. If you like AsyncAPI styling then you need to go to 👉 `node_modules/@asyncapi/react-component/style/default.min.css`.

Copy that file and then paste it into your _**assets**_ folder.
I renamed mine **asyncapi.min.css**.

You can import this in your **main.js** file with `import './assets/asyncapi.min.css'` or, as I did, add it at the end of **App.vue** file with `<style scope src="@/assets/asyncapi.min.css"></style>`.

---

### <a name="wc"></a>Web Components

To generate documentation from your AsyncAPI file, you can use it as an element of an HTML webpage or as a web component in any other web framework you choose. You can do this by implementing [web-react-components](https://github.com/asyncapi/asyncapi-react/blob/next/docs/usage/web-component.md).

1️⃣ Just create a **.html** file then copy and paste this code 👇

```
<script src="https://unpkg.com/@asyncapi/web-component@1.0.0-next.39/lib/asyncapi-web-component.js" defer></script>

<asyncapi-component
  schema='{"asyncapi":"2.4.0","info":{"title":"Account Service","version":"1.0.0","description":"This service is in charge of processing user signups"},"channels":{"user/signedup":{"subscribe":{"message":{"$ref":"#/components/messages/UserSignedUp"}}}},"components":{"messages":{"UserSignedUp":{"payload":{"type":"object","properties":{"displayName":{"type":"string","description":"Name of the user"},"email":{"type":"string","format":"email","description":"Email of the user"}}}}}}}'

  config='{"show": {"sidebar": false}}'

  cssImportPath="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/styles/default.min.css">
</asyncapi-component>
```

2️⃣ If you need support for old browsers then you need to add this script as well `<script src="https://unpkg.com/@webcomponents/webcomponentsjs@2.5.0/webcomponents-bundle.js"></script>`.

That is it! 🤯 Just awesome!

I almost forgot. There is one more way to configure the AsyncAPI sample.
You can do it through **config** props. My example `config='{"show": {"sidebar": false}}` has a sidebar off, but if you change it to _**true**_ then your document will have a sidebar.

---

### <a name="sb"></a>Standalone Bundle

If you want to render documentation from your AsyncAPI file without the use of any framework but with just an HTML webpage then you will need the [Standalone bundle](https://github.com/asyncapi/asyncapi-react/blob/next/docs/usage/standalone-bundle.md).

1️⃣ All you need is just a basic HTML template.

2️⃣ In the **head** element enter `<link rel="stylesheet" href="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/styles/default.min.css">` to get AsyncAPI document styling.

3️⃣ In the **body** element type in:

```
 <div id="asyncapi"></div>

    <script src="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/browser/standalone/index.js"></script>
    <script>
        AsyncApiStandalone.render({
            schema: '{"asyncapi":"2.4.0","info":{"title":"Account Service","version":"1.0.0","description":"This service is in charge of processing user signups"},"channels":{"user/signedup":{"subscribe":{"message":{"$ref":"#/components/messages/UserSignedUp"}}}},"components":{"messages":{"UserSignedUp":{"payload":{"type":"object","properties":{"displayName":{"type":"string","description":"Name of the user"},"email":{"type":"string","format":"email","description":"Email of the user"}}}}}}}'
            ,
            config: {
                show: {
                    sidebar: false,
                }
            },
        }, document.getElementById('asyncapi'));
    </script>
```

`<script src="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/browser/standalone/index.js"></script>` fetches everything required from the bundle.

This was only a sample of what could be done. AsyncAPI can do a lot more. Check [AsyncAPI documentation](https://www.asyncapi.com/docs/tutorials/getting-started/asyncapi-documents) for more information on how to generate docs.

I hope that you liked this quick guide through AsyncAPI Client-Side documents generation.

As usual, if you find any mistakes, don't go mad in the comments section. Just let me know and together we can fix it so this article can be even better.

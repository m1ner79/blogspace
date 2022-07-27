---
title: Event driven API documentation made simple (Client-Side Rendering).
date: '2022-07-27'
tags: ['eventdriven', 'asyncapi', 'documentation', 'guide']
draft: true
summary: ''
---

This article is a bit different from the other articles.

In my previous posts, I have written for absolute beginners, but this one is for developers looking to automate and formalize documentation generation for event-driven projects.

In this guide, to generate documentation, I am using the AsyncAPI which is an open source initiative striving to create _**" the industry standard for defining asynchronous APIs"**_.

Oh, if you are still not sure about Client-Side Rendering or Server-Side Rendering, then you can read all about it here 👉 [Website rendering for beginners](https://michals-corner.vercel.app/blog/website-rendering-for-beginners) (shameless plug 😉).

I will cover the usage for:

- [<a name="react"></a>React](#react)
- [<a name="vue"></a>Vue](#vue)
- [<a name="html"></a>HTML](#html)
- [<a name="sb"></a>Standalone Bundle](#standalone-bundle)

---

### <a name="react"></a>React

My React project is very simple. No bells or whistles.👇

![react-project-stucture](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ychwkrj5bwsal3cpwelu.png)

You can view it on [GitHub](https://github.com/m1ner79/asyncapi-docs-rendering-examples/tree/main/asyncapiReact).

1️⃣ After you have your project set up, you need to install the React AsyncAPI component by entering `npm install --save @asyncapi/react-component@next`.

2️⃣ In your _**src**_ folder create **index.js** file and type in:

```
import React from "react";
import ReactDOM from "react-dom";

import AsyncApiComponent from "@asyncapi/react-component";
import "@asyncapi/react-component/styles/default.min.css";

import { specMock } from "./testDoc";

const rootElement = document.getElementById("root");
ReactDOM.render(<AsyncApiComponent schema={specMock} />, rootElement);
```

Line 7 is where the "magic" happens. This is where I import my AsyncAPI template.

It looks like this:👇

```
export const specMock = `
{
  "asyncapi": "2.4.0",
  "info": {
      "title": "Shlink",
      "version": "2.0.0",
      "description": "Shlink, the self-hosted URL shortener",
      "license": {
          "name": "MIT",
          "url": "https://github.com/shlinkio/shlink/blob/develop/LICENSE"
      }
  },
  "defaultContentType": "application/json",
  "channels": {
      "http://shlink.io/new-visit": {
          "subscribe": {
              "summary": "Receive information about any new visit occurring on any short URL.",
              "operationId": "newVisit",
              "message": {
                  "payload": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                          "shortUrl": {
                              "$ref": "#/components/schemas/ShortUrl"
                          },
                          "visit": {
                              "$ref": "#/components/schemas/Visit"
                          }
                      }
                  }
              }
          }
      },
      "http://shlink.io/new-visit/{shortCode}": {
          "parameters": {
              "shortCode": {
                  "description": "The short code of the short URL",
                  "schema": {
                      "type": "string"
                  }
              }
          },
          "subscribe": {
              "summary": "Receive information about any new visit occurring on a specific short URL.",
              "operationId": "newShortUrlVisit",
              "message": {
                  "payload": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                          "shortUrl": {
                              "$ref": "#/components/schemas/ShortUrl"
                          },
                          "visit": {
                              "$ref": "#/components/schemas/Visit"
                          }
                      }
                  }
              }
          }
      }
  },
  "components": {
      "schemas": {
          "ShortUrl": {
              "type": "object",
              "properties": {
                  "shortCode": {
                      "type": "string",
                      "description": "The short code for this short URL."
                  },
                  "shortUrl": {
                      "type": "string",
                      "description": "The short URL."
                  },
                  "longUrl": {
                      "type": "string",
                      "description": "The original long URL."
                  },
                  "dateCreated": {
                      "type": "string",
                      "format": "date-time",
                      "description": "The date in which the short URL was created in ISO format."
                  },
                  "visitsCount": {
                      "type": "integer",
                      "description": "The number of visits that this short URL has recieved."
                  },
                  "tags": {
                      "type": "array",
                      "items": {
                          "type": "string"
                      },
                      "description": "A list of tags applied to this short URL"
                  },
                  "meta": {
                      "$ref": "#/components/schemas/ShortUrlMeta"
                  },
                  "domain": {
                      "type": "string",
                      "description": "The domain in which the short URL was created. Null if it belongs to default domain."
                  }
              },
              "example": {
                  "shortCode": "12C18",
                  "shortUrl": "https://doma.in/12C18",
                  "longUrl": "https://store.steampowered.com",
                  "dateCreated": "2016-08-21T20:34:16+02:00",
                  "visitsCount": 328,
                  "tags": [
                      "games",
                      "tech"
                  ],
                  "meta": {
                      "validSince": "2017-01-21T00:00:00+02:00",
                      "validUntil": null,
                      "maxVisits": 100
                  },
                  "domain": "example.com"
              }
          },
          "ShortUrlMeta": {
              "type": "object",
              "required": [
                  "validSince",
                  "validUntil",
                  "maxVisits"
              ],
              "properties": {
                  "validSince": {
                      "description": "The date (in ISO-8601 format) from which this short code will be valid",
                      "type": "string",
                      "nullable": true
                  },
                  "validUntil": {
                      "description": "The date (in ISO-8601 format) until which this short code will be valid",
                      "type": "string",
                      "nullable": true
                  },
                  "maxVisits": {
                      "description": "The maximum number of allowed visits for this short code",
                      "type": "number",
                      "nullable": true
                  }
              }
          },
          "Visit": {
              "type": "object",
              "properties": {
                  "referer": {
                      "type": "string",
                      "description": "The origin from which the visit was performed"
                  },
                  "date": {
                      "type": "string",
                      "format": "date-time",
                      "description": "The date in which the visit was performed"
                  },
                  "userAgent": {
                      "type": "string",
                      "description": "The user agent from which the visit was performed"
                  },
                  "visitLocation": {
                      "$ref": "#/components/schemas/VisitLocation"
                  }
              },
              "example": {
                  "referer": "https://t.co",
                  "date": "2015-08-20T05:05:03+04:00",
                  "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36",
                  "visitLocation": {
                      "cityName": "Cupertino",
                      "countryCode": "US",
                      "countryName": "United States",
                      "latitude": 37.3042,
                      "longitude": -122.0946,
                      "regionName": "California",
                      "timezone": "America/Los_Angeles"
                  }
              }
          },
          "VisitLocation": {
              "type": "object",
              "properties": {
                  "cityName": {
                      "type": "string"
                  },
                  "countryCode": {
                      "type": "string"
                  },
                  "countryName": {
                      "type": "string"
                  },
                  "latitude": {
                      "type": "number"
                  },
                  "longitude": {
                      "type": "number"
                  },
                  "regionName": {
                      "type": "string"
                  },
                  "timezone": {
                      "type": "string"
                  }
              }
          }
      }
  }
}
`;
```

I will use the above template for all examples.

3️⃣ Now all you need to do is to run `npm start` and voilà ! You should see this.👇

![generated AsyncAPI documentation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/05ma5afh6fodlmxx6y7n.png)

---

### <a name="vue"></a>Vue

1️⃣ This Vue example is just as bare bone as the previous. I even did not create a separate file for my AsyncAPI template.

React AsyncAPI component is required here as well so again we need to run `npm install --save @asyncapi/react-component@next` command.

Here is the structure of my Vue example:

![vue-project-stucture](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h52c1bmg1us2y72dx7zm.png)

Same as before, you can view it on [GitHub](https://github.com/m1ner79/asyncapi-docs-rendering-examples/tree/main/asyncapiVue).

2️⃣ In your **App.vue** just add this code:

```
<template>
  <div ref="asyncapi"></div>
</template>

<script>
import AsyncApiStandalone from '@asyncapi/react-component/browser/standalone';

const schema = `
{
  "asyncapi": "2.4.0",
  "info": {
      "title": "Shlink",
      "version": "2.0.0",
      "description": "Shlink, the self-hosted URL shortener",
      "license": {
          "name": "MIT",
          "url": "https://github.com/shlinkio/shlink/blob/develop/LICENSE"
      }
  },
  "defaultContentType": "application/json",
  "channels": {
      "http://shlink.io/new-visit": {
          "subscribe": {
              "summary": "Receive information about any new visit occurring on any short URL.",
              "operationId": "newVisit",
              "message": {
                  "payload": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                          "shortUrl": {
                              "$ref": "#/components/schemas/ShortUrl"
                          },
                          "visit": {
                              "$ref": "#/components/schemas/Visit"
                          }
                      }
                  }
              }
          }
      },
      "http://shlink.io/new-visit/{shortCode}": {
          "parameters": {
              "shortCode": {
                  "description": "The short code of the short URL",
                  "schema": {
                      "type": "string"
                  }
              }
          },
          "subscribe": {
              "summary": "Receive information about any new visit occurring on a specific short URL.",
              "operationId": "newShortUrlVisit",
              "message": {
                  "payload": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                          "shortUrl": {
                              "$ref": "#/components/schemas/ShortUrl"
                          },
                          "visit": {
                              "$ref": "#/components/schemas/Visit"
                          }
                      }
                  }
              }
          }
      }
  },
  "components": {
      "schemas": {
          "ShortUrl": {
              "type": "object",
              "properties": {
                  "shortCode": {
                      "type": "string",
                      "description": "The short code for this short URL."
                  },
                  "shortUrl": {
                      "type": "string",
                      "description": "The short URL."
                  },
                  "longUrl": {
                      "type": "string",
                      "description": "The original long URL."
                  },
                  "dateCreated": {
                      "type": "string",
                      "format": "date-time",
                      "description": "The date in which the short URL was created in ISO format."
                  },
                  "visitsCount": {
                      "type": "integer",
                      "description": "The number of visits that this short URL has recieved."
                  },
                  "tags": {
                      "type": "array",
                      "items": {
                          "type": "string"
                      },
                      "description": "A list of tags applied to this short URL"
                  },
                  "meta": {
                      "$ref": "#/components/schemas/ShortUrlMeta"
                  },
                  "domain": {
                      "type": "string",
                      "description": "The domain in which the short URL was created. Null if it belongs to default domain."
                  }
              },
              "example": {
                  "shortCode": "12C18",
                  "shortUrl": "https://doma.in/12C18",
                  "longUrl": "https://store.steampowered.com",
                  "dateCreated": "2016-08-21T20:34:16+02:00",
                  "visitsCount": 328,
                  "tags": [
                      "games",
                      "tech"
                  ],
                  "meta": {
                      "validSince": "2017-01-21T00:00:00+02:00",
                      "validUntil": null,
                      "maxVisits": 100
                  },
                  "domain": "example.com"
              }
          },
          "ShortUrlMeta": {
              "type": "object",
              "required": [
                  "validSince",
                  "validUntil",
                  "maxVisits"
              ],
              "properties": {
                  "validSince": {
                      "description": "The date (in ISO-8601 format) from which this short code will be valid",
                      "type": "string",
                      "nullable": true
                  },
                  "validUntil": {
                      "description": "The date (in ISO-8601 format) until which this short code will be valid",
                      "type": "string",
                      "nullable": true
                  },
                  "maxVisits": {
                      "description": "The maximum number of allowed visits for this short code",
                      "type": "number",
                      "nullable": true
                  }
              }
          },
          "Visit": {
              "type": "object",
              "properties": {
                  "referer": {
                      "type": "string",
                      "description": "The origin from which the visit was performed"
                  },
                  "date": {
                      "type": "string",
                      "format": "date-time",
                      "description": "The date in which the visit was performed"
                  },
                  "userAgent": {
                      "type": "string",
                      "description": "The user agent from which the visit was performed"
                  },
                  "visitLocation": {
                      "$ref": "#/components/schemas/VisitLocation"
                  }
              },
              "example": {
                  "referer": "https://t.co",
                  "date": "2015-08-20T05:05:03+04:00",
                  "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36",
                  "visitLocation": {
                      "cityName": "Cupertino",
                      "countryCode": "US",
                      "countryName": "United States",
                      "latitude": 37.3042,
                      "longitude": -122.0946,
                      "regionName": "California",
                      "timezone": "America/Los_Angeles"
                  }
              }
          },
          "VisitLocation": {
              "type": "object",
              "properties": {
                  "cityName": {
                      "type": "string"
                  },
                  "countryCode": {
                      "type": "string"
                  },
                  "countryName": {
                      "type": "string"
                  },
                  "latitude": {
                      "type": "number"
                  },
                  "longitude": {
                      "type": "number"
                  },
                  "regionName": {
                      "type": "string"
                  },
                  "timezone": {
                      "type": "string"
                  }
              }
          }
      }
  }
}
`; // AsyncAPI specification, fetched or pasted.

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

3️⃣ Before you run it there is one more thing to do. Go to 👇 `node_modules/@asyncapi/react-component/style/default.min.css`.

Copy that file and then paste it into your _**assets**_ folder.
I called mine **asyncapi.min.css**.

You can import this in your **main.js** file with `import './assets/asyncapi.min.css'` or as I did, add it at the end of **App.vue** file with `<style scope src="@/assets/asyncapi.min.css"></style>`.

4️⃣ Run `npm run dev` and you should see this 👇

![generated AsyncApi documentation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cieeaxe8g5cz3k6xyosu.png)

---

### <a name="html"></a>HTML

1️⃣ All you need is just basic HTML code. This is mine on [GitHub](https://github.com/m1ner79/asyncapi-docs-rendering-examples/blob/main/webcomponent/index.html).

2️⃣ In the **head** element enter `<link rel="stylesheet" href="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/styles/default.min.css">`

3️⃣ In the **body** element type in:

```
 <div id="asyncapi"></div>

    <script src="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/browser/standalone/index.js"></script>
    <script>
        AsyncApiStandalone.render({
            schema: `
{
  "asyncapi": "2.4.0",
  "info": {
      "title": "Shlink",
      "version": "2.0.0",
      "description": "Shlink, the self-hosted URL shortener",
      "license": {
          "name": "MIT",
          "url": "https://github.com/shlinkio/shlink/blob/develop/LICENSE"
      }
  },
  "defaultContentType": "application/json",
  "channels": {
      "http://shlink.io/new-visit": {
          "subscribe": {
              "summary": "Receive information about any new visit occurring on any short URL.",
              "operationId": "newVisit",
              "message": {
                  "payload": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                          "shortUrl": {
                              "$ref": "#/components/schemas/ShortUrl"
                          },
                          "visit": {
                              "$ref": "#/components/schemas/Visit"
                          }
                      }
                  }
              }
          }
      },
      "http://shlink.io/new-visit/{shortCode}": {
          "parameters": {
              "shortCode": {
                  "description": "The short code of the short URL",
                  "schema": {
                      "type": "string"
                  }
              }
          },
          "subscribe": {
              "summary": "Receive information about any new visit occurring on a specific short URL.",
              "operationId": "newShortUrlVisit",
              "message": {
                  "payload": {
                      "type": "object",
                      "additionalProperties": false,
                      "properties": {
                          "shortUrl": {
                              "$ref": "#/components/schemas/ShortUrl"
                          },
                          "visit": {
                              "$ref": "#/components/schemas/Visit"
                          }
                      }
                  }
              }
          }
      }
  },
  "components": {
      "schemas": {
          "ShortUrl": {
              "type": "object",
              "properties": {
                  "shortCode": {
                      "type": "string",
                      "description": "The short code for this short URL."
                  },
                  "shortUrl": {
                      "type": "string",
                      "description": "The short URL."
                  },
                  "longUrl": {
                      "type": "string",
                      "description": "The original long URL."
                  },
                  "dateCreated": {
                      "type": "string",
                      "format": "date-time",
                      "description": "The date in which the short URL was created in ISO format."
                  },
                  "visitsCount": {
                      "type": "integer",
                      "description": "The number of visits that this short URL has recieved."
                  },
                  "tags": {
                      "type": "array",
                      "items": {
                          "type": "string"
                      },
                      "description": "A list of tags applied to this short URL"
                  },
                  "meta": {
                      "$ref": "#/components/schemas/ShortUrlMeta"
                  },
                  "domain": {
                      "type": "string",
                      "description": "The domain in which the short URL was created. Null if it belongs to default domain."
                  }
              },
              "example": {
                  "shortCode": "12C18",
                  "shortUrl": "https://doma.in/12C18",
                  "longUrl": "https://store.steampowered.com",
                  "dateCreated": "2016-08-21T20:34:16+02:00",
                  "visitsCount": 328,
                  "tags": [
                      "games",
                      "tech"
                  ],
                  "meta": {
                      "validSince": "2017-01-21T00:00:00+02:00",
                      "validUntil": null,
                      "maxVisits": 100
                  },
                  "domain": "example.com"
              }
          },
          "ShortUrlMeta": {
              "type": "object",
              "required": [
                  "validSince",
                  "validUntil",
                  "maxVisits"
              ],
              "properties": {
                  "validSince": {
                      "description": "The date (in ISO-8601 format) from which this short code will be valid",
                      "type": "string",
                      "nullable": true
                  },
                  "validUntil": {
                      "description": "The date (in ISO-8601 format) until which this short code will be valid",
                      "type": "string",
                      "nullable": true
                  },
                  "maxVisits": {
                      "description": "The maximum number of allowed visits for this short code",
                      "type": "number",
                      "nullable": true
                  }
              }
          },
          "Visit": {
              "type": "object",
              "properties": {
                  "referer": {
                      "type": "string",
                      "description": "The origin from which the visit was performed"
                  },
                  "date": {
                      "type": "string",
                      "format": "date-time",
                      "description": "The date in which the visit was performed"
                  },
                  "userAgent": {
                      "type": "string",
                      "description": "The user agent from which the visit was performed"
                  },
                  "visitLocation": {
                      "$ref": "#/components/schemas/VisitLocation"
                  }
              },
              "example": {
                  "referer": "https://t.co",
                  "date": "2015-08-20T05:05:03+04:00",
                  "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36",
                  "visitLocation": {
                      "cityName": "Cupertino",
                      "countryCode": "US",
                      "countryName": "United States",
                      "latitude": 37.3042,
                      "longitude": -122.0946,
                      "regionName": "California",
                      "timezone": "America/Los_Angeles"
                  }
              }
          },
          "VisitLocation": {
              "type": "object",
              "properties": {
                  "cityName": {
                      "type": "string"
                  },
                  "countryCode": {
                      "type": "string"
                  },
                  "countryName": {
                      "type": "string"
                  },
                  "latitude": {
                      "type": "number"
                  },
                  "longitude": {
                      "type": "number"
                  },
                  "regionName": {
                      "type": "string"
                  },
                  "timezone": {
                      "type": "string"
                  }
              }
          }
      }
  }
}
`,

            config: {
                show: {
                    sidebar: false,
                }
            },
        }, document.getElementById('asyncapi'));
    </script>
```

4️⃣ Open that file with your favorite browser and you should see exactly this same screen like on previous two examples.

---

### <a name="sb"></a>Standalone Bundle

Simplicity of this bundle is just amazing 😲🤯.

1️⃣ Just create a **.html** file then copy and paste this code 👇

```
<script src="https://unpkg.com/@asyncapi/web-component@1.0.0-next.39/lib/asyncapi-web-component.js" defer></script>

<asyncapi-component
  schema='
  {
    "asyncapi": "2.4.0",
    "info": {
        "title": "Shlink",
        "version": "2.0.0",
        "description": "Shlink, the self-hosted URL shortener",
        "license": {
            "name": "MIT",
            "url": "https://github.com/shlinkio/shlink/blob/develop/LICENSE"
        }
    },
    "defaultContentType": "application/json",
    "channels": {
        "http://shlink.io/new-visit": {
            "subscribe": {
                "summary": "Receive information about any new visit occurring on any short URL.",
                "operationId": "newVisit",
                "message": {
                    "payload": {
                        "type": "object",
                        "additionalProperties": false,
                        "properties": {
                            "shortUrl": {
                                "$ref": "#/components/schemas/ShortUrl"
                            },
                            "visit": {
                                "$ref": "#/components/schemas/Visit"
                            }
                        }
                    }
                }
            }
        },
        "http://shlink.io/new-visit/{shortCode}": {
            "parameters": {
                "shortCode": {
                    "description": "The short code of the short URL",
                    "schema": {
                        "type": "string"
                    }
                }
            },
            "subscribe": {
                "summary": "Receive information about any new visit occurring on a specific short URL.",
                "operationId": "newShortUrlVisit",
                "message": {
                    "payload": {
                        "type": "object",
                        "additionalProperties": false,
                        "properties": {
                            "shortUrl": {
                                "$ref": "#/components/schemas/ShortUrl"
                            },
                            "visit": {
                                "$ref": "#/components/schemas/Visit"
                            }
                        }
                    }
                }
            }
        }
    },
    "components": {
        "schemas": {
            "ShortUrl": {
                "type": "object",
                "properties": {
                    "shortCode": {
                        "type": "string",
                        "description": "The short code for this short URL."
                    },
                    "shortUrl": {
                        "type": "string",
                        "description": "The short URL."
                    },
                    "longUrl": {
                        "type": "string",
                        "description": "The original long URL."
                    },
                    "dateCreated": {
                        "type": "string",
                        "format": "date-time",
                        "description": "The date in which the short URL was created in ISO format."
                    },
                    "visitsCount": {
                        "type": "integer",
                        "description": "The number of visits that this short URL has recieved."
                    },
                    "tags": {
                        "type": "array",
                        "items": {
                            "type": "string"
                        },
                        "description": "A list of tags applied to this short URL"
                    },
                    "meta": {
                        "$ref": "#/components/schemas/ShortUrlMeta"
                    },
                    "domain": {
                        "type": "string",
                        "description": "The domain in which the short URL was created. Null if it belongs to default domain."
                    }
                },
                "example": {
                    "shortCode": "12C18",
                    "shortUrl": "https://doma.in/12C18",
                    "longUrl": "https://store.steampowered.com",
                    "dateCreated": "2016-08-21T20:34:16+02:00",
                    "visitsCount": 328,
                    "tags": [
                        "games",
                        "tech"
                    ],
                    "meta": {
                        "validSince": "2017-01-21T00:00:00+02:00",
                        "validUntil": null,
                        "maxVisits": 100
                    },
                    "domain": "example.com"
                }
            },
            "ShortUrlMeta": {
                "type": "object",
                "required": [
                    "validSince",
                    "validUntil",
                    "maxVisits"
                ],
                "properties": {
                    "validSince": {
                        "description": "The date (in ISO-8601 format) from which this short code will be valid",
                        "type": "string",
                        "nullable": true
                    },
                    "validUntil": {
                        "description": "The date (in ISO-8601 format) until which this short code will be valid",
                        "type": "string",
                        "nullable": true
                    },
                    "maxVisits": {
                        "description": "The maximum number of allowed visits for this short code",
                        "type": "number",
                        "nullable": true
                    }
                }
            },
            "Visit": {
                "type": "object",
                "properties": {
                    "referer": {
                        "type": "string",
                        "description": "The origin from which the visit was performed"
                    },
                    "date": {
                        "type": "string",
                        "format": "date-time",
                        "description": "The date in which the visit was performed"
                    },
                    "userAgent": {
                        "type": "string",
                        "description": "The user agent from which the visit was performed"
                    },
                    "visitLocation": {
                        "$ref": "#/components/schemas/VisitLocation"
                    }
                },
                "example": {
                    "referer": "https://t.co",
                    "date": "2015-08-20T05:05:03+04:00",
                    "userAgent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36",
                    "visitLocation": {
                        "cityName": "Cupertino",
                        "countryCode": "US",
                        "countryName": "United States",
                        "latitude": 37.3042,
                        "longitude": -122.0946,
                        "regionName": "California",
                        "timezone": "America/Los_Angeles"
                    }
                }
            },
            "VisitLocation": {
                "type": "object",
                "properties": {
                    "cityName": {
                        "type": "string"
                    },
                    "countryCode": {
                        "type": "string"
                    },
                    "countryName": {
                        "type": "string"
                    },
                    "latitude": {
                        "type": "number"
                    },
                    "longitude": {
                        "type": "number"
                    },
                    "regionName": {
                        "type": "string"
                    },
                    "timezone": {
                        "type": "string"
                    }
                }
            }
        }
    }
  }'
  config='{"show": {"sidebar": false}}'

  cssImportPath="https://unpkg.com/@asyncapi/react-component@1.0.0-next.39/styles/default.min.css">
</asyncapi-component>
```

2️⃣ Now, just open your file (here is mine on [GitHub](https://github.com/m1ner79/asyncapi-docs-rendering-examples/blob/main/standalone-bundle-no-framework/index.html)) and... yes you can see a familiar screen. The standalone bundle is just 🪄🤯.

This was only a demonstration of what can be done. AsyncAPI can do a lot more. Check [AsyncAPI documentation](https://www.asyncapi.com/docs/tutorials/getting-started/asyncapi-documents) for more information on how to generate docs.

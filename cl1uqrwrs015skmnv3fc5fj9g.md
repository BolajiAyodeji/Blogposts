## How to Build an International Ecommerce Website with Sanity and Commerce Layer

One of the greatest benefits of composable, headless commerce is the flexibility it introduces to the developer experience of building shopping experiences. Decoupling website content and commerce data makes it easier for content and commerce teams of experts to work independently and more efficiently. With Commerce Layer, content managers can work with a best-of-breed headless CMS like Sanity, merchants can build their inventory in Commerce Layer, and developers can build with any stack in their most preferred programming language while utilizing Commerce Layer’s APIs.

In this tutorial, you will learn how we built the [Commerce Layer Starter](https://github.com/commercelayer/sanity-template-commercelayer) with Nextjs, Sanity studio, and deployed it to Netlify. At the end of the tutorial, you should be able to set up and build your own 1-click sanity starter with ease or integrate with Commerce Layer.

## Prerequisites

- Git installed (Learn how to install Git [here](https://github.com/git-guides/install-git) if you haven't already).
- Node and NPM installed (Learn how to install Nodejs [here](https://nodejs.org/en/download/package-manager/) if you haven't already).
- Basic knowledge of how to use the terminal.
- Basic knowledge of NPM.
- A grin on your face 😉.

## Introduction to Commerce Layer

[Commerce Layer](https://commercelayer.io) is a transactional commerce API and order management for international brands. It lets you make any digital experience shoppable, anywhere. You can build a multi-language website with Shopify, Contentful, WordPress, or any other CMS you already love. Then, add Commerce Layer for multi-currency prices, distributed inventory, localized payment gateways, promotions, orders, subscriptions, and more.

Unlike traditional solutions, [Commerce Layer was built for the new era](https://commercelayer.io/why). It natively supports the most modern development workflows, such as the Jamstack. Ecommerce businesses can integrate Commerce Layer with a single backend and serve on multiple presentation layers enabling them to build outstanding shopping experiences, go headless, and scale their business globally. You can check out our [developer resources](https://commercelayer.io/developers/) to learn more and get started.


![A screenshot of Commerce Layer's website homepage](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682449914/Isf0Kza3Z.png)

## Introducing Sanity Studio

The Sanity studio is an open-source content management system built with React.js. It offers rapid configuration, free form customization, reusable structured content, a comfortable editor, real-time collaboration, toolkits, plugins, and more features to enable you to create the best content workflow.

Sanity provides the possibility to create starter templates that can be re-used by developers easily. The starter is primarily a repository hosted on GitHub that contains some meta-information, demo content, schema, and frontend(s) that will end up in a new repository when a developer installs the starter through [sanity.io/starters](https://www.sanity.io/starters). When a developer installs the starter, Sanity creates a new project on Sanity and a new repository on GitHub with the starter code, attaches a new Sanity `datasetId` to the starter, and deploys the project to Netlify simultaneously.

Generally, a sanity starter can include a Sanity studio, a frontend application, both or multiple frontends and studios. For the purpose of this tutorial, we will create a starter that will include a studio and frontend. Our starter will include:

- An ecommerce storefront built with Nextjs and [Commerce Layer react components library](https://github.com/commercelayer/commercelayer-react-components).
- International shopping capabilities powered by [Commerce Layer APIs](https://docs.commercelayer.io/developers/v/api-reference/).
- Some ecommerce data imported using the [Commerce Layer CLI](https://github.com/commercelayer/commercelayer-cli).
- Structured content on Sanity studio.
- Localization support.
- Deployment configuration settings to Netlify.

![A GitHub repo cover image](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682532486/yZQ5D5vgy.png)

## Sanity Starter Project Structure

Sanity has a defined specification for starters which includes some required files and directories. These specifications provide information about the starter to developers using the starter and make the project function as a reusable starter. Below is the folder structure of a Sanity project with required files and directories (without any frontend added):

```bash
├── .sanity-template
├── .sanity-template/assets
├── .sanity-template/data
├── .sanity-template/manifest.json
├── README.md
```

- **`.sanity-template`** is the root directory where all meta-information for using this repository as a template on [sanity.io/starters](http://sanity.io/starters) is stored.
- **`.sanity-template/assets`** is the directory for storing assets related to displaying information about the starter. In this case, preview images for the overall project and for each site the starter contains.
- **`.sanity-template/data`** is the directory to store a Sanity dataset export if you want the starter to launch with some demo content.
- **`.sanity-template/manifest.json`** is the JSON file containing details about the Starter as well as deployment information.
- **`README.md`** is the markdown file for this project that will be displayed on the Create page.

For a finished starter project, the root of the project should contain all deployable code, including the frontend and studio. Generally, a project spun from a starter is split into three parts:

1. The root for all frontend code
2. The `/studio` directory for all studio code.
3. The `.sanity-template` for all starter meta-information.

Here is a sample from the [Commerce Layer sanity starter](https://github.com/commercelayer/sanity-template-commercelayer) as seen in the image below:

![sanity-starter-github-repo-screenshot](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682579244/W92y68XXE.jpg)

## How We Built the Commerce Layer Sanity Starter

In this section, you will learn how we built a starter with an ecommerce application with transactional functionalities powered by [Commerce Layer](https://commercelayer.io/) APIs, structured content on Sanity, imported seed data, and deployment configuration to Netlify. If you want to follow along with the guide, you can take a look at the finished project on GitHub [here](https://github.com/commercelayer/sanity-template-commercelayer) or even install the starter [here](https://www.sanity.io/create?template=commercelayer/sanity-template-commercelayer).

Here is a sequential breakdown of all the steps taken to develop a starter:

### 1️⃣  Setup a new Sanity project using the Sanity CLI

Sanity has a command-line interface that we can use to interact with Sanity, create new projects, manage datasets, import data, and much more from the CLI. We'll use this CLI to set up a new sanity project following the steps below:

**1: Install the CLI**

Run the command below to install the Sanity CLI.

```bash
npm install -g @sanity/cli
```

**2: Create a new project**

Run the command below to bootstrap a new project which will log you into Sanity, create a new project, set up a dataset, and generate the files needed to run the studio environment locally.

```bash
sanity init
```

**3: Run the studio**

Run the command below to build the initial JavaScript code required to run the studio, and start a local web server.

```bash
sanity start
```

The studio should now run on `[localhost:3333](http://localhost:3333)`. You can always run `sanity help` to get an overview of other available and useful commands in the Sanity CLI.

### 2️⃣  Content modeling for the created Sanity studio

Now that we understand how Sanity works and have set up a new sanity project, let's structure our sanity studio schema. Sanity schema defines how your content should be modeled, and this structure reflects in the studio UI. The schema describes the different field types a document consists of. Sanity uses the `schema.js` file in the `/schemas` directory to determine the content model of the project.

With Sanity, you define a block of content as a document or split your documents into modules and import them into the parent `schema.js` file. Generally, there are three categories of Sanity schema types:

- Document types ([document](https://www.sanity.io/docs/document-type) and other published custom schemas)
- Primitive types (e.g., [boolean](https://www.sanity.io/docs/boolean-type), [string](https://www.sanity.io/docs/string-type), [text](https://www.sanity.io/docs/text-type), [number](https://www.sanity.io/docs/number-type), [array](https://www.sanity.io/docs/array-type), [datetime](https://www.sanity.io/docs/datetime-type), and [URL](https://www.sanity.io/docs/url-type))
- Object types (e.g., [object](https://www.sanity.io/docs/object-type), [block](https://www.sanity.io/docs/block-type), [span](https://www.sanity.io/docs/span-type), [reference](https://www.sanity.io/docs/reference-type), [slug](https://www.sanity.io/docs/slug-type), [image](https://www.sanity.io/docs/image-type), and [file](https://www.sanity.io/docs/file-type))

You can find all of the Sanity’s types in this [reference documentation](https://www.sanity.io/docs/schema-types) or learn how to structure your content model based on your needs by reading [this comprehensive guide](https://www.sanity.io/guides/introduction-to-content-modeling).

For the Commerce Layer starter, our `schema.js` looks like so in the snippet below with imports of several other module documents. You can view the schema code for each module [here](https://github.com/commercelayer/sanity-template-commercelayer/tree/main/studio/schemas) in the GitHub repository.

```jsx
import createSchema from 'part:@sanity/base/schema-creator'
import schemaTypes from 'all:part:@sanity/base/schema-type'

// We import object and document schemas
import product from './product'
import country from './country'
import variant from './variant'
import size from './size'
import taxon from './taxon'
import taxonomy from './taxonomy'
import catalog from './catalog'
import blockContent from './blockContent'

import productImage from './productImage'
import localeString from './locale/String'
import localeText from './locale/Text'
import localeSlug from './locale/Slug'
import localeBlockContent from './locale/BlockContent'

// Then we give our schema to the builder and provide the result to Sanity
export default createSchema({
  // We name our schema
  name: 'default',
  // Then proceed to concatenate our document type
  // to the ones provided by any plugins that are installed
  types: schemaTypes.concat([
    // The following are document types which will appear
    // in the studio.
    product,
    country,
    variant,
    size,
    taxon,
    taxonomy,
    catalog,
    // When added to this list, object types can be used as
    // { type: "typename" } in other document schemas
    productImage,
    blockContent,
    localeString,
    localeText,
    localeSlug,
    localeBlockContent,
  ]),
})
```

### 3️⃣  Add content to Sanity studio

If you are working on a new project like we did when we began developing the starter, you will have to manually add content to your project using the Sanity studio running on `[localhost:3333](http://localhost:3333)`. The studio should now have the content fields populated with the configured content schemas in the “Desk” view. You can use that to add content to your project, as seen in the screenshot below.

![sanity-studio-desk-view-screenshot](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682643887/tL_1yhMVy.jpg)

If you are starting a new project using a starter or a previously saved project, then you can easily import a dataset with saved data following the steps below:

1. Extract the `production.tar.gz` file in `/.sanity-template/data` directory using the command below:

```bash
tar -xf production.tar.gz
```

The extracted folder name should look like `production-export-2021-02-26t14-15-56-557z`.

2. Run the command below in `/studio` to import the `data.ndjson` file in the extracted folder.

```bash
sanity dataset import ../.sanity-template/data/<name of extracted folder>/data.ndjson <your_dataset>
```

You should check the running Sanity studio now to preview the imported content.

### 4️⃣  Add frontend and integrate with Sanity

Before you add all frontend code to the root directory, you should move the Sanity studio code into a directory named `/studio`.

![sanity-starter-github-repo-studio-folder-screenshot](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682680953/Gf7puWQ7B.jpg)

At this stage, you will add the frontend code of your project, which can either be a blog, marketing website, CRM, or storefront. The major thing to do here is to use any of the [Sanity client](https://www.sanity.io/docs/client-libraries) libraries to integrate Sanity into your frontend and fetch data. In our case, we used the official [Javascript client](https://www.sanity.io/docs/js-client) that works in Node.js and modern browsers.

```jsx
import sanityClient from '@sanity/client'

const client = sanityClient({
  projectId: process.env.SANITY_PROJECT_ID as string,
  dataset: process.env.SANITY_DATASET as string,
  useCdn: process.env.NODE_ENV === 'production', // `false` if you want to ensure fresh data
})
```

Here’s an example of how we query Sanity to fetch the country and product data:

```jsx
import _ from 'lodash'
import {
  SanityCountry,
  SanityProduct
} from './typings'

//Countries
const sanityAllCountries = async (locale = 'en-US') => {
  const lang = parseLocale(locale, '_', '-', 'lowercase')
  const query = `*[_type == "country"]{
    name,
    code,
    marketId,
    defaultLocale,
    "image": {
      "url": image.asset->url
    },
    'catalog': {
      'id': catalog->_id
    }
  } | order(name["${lang}"] asc)`
  const countries = await client.fetch<SanityCountry[]>(query)
  return countries.map((country) => {
    const localization = {
      name: country?.name[lang],
    }
    return { ...country, ...localization }
  })
}

//Products
const sanityGetProduct = async (slug: string, locale = 'en-US') => {
  const lang = parseLocale(locale, '_', '-', 'lowercase')
  const query = `*[_type == "product" && slug["${lang}"].current == "${slug}"]{
    name,
    description,
    reference,
    slug,
    'images': images[]->{
      'url': images.asset->url
    },
    'variants': variants[]->{
      label,
      code,
      name,
      size->,
      'images': images[]->{
        'url': images.asset->url
      }
    }    
  }`
  const item: any[] = await client.fetch(query)
  return parsingProduct(_.first(item), lang)
}
```

You can explore all our queries for the Commerce Layer starter project [here](https://github.com/commercelayer/sanity-template-commercelayer/blob/main/utils/sanity/api.ts) in the GitHub repository. Also, here’s the [major code](https://github.com/commercelayer/sanity-template-commercelayer/blob/main/pages/%5BcountryCode%5D/%5Blang%5D/%5Bproduct%5D.tsx) powering our frontend alongside some hooks, utils, components, and dependencies.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682886239/Z6Fxba_BQ.png)

Now that you have a Sanity Starter set up, we’ll show you the foundation principles needed to integrate commerce data from Commerce Layer. This is where you will begin to see the powerful combination of Commerce Layer data with Sanity content. And by the end of the tutorial, you will see not only the benefits of this integration, but you will also be able to experiment with your commerce data next to Sanity to see the power of both tools together.

### 5️⃣  Get Commerce Layer API Credentials

In the starter we built, transactional functionalities of your ecommerce platform are managed by Commerce Layer, while the content is managed by Sanity studio. This will result in better order management and content management. To get started with using Commerce Layer, you will need to create an organization, perform some configurations and settings for your business, seed some demo data, and get your API credentials. The API credentials will allow you to interact with Commerce Layer in your presentation layer (frontend) and the CLI. To get the required credentials, kindly follow the steps below:

1. Create a free developer account [here](https://dashboard.commercelayer.io/sign_up). If you already have an account, kindly skip to Step 3.
2. Upon successful sign-up, skip the onboarding tutorial for the purposes of this article (we'll set up and seed the organization manually through the CLI shortly).
3. Create a new [organization](https://commercelayer.io/docs/data-model/users-and-organizations) for your business.
4. In the Commerce Layer dashboard, click on the **Sales channels** tab and create an application, with the name: `Website`. Upon successful creation, you'll get a `CLIENT ID` , `BASE ENDPOINT`, and `ALLOWED SCOPES`. Kindly remember to save that as we'll use it to interact with our application later.
5. In the Commerce Layer dashboard, click on the **Integrations** tab and create an application, with the name: `CLI` and role: `Admin`. Upon successful creation, you'll get a `CLIENT ID`, `CLIENT SECRET`, and `BASE ENDPOINT`. Kindly remember to save that as we'll use it to interact with the CLI later.

### 6️⃣  Seed Organization with Test Data

The official [Commerce Layer CLI](https://github.com/commercelayer/commercelayer-cli) helps you to manage your Commerce Layer applications right from the terminal. Installing the CLI provides access to the `commercelayer` command. You can set it up using the following steps:

1. Install the CLI using your favorite package manager:

```bash
//npm
npm install -g @commercelayer/cli

//yarn
yarn global add @commercelayer/cli
```

2. Log into your application via the CLI using the previously created [integration](https://docs.commercelayer.io/developers/roles-and-permissions#integration) application credentials like so:

```bash
commercelayer applications:login -o <organizationSlug> -i <clientId> -s <clientSecret> -a <applicationAlias>
```

Now, with the steps below, you can use the CLI to import three demo [markets](https://data.commercelayer.app/seed/markets.json) (UK, USA, and Europe), a set of [product SKUs](https://data.commercelayer.app/seed/skus.json), related [price lists](https://data.commercelayer.app/seed/price_lists.json), related [prices](https://data.commercelayer.app/seed/prices.json), [stock locations](https://data.commercelayer.app/seed/stock_locations.json), and [inventory](https://data.commercelayer.app/seed/stock_items.json) into your organization using the multi_market [business model](https://commercelayer.io/docs/data-model/markets-and-business-models).

1. Install the [seeder plugin](https://github.com/commercelayer/commercelayer-cli-plugin-seeder) using the command below:

```bash
commercelayer plugins:install seeder
```

2. Seed your organization using the command below:

```bash
commercelayer seed -b multi_market
```

### 7️⃣  Final checklist and Netlify deployment configuration

1. In order for a starter to be validated and used through [sanity.io/starters](https://www.sanity.io/starters), it needs to follow the project name must start with `sanity-template-`.
2. Configure your Sanity metadata in `sanity-template.json` and add deployment configuration for the frontend web application and Sanity studio like so:

```json
{
  "version": 2.0,
  "title": "Commerce Layer Starter",
  "description": "A multi-country ecommerce starter built with Sanity Studio, Commerce Layer, Next.js, and deployed to Netlify.",
  "previewMedia": {
    "type": "image",
    "src": ".sanity-template/assets/preview.jpg",
    "alt": "Preview image with Commerce Layer, Nextjs, and Netlify's logo"
  },
  "technologies": [
    {
      "id": "nextjs",
      "name": "Next.js",
      "url": "https://nextjs.org"
    },
    {
      "id": "commercelayer",
      "name": "Commerce Layer",
      "url": "https://commercelayer.io"
    },
    {
      "id": "netlify",
      "name": "Netlify",
      "url": "https://netlify.com"
    }
  ],
  "deployment": {
    "provider": "netlify",
    "sites": [
      {
        "id": "studio",
        "type": "studio",
        "title": "Commerce Layer Starter Studio",
        "description": "A multi-country ecommerce starter built with Sanity Studio, Commerce Layer, Next.js, and deployed to Netlify.",
        "dir": "./studio",
        "previewMedia": {
          "type": "image",
          "src": ".sanity-template/assets/studio.png",
          "alt": "A preview image of the Sanity studio."
        },
        "buildSettings": {
          "base": "studio",
          "dir": "/dist",
          "cmd": "npm run build"
        }
      },
      {
        "id": "web",
        "type": "web",
        "title": "Commerce Layer Starter Web",
        "description": "A multi-country ecommerce starter built with Sanity Studio, Commerce Layer, Next.js, and deployed to Netlify.",
        "dir": "./web",
        "previewMedia": {
          "type": "image",
          "src": ".sanity-template/assets/preview.jpg",
          "alt": "A preview image of the web demo."
        },
        "buildSettings": {
          "base": "/",
          "dir": "/out",
          "cmd": "npm run build"
        }
      }
    ]
  }
}
```

The metadata information is primarily displayed on [sanity.io/create](https://www.sanity.io/blog/a-new-way-to-get-started-with-a-sanity-powered-website) as described below by the visual explainer from [Sanity docs](https://www.sanity.io/docs/starter-templates).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1649682937904/QVBgRYBAv.png)

1. Test your `sanity-template.json` file for errors using the sanity-template command:

```bash
sanity-template check
```

2. Build your project with the configuration in `sanity-template.json` using the command**:**

```bash
sanity-template build
```

3. You need to refactor your project's `name`,  `projectId` and `dataset` in `studio/sanity.json` to a dynamic variable so when a user installs your starter via [sanity.io/starters](https://www.sanity.io/starters), Sanity can populate it with new values. To this, you pass the string value in `<#< ... >#>` as seen in the snippet below:

```json
 {
  "root": true,
  "project": {
    "name": "<#< sanity.projectTitle >#>",
    "basePath": "/"
  },
  "api": {
    "projectId": "<#< sanity.projectId >#>",
    "dataset": "<#< sanity.dataset >#>"
  }
}
```

4. You can also set up [Renovatebot](https://github.com/renovatebot/renovate) to automatically make and merge pull requests that bump the Sanity dependencies upgrades in `studio/package.json`. All you need to do is add a `renovate.json` to the root directory, with the following configuration:

```json
{
  "extends": [
    "github>sanity-io/renovate-presets:sanity-template"
  ]
}
```

5. Run the command below to build the studio to a static bundle and deploy it to Sanity cloud on a `<your-project>.sanity.studio` URL. You can also deploy anytime you make any change to your studio.

```bash
sanity deploy
```

PS: You can still host a studio on any cloud platform you choose too (here’s [how to deploy to Netlify](https://github.com/BolajiAyodeji/cl-jamstack-ecommerce-workshop#continous-deployment-on-netlify)) so you don't have to manually deploy after every change.

6. Lastly, push your finished code to GitHub and test it live by ****deploying the starter on Sanity following the starter specification:

```
https://www.sanity.io/create?template=[githubhandle]/sanity-template-[starter-name]
```

## Conclusion

Now that you have built a Sanity starter and integrated Commerce Layer, you can start to add more items and product data stored in Commerce Layer so you can see how your products and prices show up within your content. The power of Commerce Layer is that you can really localize your commerce data to make it work for multiple markets, all of which likely have different prices, SKUs, promotions, and even simple things like item weights and measurements. Commerce Layer gives you tremendous flexibility to sell your products locally and paired with a powerful tool like Sanity, you will be on your way to building the best, most optimized shopping experience for your customers.

You can get started with the Commerce Layer starter by visiting [this link](https://www.sanity.io/create?template=commercelayer/sanity-template-commercelayer), creating a new project and following the instructions in the link. Feel free to join the [Commerce Layer Slack](https://slack.commercelayer.app) community to share what you are able to build after reading this tutorial or [showcase the starter on Sanity](https://community.sanity.tools/desk/contribution.starter%2Ctemplate%3Dcontribution.starter;WzXQvbBRsm9g2XBDjGSTY%2Ctemplate%3Dcontribution.starter). For further knowledge, you can [learn the central concepts](https://www.sanity.io/docs/starter-templates) needed to create a 1-click Sanity Starter, learn [how to build headless commerce web experiences](https://github.com/BolajiAyodeji/cl-jamstack-ecommerce-workshop) with Commerce Layer, or learn how to [sell internationally with a single Shopify store and Commerce Layer](https://commercelayer.io/blog/how-to-sell-internationally-with-a-single-shopify-store-and-commerce-layer).

Thanks for reading! 🖤
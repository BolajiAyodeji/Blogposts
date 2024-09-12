---
title: "How to Build Design Editing Apps using Nextjs, Clerk, and IMGLY’s CE.SDK Engine"
seoTitle: "How to Create Design Editing Apps using Nextjs and IMGLY’s CE.SDK"
datePublished: Wed Sep 11 2024 14:58:16 GMT+0000 (Coordinated Universal Time)
cuid: cm0xzjmmk000209jn8jg0btqw
slug: how-to-build-design-editing-apps-using-nextjs-clerk-and-imglys-cesdk-engine
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726066517452/8f221380-a620-43fd-8899-0a4d571259c8.png
tags: software-development, javascript, design, reactjs, sdk, nextjs, clerkdev

---

Creative designs have become more important than ever in the software ecosystem today with many industries and end-consumers having several use cases that require them to offer design editing solutions to either designers or end-consumers. Every business creates and uses different digital and print designs for marketing or day-to-day customer service purposes. They do this mostly to allow customers to personalize and customize certain services before they make purchases in the case of e-commerce. With the rise of customer demands, software builders now have to develop editing user interfaces to power different kinds of use cases for their users across the world. Sounds like a lot of work, right? Maybe it is. But could it get any better? Yes!

We’re in the age of composability, a term that describes the ability of engineering teams to compose different optimal tools to build the perfect experience for their users. With that in mind, I spent some time experimenting on how to build media design editing apps and I found a tool called the CreativeEditor SDK Engine that allows you to build fully customizable design editors with fewer lines of code. In this tutorial, I will show you how to use the CE.SDK Engine in a Nextjs web application to build a simple image editor and even a Canva-like editor! As a bonus, I’d also show you how you can build an image background removal app (using the [background-removal.js](https://github.com/imgly/background-removal-js) library) and integrate with Clerk Auth.

> If you want to see the final code integration, you can [head to this repository](https://github.com/BolajiAyodeji/attraktives-headshot) now, but you might want to read along to learn one or two things, especially if you’re new to this :).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726048202291/1dd05084-52ff-45fd-8c51-fbb3c861047e.png align="left")

## Prerequisites

To get the best out of this tutorial, you need to have the following:

* Nodejs and NPM installed on your computer.
    
* An IDE and terminal installed on your computer.
    
* A web browser installed on your computer.
    
* A stable connection to the internet.
    
* Some prior knowledge of the JavaScript programming language.
    
* Some prior knowledge of the Reactjs JavaScript framework.
    
* A smile on your face :).
    

## The CreativeEditor Engine

IMG․LY has built a creative engine that allows developers and businesses to add video and photo editing features to their applications. The engine is used to build different SDKs, that can power photo, video, design editing, and creative automation features for unlimited distributed end-users. They currently provide a [CreativeEditor SDK](https://img.ly/products/creative-sdk?ref=bolajiayodeji) (CE.SDK), [PhotoEditor SDK](https://img.ly/products/photo-sdk?ref=bolajiayodeji), [VideoEditor SDK](https://img.ly/products/video-sdk?ref=bolajiayodeji), and [Camera SDK](https://img.ly/products/camera-sdk?ref=bolajiayodeji) on different platforms including, Web, Server, iOS, and Android. This means you can use these SDKs with a wide range of frameworks like Vanilla JS, Reactjs, Nextjs, Vuejs, Angular, Svelte, Electron, Flutter, ReactNative, Ionic, etc. All these SDKs can be used for a wide range of use cases and industries like:

* Personalized printing.
    
* Ecommerce product customization.
    
* Web2Print.
    
* Automated design templates.
    
* Photo editors.
    
* Video editors.
    
* Design editors (like Canva).
    
* Website editors (like Wix).
    

The beautiful part is that you can use the SDK to programmatically automate different creative design tasks, workflows, and ideas you have in mind, making your business even more efficient. From code, to design, to export, to print, to ♾️! Fortune 100 businesses and other startups like HP, ZARA, Shopify, Flickr, etc. are already using the SDKs to power hundreds of applications.

## Building a Demo Image Background Editing App

To show you the basics of CE.SDK Engine, let’s build a simple Nextjs web application that enables users to craft an attractive profile picture for social media platforms. With this application, a user can upload a professional headshot image (or maybe a cute image of their pet 🙃) without a background (usually in PNG format). We will then use the CE.SDK Engine to apply different background options and allow the user to download all the edited variations. In summary, this is what the flow of the application looks like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726048298772/53ec05cd-29eb-47e3-ae2b-2218d63ce992.png align="left")

Now, let’s get started!

### \[I\] Install Packages and Setup Project Structure

First, use `create-next-app` to set up a new Nextjs project with TypeScript and App Router like so:

```bash
npx create-next-app@latest
```

Next, install all the packages we need:

```bash
npm install @cesdk/engine @cesdk/cesdk-js @imgly/background-removal @clerk/nextjs
```

Next, create some extra directories and files, as seen in the file structure below (the ones with an asterisk \* beside the name are the new files):

```plaintext
┌── app
	├── bg-add*
		├── page.tsx
    ├── bg-remove*
		├── page.tsx
	├── components*
		├── editorCanvas.tsx
		├── headshotCanvas.tsx
	├── editor*
		├── page.tsx
	├── start*
		├── page.tsx
	├── utils*
		├── grids.ts
    ├── layout.tsx
    ├── page.tsx
┌── public
├── .env.local
...
├── middleware.ts*
├── package.json
└── tsconfig.json
```

### \[II\] Some Key Terms

Before we proceed further, here are some unique key terms used in the CE.SDK engine which are the fundamental components that make up the engine canvas.

* **Canvas**: the HTML element used to draw graphics using JavaScript on the web.
    
* **Scene**: the root of the canvas for each instance of the engine accessed with the [Scene API](https://img.ly/docs/cesdk/engine/api/scene/). Generally, a scene will contain multiple pages which will also contain other blocks.
    
* **Page**: the parent block of all elements in the scene (usually used to group all blocks/elements together).
    
* **Block** (or design block): the main building unit in CE.SDK accessed with the [Block API](https://img.ly/docs/cesdk/engine/api/block/) and organized in a hierarchy structure through parent-child relationships inside the scene. Every element is a block in the canvas (e.g., graphics, shapes, images, texts, etc.).
    
* **Fill**: an object that defines the contents within a design block (e.g., images, videos, solid colors, gradients, etc.).
    

### \[III\] Setup the CE.SDK Engine

The CreativeEditor SDK Engine (`@cesdk/engine`) provides different APIs for powering any editing UI. To get started, we need to initialize the engine and pass in the config object. In the `/components/headshotCanvas.tsx` file you created earlier, add the following code:

```ts
"use client";
import { useEffect, useRef, useState, ChangeEvent } from "react";
import CreativeEngine from "@cesdk/engine";

const config = {
  license: process.env.NEXT_PUBLIC_CESDK_LICENSE,
  userId: "guides-user",
  baseURL: "https://cdn.img.ly/packages/imgly/cesdk-engine/1.24.0/assets",
};

export default function BgAddPage() {
  const cesdk_container = useRef<HTMLDivElement>(null);

  const initializeCESDK = () => {
    CreativeEngine.init(config).then((engine) => {
      // Append the engine element to the container.
      const container = cesdk_container.current!;
      container.innerHTML = "";
      container.append(engine.element);
      
      // Create a new scene and page.
      let scene = engine.scene.create();
      const page = engine.block.create("page");
      engine.block.setWidth(page, 500);
      engine.block.setHeight(page, 500);
      engine.block.appendChild(scene, page);
    });
  };
  
  useEffect(() => {
    initializeCESDK();
  }, []);
  
  return (
    <div
      ref={cesdk_container}
      style={{ width: "100vw", height: "100vh" }}
      >
    </div>
  );
}
```

In the code snippet above, we:

* Setup the `config` object and add the following parameters:
    
    * `license`: the CE.SDK API key. You can get one and test the platform free for up to 30 days once you sign up using [this form](https://img.ly/forms/free-trial). For testing in development, you can use the `mtLT-_GJwMhE7LDnO8KKEma7qSuzWuDxiKuQcxHKmz3fjaXWY2lT3o3Z2VdL5twm` license publicly available on the CE.SDK documentation. Only ensure to add that to your `.env` file using the `NEXT_PUBLIC_CESDK_LICENSE` name.
        
    * `userID`: an optional unique ID tied to your application's user. This is used mainly for tracking user data, specifically to calculate monthly active users.
        
    * `baseURL`: link to a public URL where different asset files are stored.
        
* Use the `CreativeEngine.init(config)` function to start up a new instance of the engine inside an HTML div element with a `useRef` reference to the element. This element will then contain the engine's `<cesdk-canvas/>` and will fill out its container.
    

Next, add the following code in the `/bg-add/page.tsx` file to render the `/components/headshotCanvas.tsx` component above in a page (`/bg-add` in this case):

```ts
import dynamic from "next/dynamic";

const CreativeEditorSDKWithNoSSR = dynamic(
  () => import("../components/headshotCanvas"),
  {
    ssr: false,
  }
);

export default CreativeEditorSDKWithNoSSR;
```

We’re doing this to avert errors like `ReferenceError: document is not defined` which will come up when the page renders with SSR. The CE.SDK Engine is a client-side library that requires various browser features (like `document`), hence it must be loaded and executed in the browser upon render. With this logic, we will load the library dynamically using [`next/dynamic`](https://nextjs.org/docs/app/building-your-application/optimizing/lazy-loading#nextdynamic) and disable server rendering when the page is loaded in the browser.

---

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Tip: <strong>CE.SDK</strong> is an acronym for <strong>CreativeEditor SDK</strong>.</div>
</div>

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">The <code>@cesdk/engine</code> package is the<strong> CreativeEditor Engine </strong>or<strong> CreativeEngine </strong>or<strong> CreativeEditor SDK Engine</strong> used in building the CreativeEditor SDK too (you use this to render designs on your own UI). Likewise, the <code>@cesdk/cesdk-js</code> package is the <strong>CreativeEditor SDK</strong> (the customizable Design UI and Studio UI editor you can integrate directly into your application). Quite confusing, right 😃? It took me a while to wrap my head around this and I’m sure you’d get it too :).</div>
</div>

---

### \[IV\] Add Color and Image to Page

In the same `/components/headshotCanvas.tsx` file, let’s add more code like so:

```ts
"use client";
import { useEffect, useRef, useState, ChangeEvent } from "react";
import CreativeEngine from "@cesdk/engine";

const config = {
  license: process.env.NEXT_PUBLIC_CESDK_LICENSE,
  userId: "guides-user",
  baseURL: "https://cdn.img.ly/packages/imgly/cesdk-engine/1.24.0/assets",
};

// Default image for the page (user can update later).
const defaultImage =
  "https://github.com/BolajiAyodeji/attraktives-headshot/blob/main/public/headshot.png?raw=true";

export default function BgAddPage() {
  const cesdk_container = useRef<HTMLDivElement>(null);

  const initializeCESDK = () => {
    CreativeEngine.init(config).then((engine) => {
      const container = cesdk_container.current!;
      container.innerHTML = "";
      container.append(engine.element);
      
      let scene = engine.scene.create();
      const page = engine.block.create("page");
      engine.block.setWidth(page, 500);
      engine.block.setHeight(page, 500);
      engine.block.appendChild(scene, page);
      
      // Create a graphic block, set the shape/size,
      // get the color fill block of the page,
      // add a color to the block,
      // and add the block to the scene's page.
      const block = engine.block.create("graphic");
      engine.block.setShape(block, engine.block.createShape("rect"));
      engine.block.setFill(block, engine.block.createFill("color"));
      engine.block.setWidth(block, 500);
      engine.block.setHeight(block, 500);
      const colorFill = engine.block.getFill(page);
	    // Red RGB color
      engine.block.setColor(colorFill, "fill/color/value", {
        r: 1.0,
        g: 0.0,
        b: 0.0,
        a: 1.0
      });
      engine.block.appendChild(page, block);

      // Create a block with an image fill
      // and add it to the scene's page.
      const imageFill = engine.block.createFill("image");
      engine.block.setString(
        imageFill,
        "fill/image/imageFileURI",
        defaultImage
      );
      engine.block.setFill(block, imageFill);
    });
  };
  
  useEffect(() => {
    initializeCESDK();
  }, []);

  return (
    <div
      ref={cesdk_container}
      style={{ width: "100vw", height: "100vh" }}
      >
    </div>
  );
}
```

In the code snippet above, we:

* Create a graphic block, set the shape/size, add a color to the block using the `fill/color/value` fill, and add the block to the page on the scene. Colors can be specified with either RGB, CMYK, or Spot color formats (I used RGB here).
    
* Create another block using the `fill/image/imageFileURI` fill and add it to a block.
    

At this point, you should start seeing the page rendering with a red color on the canvas like so:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726048693917/9c4b56e1-e530-4b31-b332-e1bbb81daa1c.png align="left")

### \[V\] Display Multiple Pages on the Scene

Now let’s attempt to display multiple pages in a grid-like format on the same. In the same `/components/headshotCanvas.tsx` file, now add more code like so:

```ts
"use client";
import { useEffect, useRef, useState } from "react";
import CreativeEngine from "@cesdk/engine";
import { grids } from "@/app/utils/grids";

const config = {
  license: process.env.NEXT_PUBLIC_CESDK_LICENSE,
  userId: "guides-user",
  baseURL: "https://cdn.img.ly/packages/imgly/cesdk-engine/1.24.0/assets",
};

const defaultImage =
  "https://github.com/BolajiAyodeji/attraktives-headshot/blob/main/public/headshot.png?raw=true";

export default function BgAddPage() {
  const cesdk_container = useRef<HTMLDivElement>(null);

  const initializeCESDK = () => {
    CreativeEngine.init(config).then((engine) => {
      const container = cesdk_container.current!;
      container.innerHTML = "";
      container.append(engine.element);

      let scene = engine.scene.create();

      // Display multiple pages in the scene (as grid)
      // using the same properties but different positions and colors.
      for (let i = 1; i <= 6; i++) {
        const page = engine.block.create("page");
        engine.block.setWidth(page, 500);
        engine.block.setHeight(page, 500);
        engine.block.setPositionX(page, grids[i].x);
        engine.block.setPositionY(page, grids[i].y);
        engine.block.appendChild(scene, page);

        const block = engine.block.create("graphic");
        engine.block.setShape(block, engine.block.createShape("rect"));
        engine.block.setFill(block, engine.block.createFill("color"));
        engine.block.setWidth(block, 500);
        engine.block.setHeight(block, 500);
        const colorFill = engine.block.getFill(page);
        engine.block.setColor(colorFill, "fill/color/value", grids[i].color);
        engine.block.appendChild(page, block);

        const imageFill = engine.block.createFill("image");
        engine.block.setString(
          imageFill,
          "fill/image/imageFileURI",
          defaultImage
        );
        engine.block.setFill(block, imageFill);
      }
    });
  };

  useEffect(() => {
    initializeCESDK();
  }, []);

  return (
    <div
      ref={cesdk_container}
      style={{ width: "100vw", height: "100vh" }}
      >
    </div>
  );
}
```

Also, add the following code in the `/utils/grids.ts` file:

```ts
interface gridLayout {
  [key: number]: {
    x: number;
    y: number;
    color: { r: number; g: number; b: number; a: number };
  };
}

// Red, Blue, Green, Yellow, Pink, and Orange colors (in that order).
export const grids: gridLayout = {
  1: { x: -800, y: -50, color: { r: 1.0, g: 0.0, b: 0.0, a: 1.0 } },
  2: { x: -250, y: -50, color: { r: 0.0, g: 0.0, b: 1.0, a: 1.0 } },
  3: { x: 300, y: -50, color: { r: 0.0, g: 1.0, b: 0.0, a: 1.0 } },
  4: { x: -800, y: 500, color: { r: 1.0, g: 1.0, b: 0.0, a: 1.0 } },
  5: { x: -250, y: 500, color: { r: 1.0, g: 0.0, b: 1.0, a: 1.0 } },
  6: { x: 300, y: 500, color: { r: 1.0, g: 0.5, b: 0.0, a: 1.0 } },
};
```

In the code snippets above, we:

* Use a for loop to create multiple pages using the same properties we used earlier.
    
* Use the `setPositionX` and `setPositionY` options to position each page on the scene (coordinate of an element in a document—x and y axis on a graph) so they all appear in a grid sequence. This was a good hack for the grid layout and ideally you might want to display multiple pages horizontally or vertically.
    
* Create a `grids` object to store the values for the positions and color and dynamically use them inside the loop (`grids[i].x`, `grids[i].y`, and `grids[i].color`) based on the object’s key matching the loop’s index (`i`).
    

At this point, your canvas should get polished with a beautiful grid as seen below. NB: the scene will be displayed a little below the default view point on your screen but remember this is a canvas and you can drag the entire scene in any direction you want and reposition.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726048800225/b75957e4-a614-4eda-8f37-267032654189.png align="left")

### \[VI\] Upload an Image Locally to the Scene

Now, let’s add some more logic to allow a user to upload their own image locally. We can easily do this without having to handle any images in the cloud by using the `<input type="file>` element which will store the accessed files in the [`FileList`](https://developer.mozilla.org/en-US/docs/Web/API/FileList) JavaScript object returned by the [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File) property in the input element. We can then convert the file into a [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) URL, save it in state, and display it in the canvas using the `src` attribute of an `<img>` HTML element.

In the same `/components/headshotCanvas.tsx` file, now add more code like so:

```ts
"use client";
import { useEffect, useRef, useState, ChangeEvent } from "react";
import CreativeEngine from "@cesdk/engine";
import { grids } from "@/app/utils/grids";

const config = {
  license: process.env.NEXT_PUBLIC_CESDK_LICENSE,
  userId: "guides-user",
  baseURL: "https://cdn.img.ly/packages/imgly/cesdk-engine/1.24.0/assets",
};

const defaultImage =
  "https://github.com/BolajiAyodeji/attraktives-headshot/blob/main/public/headshot.png?raw=true";

export default function BgAddPage() {
	// State to store the Blob URL of the uploaded image.
  const [imagePath, setImagePath] = useState<string>("");
  const cesdk_container = useRef<HTMLDivElement>(null);

  const initializeCESDK = (imagePath: string) => {
    CreativeEngine.init(config).then((engine) => {
      const container = cesdk_container.current!;
      container.innerHTML = "";
      container.append(engine.element);

      let scene = engine.scene.create();

      for (let i = 1; i <= 6; i++) {
        const page = engine.block.create("page");
        engine.block.setWidth(page, 500);
        engine.block.setHeight(page, 500);
        engine.block.setPositionX(page, grids[i].x);
        engine.block.setPositionY(page, grids[i].y);
        engine.block.appendChild(scene, page);

        const block = engine.block.create("graphic");
        engine.block.setShape(block, engine.block.createShape("rect"));
        engine.block.setFill(block, engine.block.createFill("color"));
        engine.block.setWidth(block, 500);
        engine.block.setHeight(block, 500);
        const colorFill = engine.block.getFill(page);
        engine.block.setColor(colorFill, "fill/color/value", grids[i].color);
        engine.block.appendChild(page, block);

        const imageFill = engine.block.createFill("image");
        engine.block.setString(
          imageFill,
          "fill/image/imageFileURI",
          imagePath || defaultImage
        );
        engine.block.setFill(block, imageFill);
      }
    });
  };

	// Function to process the image file upload on input change.
  const uploadImage = async (event: ChangeEvent<HTMLInputElement>) => {
    if (event.target.files) {
	    // Get the first file in the list
      const file = event.target.files[0];
      // Create a Blob URL from the file.
      const blobUrl = URL.createObjectURL(file);
      // Set the Blob URL to state.
      setImagePath(blobUrl);
    }
  };

	// Add imagePath to the useEffect dependency.
  useEffect(() => {
    initializeCESDK(imagePath);
  }, [imagePath]);

  return (
    <div className="flex flex-col items-center justify-center">
      <label htmlFor="upload-headshot" className="hidden">
        Upload your image
      </label>
      <input
        type="file"
        accept="image/png, image/jpeg, image/jpg"
        id="upload-headshot"
        name="upload-headshot"
        className="mt-6 text-white border-2 border-white rounded-full 
        file:mr-3 file:px-3 file:py-2 file:border-0 
        file:bg-white file:text-black hover:file:bg-blue-200"
        onChange={uploadImage}
        required
      />
      <div
        ref={cesdk_container}
        style={{ width: "100vw", height: "100vh" }}
        className=""
      ></div>
    </div>
  );
}
```

In the code snippet above, we:

* Use the [`URL.createObjectURL()`](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL_static) method to create a Blob string URL representing the image file. This string URL’s lifetime is tied to the current [`document`](https://developer.mozilla.org/en-US/docs/Web/API/Document) in the window.
    
* Use the `useState` hook to store the Blob URL of the uploaded image.
    
* Add `imagePath` to the `useEffect` dependency, so the `initializeCESDK()` function is called again whenever `imagePath` changes ensuring that the UI updates accordingly without reloading the page.
    
* Add the new `<input type="file">` HTML element with an `onChange` event.
    

Now you should be able to upload a new image in the canvas and get the same background colors applied (**NB**: ensure you’re uploading PNG images with a transparent background).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726048882485/6f02fc12-fc20-4957-aa3d-b76c5dabb5c8.png align="left")

### \[VII\] Download all Pages as PNG Image

Now let’s add the last feature to allow a user to download all the generated variations of their headshot. In the same `/components/headshotCanvas.tsx` file, add more code like so (this is the final code of this entire component):

```ts
"use client";
import { useEffect, useRef, useState, ChangeEvent } from "react";
import CreativeEngine, { MimeType, ExportOptions } from "@cesdk/engine";
import { grids } from "@/app/utils/grids";

const config = {
  license: process.env.NEXT_PUBLIC_CESDK_LICENSE,
  userId: "guides-user",
  baseURL: "https://cdn.img.ly/packages/imgly/cesdk-engine/1.24.0/assets",
};

const defaultImage =
  "https://github.com/BolajiAyodeji/attraktives-headshot/blob/main/public/headshot.png?raw=true";

export default function BgAddPage() {
  const [imagePath, setImagePath] = useState<string>("");
  const cesdk_container = useRef<HTMLDivElement>(null);

  const initializeCESDK = (imagePath: string) => {
    CreativeEngine.init(config).then((engine) => {
      const container = cesdk_container.current!;
      container.innerHTML = "";
      container.append(engine.element);

      let scene = engine.scene.create();

      for (let i = 1; i <= 6; i++) {
        const page = engine.block.create("page");
        engine.block.setWidth(page, 500);
        engine.block.setHeight(page, 500);
        engine.block.setPositionX(page, grids[i].x);
        engine.block.setPositionY(page, grids[i].y);
        engine.block.appendChild(scene, page);

        const colorFill = engine.block.getFill(page);

        const block = engine.block.create("graphic");
        engine.block.setShape(block, engine.block.createShape("rect"));
        engine.block.setFill(block, engine.block.createFill("color"));
        engine.block.setColor(colorFill, "fill/color/value", grids[i].color);
        engine.block.setWidth(block, 500);
        engine.block.setHeight(block, 500);
        engine.block.appendChild(page, block);

        const imageFill = engine.block.createFill("image");
        engine.block.setString(
          imageFill,
          "fill/image/imageFileURI",
          imagePath || defaultImage
        );

        engine.block.destroy(engine.block.getFill(block));
        engine.block.setFill(block, imageFill);
      }

      // Export all pages on the scene.
      const exportButton = document.getElementById("export_button")!;
      exportButton.removeAttribute("disabled");
      exportButton.onclick = async () => {
        // Specify the image format (PNG).
        const mimeType = "image/png" as MimeType;
        // Specify compression level (original default for PNG is 5).
        const options: ExportOptions = {
          pngCompressionLevel: 9,
        };

        const pages = engine.scene.getPages();
        // Loop through all the pages on the scene.
        pages.map(async (page) => {
          // Download multiple Blob files as PNG for each page.
          const blob = await engine.block.export(page, mimeType, options);
          const anchor = document.createElement("a");
          anchor.href = URL.createObjectURL(blob);
          anchor.download = `attraktives-hs-${page}.png`;
          anchor.click();
        });
      };
    });
  };

  const uploadImage = async (event: ChangeEvent<HTMLInputElement>) => {
    if (event.target.files) {
      const file = event.target.files[0];
      const blobUrl = URL.createObjectURL(file);
      setImagePath(blobUrl);
    }
  };

  useEffect(() => {
    initializeCESDK(imagePath);
  }, [imagePath]);

  return (
    <div className="flex flex-col items-center justify-center">
      <label htmlFor="upload-headshot" className="hidden">
        Upload your image
      </label>
      <input
        type="file"
        accept="image/png, image/jpeg, image/jpg"
        id="upload-headshot"
        name="upload-headshot"
        className="pt-6 text-white
        file:mr-4 file:py-2 file:px-4
        file:rounded-full file:border-0
	      file:bg-white file:text-black
	      hover:file:bg-blue-200"
        onChange={uploadImage}
        required
      />
      <button
        id="export_button"
        className="w-80 lg:w-52 px-6 py-4 mt-6 text-center bg-white text-black hover:bg-blue-200"
      >
        Download Pages &nbsp; ↯
      </button>
      <div
        ref={cesdk_container}
        style={{ width: "100vw", height: "100vh" }}
      ></div>
    </div>
  );
}
```

In the code snippet above, we:

* Specify the image format and compression level of the export.
    
* Loop through all the pages on the scene and download multiple Blob files as PNG for each page.
    
* Add a `<button>` element to the page and use the `id` of the element to add a `<a href="" download="">` element so clicking the button will automatically trigger the downloads. Since there are just six images, this probably is sufficient and there’s no need to add a zip file logic (if the pages on the scene increase, a zip file will be best!).
    

Here’s what the final page should look like now. You can now use other different images from your computer and download them swiftly :).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726048945799/c30f7297-bfe5-494f-98d0-6db5de4cf4e7.png align="left")

## Bonus: Building an Image Background Removal App

For users to effectively use the app we just built, they need to always upload a transparent image with its background removed. So why not build another app that allows a user to remove the background of an image first before proceeding to add background colors? Well, IMG․LY also built a [background-removal.js](https://github.com/imgly/background-removal-js) library that allows you to remove backgrounds from images right in the browser environment with no additional costs or privacy concerns! The library used the Neural Network ([ONNX model](https://onnx.ai/)) and WASM files which are hosted by default.

You can pass either an `ImageData`, `ArrayBuffer`, `Uint8Array`, `Blob`, `URL`, or `string` to the `imglyRemoveBackground()` function from the package and the result will be another Blob URL (PNG image format). You can learn more by reading the [documentation](https://github.com/imgly/background-removal-js/tree/main/packages/web). That said, I gave the library a quick spin and this is what the code looks like (in the `/bg-remove/page.tsx` file):

```ts
"use client";
import { useState, ChangeEvent } from "react";
import Image from "next/image";
import imglyRemoveBackground from "@imgly/background-removal";

const loadingGif = "/loading.gif";

export default function BgRemovePage() {
	// State for the initial Blob URL of the uploaded image.
  const [initialImagePath, setInitialImagePath] = useState<string>("");
  // State for the final Blob URL of the processed image.
  const [finalImagePath, setFinalImagePath] = useState<string>("");
  // State to track when the image is processing.
  const [loading, setLoading] = useState<boolean>(false);

  const uploadImage = async (event: ChangeEvent<HTMLInputElement>) => {
    setLoading(true);
    setFinalImagePath("");
    if (event.target.files) {
      const file = event.target.files[0];
      const initialBlobUrl = URL.createObjectURL(file);
      setInitialImagePath(initialBlobUrl);
      imglyRemoveBackground(initialBlobUrl)
        .then((blobUrl) => {
          const finalBlobUrl = URL.createObjectURL(blobUrl);
          setFinalImagePath(finalBlobUrl);
        })
        .catch((error) => {
          console.error("Something went wrong.", error);
        })
        .finally(() => {
          setLoading(false);
        });
    }
  };

  return (
    <div className="flex flex-col h-screen items-center justify-center">
      <label htmlFor="upload-image" className="hidden">
        Upload your image
      </label>
      <input
        type="file"
        accept="image/png, image/jpeg, image/jpg, image/webp"
        id="upload-image"
        name="upload-image"
        className="text-white border-2 border-white rounded-full 
        file:mr-3 file:px-3 file:py-2 file:border-0 
      file:bg-white file:text-black hover:file:bg-blue-200"
        onChange={uploadImage}
        disabled={loading}
      />

      {initialImagePath && (
        <div className="grid grid-cols-2 gap-8 m-12">
          <Image
            src={initialImagePath}
            alt="Preview Initial Image"
            width={400}
            height={400}
            className="border-2 border-white"
          />
          <Image
            src={!finalImagePath ? loadingGif : finalImagePath}
            alt="Preview Final Image"
            width={400}
            height={400}
            className={`${finalImagePath ? "border-2 border-white" : ""}`}
          />
        </div>
      )}

      {initialImagePath && !finalImagePath && (
        <p>
          Hang on :). Removing image background
          <span className="inline-block ml-2 animate-ping">...</span>
        </p>
      )}

      {finalImagePath && (
        <a
          className="w-80 lg:w-52 px-6 py-4 text-center bg-white text-black hover:bg-blue-200"
          href={finalImagePath}
          download="attraktives-hs"
        >
          Download Image
        </a>
      )}
    </div>
  );
}
```

As seen in the documentation, the [`SharedArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) object has some security requirements and hence two headers need to be set to cross-origin isolate the page where the library is being used. To add this, update your `next.config.mjs` config file like so:

```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  async headers() {
    return [
      {
        source: "/bg-remove",
        headers: [
          {
            key: "Cross-Origin-Opener-Policy",
            value: "same-origin",
          },
          {
            key: "Cross-Origin-Embedder-Policy",
            value: "require-corp",
          },
        ],
      },
    ];
  },
};

export default nextConfig;
```

This is what the result looks like. Works like magic!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726049030490/2a2a00bb-f6ea-4f31-8b82-205c173e9246.png align="left")

This app doesn’t require a license so you can use it as much as you want [here](https://attraktives-hs.vercel.app/bg-remove) (I deployed the finished code and will probably make more changes later to make the experience better). For first-time use, the `WASM` and `ONNX` model files are fetched in the browser and this might take some time depending on your bandwidth. But it would be faster for subsequent requests since the files are cached. Give it a spin and feel free to share it with your friends and enemies too :).

## Bonus: Building a Canva-Like Design Editor

So far, we’ve explored how to use the CE.SDK Engine (`@cesdk/engine`). But there’s also the CE.SDK (`@cesdk/cesdk-js`) that offers more customizable editing UI components (more like a full-suite Canva-like design editor experience). You get the chance to customize the editor as much as your need requires. I won’t go into much detail here since we’ve covered quite a lot already but you can read the [documentation](https://img.ly/docs/cesdk/) to learn more. To test this quickly, you can add the code below in the `/coomponents/editorCanvas.tsx`:

```ts
"use client";
import { useEffect, useRef } from "react";
import { UserButton } from "@clerk/nextjs";
import CreativeEditorSDK, { Configuration } from "@cesdk/cesdk-js";
import { useRouter } from "next/navigation";

export default function EditorPage() {
  const cesdk_container = useRef(null);
  const router = useRouter();

  const config: Configuration = {
    license: process.env.NEXT_PUBLIC_CESDK_LICENSE,
    userId: "guides-user",
    baseURL: "https://cdn.img.ly/packages/imgly/cesdk-js/1.24.0/assets",
    ui: {
      elements: {
        view: "default",
        navigation: {
          show: true,
          action: {
            close: true,
            back: true,
            load: true,
            save: true,
            export: {
              show: true,
              format: ["application/pdf", "image/png"],
            },
            download: true,
          },
        },
        panels: {
          settings: {
            show: true,
          },
        },
      },
    },
    callbacks: {
      onUpload: "local",
      onBack: () => {
        router.push("/start");
      },
      onClose: () => {
        router.push("/start");
      },
    },
  };

  useEffect(() => {
    const container = cesdk_container.current!;
    if (container) {
      CreativeEditorSDK.create(container, config).then(async (instance) => {
        instance.addDefaultAssetSources();
        instance.addDemoAssetSources({ sceneMode: "Design" });
        await instance.createDesignScene();
      });
    }
  });

  return (
    <>
      <div className="flex flex-col items-center p-2">
        <UserButton afterSignOutUrl={"/start"} />
      </div>
      <div
        ref={cesdk_container}
        style={{ width: "100vw", height: "100vh" }}
      ></div>
    </>
  );
}
```

The setup is similar to the previous we covered. All we need to do now is add the following code in the `/editor/page.tsx` file to render the component above in a page (`/editor` in this case):

```ts
import dynamic from "next/dynamic";

const CreativeEditorSDKWithNoSSR = dynamic(
  () => import("../components/editorCanvas"),
  {
    ssr: false,
  }
);

export default CreativeEditorSDKWithNoSSR;
```

With this, your canvas should looks like the amazing screenshot below!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726049084041/421ba50a-84b8-4647-b5b7-23fa93c00be8.png align="left")

## Authentication and Protected Pages with Clerk

If you observed, I imported a `@clerk/nextjs` package in the snippet above. That’s Clerk, a complete suite of embeddable UIs, flexible APIs, and admin dashboards to authenticate and manage users. By installing the SDK package and importing a few components, you can setup auth routes, authenticate users, and protect certain pages from unauthenticated access. The major configuration is done in the `/middleware.ts` file as seen in the code snippet below where I specify the `/editor` route to protect (will not be accessible unless the user signs in). You can learn more by reading [Clerk’s Nextjs documentation](https://clerk.com/docs/references/nextjs/overview) and exploring my setup in [the repository](https://github.com/BolajiAyodeji/attraktives-headshot/tree/main/app/auth).

```ts
import { clerkMiddleware, createRouteMatcher } from "@clerk/nextjs/server";

const isProtectedRoute = createRouteMatcher(["/editor"]);

export default clerkMiddleware((auth, req) => {
  if (isProtectedRoute(req)) auth().protect();
});

export const config = {
  matcher: ["/((?!.+\\.[\\w]+$|_next).*)", "/", "/(api|trpc)(.*)"],
};
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726049140632/f8a7ddee-2fc4-4249-a9b2-58a87156f7b7.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726049146886/f0f3bd6b-7c28-41e9-ad5a-beeb6f5151e9.png align="left")

## Conclusion

Phew (happy sigh 😅)! That was quite some learning and building! Trust me, there’s so much more you can do with the CE.SDK Engine and CE.SDK; we only attempted to scratch the surface in this tutorial. But I believe you’ve learned some new things here and this gives you a good foundation to get started with and then you can further your learning (I’ve attached some helpful resources in the next section that you might want to check out). Do let me know what you think and how helpful all of the information is to you! I’m keen to hear what you plan to build next with CE.SDK or any use case you have in mind (feel free to leave a comment below). You can explore the code on [GitHub](https://github.com/BolajiAyodeji/attraktives-headshot) too. Thanks for reading this far!

## Further Resources

* [CreativeEditor SDK documentation](https://img.ly/docs/cesdk).
    
* [CreativeEditor SDK collection of examples](https://img.ly/docs/cesdk) (for different platforms).
    
* [Collection of preconfigured starter-kits](https://img.ly/showcases/cesdk).
    
* [Clerk guides and resources](https://clerk.dev/docs).
    

---

> **Friendly disclaimer**: This is not a paid ad for IMGLY or so :). I built this app and wrote this tutorial months ago as part of an interview process and I’m happy to share my learnings with everyone as always. I hope you still find the content useful; there’s quite a lot you can learn here even beyond the product. Cheers!
## Top 15 Recommended Tools for React Developers

As a software developer, the tools you use daily actually surpass the original languages you write code in. Over the years, I have discovered and used some amazing tools that have improved my productivity and efficiency in developing applications with Reactjs. I thought to share some of them today.

*This is no such definite list; all tools listed here are all recommendations based on my experience with them. If you find or know a better tool or one you would recommend, kindly let me and other readers know by leaving a comment.*

## Introduction to Reactjs

React is a declarative, efficient, and flexible frontend JavaScript library for building user interfaces. It lets you compose a complex user interface from small and isolated pieces of code called “components.”

React was initially developed by [Jordan Walke](https://twitter.com/jordwalke), a software engineer at Facebook, who released an early prototype of React called "[FaxJS](https://github.com/jordwalke/FaxJs)." It was first deployed on Facebook's News Feed in 2011 and later on Instagram in 2012 and was open-sourced at [JSConf US](https://www.youtube.com/watch?v=GW0rj4sNH2w) on 29th May 2013. It is maintained by [Facebook](https://github.com/facebook/react/) and a [community of developers](https://github.com/reactjs).  
React has grown to be the developer's choice as it has topped several polls and is highly demanded by several companies today.

---

If you have been considering to get started with learning Reactjs, here are some snippets to show how React code looks like and maybe inspire you to get started as soon as possible.

React components implement a **render()** method that takes input data and returns what to display. 

This would display a heading saying, “Hello, world!”.

```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```
This is a component written like a [JavaScript function](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) and would display a heading but accepts a property (your name) before rendering.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
This is a component written with [JavaScript ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) and would display a heading but accepts a property (your name) before rendering.

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

This component can then be reused in several pages by passing the name property to the component like so:

```js
<Welcome name="Bolaji" />
{/* Would render a heading with output: Hello, Bolaji*/}

<Welcome name="Hashnode" />
{/* Would render a heading with output: Hello, Hashnode*/}
```
Here is a sample code sandbox that shows how this logic is used with a user interface. Play around with the code and be creative :).

%[https://codesandbox.io/s/magic-react-busbe?fontsize=14&hidenavigation=1&theme=dark]

Want to get started now? I'll recommend you start with the official [React Docs](https://reactjs.org/tutorial/tutorial.html) and [Getting Started with React - An Overview and Walkthrough Tutorial](https://www.taniarascia.com/getting-started-with-react/) by Tania Rascia. Prefer visuals? Check out [ReactforBeginners](https://reactforbeginners.com/) by Wes Bos (PAID) and [Learn React JS - Full Course for Beginners - Tutorial 2019](https://www.youtube.com/watch?v=DLX62G4lc44) by FreeCodeCamp (FREE).

---

## The 15 Amazing React Dev Tools

React is a famous JavaScript library with tons of frameworks and tools created around it daily. While the numerous lists of tools provide you with a wide range of options, choosing which tool to use can be daunting for a beginner or intermediate. Below is a list of recommended React Dev Tools you can consider.

> PS: All the screenshots used in this article are in Dark mode, my eyes hurt with too much white light, so I view everything in Dark mode (all thanks to [NightEye](https://nighteye.app/)).

### 1. [React Developers Tools](https://github.com/facebook/react-devtools)

This is the most popular tool as the Reactjs team itself created it.
React Developer Tools is a DevTools extension available on [Google Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) and [Mozilla Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/). It allows you to inspect a React tree, including the component hierarchy, props, state, and more. To get started, open the Devtools in your browser and switch to the "⚛️ Components" or "⚛️ Profiler" tab.

![dev-tools-demo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1578629746922/IRdsunMJ4.png)

The Components tab shows you the root React components that were rendered on the page, as well as the subcomponents. When you select one of the components in the tree, you can inspect and edit its current props and state in the panel on the right.

The Profiler tab uses the [experimental Profiler API](https://github.com/reactjs/rfcs/pull/51) to measure how often a React application renders and what the “cost” of rendering is to help identify slow parts of an application and how it can be optimized. Only **react-dom 16.5+** supports profiling in Dev mode. 

You can also install the standalone shell to support Safari and ReactNative like so:

```
npm install -g react-devtools@^4
```

### 2. [React Docs](https://reactjs.org/)

This is the official documentation of Reactjs and is the best way to get started with learning Reactjs. It contains Installation, Main Concepts, Advanced Guides, API Reference, Hooks, Testing, Concurrent Mode (Experimental) guides, and more.

%[https://reactjs.org/]

### 3. [Scrimba React Bootcamp](https://scrimba.com/g/glearnreact)

Scrimba is the easiest way to learn how to code with interactive screencasts. The Scrimba React Bootcamp provides a comprehensive introduction to React for beginners. This tutorial course contains 57 interactive screencasts and is the perfect starting point for aspiring React developers. You'll learn all the key concepts while building two apps and doing coding challenges along the way, all for FREE!

By the end of this course, you'll have a solid understanding of:

- JSX
- Props and state
- Conditional rendering
- Functional components
- Class components
- Styling components
- Lifecycle methods
- Fetching data from APIs
- Handling events
- Forms in React
- Controlled components
- Writing modern React
- Local dev setup
- React Hooks

%[https://scrimba.com/g/glearnreact]

### 4. [Create React App](https://create-react-app.dev/)

Create React App lets you focus on code, not build tools. It is an officially supported way to create single-page React applications. It offers a modern build setup with no configuration.

```
npx create-react-app my-project
cd my-project
npm start
```
This will create a directory called **my-project** inside the current folder and will generate the initial project structure and install the transitive dependencies:

```
my-project
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
```
- `public/index.html` is the page template;
- `src/index.js` is the JavaScript entry point.

Your application will contain all the essential tools and configurations needed:

- React, JSX, ES6, TypeScript, and Flow syntax support.
- Language extras beyond ES6 like the object spread operator.
- Autoprefixed CSS, so you don’t need -webkit- or other prefixes.
- A fast, interactive unit test runner with built-in support for coverage reporting.
- A live development server that warns about common mistakes.
- A build script to bundle JS, CSS, and images for production, with hashes and sourcemaps.
- An offline-first service worker and a web app manifest, meeting all the Progressive Web App criteria.
- Hassle-free updates for the above tools with a single dependency.

### 5. [React Extension Pack](https://marketplace.visualstudio.com/items?itemName=jawandarajbir.react-vscode-extension-pack)

This is a popular VS Code extensions pack for React development.
It contains the following extensions and is constantly updated:

- [Reactjs code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.ReactSnippets) - Adds code snippets for React development in ES6
- [ES Lint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) - Integrates ESLint into VS Code.
- [npm](https://marketplace.visualstudio.com/items?itemName=eg2.vscode-npm-script) - Run npm scripts from the command palette and validate the installed modules defined in package.json.
- [JavaScript (ES6) Snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets) - Adds code snippets for JavaScript development in ES6 syntax.
- [Search node_modules](https://marketplace.visualstudio.com/items?itemName=jasonnutter.search-node-modules) - Quickly search for node modules in your project.
- [NPM IntelliSense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense) - Adds IntelliSense for npm modules in your code.
- [Path IntelliSense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense) - Autocompletes filenames in your code.

![react-ext-pack.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1578631414275/ersEP8Ran.png)

### 6. [React Cheat Sheet](https://devhints.io/react)

This cheat sheet is a collection of several React concepts and examples. These guide targets React v15 to v16 from Components, States, Props, Nesting, Lifecycle, Hooks, JSX Patterns, DOM nodes, and more.

%[https://devhints.io/react]

### 7.  [React Axe](https://github.com/dequelabs/react-axe)

React Axe allows you to test your React application with the [axe-core](https://github.com/dequelabs/axe-core) accessibility testing library.

Axe is an accessibility testing engine for websites and other HTML-based user interfaces. It's fast, secure, lightweight, and was built to seamlessly integrate with any existing test environment so you can automate accessibility testing alongside your regular functional testing. ~ [Axe Docs](https://github.com/dequelabs/axe-core)

- Install the package

```
#npm
npm install --save-dev react-axe

#yarn
yarn install --save-dev react-axe
```
- Initialize the module

```
import React from 'react';
import ReactDOM from 'react-dom';

if (process.env.NODE_ENV !== 'production') {
  let axe = require('react-axe');
  axe(React, ReactDOM, 1000);
} else {
  ReactDOM.render(<App />, document.getElementById('root'));
}
```
- Add configuration rules

```
let config = {
  rules: [
    { id: 'heading-order', enabled: true },
    { id: 'label-title-only', enabled: true },
    { id: 'link-in-text-block', enabled: true },
    { id: 'region', enabled: true },
    { id: 'skip-link', enabled: true }
  ]
};

axe(React, ReactDOM, 1000, config);
```

- Check the available Axe core [configuration rules](https://github.com/dequelabs/axe-core/blob/master/doc/API.md#api-name-axeconfigure) and add based on your needs.

I wrote extensively about the Axe Library in my past article; you might want to check it out.

%[https://bolajiayodeji.com/accessibility-auditing-with-axe-for-automated-web-ui-testing-ck3tyrb4j01kt6qs180hpzaso]

### 8. [Storybook](https://storybook.js.org/)

While React allows you to build components in a declarative way, visualizing these components become dependant on the app itself and it's dependencies.

Storybook is a user interface development environment and playground for UI components. The tool enables developers to create components independently and showcase components interactively in an isolated development environment. ~ [Docs](https://storybook.js.org/docs/basics/introduction/)

Storybook runs outside of the main app so users can develop UI components in isolation without worrying about app-specific dependencies and requirements.

![storybook.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1578634223452/vd5qi6pYp.png)

- Install Storybook

```
npx -p @storybook/cli sb init
```
- Run Storybook

```
npm run storybook
```

An exciting part of Story is the Addons, which enable advanced functionality and unlock new workflows.

- [Knobs](https://github.com/storybookjs/storybook/tree/master/addons/knobs): Interact with component inputs dynamically in the Storybook UI
- [Actions](https://github.com/storybookjs/storybook/tree/master/addons/knobs): Get UI feedback when an action is performed on an interactive element.
- [Source](https://github.com/storybookjs/storybook/tree/master/addons/knobs): View a story’s source code to see how it works and paste into your app.
- [Docs](https://github.com/storybookjs/storybook/tree/master/addons/docs): Document component usage and properties in Markdown
- [Viewport](https://github.com/storybookjs/storybook/tree/master/addons/viewport): Build responsive components by adjusting Storybook’s viewport size and orientation
- [Storyshots](https://github.com/storybookjs/storybook/tree/master/addons/storyshots): Take a code snapshot of every story automatically with Jest
- [Backgrounds](https://github.com/storybookjs/storybook/tree/master/addons/backgrounds): Switch backgrounds to view components in different settings
- [Accessibility](https://github.com/storybookjs/storybook/tree/master/addons/a11y): Test component compliance with web accessibility standards
- [Console](https://github.com/storybookjs/storybook-addon-console): Show console output like logs, errors, and warnings in the Storybook
- [Links](https://github.com/storybookjs/storybook/tree/master/addons/links): Link stories together to build demos and prototypes with your UI components

And many more created by the [community](https://github.com/storybooks/storybook/tree/master/addons). Learn more about Storybook [here](https://storybook.js.org/docs/guides/guide-react/)

### 9. [React Styleguideist](https://react-styleguidist.js.org)

This tool also enables developers to create components independently and showcase components interactively in an isolated development but with a living style guide. You can also share components with your team, including designers and developers.

![react-style.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1578658094083/6Kwtv5nur.png)

- Install Styleguidist

```
npm install --save-dev react-styleguidist
```

- Start a style guide dev server.

```
npx styleguidist server
```
- Build a production HTML version.

```
npx styleguidist 
```
Learn more about React Styleguidist [here](https://react-styleguidist.js.org/docs/getting-started.html)

### 10. [React Bootstrap](https://react-bootstrap.github.io/)

Bootstrap is the most popular front-end framework. If you're coming from the native HTML background, you should have used this a lot. Well, Bootstrap was rebuilt for React, awesome, right?

React-Bootstrap is a complete re-implementation of the Bootstrap components using React. It has no dependency on either bootstrap.js or jQuery. ~ [Docs](https://react-bootstrap.github.io/getting-started/why-react-bootstrap/)

It also allows you to pass state, props, and more.

![react-bootstrap.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1578659058650/Bom8K3x8i.png)

- Install the package

```
npm install react-bootstrap bootstrap
```

- Import Bootstrap stylesheet in `src/index.js` or `App.js`

```
import 'bootstrap/dist/css/bootstrap.min.css';
```

- Import individual components

```
import { Button } from 'react-bootstrap/Button';
import { Alert } from 'react-bootstrap/Alert';
```
- Reuse the component

```
<Button variant="primary">Primary</Button>
```
Learn more about React Bootstrap [here](https://react-bootstrap.github.io/getting-started/introduction)

### 11. [Styled Components](https://www.styled-components.com)

Styled Components allow you to use ES6 and CSS to style your apps without stress. This improves the developer experience of styling React component systems.

Styled Components allow automatic critical CSS, code splitting, no class name bugs, easier deletion of CSS, simple dynamic styling, extending styles, nesting, painless maintenance, and more.

- Install styled-components

```
npm install --save styled-components
```

With styled-components, you're defining your styles and creating a normal React component, that has your styles attached to it because it uses [tagged template literals](https://wesbos.com/tagged-template-literals/) to style your components.

```
import styled, { css } from 'styled-components'

const Button = styled.button`
  background: transparent;
  border-radius: 10px;
  border: 2px solid blue;
  color: blue;
  margin: 0.5em 1em;
  padding: 0.25em 1em;

  ${props => props.primary && css`
    background: blue;
    color: white;
  `}
`;

const Container = styled.div`
  text-align: center;
`

render(
  <Container>
    <Button>Normal Button</Button>
    <Button primary>Primary Button</Button>
  </Container>
);
```

![styled-comp.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1578664477622/23e_NoTCR.png)

Learn more about Styled Components [here](https://www.styled-components.com/docs)

### 12. [CodeSandBox](https://codesandbox.io)

CodeSandbox is an online code editor and prototyping tool that makes creating and sharing web apps faster. ~ [Docs](https://codesandbox.io)

Codesandbox enables you to start new React projects quickly and prototype rapidly. With CodeSandbox, you can create web apps, experiment with code, test ideas, and share creations easily.

%[https://codesandbox.io]

### 13. [React Testing Library](https://testing-library.com/react)

The React Testing Library is a very light-weight solution for testing React components. It provides light utility functions on top of react-dom and react-dom/test-utils, in a way that encourages better testing practices. ~ [Docs](https://testing-library.com/docs/dom-testing-library/intro)

```
npm install --save-dev @testing-library/react
```

%[https://testing-library.com/]

### 14. [React Interview Questions and Answers](https://github.com/sudheerj/reactjs-interview-questions)

This contains a list of top 500 ReactJS Interview Questions & Answers.

%[https://github.com/sudheerj/reactjs-interview-questions#table-of-contents]

### 15. [Awesome React](https://github.com/enaqx/awesome-react)

This is, in fact, the most important tool in this article as it comprises of all the tools I've mentioned above and more. Awesome React is a collection of awesome things regarding the React ecosystem (Resources, Tools, Community, Tutorials, Demos, Videos, Conference Talks, ReactNative, Redux, GraphQL, Apollo, and more.)

%[https://github.com/enaqx/awesome-react]

## Conclusion

React has a community of millions of developers, and it continuously built by amazing developers across the globe.

The [Hashnode React Community](https://hashnode.com/n/reactjs) is an online forum for discussion about best practices and application architecture, as well as the future of React.

Feel free to drop by and ask questions when you need help :).

%[https://hashnode.com/n/reactjs]
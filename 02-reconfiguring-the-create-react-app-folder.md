# Reconfiguring the `create-react-app` source-code folder

After building a project template folder using `create-react-app`, you are left with a default project that needs to be cleared and reorganized before starting the next project. Let's look at the files we are left with and how to best re-organize the source files in preparation of our new application.

## The project `src` code

The sample project's source code is all stored inside of a root sub-folder named `/src`. Let's take a look at the important files, their purpose, and which files we will need to keep, delete, or modify to start building our own application.

### Before getting started

Before diving into the `/src` code, notice that `index.html` (the file that the browser actually opens to run this application) is located in the project subfolder `/public`. Open it up now and take a peek before diving into the `/src` code. 

Notice there is a single DOM element present in the `<body>` of the document: `<div id="root"></div>`. This is where your application will be rendered.

### Most important files

- **index.js**: This is the starting Javascript file that will kick things off. This files only real job is to manage your Service Worker and render the `App` component to the `#root` element in `index.html`.
- **App.js**: The application Component. Currently holds the source code for the React sample application. This Component will server as the application's "brain" in most applications (for example, interacting with our data source, storing our site's structural HTML, and holding the router for an SPA).
- **index.css** and **App.css**: These CSS files are imported from their respective JS files. `index.css` is meant to hold all general style rules, with `App.css` holding the rules specific to the HTML rendered in `App.js`. If you plan to have all of your CSS in one document, let it be `index.css` (in that case, delete `App.css` and the corresponding `import` line from `App.js`).
- **serviceWorker.js**: Used to handle browser behaviors for your application in certain states or circumstances, like when a user goes offline while using the application, etc. You can leave this file where it is for the time being (likely also forever) and forget all about it.

### Other files

The following files can be removed from the `/src` folder:
- **App.test.js**: Used for writing [Jest](https://jestjs.io/) test cases.
- **logo.svg**: The React logo used in the demo. 


## Step-by-step: Cleanup and prepare

### Before getting started

Because we will be moving files around into folders to better organize things, to make our pathing easier, create a file called `jsconfig.js` in the project's root folder (where `package.json` is located). Paste in the following code, save it, then exit:

```json
{
  "compilerOptions": {
    "baseUrl": "src",
    "paths": {
      "*": [ "*" ]
    }
  }
}
```

This file configures Javascript import statements to assume imported files will be found relative to the `/src` folder, rather than relative to the importing file itself.

### The steps

After removing the files mentioned above, let's do some restructuring and cleanup of the files in `/src` to get our project ready for a new custom application:

1. In `/src`, create a few subfolders:
    * `/components`
      * `/pages`
    * `/css`
    * `/img`
2. Let's move a few files around:
    * Move `App.js` into `/components`
    * Move `App.css` into `/css`
    * Move `index.css` into `/css`
3. If you typically use a *css reset* for your projects, add the reset file as `reset.css` to the `/css` folder
    * You can [view or download my personal `reset.css` file here](https://github.com/juneate/css-reset)
4. Cleanup and modify files
    * `index.js`:
    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom';
    import 'css/reset.css'; // if applicable
    import 'css/index.css';
    import App from 'components/App';
    import * as serviceWorker from 'serviceWorker';

    ReactDOM.render(<App />, document.getElementById('root'));

    serviceWorker.unregister();
    ```
    * `App.js`:
    ```javascript
    import React from 'react';
    import 'css/App.css';

    const App = () => {
        return <></>;
    }

    export default App;
    ```
    * Remove the contents (rules) from `index.css` and `App.css`

Confirm that your application still compiles without issue by running `npm start`. If it builds a blank page without error, you are ready to go!

### Alternative file structures

As you can imagine, there are plenty of ways to organize a `/src` folder, and each is entirely unique to the project at hand. 

[Dan Abramov suggests](https://twitter.com/dan_abramov/status/1027248875072114689) starting simple, feeling it out and refactoring as needed (which is pretty solid advice for programming in general).

The above works well for a project coming from an HTML prototype, where the CSS is likely already written into one big document, or if you are accustomed to splitting files by type. The `/pages` subfolder will hold all of the pages that we route to from the `App` (could also be named `/routes`).

Another strategy for organizing components might be to create a `/components` folder with one sub-folder for each component, which would include the component's `.js` file, any specific `.css` files for this component, and any other associated file (testing, etc). You might also move the `/pages` (or `/routes`) up to the `/src` file directly and reserve `/components` only for the inner parts of a page, not the page templates themselves. 

The possibilities are endless. But the trick is to maintain order and organization (and **re**organization) as soon as things feel too hard to manage easily.

# Setup a single-page application with React Router

## Step-by-step: Adding React Router

From the CLI in the project folder...

1. Install React Router into this project: `npm install react-router-dom`
2. Inside of `App.js`, add the following directly under the React import statement (likely on line 1): `import { BrowserRouter as Router, Route, Link } from 'react-router-dom';`;
3. Create a `Home` component as `Home.js` and save it to `components/pages`
   * Ensure `Home.js` exports the component: `export default Home;`
   * `return` a React fragment `<></>` to start off
4. Import `Home.js` into `App.js`: `import Home from 'components/pages/Home';`
5. Create a `<Router>`, where `<Link>` is the anchor to a new "page" and `<Route>` is the resulting rendered page component:
    ```JSX
    <Router>
        <Link to="/">Home</Link>
        <Route path="/" exact component={Home} />
    </Router>
    ```

You should see a single link displayed as "Home" which will link to the domains' root directory `http://localhost:3000/`. To be sure you understand what you're seeing, add some HTML (perhaps a heading) inside of the fragment returned in `Home.js`. 

Noticed the new HTML you write shows up directly under the "Home" link - both exist together. The anchor is the `<Link>` and the HTML from the `Home` component is the `<Route>`.

## Step-by-Stop: Template setup and routing to pages

1. Create two more sample page components in `About.js` and `Contact.js`, saved to the folder `components/pages`. An example of the file might look like this:
    ```javascript
    import React from 'react';

    const About = () => {
        return <>
            <h1>About</h1>
        </>;
    }

    export default About;
    ```
2. Modify `App.js` to import the two new pages for a total of three page imports:
    ```javascript
    import Home from 'components/pages/Home';
    import About from 'components/pages/About';
    import Contact from 'components/pages/Contact';
    ```
3. Expand the `<Router>` in `App.js` to look like this:
    ```javascript
    const App = () => {
        return <>
            <Router>
                <header>
                    <ul>
                    <li><Link to="/">Home</Link></li>
                    <li><Link to="/about">About</Link></li>
                    <li><Link to="/contact">Contact</Link></li>
                    </ul>
                </header>
                <main>
                    <Route path="/" exact component={Home} />
                    <Route path="/about" component={About} />
                    <Route path="/contact" component={Contact} />
                </main>
                <footer>Copyright &copy;</footer>
            </Router>
        </>;
    }
    export default App;
    ```

Each `<Link>` should now change the browser URL, which in turn will hot load a new "page", all within a single `index.html` file, hence: "single-page application".

The `<Link>` and `<Route>` elements must exist within the <Router>. The `<footer>` can be inside or outside of `<Router>` in this case. But consider that the footer often has links to various parts of the site. To be forward-thinking, the `<footer>` is added to the `<Router>` and ready to hold `<Link>` elements if necessary.

## Importing pages with one statement

Because we will end up with many pages, rather than linking them all to `App.js` one line at a time, import them all together by setting up an `index.js` in the `/pages` folder to list all the files, then importing that index and destructuring the variables.

1. Create a file called `index.js` in `/components/pages` with an individual export for each component, like this:
    ```javascript
    export {default as Home} from './Home';
    export {default as About} from './About';
    export {default as Contact} from './Contact';
    ```
2. Import the components using JS object-destructuring by importing the entire folder (which will read the `index.js` file for a listing of available components): `import { Home, About, Contact } from 'components/pages';`

This method works for any folder, not just `/pages`. In fact, the `/components` folder might be a good candidate for this adjustment once the project grows to have multiple components.

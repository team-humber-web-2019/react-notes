# Creating a React application using `npm` package `create-react-app`

Now that we: understand what problems React is meant to help us solve, know what a Component is, and have seen the basic syntax, let's build a production-ready project folder to confirm all of the necessary React dependencies are available on our development computer, and give us a starting project template to work from.

## Before getting started

Before running the following commands, ensure [the latest version of Node.js](https://nodejs.org/en/) is installed on your computer. From the CLI, you can check that Node is available (and the installed version) by executing the command `node --version` from any directory.

## The steps

1. In your CLI (Terminal), navigate to the folder that you project will be created within
2. Update npm `npm install npm@latest -g`
3. Install the React installer `npm install -g create-react-app`
4. Create a React project `npm init react-app project-folder-name-here`
   * replace `project-folder-name-here` of course
5. Open the project in VS Code using _either_ option:
   1. **Terminal**: Navigate to the folder and open the project in VS Code using the command line
       * `cd project-folder-name-here`
       * `code .`
   2. **VS Code**: Open the project from the application (file>open _or_ drag+drop)
       * Be sure to open a terminal instance to the project from within VS Code
6. From the command line, start the local server: `npm start`

Note: you can hit <kbd>ctrl</kbd><kbd>c</kbd> at any point from the CLI to stop a running script like `npm start`.

## What are we looking at?

Your default browser should have opened up to <http://localhost:3000> (or similar), which is pointing to a local server booted-up from the CLI, specifically to run this React application. If the browser does not open to that URL with a working application, check your command line for errors, or try opening up the browser manually with the above address.

If things were successful, you should be looking at a spinning React logo with some text beneath it. More importantly, this is a React test application built in your local environment, confirming that all React dependencies are installed correctly. What this also gives you is a working project folder configured to build your React application. 

A great start!

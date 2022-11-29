# Creating a react app without using "npx create-react-app"

* [URL](https://medium.com/@JedaiSaboteur/creating-a-react-app-from-scratch-f3c693b84658)

## Steps

1. npm init
2. git init
3. create structure
	.
	+-- public
	+-- src
	+-- test     // this was missed out by the article
4. add a .gitignore file for: node_modules, dist directories, and package-lock.json
5. create public/index.html file from [URL](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html)
6. Install and set up for *babel*
* this may need some future-proofing: npm install --save-dev @babel/core@7.1.0 @babel/cli@7.1.0 @babel/preset-env@7.1.0 @babel/preset-react@7.0.0
* I needed to do "npm audit fix"
* create a .babelrc in the root and populate it with:
	{
 	 "presets": ["@babel/env", "@babel/preset-react"]
	}
7. Install and configure *webpack*
* npm install --save-dev webpack@4.19.1 webpack-cli@3.1.1 webpack-dev-server@3.1.8 style-loader@0.23.0 css-loader@1.0.0 babel-loader@8.0.2
* npm audit fix
* npm audit fix --force (still get 5 high vulnerabilities)  **Needs work**
* create webpack.config.js and populate it with a generic template from the tutorial website:
[URL](https://medium.com/@JedaiSaboteur/creating-a-react-app-from-scratch-f3c693b84658)
8. Install React dependencies
* npm install --save-dev react@16.5.2 react-dom@16.5.2
* I started with : npm install --save-dev react react-dom ... that FAILED!
* then tried npm install --save-dev react@16.5.2 react-dom@16.5.2 ... that FAILED!
* ok, try: npm install --save-dev react@18.2.0 react-dom@18.2.0
9. update-npm-dependencies
* [Flavio Copes to the rescue](https://flaviocopes.com/update-npm-dependencies/)
* npm install -g npm-check-updates
* run it: ncu -u
* run npm install
10. Now run npm install --save-dev react@18.2.0 react-dom@18.2.0 ==> SUCCESS!
11. Tell *react* where to hook into the DOM (in our public/index.html)
* create the file src/index.js and populate it with:
	import React from "react";
	import ReactDOM from "react-dom";
	import App from "./App.js";
	ReactDOM.render(<App />, document.getElementById("root"));
12. Also, as *webpack* processes *css*, create src/App.css and populate it with something simple like:
	.App {
  	  margin: 1rem;
      font-family: Arial, Helvetica, sans-serif;
	}
13. Should have a working react app. Start it running with:
npm webpack-dev-server --mode development **OK**
* hmm it doesn't seem to be installed => npm webpack-dev-server
* that makes me think the ff are also not installed:
* style-loader, css-loader, babel-loader, so install them too:
* npm install style-loader css-loader babel-loader	**OK**
14. Troubleshoot how to run webpack-dev-server:
* when running it seems the API has changed from when the article was written, as 'hotOnly' and'publicPath' are options object that do not match the API schema. Then looking at the API here [URL]() I couldn't figure out how to translate these old API schema options objects.
15. Found this [URL](https://namespaceit.com/blog/webpack-options-has-an-unknown-property-hotonly-invalid-options-object-dev-server-has-been-initialized-using-an-options-object)
16. Now run	"npx webpack-dev-server --mode development"
17. Error, need a src/App.js file
18. Ok, still my App.js is not seeming to do anything, I noted that in the deprecated API there was a path for putting the "bundle.js", I had just commented out "publicPath" for that piece, but ... make webpack.config.js a .BAK file and
19. Do "npx webpack init" and follow the questions to create a useable webpack.config.js file
* hmm not sure about the answers to all the question, and in the midst of using "npx webpack init" it wants to re-write package.json, so I copied that to a .BAK file as well.
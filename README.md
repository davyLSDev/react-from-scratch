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
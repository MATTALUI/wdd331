# Node and NPM
### Overview
At the start of the semester, one of the things we were asked to install was [Node](https://nodejs.org/en/about/). Node is a runtime for the Javascript programming language that you use by running commands in the command line (CLI), which makes it a great tool for building frontend applications since Javascript is what runs in the browser! When you install Node, it will also install a handy tool called [NPM](https://www.npmjs.com/). NPM is Node's package manager (Though, don't you **DARE** think that's what it stands for, [it's got a different meaning every time you check the website](https://github.com/MATTALUI/wdd331/tree/main/docs/images/npm-meaning.png)). A Node package is a third-party (meaning someone else wrote it) javascript program that you can install and plug into your work so that you can use it.

[Parcel](https://www.npmjs.com/package/parcel) is a good example of a package since we've used it in this class. Install it using NPM and voila! You've got a package that bundles and serves your HTML, JS, and CSS as if it were on a real web server! [Bootstrap](https://www.npmjs.com/package/bootstrap) is another one, though less interesting since all it does is install the boostrap CSS files in the right place for you.

You should consider exploring NPM's website if you're interested in frontend/Node development since there's all kinds of cool stuff there (Like [the official Dominos package](https://www.npmjs.com/package/dominos) that allows you to write programs that order pizzas from dominos...)
### Making sure you've got Node and NPM
To make sure you've got these installed correctly, go to your command line and run
```bash
node -v
```
and
```
npm -v
```

If both of these give you a version number instead of an error message, then you're ready to rock! If they don't then you should [checkout the download and installation process for your machine](https://nodejs.org/en/download/).

### Installing packages
Installing packages is super easy. All you have to do is find the name of the package that you want you want to install, go to the command line and type in

```bash
npm install [package name here]
```

or use the shorthand version `i` instead of `install`

```
npm i [package name here]
```

#### Where do the packages "live"?
When you install packages with NPM, a directory called `node_modules` gets created and all of the source code for those packages ends up living in there. Though it might not affect you a lot in this class, you should know that there are (typically) two "levels" a node package can be installed to:

##### 1 ) Globally

This means that a package will be installed in a place on your computer that will allow you to use it from anywhere in from your command line. We probably won't use this very much in this class since, usually this is something you'll only want to do for development tools, and it requires you to pass in a special `-g` option when installing it. An example of one I use all the time is [Nodemon](https://www.npmjs.com/package/nodemon). If I were to install it globally I would want to run.
```bash
npm install -g nodemon
```


##### 2 ) Locally
This means that a package is installed into your computer in the place where you run the command. This is good for project-specific packages that you need to use.

So, for example, we're using parcel in this class in order to help with our `style-guide-template` project. You would directory where you're keeping that project using the `cd` command, and you would run
```
npm i parcel
```
This will create a `node_modules` directory inside of your `style-guide-template` project. If you open it up you'll see that **one of** the directories in there is called `parcel`. That's the source code that you installed for Parcel! Any time your code needs to use Parcel now it knows to check `node_modules` to find the code you're looking for in `node_modules/parcel`

There are also probably a bunch of other directories in your `node_modules`, that's because Parcel will probably have its own dependencies that it needs in order to work so those get installed as well.

#### JSON package files
When you installed an NPM package, you might have noticed that in addition to a `node_modules` directory getting created a file called `package-lock.json` also got created. What the heck is that? Well, let me introduce you to the other two key files in a node project!

###### package-lock.json
The `package-lock.json` is a [JSON-format](https://www.json.org/json-en.html) file that NPM generates for itsself in order to keep track of things like the version numbers of packages installed, where they came from, etc. This is important because `node_modules` are so hefty that when sharing your project with others (like with git and Github) it can take a long time to copy them all. So it's faster just to let NPM know what you downloaded so that someone else's NPM can can download the exact same package. Honestly, most of the time this file can be ignored. It's definitel more important to know `package-lock.json`'s more handsome older brother...

###### package.json
Now you're ready to cook with gasoline! The `package.json` file is where it all comes together. It is really the central "brain" of your project. If you're staring up a new project, you can generate a `package.json` file by running
```bash
npm init
```
It'll ask you some questions and then generate a file that looks somehting like this:
```json
{
  "name": "wdd331",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "directories": {
    "doc": "docs",
    "test": "test"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/MATTALUI/wdd331.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/MATTALUI/wdd331/issues"
  },
  "homepage": "https://github.com/MATTALUI/wdd331#readme"
}
```
Since this probably isn't that interesting yet, take a look at the `package.json` file that came with the `style-guide-template` project. [I have it committed to my repo here](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json). Let's disect this!

###### Dependencies

The first thing I want to point out are the dependencies. At the time of writing this readme, you can find that they start on lines [15](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L15) and [20](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L20). [devDependencies](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L15-L19) are NPM packages that should be installed whenever you're developing the code. Lines [16-18](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L16-L18) show us that we want to install `parcel-bundler`, `rimraff`, and `sass`. [dependencies](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L20-22) should always be installed when running the project. Line [21](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L21) shows that `js` is the only normal dependency that we have here. One of the benefit of having all of your dependencies inside of the `package.json` files is that when you're in a directory that has a `package.json` file, you can run
```bash
npm install
```
or
```bash
npm i
```
and instead of having to install of your packages separately, NPM will look in your dependencies list there and istall them all for you! Much more convenient! Imagine having a project with **hundreds** of dependencies!

###### Scripts
[Lines 6-12](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L6-12) allow us to tell Node and NPM about some helpful shortcuts we want to be able to run quickly. You can add pretty much anything you want here, but we'll focus on the [start script](https://github.com/MATTALUI/wdd331/blob/main/style-guide-template/package.json#L8). If you look at that, you'll see the command `parcel src/index.html -d build/`. That is actually the command that you have to run ion order to start the project! Paste that into your command line and you'll see it start up! However, it can be pretty inconvenient to remember that weird command, so instead you can run
```
npm run start
```
or
```
npm start
```
And Node will look in your `package.json` file, find the script called `start` and run that command. So you don't have to remember how complex it is!

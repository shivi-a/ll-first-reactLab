# Walkthrough

Welcome to the async version of reactLab #1!

To start, clone this repo (On an LL machine open Terminal; then enter the commands `cd development` and `git clone https://github.com/learninglab-dev/ll-first-reactLab.git`) and open the code in your favorite editor. (Again, on an LL machine, `cd ll-first-reactLab` and `atom .`)

### What You'll Make
Before we take a look at the code, let's first take a look at what we'll make. Over in Terminal, enter `npm i` to install dependencies and then when that finishes `npm start`. You should see a message that says "Starting the development server..." and React should automatically open `localhost:3000` in your browser. (Btw, if you've never started a React app in development mode, now you know how!)

If you check out the app, you'll see a grid of images. As of this writing, they feature four-legged friends, but hopefully by the time the semester starts, you'll see some familiar faces. Clicking on the images will toggle them to gifs and back again.

Why is this a cool first React project? Well, for one thing, who doesn't want a people landing page with headshots and gifs?? More seriously, as a tool React is most useful for pages that change frequently in response to user interactions or new data. React components are also modular and resusable, so you can write code once, but use your page element many times. We'll get into both of those benefits more as reactLab gets going, but as you can see, the image-gif grid checks both boxes: what the user sees changes as they interact with the page; and we have a component, the image-gif button, that we're reusing multiple times.

### How to Navigate
Okay, let's get into the code! If you jump over to Atom (or your other text editor), you'll see the app's structure. At the top level, there are two folders: `public` and `src`. Your `node_modules` and `package.json` are there too, but we're not going to edit those.

Start by opening up the `public` folder. The essential file in here is `index.html`. If you open it up, you'll see that it's pretty, well, uninteresting. The html file is essentially a stem. This is because React is going to generate our html for us. When you build a React app, you write javascript that describes the DOM, that is, what the page should look like, for every possible state of your app. React uses a tool called Webpack to package all your scripts together and send them to the browser in a bundle. When a user interacts with your app, React runs your code and renders the appropriate html. The client never needs fetch html from your server after the initial download.

Back to our file structure: Now open `src`. All the code we'll write needs to be in this folder. Otherwise, Webpack won't see it to package it into our app. This app looks a little funny because I've made two copies of it for you. In the folder `01_example` is the completed code; the code you're currently running. In the folder, `02_starter` is a template; this is where you'll write your code. 

### Index.js: The Entry Point
Every react app has an entry point... To get started, open up `index.js`. At the top you'll see some `import` statements. One is commented out. Uncomment it and then comment out the statement that says `import App from './01_example/App'.` This switches from running the example app to the starter pack. If you check back in your browser, you should now see a blank page. (If you've stopped your server in the meanwhile, head back over to Terminal and hit `npm start` again to get the blank page.)

So what's this index file doing? Because it's so short, let's walk through it line by line:

```
import React from 'react'
import ReactDOM from 'react-dom'
```
Here we're simply importing React itself. That first line needs to be at the top of every javascript file you write that's a react component, so you'll write it over and over. It's the core React library. ReactDOM, on the other hand, we import only once here in `index.js`. This library basically tells React to output html and not native elements or something else. We're creating an app to be viewed in a browser.

```
import App from './01_example/App'
```
Next, we're importing our own code. (By the way, `import` is pretty much the es6 version of `require`. I'll leave it to you to google the differences if you want.) In react, components are organized in a tree. There are parent components and children. Here, as in most react apps you'll build, `App` is the top of our tree. It's the top-level parent.

```
ReactDOM.render(<App />, document.getElementById('root'))
```
Finally, we call the `ReactDOM.render()` function. This function tells react to go to work. React will start from the component we feed it, in this case App, and render that component and all of its children into html. It will "insert" this generated html into the dom element we've identified, which is `root`. If you remember from our quick look at `index.html`, root is just a solo `<div>` inside `<body>`, so the html react generates will become the body of our page.  

### JSX... What?
One thing you'll notice when working with a react app is that it automatically updates what you see in the browser every time you save your code. So let's do it! Open the folder `02_starter` and then the file `App.js`.

As we said, `App` is our the top-level component. We'll get to what's going on in this file in a bit, but first, let's make a change so we can see a change in the browser. Update the `return` statement so it looks like this. You can put any text you like; "hello world!" is just tradition:

```
return (
  <Layout>
    <h2>hello world!</h2>
  </Layout>
)
```
If you check over in your browser, you should see your message. Okay, so that wasn't very exciting, but you did just write your first (assuming this is your first react tutorial) bit of JSX. That's cool! But, wait... it looked a whole lot like html. Exactly. JSX is an extension of javascript that allows you to make use of your existing html knowledge. The majority of the time, html is your friend in react. If you want to insert a new div, go ahead and pop in a `<div>` tag.

There are some differences, however. For example, all attributes you put inside an opening tag are camelCased, e.g. `onClick` in JSX rather than `onclick` in html. In general, I'd recommend that you try the html you know; if the code doesn't work as expected, that's a good moment to google jsx-html differences.

Just to be clear, JSX is NOT html. We could have used [just javascript](https://reactjs.org/docs/react-without-jsx.html) and instead written:
```
React.createElement('h2', null, 'hello world!')
```
This is, afterall, what our JSX gets compiled to before react generates the actual html for our app.

### First Component
Okay, we're finally ready to write our first component. Let's jump over to the file `Img.js`. As we said awhile back, every file that contains a react component begins by importing react, so add this first line to your file:
```
import React from 'react'
```
Now we need to create our component. But what's a component? It's just a function, a function that returns JSX (or a child component(s) which somewhere down the tree return JSX) rather than some other type of value. That is, a component is a function that returns an element of our DOM, or technically a description of it.

So we'll start by writing a function:
```
export default function Img() {

}
```
Two quick things to note here: (1) The function declaration is preceded by the `export` keyword. This is the es6 version of `module.exports`. (2) The function/component name is capitalized. This is important. React will only treat a function as a react component if the name is capitalized in the declaration.

Next we said that components are functions that return JSX. So, let's do that Add a return statement to `Img()` as follows:
```
export default function Img() {
  return (
    <div style={{maxHeight: '500px'}}>
        <img src='[YOUR IMAGE URL]' alt='my img' width='300px' />
    </div>
  )
}
```
Be sure to add in a real image url or you won't see anything. Save and hop over to your browser. But wait! Nothing's changed...

### Composition

Now, we'll start with a very important react principle, composition...
`
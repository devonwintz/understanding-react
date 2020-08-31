## Understanding Pure React
In order to understand how React runs in the browser, and in the long run be more efficient with the library, it is vital to first understand pure React, that is React without JSX.

#### Getting Started with the Page Setup
There are two libraries that required for React to run in the browser: *React* itself and *ReactDOM*. React is responsible for creating views. The react package holds the react source for components, state, props and all the code that is react. While ReactDom on the other hand, is the library that is used to actaully render the UI in the browser. ReactDom is the glue between React and the DOM. Often, you will only use it for one single thing: mounting your application to the index.html file with ReactDOM.render().

**Why the Splitting?**
React and ReactDOM were divided into two libraries with the arrival of *React Native* (A React Platform for Mobile Development).

The power of React stems from the way it allows you to organize the parts (components) of the UI. This power has spread into the development of mobile applications. ReactDom is only used for web applications.

The following code snippet shows the *minimum* requirements for setting up your page to begin coding, using React.

```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Pure React Samples</title>
</head>

<body>
<!-- Target container -->
<div id="react-container"></div>

<!-- React library & ReactDOM-->
<script src="https://unpkg.com/react@15.4.2/dist/react.js"></script>
<script src="https://unpkg.com/react-dom@15.4.2/dist/react-dom.js"></script>

<script>
// Pure React and JavaScript code
</script>

</body>
</html>
```
#### The Virtual-DOM
At this point, I will attempt to do something that I normally do not do, which is assuming you know what the DOM (Document Object Model) is, or would have read about it. In short, the DOM is a programming API for HTML and XML documents. It defines the logical structure of documents. To understand more about the DOM, you can read view [this page](https://www.w3.org/TR/WD-DOM/introduction.html).
So far, we have not mentioned anything about the whole concept of the virtual-DOM. In order to understand that, we need to understand how the DOM itself works.  We usually use JavaScript to interact with the DOM, because… Well, nobody knows why.Whenever we want to dynamicly change the content of the web page, we modify the DOM, which may look something like:
```
//Change the colour of text in a div with id, "main-content

document.getElementById("main-content").style.color="blue"
```
The code snippet above would require the entire DOM to reload, in order for the update to be rendered. Now imagine if we have over 1,000 `divs` that need to be modified. This would definitely affect the performance of your website. We need to modify the DOM tree incessantly and a lot. And this is a real performance and development pain. The two problems here are:
* It is hard to manage
* It is inefficient
Before we continue, please note that the Virtual DOM was not invented by React, but React uses it and provides it for free.

The Virtual DOM is an abstraction of the HTML DOM and since the DOM itself was already an abstraction, the virtual DOM is, in fact, an abstraction of an abstraction.
You can think of the virtual DOM as React’s local and simplified copy of the HTML DOM. The virtual DOM is made up of React elements, which conceptually seem similar toHTML elements, but are actually JavaScript objects. It is much faster to work directly with JavaScript objects than it is to work with the DOM API.

#### React Elements
The DOM is made up of a number of elements that are placed in a tree like structure. Using raw HTML, we simple create an element by using a tags such as:
```
<h1>My Portfolio</h1>
```
React elements on the other hand, are instructions for how the browser DOM should be created. To accomplish this, React uses `createElement`.

The above code snippet, would therefore look like:
```
var myHeader=React.createElement("h1", null, "My Portfolio")

// React.createElement(component, props, ...children)
```
The first argument defines the type of element. The second element defines the element properties/attributes. While the last argument represent's the children (*could be nodes*).
During rendering, React will convert the above code to the one you saw first or is accustom to seeing or writing:
```
<h1>My Portfolio</h1>
```
So, what if you wanted to add a property, such as an id to the element we created, how will that look?
```
var myHeader = React.createElement("h1",
    {id: "my-header"},
    "My Portfolio"
)
```

#### ReactDOM
Can you recall why we need ReactDOM? It is necessary for rendering React elements in the browser. We do this by using `ReactDOM.render`. 
```
//ReactDOM.render(element, target-node)
```
In order render our `h1` element created above to our target node with `id` 'react-container, we would need write:
```
ReactDOM.render(myHeader, document.getElementById('react-container'))
```

**What if you want to create a nested element? In other words, an element with children, using the React.createElement**

Continuing with our *Portfolio* example, we will create a **Skills** heading, then have an unordered list with the skills. In order to do this, we will need to create to use a series of createElement calls.

```
React.createElement("h1", null, "My Portfolio",
    React.createElement("h2",
        null,
        "My Skills",
            React.createElement("ul",
            null,
            React.createElement("li", null, "HTML"),
            React.createElement("li", null, "CSS"),
            React.createElement("li", null", JavaScript")    
            )
    )
)
```
**Note:** So far, the only attribute I would have mentioned is the `id`. But if you have been working with HTML, you would know that there is the `class` attribute as well. In React, we define this attribute as `className`, sinc class by itself is a reserved word in React.

#### Constructing Elements With Data
 One of the power of React, is the ability to separate data from UI elements. **What if we want to dynamically add to our list of skills, do we have to continuously make `createElement` calls?** The answer is no. Let us first represent our skillset in an array.
 ```
 var mySkills = ["HTML", "CSS", "JavaScript"]
 ```
 We can now use the `Array.map` function. Read more about this [here](https://www.w3schools.com/jsref/jsref_map.asp). 

```
React.createElement("h1",
    null,
    "My Portfolio",
        React.createElement("ul",
            null,
                mySkills.map((skill)=>{
                    React.createElement("li",
                        null,
                        skill
                        )
                })
            )
        )
)
```

#### createClass
```
const mySkills = React.createClass({
    render(){
        return React.createElement("ul",
            null,
            React.createElement("li", null, "HTML"),
            React.createElement("li", null, "CSS"),
            React.createElement("li", null, "JavaScript")
        )
    }
})

const skillSet = React.createElement(mySkills, null, null)

ReactDOM.render(
    skillSet,
    document.getElementById("react-container")
)
```
## Understanding React with JSX






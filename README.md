# INTRODUCING REACT TO-DOs:

In your text editor open folder ```home/to-do-list``` or search for to-do-list 

## Explanation of JavaScript, HTML, CSS & React


HTML can be described as a noun just like JavaScript can be described as a verb and CSS, the styling language can be described as an Adjective. 


##Meaning 
HTML describes what will be on the page.
JavaScript tells the page what to do.
CSS describes what the page should look like.


So today we’re going to learn how to write a To-Do-List in React.Js, which is a framework for writing JavaScript. Frameworks help us organise and standardise our code, so we can get more done.


This is how you would write a to do list in Vanilla (Vanilla refers to writing just JavaScript without using any frameworks). As you can see, we have JS in our HTML (in the onclick), and HTML in our JS (in our newListItem function), which is going to make it difficult to debug or add features.

``` put the vanila code here```

You can easily split this into different files to make it look a little cleaner but what you can’t do without a whole bunch of work is make it efficient and accurate to render on the screen, hence React. React will do a whole bunch of organisation using something called a virtual dom. The virtual dom let’s us write clean code which is still efficient

So does everyone have their ```To-Do-List folder```? Great! 
(in your text editor click open and search for to-do-list)


So inside your text editor(I told everyone to download Atom but you can use whichever text editor you’re comfortable with), please open up the ```src/App.js``` file which should already be there. (go to src, then click on ```App.js```)
.
You should inside the ```render()```  function (towards the bottom of ```App.JS```), see some stuff that looks like HTML (the code with ```<>``` ), because the create-react-app gives you an already built page let’s go ahead and delete some of the unnecessary code, and we should add a 
You should delete: 


```html
<div className="App">
<header className="App-header">
<img src={logo} className="App-logo" alt="logo" />
<p> Edit <code>src/App.js</code> and save to reload. </p>
<a className="App-link"
href="https://reactjs.org"
target="_blank"
rel="noopener noreferrer">
Learn React
</a>
</header>
</div> 
```



Please add


```html
<div>hello TLV</div>
```


Check progress in your browser by running. 
```npm run start```
Inside your terminal from your project root


You should see inside your browser by going to the address “localhost:3000” just like typing in a website the text Hello TLV!


Congratulations on your first React App!

Now that you’re all Junior React.JS developers we should learn about the state. 
```state = {};```


The state is a place to keep all the information in the app that changes. The reason is because different things change from different places, you don’t always want keep in mind what is changing what... but you do want to know know exactly all the important stuff in the App. 


So below the component declarations lets copy in a state with an empty list for your to-dos 
```js
state =  { 
toDos: [ ]
};
```


Ok now that we have a place to keep the to-dos let's think about how we’re going to fill it. 


<details>
<summary>
What do we need to see on the page so that we can add stuff to a list??
</summary>
<p>
 A list
 A Button 
 A Input field
</p>
</details>


Ok so let’s get started. Underneath the Hello TLV we want to add a button, a input box and a list so that we can add to-do’s to it.

Copy paste this: 
```js
render() { 
Return (
<div>
Hello TLV
<input/>
<button>submit</button>
<List/>
</div>
);
} 
```



Anyone with any experience in HTML should notice something wrong here. 


That’s because in react we use components to split apart our code and make it way more readable.


Great, now if we’ve done this properly the browser should be giving us an error


Let’s fix that.


Everyone create a new file inside the ```src``` of the project so ```src/List.js``` 
In your finder or where ever you are most comfortable creating files go to code/to-do-list 


Inside this file we’re going to write the list setup!


```js
Import React from 'react';
Const List = props => (
<ul>
{
props.toDos.map((item, index) => (
<li key={index}>
{item}
</li>
))
}
</ul>
);
Export default List;
```

This will allow us to render as many to-do items as we want because it maps over all the “toDos” in our state and makes a new list item for each one.


We do need to import this new “component” to our ```src/App.js```  by putting this line at the top of the ```src/App.js```  file. So go to ```App.js``` and at the top of the file.

```import List from './List';```


Anyone who has experience in Javascript should be wondering what “props” is and rightly so.
One reason is because we haven’t even passed it any “props” and the other is what does props mean?

Props simply means properties and we can pass it whichever properties we want when we call our new component, so in our src/App.js lets pass it the necessary props so that we can get it to print some “List Items” or ```<li>Items</li>``` on the page.

```js
render() { 
Return (
<div>
Hello TLV
<input/> 
<button>submit</button>
<List toDos={this.state.toDos} />
</div>
);
} 
```

Now in our state object at the top of the file underneath the class function  (WHERE IS STATE) lets add a few toDos’ so we can see it working… 


```js
toDos: ["your homework", "drink water", "light Chanukia"]
```



Great!


Let’s quickly add a done button so we can remove items from the list.


In the ```src/App.js``` lets add a new prop to our list component which, when called call a function so that we can remove an item from our state.toDos.


```js
render() { 
Return (
<div>
Hello TLV
<input/> 
<button>submit</button>
<List<List toDos={this.state.toDos} deleteItem={this.deleteItem}/>
</div>
);
} 
```

And inside our  ```src/List.js```  Lets add a button that will call this prop with the index of the item the user wants to delete, like this: 


```js
Import React from 'react'
Const List = props => (
<ul>
{
props.toDos.map((item, index) => (
<li key={index}>
{item}
<button onClick={()=>props.deleteItem(index)}>Delete</button>
</li>
))
}
</ul>
);
Export default List;

```

Now in our  ```src/App.js```  above the render function lets add the function we’re going to call when the user clicks that delete button.


```js
deleteItem = (index) =>
this.setState({
toDos: this.state.toDos.filter((_, 
i)=> (i !== index))
})
```

This function will go through the toDos in our state and filter each one to find the index (location in the list) and when it finds the to do with the same index as the one we pass to the function on the button it will filter it out of the list.  (in the real world, we’d likely have item.id to filter by… this “index” might break if we have sorting on the List.items)


Now let’s get that input field working.. To explain we have an input field and we need to take the value the user adds and save that somewhere. When the user clicks the submit button we can add our value to our list of toDos in the state and React can render it all out onto our page. 


So first let’s add this to our input


```js
render() { 
Return (
<div>
Hello TLV
<input value={this.state.nextToDo} onChange={this.setNextToDo}/> 
<button>submit</button>
<List<List toDos={this.state.toDos} deleteItem={this.deleteItem}/>
</div>
);
} 
```


And a field called nexToDo to our state, this will be the place we’re going to save the users input text until he/she is ready to submit it to the page. 


So let’s add a field called nextToDo on the state object at the top of our src/app.js so that we can save our users input. 


And because in the onChange we need to call a function so we can save it, let's add this function to the app
Anywhere underneath the stateAdd this function: 


```js
setNextToDo = (event) => {
 this.setState({ nextToDo: event.target.value})
}
```


Every time the user writes anything in the ```input``` box this function will take the value of the input and save it to our state.nexToDo


Now we want to write the functionality for our input box.
Inside the render, let's add a function call to the onClick attribute.


```html
onClick={this.addToDo}
```


Whenever the user clicks the button it’s going to a call a function called addToDo.

```js
addToDp = (event) => 
 this.setState({
  nextToDo: '',
  toDos: [... this.state.toDos, this.state.nextToDo]
});
```

This function can go on top of the render function that we have inside the app


This function will take the nextToDo that we added whenever the user types into the input, and append it to the end of the current toDos in the state.


The problem with vanilla was that state was all over the place and our HTML and JS got mixed together…


we solved that by changing to ReactJS and using the state, setState, and some JSX attributes. ... Great!




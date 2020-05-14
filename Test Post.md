The JavaScript community is in some-ways lucky to have a large amount of Libraries, Frameworks & Tools available to you. Many of which help in solving very specific problems, but this is a huge headache for some people.

####"*A day doesn't go by without a new JavaScript Framework emerging out of nowhere*" ~ Someone, Probably

As a new developer, It can be very overwhelming to decide which framework is it that you wanna learn before any other. But believe me, It used to be a whole lot worse.

**Today, there are only 3 major frameworks which aren't going anywhere:**
* **Angular** (Developed by Google)
* **React** (Developed by Facebook)
* **Vue** (Community Driven)

Of course, there are tons of other frameworks such as **Preact**, **Inferno**, **Ember** & more which are also loved by their marginally smaller communities.

...But not **Svelte**

"**Svelte is a radical new approach to building user interfaces. Whereas traditional frameworks like React and Vue do the bulk of their work in the browser, Svelte shifts that work into a compile step that happens when you build your app."** ~ [Official Svelte Website](https://svelte.dev)

Svelte doesn't consider itself to be a "Traditional" JavaScript framework, and for very good reason.

**Svelte is a Compiler**. 

It takes your code and turns it into vanilla JavaScript that runs in the browser without any additional dependencies. This makes Svelte fundamentally different from React, Vue, Angular & other Frameworks.

[Rich Harris](https://twitter.com/Rich_Harris) (The Creator of Svelte) believes that Svelte is how frameworks should be built from now on.

**Svelte applications are blazing fast, they load up quickly & have impressively small bundle sizes.**

..Phew, that was a lot of reading. Now let's jump to the list of reasons & read some beautiful Svelte code :)


### **1. Svelte is Easy to Learn.**
Consider the following example: 
```html
<script>
    let count = 0;

    const increment = () => count += 1;
    const decrement = () => count -= 1;
</script>

<div class="counter-component">
    <p>The count is {count}!</p>
    <button on:click={increment}>Increment +</button>
    <button on:click={decrement}>Decrement -</button>
</div>

<style>
    .counter-component {
        font-family: Arial;
        padding: 15px;
    }
</style>
```

In this example, we see a Basic Svelte component. **Vue** developers will feel some resemblance between a Svelte component & a Vue component.

Svelte components are comprised of:
* A **Script** Tag which deals with the functionality of the component.
* A **Style** Tag which holds the scoped styles for the component.
* Everything else is considered Markup for the component.

The **{ }** syntax is used inside the Template for outputting expressions, assigning event listeners / dynamic values to props. & I can guarantee that you already know what **on:event** does :)

The code is expressive & without much effort, one can understand what it does.

### **2. Lack of Boilerplate.**

This goes hand in hand with the first reason. As you can clearly notice from the example above, There is **absolutely no boilerplate** in our component.

Everything just magically works because of the things Svelte does under the hood.

Here is the same example in **React**:

```js
import React, { useState } from "react";

const Counter = () => {
    const [ count, setCount ] = useState(0);

    const increment = () => setCount(count + 1);
    const decrement = () => setCount(count - 1);

    return(
        <div style={{
            padding: "15px",
            fontFamily: "Arial"
        }} className="counter-component">
            <p>The count is {count}!</p>
            <button onClick={increment}>Increment +</button>
            <button onClick={decrement}>Decrement -</button>
        </div>
    ); 
}

export default Counter;
```
It might just be me.. But the the code above doesn't really look elegant & clean. This is of course due to the boilerplate that React introduces on top of your components. *and lack of a cleaner way to achieve scoped css makes it worse..*

Not having to deal with any boilerplate severely improves Developer Experience.

This is of course true for **Vue** & **Angular**. Although Vue's boilerplate is somewhat similar to Svelte's basic setup, It enforces a specific syntax for defining methods, props & state.. which brings me to my next point.

### **3. Svelte is Not Opinionated.**

Svelte doesn't enforce any special syntax on you on how to define methods, how to update your state, & more. 

Svelte only has a handful of Syntax rules & they are just vanilla JavaScript.

* You define your variables normally using the **'let'** keyword. Any variable used inside the template will be considered a state variable.

```html
<script>
    let name = 'John Doe';
</script>

<p>Hello {name}!</p>
```

* To differentiate between a normal variable & a prop (Data passed down from parent), We put the **'export'** keyword in front of the variable name.

```html
<script>
    // The "name" property can now be passed down from a parent component.
    export let name = 'John Doe'; // We can also optionally assign a default value.
</script>

<p>Hello {name}!</p>
```

* We define our methods normally as Arrow Functions **() => { }** or normal functions using the **'function'** keyword.

```html
<script>
    let count = 0;

    const reset = () => count = 0;
</script>

<p>The count is {count}</p>
<button on:click={reset}>Reset Counter</button>
```

* We can use the **'$:'** operator to specify that a value depends on another value, Also known as a Computed Property. This is valid javascript syntax by the way. This is the only "weird" part of Svelte's basic syntax as far as my opinion goes.

```html
<script>
    let count = 0;
    $: count_squared = count * count;
</script>

<p>The count is {count}</p>
<p>The count squared is {count_squared}</p>
```
### **4. Svelte has a Clean templating syntax.**

Svelte templates are very easy to read. Even without prior-experience, you can tell what's going on.

* You can include any JavaScript expressions in your code using **'{ }'**.
```html
<script>
    let name = 'John Doe';
</script>

<p>Hello {name}!</p>
```
* You can include comments in your code as you would in HTML.
```html
<script>
    let name = 'John Doe';
</script>

<!-- My Epic Comment -->
<p>Hello {name}!</p>
```
* You can use the **{#if expression}** directive to add conditional rendering.
```html
<script>
    let condition = 1;
    let name = 'John Doe';
</script>

{#if condition === 1}
    <p>Hello {name}!</p>
{:else if condition === 2}
    <p>Hi {name}!</p>
{:else}
    <p>Howdy {name}!</p>
{/if}
```
* Iterative rendering is done using the **{#each array as item, index}** directive.
```html
<script>
    let users = [
        {
            name: 'John Doe',
            age: 53,
        },
        {
            name: 'John Does',
            age: 55,
        },
        {
            name: 'John Does Not',
            age: 60,
        },
    ];
</script>

{#each users as user, i}
    <p>{user.name} is {user.age} years old.</p>
{/each}
```
* You can add the **'on:eventname'** attribute on any Tag / Component to listen to any events & assign event listeners. *ps, you can create custom events and other components can listen to them in Svelte.*
```html
<script>
    const clickHandler = (e) => alert('I was cliked!');
</script>

<button on:click={clickHandler}>Click to Alert</button>
```
* You can bind the properties of a Tag / Component using the **'bind:property'** attribute.
```html
<script>
    let text_value = '';
    const clickHandler = (e) => alert(text_value);
</script>

<input type="text" bind:value={text_value} />
<button on:click={clickHandler}>Click to Alert Value</button>
```
* You can use the **{@html string}** to output plain HTML wherever you desire.
* You can find all about the framework in the [Docs](https://svelte.dev/docs).

### **5. Svelte apps are Blazing fast & Extremely small.**

As we saw earlier, Svelte is not a framework. **It's a compiler**. Which means that after compiling your code, It doesn't have anything to do with it.

The code is standalone, & does not include any additional dependencies.

Svelte applications are **extremely small** compared to React, Angular & Vue.

In my personal experience of benchmarking the bundle size.. 
I experienced a reduction of around **8 Times** in an application of a Significant size & functionality.

Of course the numbers will differ between projects but Svelte applications are generally a speck of the total bundle size of the other frameworks.

![Svelte Benchmark](https://pbs.twimg.com/media/DssqmdjVsAE8Il4?format=jpg&name=large)

Screenshot by [Rich Harris @ Twitter](https://twitter.com/Rich_Harris/status/1065992585095929857/photo/1)

Operations / seconds is not a definite measure to consider Svelte better but It still matters a whole lot & significantly improves the user experience. But the more interesting thing in the benchmarks above is the **"Library Size"** listed below the scores.

Companies like [Stone.co](https://www.stone.co/), Many Russian & Indian companies, Smart TV Manufacturers, & others are using Svelte for this very reason.

They make low powered products that don't have the capacity to run frameworks like React, Angular or Vue. That's where Svelte shines due to it's impressive speed.

Low Powered Devices aren't the only place where Svelte shines. It greatly improves user experience with a very small size & due to it's speed, it makes sure that the Application stays responsive, snappy & agile across any hardware. 

American Companies like [GoDaddy](https://godaddy.com/) & [Sucuri](https://sucuri.net/) also have Svelte in their Technology Stack. This list is only gonna grow larger with time.

### **6. Svelte is "Truly Reactive"**

React uses **this.setState()** or an appropriate setter from **useState()** to update the state & other frameworks use similar syntax.

It's not **reactivity** if you have to deliberately specify to the framework that you're about to update the state.
As [Rich Harris](https://twitter.com/Rich_Harris) put it.. React is kind of terrible at being Reactive.

Svelte tackles this by removing any sort of "State Update" middleware, and just relies on **Assignments** to detect state changes.
This is **"True Reactivity"** since the update is triggered automatically whenever you assign a new value to a state variable.

### **7. Things to keep in mind before learning Svelte.**

Svelte is a framework which I'd encourage everyone to learn.

In my personal experience, It's a better choice than React, Vue or Angular for most projects.

You can even build "Military Grade Web Applications" *Large Scale Web Applications with Routing, Server-Side Rendering, Code-Splitting & More* with Svelte using **Sapper** which is the older brother of Svelte. Sort of how **Next.js** is to **React**.

**If you're learning to get a job, Svelte might not be the best choice ..for now**

As I said earlier, The market is currently dominated by **React**, **Vue**, & **Angular**.

These frameworks are here to stay for a little longer because:

* Tons of Companies & People are using them. A lot more than these smaller frameworks.
* The Job Markets are flooded with React, Vue & Angular jobs with other frameworks being minuscule portions.
* React & Angular are backed by Facebook & Google respectively, meanwhile most frameworks are community driven.
* And finally.. React, Vue, and Angular just might be good enough. While Svelte is undoubtedly better (in my opinion), Those frameworks are't "terrible" or "bad".

All of these factors combined, make it very difficult for a new framework to take their place, But I'm confident that Svelte has what it takes.

But only we, the developers ultimately decide what stays on top. So I recommend learning Svelte & making some apps with it the next chance you get :)

### **8. Resources for learning Svelte**

There are many great resources for learning Svelte. If you already have experience with another Front-end framework, You can learn Svelte in an afternoon. Yeah, It really is that easy.

* [Offical Svelte Tutorial](https://svelte.dev/tutorial/basics) - The Official Tutorial for Svelte which explains everything and includes a Live Code Editor.
* [The Svelte Documentation](https://svelte.dev/docs) - Everything about the framework.
* [Svelte Crash Course by Traversy Media @ YouTube](https://www.youtube.com/watch?v=uK2RnIzrQ0M) - Learn the fundamentals, & build a basic application in 30 Minutes.
* [Svelte Quickstart by Fireship @ YouTube](https://www.youtube.com/watch?v=043h4ugAj4c) - Concepts of Svelte explained very fast.
* And many more that you can find with a Quick Search.

```html
<script>
    let count = 0;

    const increment = () => count += 1;
    const decrement = () => count -= 1;
</script>

<div class="counter-component">
    <p>The count is {count}!</p>
    <button on:click={increment}>Increment +</button>
    <button on:click={decrement}>Decrement -</button>
</div>
```

Clean, Elegant, No Boilerplate, No weird terminology & everything still works flawlessly.

Svelte really is.. **Svelte**.

Thank you for reading!

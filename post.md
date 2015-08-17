## Background
Being effective in your working environment is very important to developers. Many web developers I've met transitioned from server-side development, but never got any training on their new set of tools.

Chrome DevTools (CDT) is one of the most useful tools for web developers. It allows us to create, manipulate, and debug websites in the browser. Before tools like CDT and Firebug, working in the browser's runtime environment was like getting dental work done at a Kenny G concert.

![Party on, Garth](http://i3.ytimg.com/vi/Zy6KWBEoDRU/mqdefault.jpg)

In the Dark Ages, we were forced to add debug HTML and JavaScript alerts if we wanted to see what was happening in the browser.

##Our Workspace

Although frameworks are all the rage these days, we will look at examples on a simple site built with pure HTML, JavaScript, and CSS.  This will help us focus on the features of CDT rather than worrying about how a particular framework generates markup or handles events and scope.

## Sample Site
<!-- You may want to fork Anonymous Function and point to the version
     that won't change over time (since you've mentioned you want to
     revamp your web site). -->
**Site:** Available on <a href="http://anonymous-function.com/airpair/dev-tools/" target="_blank">Anonymous-Function</a><br>
**Source:** Available on <a href="https://github.com/AnonymousFunction/anonymousfunction.github.com/tree/master/airpair/dev-tools" target="_blank">GitHub</a>

Let's look at what features our simple site has:
- Table of games
- Inputs and a button to add new games
- Bold games have a CSS class of "radical"
- Hover over a game to hightlight it

## Starting DevTools
To open DevTools, right-click anywhere in the browser's viewport and select **Inspect Element**. This will open DevTools and bring focus to the selected element in the window.

**Mac:** Cmd(⌘) + Option + I

**Windows:** F12 -or- Ctrl + Shift + I

## HTML Elements

***Keep in mind that any HTML/JavaScript/CSS changes made in CDT are lost if the page refreshes***

You can edit HTML on-the-fly using CDT.  Let's take a look at how we can change some HTML: 

<iframe width="420" height="315" src="https://www.youtube.com/embed/4ARMf5jd988" frameborder="0" allowfullscreen></iframe>

Using the magnifying glass, I select the element I want to change. Then I double-click on the value in the Elements pane to edit it.  Alternatively, I could drill down through the nodes to find the value.

Select **Edit as HTML** from the right-click-menu to open an inline text editor. This makes it easier to do any type of change or multiple changes.

Select **Add Attribute** from the right-click-menu to add a specific HTML attribute such as **class** or **style**

Tag names and attributes can also be changed, just double-click an attribute or its value to change it just like the element's text value.

You can use the delete key or select **Delete** from the right-click menu to remove entire nodes and their children. 

Also from the right-click menu you have the option to force an element state such as hover or active.  This makes it much easier to inspect the applied styles for those elements.


### Shortcuts
| Key               | Action |
|-------------------|-------------|
| Cmd(⌘) + Z | Undo last change |
| Cmd(⌘) + &uarr; (&darr;) &nbsp; | Move element up/down |
| H                 | Hide element   |
| Del               | Delete element |


##Styles

You can also view and change styles using CDT.  You can change the CSS of a single element, add new or modify existing rules, and even see what rules apply to specific elements.

<iframe width="420" height="315" src="https://www.youtube.com/embed/pfWqSaJRK0s" frameborder="0" allowfullscreen></iframe>

When an element is selected, you can click on **element.style** to apply inline styles.  CDT provides an auto-complete to help with both properties and values.  Use **Tab** to shortcut between properties and values and **Shift + Tab** to go backwards.  You can also toggle specific styles on/off by using the checkbox next to the property name.

Clicking the plus (+) icon lets you add rules dynamically to the inspector stylesheet.  Then you can edit the HTML to match the selectors.  In the example we created a new rule of *.cool* and added that class to one of the table rows.

When viewing an element, you'll see a list of all the rules/styles that apply and where they come from in the source.  This is useful when trying to answer questions such as "Why is this stupid thing bold?".  In the video, clicking `app.css` takes us to the working copy Chrome has loaded.  We can even make changes in Source view!  This is very useful when you are building in the browser and copying back to your code editor.

##Console
CDT provides access to the browser's JavaScript runtime through the Console.  You can use the Console to invoke and modify JavaScript or just treat it like a terminal. For example, you can:

<ul>
    <li>Log objects for debugging</li>
    <li>Run functions</li>
    <li>Add new functions</li>
    <li>Assign event handlers</li>
    <li>Do math!</li>
</ul>

Let's review the JavaScript for this page before looking at another video. View the annotated source on <a href="https://github.com/AnonymousFunction/anonymousfunction.github.com/blob/master/airpair/dev-tools/app.js" target="_blank">GitHub</a>.

````javascript
console.log("Hello World!");

function buttonClick(){
    var consoleText = document.getElementById("game-console").value;
    var titleText = document.getElementById("game-title").value;

    addNewGame(consoleText, titleText);
    document.getElementById("game-console").value = "";
    document.getElementById("game-title").value = "";
}

function addNewGame(consoleText, titleText) {
    var gameTable = document.getElementById("game-table");
    var el =  document.createElement("tr");
    el.innerHTML = "<td>" + consoleText + "</td><td>" + titleText + "</td>";
    gameTable.appendChild(el);

    console.log("Game Added!", consoleText, titleText);
}
````
<br>
<iframe width="420" height="315" src="https://www.youtube.com/embed/QDMowuDTunA" frameborder="0" allowfullscreen></iframe>

This first thing we see in the Console is the text "Hello World".  That comes from line 1 in the JavaScript and is a good way to make sure the browser is loading the script properly when you add a new file.

When I click the Add button in the UI, it will eventually run `addNewGame()` and we can see the "Game Added!" text along with the name of the console and game. We can get the same result by running `addNewGame()` directly in the Console.

You can also reassign function/variable definitions in the the Console.  In the video, I reassign it a function that does nothing but a log statement, and by running it again we can see it takes effect immediately.  Executing just the variable name will show you that it is a function reference.  If the variable name were an object instead of a function, it would log its value.

##Debugging
Debugging JavaScript can be very useful when the Console alone isn't good enough.  You can use the `debugger` keyword anywhere in your JavaScript and CDT will pause the execution as long as it's open. Video time.

<iframe width="420" height="315" src="https://www.youtube.com/embed/bnkLJCaQtQo" frameborder="0" allowfullscreen></iframe>

In the Sources tab you have access to all the scripts currently loaded by Chrome.  By opening `app.js` and clicking a line number, I can toggle a breakpoint. A list of all breakpoints (whether active or not) is visible in the bottom on the window.

Let's set a breakpoint at the beginning of `addNewGame()`.  As soon as the function runs, whether through the UI or from the Console, the browser will pause execution.  The Scope panel show you the current state of all variable in both window and global scope.  You can even use the Console to run commands against the current snapshop of the variables.

Using F10 (Step-Over) will take you step-by-step through the function and after each step you can see how the variables change in Scope.  You can expand any objects to drill-down into their properties.

Clicking the play button (F8) will continue execution until the next breakpoint.  If no other breakpoints are set it will playthough to the end of the function.

##Deeper Dive
We just barely scratched the surface of what Chrome DevTools has to offer but this will get any developer started. We'll take a look at advanced features such as monitoring network traffic and performance in Part 2. We'll also look at some ways to use CDT when working with frameworks like AngularJS.

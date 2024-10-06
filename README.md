# My Calculator App using React

This project was built for my Cousera's assignment - React Basics with Meta. Sharing some of my learnings, as well as the scope of this project.

---

## 2 types of Components in React. 

* Class Component
* Functional Component

## Class Component
Before React 16.8, class component were the standard way of defining components. They are still used in some legacy codebases and for certain complex use cases.

## Functional components
Fast forward, functional component was introduced and enhance further with the help of React hooks in React 16.8, Feb 2019. Today, it is widely used in most of the modern web application.

---

## React Hooks

#### Some of the hooks are:
* useState
* useRef
* useEffect
* useContext
* useReducer

## What is Hook?
Hooks are special function in React that allow you to handle and manage state inside a function componenet.

## What is State?
State are like variables that holds/stores a data or value within the componenet itself. These data or values are dynamic, they can mutable over 
the time. When the State changes, the component will auto update and re-render to reflect the changes.

## What is Prop?
Props are data recevied from the parent component who are the one managing and handling the state. These 
props are immuatable, read-only & cannot be modifiy directly. Meaning, we don't "hard-code" value directly inside them. 

The Child Componenet use this data (props) to perform business logics and renders the UI. Any modification 
to props are done using functions such as; callback functions or event handlers.

---

## In this Calculator App;

* The data are being passed from parent to child component using props(setResult, result, inputRef)
* useState and useRef hooks were used.
* Callback functions & Event handlers were used.


## Calculator Componenet (Parent)

### Syntax of useState:

```const [result, setResult] = useState(0);```

* result: The variable that holds the data.
* setResult: The method/function that mutates that data.
* useState: The hook that initialize the data at the beginning.

### Syntax of useRef:

```const inputRef = useRef(null);```<br>
```const resultRef = useRef(null);```


* inputRef: This will be used to reference the input field where the user types a number.
* resultRef: This will be used to reference the paragraph that displays the result.

>The useRef hook allow the app to focus on the input field when user type a number, or focus on the result field when 
a button is clicked. Both actions are execute without having to re-render the entire page, making it easier to reference the DOM elements directly.

---

## Addition Component (Child)

It recevied the data from the Calculator Component(Parent) and apply the business logic.

This component accepts 3 props (setResult, result, inputRef) from its parent.

* setResult: A function that updates the result state.
* result: The current result value (though it's not used within this component).
* inputRef: A reference to an input element, which allows the component to access the input's current value.




Function: This is an event handler named plus that gets called when the button is clicked.

Prevent Default Behavior: 
e.preventDefault() is called to prevent the default form submission behavior (Eg; button is pressed).

e: It refers to the event object that is passed to an event handler (like a click, form submission, or key press)
preventDefault(): A method available on the event object that prevents the default behavior associated with the event from occurring. Eg; rendering/refreshing the webpage


Updating Result (callback function)
setResult((result) => result + Number(inputRef.current.value)): This updates the result state. It takes the current value of result, converts the value from the inputRef to a number using Number(), and adds it to the current result.
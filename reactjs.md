* What is react?
   *  javascript library for building UI
        • Declarative 
        • component-Based
   * Any screen update in a React app happens in three steps:
      * Trigger (setValue)
      * Render (comparing state)
      * Commit (render latest state)
   * You can use Strict Mode to find mistakes in your components.
   * React does not touch the DOM if the rendering result is the same as last time
    
* Steps 
    1. Create div with id ="root"
    2. Adding cdn of react and react-dom
    3. Adding a script with scr to a js file.
    4. The js file has react code
           • const e = React.createElement;
           • class LikeButton extends React.Component {
                    constructor(props) {
                        super(props);
                        this.state = { liked: false };
                    }
                    
                    render() {
                        Return text 
                        if (this.state.liked) {
                            return 'You liked this.';
                        }
                        Return a new element of button
                        return e(
                            'button',
                            { onClick: () => this.setState({ liked: true }) },
                            'Like'
                        );
            }
           • 
    5. const root = ReactDOM.createRoot(document.getElementById('root'));
        This target the div which we created with id root
        as a spot of putting components using ReactDom.createRoot as root DOM node. 
    6. root.render(<h1>Hello, world!</h1>);
        this line of code render our create component inside root DOM node.
    7.
  
* JSX
   * syntax extension to JavaScript
   * JSX with in build rendering tendency
   * Embedding Expressions in JSX 
   *  React DOM escapes any values embedded in JSX before rendering them.
   * JSX Represents Objects
      Babel compiles JSX down to React.createElement() calls.
   * 
* Function Components
   function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
   }
* Class Components
   class Welcome extends React.Component {
      render() {
         return <h1>Hello, {this.props.name}</h1>;
      }
   }

* Rendering a Component 
   const element = <Welcome name="Sara" />;
   root.render(element);

* Composing Components
   bottom-up approach to render element components.
   <Welcome name="Sara" />      
   <Welcome name="Cahal" />      
   <Welcome name="Edite" />

   * Extracting Components : Don’t be afraid to split components into smaller components.

* Props are Read-Only 
   * pure function and impure function.

* Converting a Function to a Class 
   1. Create an ES6 class, with the same name, that extends React.Component.
      * class Clock extends React.Component { }
   2. Add a single empty method to it called render()
      class Clock extends React.Component { 
         render() {}
      }
   3. Move the body of the function into the render() method.
      Body parts code will be the same.
   4. Replace props with this.props in the render() body.
      props.date -> this.props.date

*  Lifecycle Methods to a Class 
   
   * mounting 
      set up a component's elements when it load for first time in DOM.
   * unmounting
      reset input value and clear its elements after component get remove from DOM

   * special methods on the component class
      1. componentDidMount() { 
         //mount function
         what we do on load in DOM.
      }
      2. componentWillUnmount() {  
         //Unmount Function
         what we just do after unmount component.

      }
   *

*  Using State Correctly 
   * Do Not Modify State Directly 

      // Wrong error in rendering
      this.state.comment = 'Hello'; 

      // Correct
      this.setState({comment: 'Hello'});

   * State Updates May Be Asynchronous
      // Wrong (this.props) and (this.state) should not calculated Correctly due to Asynchronous behavior of DOM.
         this.setState({
            counter: this.state.counter + this.props.increment,
         });
      // Correct always use function method to set setState value.
         this.setState((state, props) => ({
            counter: state.counter + props.increment
         }));
   * 

* The Data Flows Down

   state is called local or encapsulated because no any component do not know wether a component has stateful or stateless , and define by class or function method.

   state data can pass. it follow top-down” or “unidirectional” data flow.
      <FormattedDate date={this.state.date} />
      child do not know from where or which part of code that data come from parent (its state or its prop)
   
* Conditional Rendering   
   * Inline If with Logical && Operator 
      {condition && <h1></h1>}
      condition -> true : run the <h1>
      condition -> false : skip the statement

   * Inline If-Else with Conditional (ternary) Operator

      condition ? true : false

   * Preventing Component from Rendering
      if (!props.warn) {    
         return null; //it not render on condition 
      }

* Lists and Keys
   map()
      working with array
      {numbers.map((number) => 
         <ListItem key={number.toString()} value ={number} />      
      )}

   A “key” is a special string attribute you need to include when creating lists of elements

   It helps identify which items have changed, are added, or are removed
      ways to add key to list.
         1. key={number.toString()
         2. key={todo.id}
      NOTE: a key is to use a string that uniquely identifies
   

*  Forms 
   * form elements such as <input>, <textarea>, and <select> typically maintain their own state and update it based on user input. Unable to render using react.

   * To manage state of them using react, do
      <input type="text" value={this.state.value} onChange={this.handleChange}

      //onChange function we setState input
      // and we pass state value as a value to the form elements. 

   * Handling Multiple Inputs 

      handleInputChange(event) {
         const target = event.target;
         const value = target.type === 'checkbox' ? target.checked : target.value;
         const name = target.name;

         this.setState({
            // state the current value to the named input.
            [name]: value    
         });
      }
   *  react form use Formik library.
         it is validation, keeping track of the visited fields, and handling form submission
   * uncontrolled component

* Lifting State Up 

   The input state value come from parent state. and child get the parent state value as a props.

   that lead to make a component to store state values , and we just pass state value as props to children component.


* Composition vs Inheritance
   * Composition
      when you do not know how many data passed by parent.
      * How to handle it
         * Containment 
            parent {
               <child 
                  left= {<leftComponent />}
                  right = {<rightComponent />}
               />
            }
            child {
               <div> {props.left} </div>
               <div> {props.right} </div>
            }
            we can pass other component as a props
         * Specialization 
            When we want to pass different props value in special case.

            parent {
               child {
                  name="title"
                  work="home"
               }
               child {
                  name="hhh"
                  work="office"
               }
            }
            different props value at different instance.
   * Inheritance 
      At Facebook, we use React in thousands of components, and we haven’t found any use cases where we would recommend creating component inheritance hierarchies.

      Officials says Always use composition concepts

* Thinking in React 
   Steps to build React App.

   1. Understand Data come from API and UI design
      how to data look?
      how we are going to show the data?
   2. Based on your understanding Break The UI Into A Component Hierarchy
      * Draw boxes around every component (and subComponent) in the UI and give them all names.
      * For making components use single responsibility principle, that is, a component should ideally only do One Thing.
         AT the end , it should be decomposed into smaller subComponents.
         Always think About designing Reusable component.
   3. Now the JSON data nicely map with your required component
      <img scr="https://reactjs.org/static/9381f09e609723a8bb6e4ba1a7713b46/90cbd/thinking-in-react-components.png" />


      1. FilterableProductTable (orange): contains the entirety of the example
      2. SearchBar (blue): receives all user input
      3. ProductTable (green): displays and filters the data collection based on user input
      4. ProductCategoryRow (turquoise): displays a heading for each category (use composition concept to map and render all categories)
      5. ProductRow (red): displays a row for each product (use composition concept to map and render all subElements of passed categories).

   4. Identify The Minimal (but complete) Representation Of UI State 
      you first need to think of the minimal set of mutable state that your app needs. The key here is DRY: <b>Don’t Repeat Yourself</b>.
      <h4>Keep Components Pure</h4>

      For example, if you’re building a TODO list, keep an array of the TODO items around. When you needed just fetch the data from it. 
      Do not make separate state for count items else.
   5. Identify Where Your State Should Live 
      Next, we need to identify which component mutates, or owns, this state.

      Note: <b>React is all about one-way data flow down the component hierarchy.</b>

      Steps to figure out this: 
         For each piece of state in your application:
         1. Identify every component that renders something based on that state.
         2. Find a common owner component (a single component above all the components that need the state in the hierarchy).
            * Either the common owner or another component higher up in the hierarchy should own the state.
         3. If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common owner component.
         * In summery, always Think to manage state values in parent component and just pass required state values to the child.

   6. Add Inverse Data Flow
      Its is a concept, that is,When a child change the state value of the parent by using callback function passes by the parent in child props.

* AdvancedGuild
   * Accessibility 
      These topics make us to accessible test for our website.
      * WAI-ARIA 
         (Web Accessibility Initiative - Accessible Rich Internet Applications)
         It's help to Screen Readers and visible challenge user.
         
         All aria-* HTML attributes are in camelCased.

      * Semantic HTML 
         Using the various HTML elements to reinforce the meaning of information in our websites will often give us accessibility for free

         All table , list is wrap under div
         React Fragments 
            <Fragment></Fragment>
            <></> //when you not need props
      * Accessible Forms 
         * Labeling
         * Notifying the user of errors
         * Focus Control 
            Ensure that your web application can be fully operated with the keyboard only:
            * Keyboard focus and focus outline
      * Mechanisms to skip to desired content 
            Skiplinks or Skip Navigation Links are hidden navigation links that only become visible when keyboard users interact with the page
            * WebAIM - Skip Navigation Links
               use landmark elements and roles, such as <main> and <aside>, to demarcate page regions as assistive technology allow the user to quickly navigate to these sections
               * Accessible Landmarks 
         * Programmatically managing focus   
            To set (after lose) focus on keyboard on section we want to focus.

               To set focus in React, we can use Refs to DOM elements.

         * Mouse and pointer events 
            make sure only one focus is active either we access by keyboard or mouse.

         *  Other Points for Consideration 
            *  Setting the language 
               Indicate the human language of page texts as screen reader software uses this to select the correct voice settings:
            * Setting the document title 
               so that screen reader can understand
             * Color contrast 

      * Development and Testing Tools  
         * The keyboard
            Access your website only by keyboard.
         * Development assistance 
            * eslint-plugin-jsx-a11y 
               Its is giving feedback regarding accessibility issues in your JSX
            * Create React App has this plugin with a subset of rules activated. If you want to enable even more accessibility rules, you can create an .eslintrc file in the root of your project with this content:

            * Testing accessibility in the browser 
               * aXe, aXe-core and react-axe 
                  * The Accessibility Engine or aXe, is an accessibility inspector browser extension built on aXe-core.
                  * You can also use the @axe-core/react module to report these accessibility findings directly to the console while developing and debugging.

               * WebAIM WAVE 
                  The Web Accessibility Evaluation Tool is another accessibility browser extension
               * Accessibility inspectors and the Accessibility Tree 
               * Screen readers 
                  * NVDA in Firefox
                  * VoiceOver in Safari 
                  * ChromeVox in Google Chrome

* React Hooks
   * React Hooks only use in functional components.
   * React hooks execute in same order, never use it under certain condition,loop or any thing.
   * State is private to the component. Every components have their own instance of state  
   * Updating the same state variable multiple times before the next render (batching concept). To make this possible always use function version of setHook.

   
   * Updating Objects in State 
         * do not use value to update obj properties  value.
            it is not working
            Always use setObj method to update thing.

         * eg: 
            const [obj, setObj] = useState[{
               x: 22,
               y: 33
            }]
            obj.x = 55; //not working
            setObj({x: 55});

   *  Updating Arrays in State 
      In React state Array are treat as immutable.
      so instead of This   use this non-mutated method. 
      It can the array but it do not re-render the contents.
      All non-mutable method return a new array instead.

      * Adding      (push , upshift)      concat,[...arr] (use concat with spread operator);
      * removing     (pop,shift,splice)      (filter, slice);
            eg: 
            * filter
               setArtists(
                artists.filter(a =>
                  a.id !== artist.id
                )
              );
            * 
      * Transforming an Array
         Transverse across the array
         Splice , arr[i] = ..     : -> (map)
         * eg :
            array.map(()=> {

            });
      *  Replacing items in an array 
         Modifying items value
         always use map.

      *  Inserting into an array
         Inserting at a particular position
         Eg: 
            combining all the parts in new array
            const nextArtists = [
               // slice Items before the insertion point:
               ...artists.slice(0, insertAt),
               // New item:
               { id: nextId++, name: name },
               //slice Items after the insertion point:
               ...artists.slice(insertAt)

               //combining all the parts in new array
            ];
            //passing that updated array in setArray
            setArtists(nextArtists);

      *  Reversing and Sorting
         Eg: 
            //Copying an array
            const nextList = [...list];
            // Applied reverse in new array
            nextList.reverse();
            // Pass it to setArray
            setList(nextList);

      *  Updating objects inside arrays
         * Eg: 
            setMyList(myList.map(artwork => {
               if (artwork.id === artworkId) {
                  // Create a *new* object with changes
                  return { ...artwork, seen: nextSeen };
               } else {
                  // No changes
                  return artwork;
               }
            });
      *  Write concise update logic with Immer 
         * It is useful then you are so want to change so deeply nested (like 2 level deep).Then,
            * you use useImmer()
               * npm i immer use-immer
               * It is convenient but mutating syntax and take care of producing the copies for you.
               * It make immutable syntax to mutable object/array.
               * const [obj, setObj] = useimmer({
                  n: 1,
                  name: {
                     a: {
                        b..
                     }
                  }
               });
               // You can use mutable syntax
               setObj((item) => {
                  item.name.a.b = 44;
               })
               thats its.

            

   
   1. useState()
      * const [count, setCount] = useState(4);
      //It return an arr ,we just destructured it [value, setValueFunction];
      //useState(DefaultValue); 

      * When we set current value by using previous Value , Then use function structure of it. 
         * setCount((prevCount) => {
             prevCount + 1;
         })

      * Unlink class state, it is define in constructor , it run once, 
         but in useState, it run every time we re-render that function.
         * To Avoid this Use function version of it which run once of the very first time only.
            const [count, setCount] = useState(() => {
               console.log("count state define");
               return 4
            })
      * In useState , when we define a object inside useState,
         const [state, setState] = useState({
            count: 4,
            theme: blue,
         });
         Then, If we set
            setState (prevState => {
               return {count: prevState.count - 1};
            });

            then it over write all object structure.
            //state.theme :-> undefine error
            
            Always use spread operator to provide all previous value like:
               setState (prevState => {
                  return {...prevState , count: prevState.count - 1};
               });
               //object merging not happened , This is because we can make as much different state using its own useState hooks. and avoid state collisions.
   
   2. useEffect()
         *  When we use to change 
         *  similar mounted in class concept, it do sideEffect render on certain tasks.
         * Eg: 
            we have post API, User API, comments API.
            we want to render a particular API component when that button click

            const resourceType = post

            useEffect(()=>{
               console.log(resourceType);
            })
         * problem 1. useEffect run every time we render that component.
            To make it run on specific input. then give to it.
            * useEffect(()=>{
               console.log(resourceType);
            }, [resourceType]);
            Its runs only When resourceType value change. 

         * We can use useState to store particular  fetched value from API.
            const [items ,setItems]= useState([]);
            useEffect(()=> {
               fetch(`...../${resourceType}`)
                  .then(response => response.json())
                  .then(json => setItems(json));
            }, [resourceType]);
            //Every time resourceItem Change , the items value is auto updated.
         
         *  Advanced
            Now we want to change value of variables using external factors like event listener

            * const [windowWidth, setWindowWidth] = useState(window.innerWidth());
            * error not update automatically.
            * In Class component
               * in didMount method , we add event listener 
               * in WillMount method , we remove event listener.
            * By Use useEffect() hook
                  const
               *  useEffect (() => {

                     window.addEventListener('resize', handleResize);

                     // Clean function (un-mutate method)
                     // It is run every time when it un-mutated (re-render)
                     return () => {
                        return {
                           window.removeEventListener('resize', handleResize);
                        }
                     }

                  },[]) //[] pass because it is make run on mount once.


   * useContext()
      * Two Part
         * Provider component 
            * it provide state value to their children and their children and their children ...soon
            * export const ThemeContext = React.   createContext();

            * const [value, setValue] = useState(true);
            * const handleClick = (value) => {
               return 
                  setValue(preValue => !preValue);
            }

            *  <ThemeContext.Provider value={}>

                  All Component That use That Values
                  <button onCLick>
               </ThemeContext.Provider value={}>
         * consumer component
            * It consumes the state value that provided by context.

            *  In class 
               * import {ThemeContext} form './App';
               * <ThemeContext.Consumer>
                  * {value => {
                     * return 
                        //All contexts inside this return
                        <div style={{backgroundColor: value}}>
                  }}
               </ThemeContext.Consumer>

            *  In Functional Component 
               * import {ThemeContext} form './App';
               
               * export default function FunctionalComponent () {
                  * const Value = useContext(ThemeContext);
                  // Now You can use any Where in funcCom();

                  return 
                  <div style={{backgroundColor: value}> </div>

               }
         
      * Simplified version
         * make a file themeContext.js

         *  const Theme = React.createContext();
         *  const ThemeUpdateContext = React.createContext()

         *  export function ThemeProvider({children}) => {
            //That function going to do all context provider stuff
            * const [value, setValue] = useState(true);
            * const handleClick = (value) => {
               return 
                  setValue(preValue => !preValue);
            }

            return (
               <ThemeContext.Provider value={value}>
                  //That provides value to all Children

                  <ThemeUpdateContext.provider value= {handleClick}>
                  //That provide handleClick to all children
                     {children}
                  </ThemeUpdateContext.provider>
               </ThemeContext.Provider>
            )

         }

         * Inside app.js
            * import {ThemeProvider} from "./themeContext.js"
            *  export default function app () {
               return (
                  <ThemeProvider>
                     <FunctionalComponent />>
                  </ThemeProvider>
               )
            }

         *  Now We can access value and method any where inside their children.

            * To make access to children
               *  we make function to access then inside themeContext.js file

               * export function useThemeValue() {
                  return useContext(ThemeContext);
               }

               * export function useThemeUpdateValue() {
                  return useContext(ThemeUpdateContext);
               }
            
            *  Now inside functionComponent
               * import { useThemeValue, useThemeUpdateValue } from './themeContext.js'

               functionComponent () {
                  const themeValue = useThemeValue();
                  const toggleTheme = useThemeUpdateValue();

                  return {
                     <>
                        <button onClick={toggleTheme} >         
                           Toggle button
                        </button>
                        <div  style={{background-Color: {themeValue}}}> </div>
                     </>
                  }
               }





   

      



   * useRef()
      * most miss Use and most flexible

      * make a variable to count the number of re-render 
         * we are going to use 
            const [renderCount, setRenderCount] = useState(0);

            useEffect(()=> {
               setRenderCount((prevRender) => prevRender + 1);
            })
         //error in stuck in infinite loop, useEffect change state value every time and useState() re-render on chnage.

      * Solution
         useRef()
         * It is not cause re-render But it persistence among every count. we can change as many we want but the value is not change on render.

         * const renderCount = useRef(1)
         // It has single value
         // it return a single value object.
         // {current = 1}

            useEffect(()=> {
               renderCount.current = renderCount.current + 1;
            });

         *  Most Use case
            * To give auto focus on input

               *  const inputRef = useRef();

               * const focus = () => {
                  inputRef.current // it is return ref input   tag. It is like query select

                  inputRef.current.focus() // now it set focus    on input box
               }

               * <input ref={inputRef}>
                  <button onClick={focus}>

            * It is also use to store previous value of state.
               * const [name,setName] = useState();
               * const prevNameValue = useRef();
               * useEffect(()=> {
                     prevNameValue.current = name;
               }, [name])

   *  useMemo()
      * it is use for memorization 

      * Usage Case
         * When a slow function run every time with the same input 
            * const [number, setNumber] = useState(2)
            * const doubleTheNumber = slowFunction(number);
            //it calculate Every time for 2(same value)
            // why not you just memories that result , stop calculating everything 

            * Use useMemo hook in this case.

               * const doubleTheNumber = useMemo(() => {
                  return slowFunction(number)
               }, [number]);
               //Now it is only going to run on when number value get change.


         * reference inEquality 
            it say every time we render, if we define any array or object. It is always going to represent totally different object/array.

            Eg: 
               const obj = { name: "test", age: {AgeTest}}

               useEffect(()=> {
                  console.log(obj);
               }, [obj]);
               //its re-render again every time because obj is totally different from previous one

            * useMemo() hook is use here to refer the same object after every render.

            * const obj = useMemo(()=> {
               return { name: "test" age: {AgeTest}}
            }, [AgeTest]) ;
            //it is going to re-render only if when you change AgeTest Value.


   *  useCallback()
      *  It is almost similar to useMemo() Hook. But useMemo() return value to variable as in useCallback() it return function.
      *  Usage case
         *  It is similar usage case like useMemo(),But It deals with function declaration.
         const getItem = (number) => {
               return [number + 1, number + 2, number + 3]
         }
         //it is going to decelerated and run every time.

         * const getItem = useCallback((number) => {
               return [number + 1, number + 2, number + 3]
         }, [number]);
         // It is decelerated and run only when number value change.
         
   * useReducer()
      * it is also manage state.
      * It gives you more contrite way to manage state. you have your own custom set state method thats make re-render your new state.

      *  const [state, dispatch] = useReducer( ManageStateFunction,{initialValue});
         * // state has current state value.
         * //  ManageStateFunction is a custom function that going to manage state value. it has various method to dispatch 
         * using 
            dispatch({type: "ActionType"});
            //ActionType is going to applied on state.
         
      * In whole it look like this
         const [state, dispatch] = useReducer( ManageStateFunction,{count: 0});
         
      * Basic ManageStateFunction() syntax
         const ACTION = {
            INCREMENT: 'increment',
            DECREMENT: 'decrement'
         } // conditional string function name.

         function ManageStateFunction(state, action) {
            switch(action.type){
               case 'ACTION.INCREMENT'
                  return { count: state.count + action.payload.passingValueToFunction}
            }
            switch(action.type){
               case 'ACTION.DECREMENT'
                  return { count: state.count - action.payload.passingValueToFunction}
            }
            Default: 
               return state
         }
      *  Change state value using dispatch
         * const [state, dispatch] = useReducer( ManageStateFunction,{count: 0});

         function onClickIncrement() {
            return dispatch({ type: 'ACTION.INCREMENT', payload: {passingValueToFunction: 1}})
         }

      *  It is to manage a complex state .
         let Make a todo application

         1. export default function app() {
            const [todoList, dispatch] = useReducer(reducer, []);
            // [] : initial todoList State
            // reducer is ManageStateFunction

            return (
               <>
                  <form onSubmit={handleSubmit}>
                     <input type="text" onChange={(e) => {
                        setName(e.target.value)
                     }} />
                     {todoList.map((todo)=> {
                        return <Todo key={todo.id} todo={todo} dispatch= {dispatch} />
                        //We pass useReducer dispatch function to do all state function
                     })}
               </form>
            )
         }

         2. Making all component of reducer
            2. 1. export ACTIONS = {
               ADD_TODO: "add_todo",
               TOGGLE_TODO: "toggle_todo",
               DELETE_TODO: "delete_todo"
            } 
            //All actions type names used in reducer
            //We export it because we need it in different component to access action type name. (like todo component)

            2. 2. function reducer(todoList, action) {
               switch (action.type) {
                  case ACTIONS.ADD_TODO:
                     return [...todoList, newTodoItem(action.payload.name)]
                  case ACTIONS.TOGGLE_TODO:
                     return (todoList.map((todo)=> {
                        if(todo.id === action.payload.id) {
                           return {...todo, complete: !todo.complete}
                           // that return a new object with all same items and with a change in complete: !todo.complete item.
                        } 
                        
                        return todo
                  
                     }))
                  
                  case ACTIONS.DELETE_TODO:
                     return (todoList.filter((todo) => todo.id !== action.payload.id));

                     //the filter return a new Array of todoList with items which are not certified the filter condition.
               }
            }
            2. 3. Model function for new Item
               function newTodoItem(name) {
                  return { id: Date.now(), name: name, complete: false}
               }
            // completed all require component in reducer section
            
         3. Setting up Todo component
            export default function Todo ({todo, dispatch}) {
               return (
                  <div>
                     <span style={{color: todo.complete ? '#AAA' : '#000'}}>
                     </span>
                     <button onClick={()=> dispatch({type: ACTIONS.TOGGLE_TODO, payload: {id: todo.id}});
                     }>
                        Toggle
                     </button>
                     <button onClick={()=> dispatch({type: ACTIONS.DELETE_TODO, payload: {id: todo.id}});
                     }>
                        Delete
                     </button>
                     //we just change method type , to change action on list
                     // neither we make separate function of it and pass it to todo separately.
                  </div>
                     
                  
               )
            }
            // complete todo app that all we need to do



   * REACT 18 HOOK
      * useTransition
      *  it is need when you app slow down and not responsive. it is used to speed up the app

      * Usages 
         *  if you have a input and it combine with a function which is going to filter out data from  / enter data in a large set of data ( a lot of computation) then it do not show/re-render the updated list until it do all the local state change operation.
            * useTransition hook used to prioritize the statements.


      * Not Usage
         *  use useTransition when you really need.
            if you have something that slow down application/ you have some component that slow down your application.
            it make re-render when low priority work done

      * Syntax 

         const [isPending, startTransition] = useTransition();
         * function handleChange (e) {
            setInput(e.target.value);

            startTransition(() => {
               //it is low priority code section

               const list = []

               for (let i = 0; i < LIST_SIZE; i++) {
                  list.push(e.target.value);
               }

               setList(list)
            });  
               
         }

         * ... return (
            {isPending ? "loading..." : List.map((item, index) => {
               return <div key={index}>{item}</div>
            })}
            //isPending use to give startTransition state
               return 
               if startTransition isDoing : return true
               if startTransition completed: return false
               // it can used to add loading effect on doing 
         )


      * useDeferredValue()
      * It similar concept like deBounce and thralling.
      *  It is update some value after a quite of time (make the value change less priority)

      *  function slowFunction({name}) {
         const largerNo = 1000000;

         const slow = useMemo(() => {
            const l = []
         for (int i = 0; i< largerNo ; i ++) {
            l[i] = name;
         }
         setList[l]
         // it is going show latency in input value;
         }, [name])

         
         To make it wait some time after name Value before run this function

            const deferredInput = useDeferredValue(input);
            const slow = useMemo(() => {
               const l = []
            for (int i = 0; i< largerNo ; i ++) {
               l[i] = name;
            }
            setList[l]
            // it is going show latency in input value;
            }, [deferredInput]);
      }
   
   *  Optional hooks
      *  useLayoutEffect()
         *  similar to useEffect()
         *  use Effect async function do not disturb the DOM. 
         *   it is synchronous function, it is run along with DOM.   when react paint the DOM (calculate position of component ) along that it run 
         *   it is useful when you need to move something on screen.
         *  useEffect: it is run after DOM render all component then it run. on the other hand it run alone with DOM to set the position for layout then the component run and set on that position.
         * it is less performance then useEffect.
         


      *  useDebugValue()
         *  it is use to make custom hook easier
         *  It use to name the hooks to make debug easier
         *  it is only work on custom hooks.
         *  * by default it run every time 
            * to make it run 
               * it only run  in develop 
               *  only run when you open developer tools
            *  useDebugValue(value, v => {
               getValueSlow(v)
            });
      
      *  useImperativeHandle()
         *  it is use to change the default behavior of  ref for component.
         * if you set ref for a component 
            * react.forwardRef(customInputComponent);
            *  and then pass ref value to function.
            and then set ref value to the require section.
         *  useImperativeHandle() total customize ref.
            *  useImperativeHandle(ref, ()=> {
               return { alertHi: ()=> alert("hi")}
            }, [])

            *  Usages
            *  <customInputComponent ref={inputRef}
            *  <button onClick={()=> inputRef.current.alertHi()}> Focus </button>
            // It call the function when you ref to this

            * it is going to use when you have buttons out the main component. when you try to manage multiple component using same ref
            *  Eg: 
               custom function (..., ref) {
                  const closeButton = useRef();
                  const confirmButton = useRef()
                  const denyButton = useRef()

                  useImperativeHandle(ref, () => {
                     focusCloseBtn: () => closeButton.focus(),
                     focusConfrimBtn: () => confirmButton.focus(),
                     focusDenyBtn: () => denyButton.focus(),
                  })

                  return (
                     <>
                        <closeComponent name="close button" ref={closeButton}>
                        <confirmComponent name="confirm button" ref={confirmButton}>
                        <denyComponent name="deyn button" ref={denyButton}>
                     </denyComponent>
                  )
               }
               export default React.forward(custom function);

               * main function 
                  const modelRef = useRef();


                  <button onClick=(()=> model.current.focusCloseBtn)>

                  <button onClick=(()=> model.current.focusConfrimBtn)>

                  <button onClick=(()=> model.current.focusDenyBtn)>

                  <customFunction 
                     ref={modelRef}
                  />

      * useId() 
         *  it give id to the component.
         *  it is always generate same id order every time.
         *  it give id as like id = ":r1:"
            *  that id is impossible to access by querySelector.
            * that enforcing us to use ref to reference any component element.
         *  modified useId use
         const id = useId()
            <element id=(`{id}-email)>
            <element id=(`{id}-name)>
            ...so on 
            it use same id to for all with some specific name change.





   * Custom Hooks
      * we combine hooks to make custom hooks
      * syntax
         1. customHooks.js
         2. function useRequired(initialValue) {
            const [value, setValue] = use preDefinedHooks(initialValue) ;

            return [value, setValue];
         }
         it is like a function with a set of hooks to manage a specifics tasks.

         *   useToggle()
            *  export default function useToggle(defaultValue) {
               const [value, setValue] = useState(default);

               function toggleValue(value) {
                  setValue(currentValue => {
                     typeof value === "boolean" ? value : !currentValue
                  })
               }

               return [value, toggleValue];
            }

            *  use in different components
               const [value, toggleValue] = useToggle(false);

               <button onClick={toggleValue}> Toggle Value</button>
               <button onClick={() => {
                  toggleValue(true)
               }}> make the value true </button>

               <button onClick={() => {
                  toggleValue(false)
               }}> make the value false </button>

            *  Timeout Hook
               export   default function useTimeout(callback, delay) {
                  const callbackRef = useRef(callback); //it saves callback function that is passed
                  
                  const timeoutRef = useRef();

                  useEffect (()=> {
                     callbackRef.current = callback
                  }, [callback]);

                  const set = useCallback(() => {
                     //we set a timeout funtion to return call back after a delay.
                     timeoutRef.current = setTimeout(() => {
                        return ( callbackRef.current() , delay);
                       
                     })
                  }, [delay]);

                  const clear = useCallback(() => {
                     // we forced running timeout function to stop.
                     timeoutRef.current && clearTimeout(timeoutRef.current);
                  }, []);

                  useEffect(() => {
                     //we reset set value and clear the running set timeout , if we call this  function over a pre-running function.
                     set()
                     return clear
                  }, [delay, set, clear]);

                  const reset = useCallback(() => {
                     clear()
                     set()
                  }, [clear, set])

                  return { reset, clear}

               } 

               * Usages
                  *  const {  clear, reset} = useTimeout(
                     () => setCount(0),
                     1000
                  ) 
               *   we can implement Debounce use this hook   
                  *  useDebounce(() => alert(count), 1000, [count]);

                  *  export default function useDebounce(callback, delay, dependencies) {
                     const {reset, clear} = useTimeout(callback, delay);

                     // 2. after that it measures the change on all dependencies or reset value
                     useEffect(reset, [...dependencies, reset]);

                     // 1. it clear the useTimeout for the same time
                     useEffect(clear, []);
                  }
   
   * optional 


* Code Splitting
   * download code when we need them
   * methods to implement it
      * using Dynamic import
         * import ("../sum.js").then(module=> {
                 alert(module.sum(2, 2));
              });
         * lazy (react tool)
            1. import {lazy} from "react"
            2. const Home = lazy(() => import ("./
                  components/Home"));
            * Error not it working on the very first time
               * Suspense components
                  <Suspense fallback={that run until 
                      loading done} >
                        <Outlet /> // lazy loaded components 
                  </Suspense>
            * lazy do need a default import
                  * unable to load named function
                  *  {default: fucn}
                  * but in module {default: fuc, namedfuc}

                  * fixing
                     * .... => import ("./components/About").then(module => {
                           return { default: module.About }
                           // We rename default export 
                         }
            * Not want to show fallback ,
               we need old data there, until new data Is loaded
                  * By using react hook (useTransition)
                        * it allows to enable not urgent update 
                           * const [isPending, startTransition] = useTransition ()
                           * startTransition (() => {
                               Condition State change fuc
                            });
                              * it doesn't change UI utill loading 
                             done ,so lazy(fallback) not show
                           * To show transition state
                              *  {isPending ?? "Loading.."}
                                   on tab click 
                                • 
                             •  
                          • 
                     * to simplifying lazy load import statement 
                        * Components lazyload
                           * export default const fucntion lazylaod(path, namedExport) => {

                           
                             * promise = import (path)
                             * if ( namedExport == null ) {
                                 return promise 
                              } else {
                                 return promise.then(module=> ({ default : module[namedExport] 
                              }))
                            }
                           }
                         


      










* Coding mistake or improving your mistake
   *  useState hook
        • Asked the question again, it really need 
           hook
           • on form submission
             • it need value once on submit
             • useRef instead
                • const emailRef = useRef()
                • input ref={emailRef}
                • onSubmit := 
                     email: emailRef.current.value
                •     
           • when you use previous value to change 
              new value,then you function version of 
              setuseState hook
              • setCount(count + amount) // wrong 
                • error when you have more then 1 
                   statement update. 
                   when State value change after next 
                   render
                    
              • setCount( currentCount => {
                   return currentCount + amount 
                 })
              • Count value is not change until next 
                 render is not completed.
                 So when you access count next of 
                 • setcount we do not get updates 
                 • so use useEffect to get updates count
                    • useEffect (() => {
                        console.log(count);
                       }, [count]);
                     • 
                 • 
              • 
           • 
        • 
    • useEffect
        • problem 1 : takecare about data change and 
          fetching data statement , it may cause 
          useless rendering 
             • useEffect(()=> {
                  fetch("#").then(d => { 
                     setData(d);
              
                   })
                }, []);
             • useEffect (() => { }, [data])
                 It render data several time utill data fully    
                 loaded . So use get data after fetch 
                 instead
           • Problem 2: On the time of redender 
                                 equality 
                
               • UseSet(dark mode);
               • cosnt person = { name, age}       
               • useEffect(() => {
                   
                  }, [person]);
               • when we change dark mode state only , 
                  although it run useEffect peroson;
                     • It is because simpler objects in 
                        javascript is not equal.
                        {} === {} // False
                        After every render ,we create new 
                        object of person same value, but 
                        technical it not same.
               • To use useMeno : it keep previous object
                  value arround until value of object / 
                  change.
                 • Const peroson = useMemo(() => {
                       return {age, name};
                    }, [age, name]);
                    When you using array / object takecare 
                    of references equality. 
                    Use with useMemo hook
                    
         • Problem 3: When you have useEffect triger 
           on URL change
            • it create new fetch everything when URL
              changes.
              So to avoid it , use useEffect clearup 
              function 
              
              useEffect ( () => {
                  const controller = new AbortController()
                  // Build in fetch function
                  
                  setLoading(true) // useState hook var
                  
                  fetch(url , { signal: controller.signal})
                      .then(setData)
                      .catch(setError)
                      .finally(() => setLoading(false)
                   ); 
                   return () => {
                     //UseEffect cleanUp function 
                     controller.abort();

                      // it abort previous url fetch request if
                          Any is in process.
                   }
 
              }, [url])
              
         • 
    • 
•
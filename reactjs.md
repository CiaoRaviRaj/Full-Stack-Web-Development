• What is react?
    • javascript library for building UI
        • Declarative 
        • component-Based
    • 
    
• Steps 
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
  
• JSX
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
   form elements such as <input>, <textarea>, and <select> typically maintain their own state and update it based on user input. Unable to render using react.

   To manage state of them using react, do
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

#AdvancedGuild
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
                         












• Coding mistake or improving your mistake
    • useState hook
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
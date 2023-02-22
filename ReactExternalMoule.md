* react-router-dom 
    <BrowserRouter>//manage location {it is context to provide all router related to children}
         <Routers>//switch case for render
               <Route //if statement 
                     path="/"
                     elements={}
         </Routers>
    </BrowserRouter>

    * create route
      1. const router = createBrowserRouter([
        {
            path: "/",
            element:    <root />,
            errorElement: <ErrorPage /> 

            // it is an error screen that show when you get an error.
            //import { useRouteError } from "react-router-dom"; to get the error message.
        },
        {
            path: "/age",
            element: <age />,
        },
        {
            path: "contacts/:contactId",
            element: <Contact />,
            //Passing params in url like this.
            //
        },

        {
            //Nesting routes
            {
                path: "/",
                element: <Root />,
                errorElement: <ErrorPage />,
                children: [
                    {
                        path: "contacts/:contactId",
                        element: <Contact />,
                    },
                ],
                // specified the place to see in root.jsx
                //  <div id="detail">
                        <Outlet />
                    </div>
            },
        }
    ])

      2. ReactDOM.createRoot(document.getElementById("root")).render(
        <React.StrictMode>
            <RouterProvider router={router} />
         </React.StrictMode>
      );

      3. hash router : it do not change url just change url value adding 3 to your url.
      4. unStable_historyRouter: 

    
    3.  <Navigate>
    * Client Side Routing
        <Link> : Client side routing allows our app to update the URL without requesting another document from the server. Instead, the app can immediately render new UI. 
    
        <Link to={`contacts/1`}>Your Name</Link>
    
    * Loading Data
        * load data ob api 
        1. export async function loader() {
                const contacts = await getContacts();
                return { contacts };
            }
        2. import that method on router file
            const router = createBrowserRouter([
            {
                path: "/",
                element: <Root />,
                 errorElement: <ErrorPage />,
                loader: rootLoader, //specified the data on load
                    
            },
        ]);

        3.  import {
                Outlet,
                Link,
                useLoaderData,// that load the data 
            } from "react-router-dom";

            const { contacts } = useLoaderData();


    
    <Outlet context={ "context to child route"  }>// used to render child components using route condition.
    <NavLink> // is used to show or style active state
    *  react router Form
        //client side routing
        *   you cam specified form method, but it use react router Form , instead
        1.  import {
                ...,
                 Form,
            } from "react-router-dom";
        2. export async function action() {
            const contact = await createContact();
            return { contact };
        }
        3. <Form method="post">
            <button type="submit">New</button>
          </Form>
        4. in main.js
            import Root, {
                loader as rootLoader,
                action as rootAction,
            } from "./routes/root";
        


        5.  const router = createBrowserRouter([
        {
             path: "/",
            element: <Root />,
            errorElement: <ErrorPage />,
            loader: rootLoader,
            action: rootAction, //
            children: [
              {
                path: "contacts/:contactId",
                element: <Contact />,
              },
            ],
        },
        ]);


    * URL Params in Loaders
        path: "contacts/:contactId"

        *   :contactId = dynamic segment (URL Params / params)

        *   :contactId is the key to access params value
            i.e params.contactId

        *   export async function loader({ params }) {
            return getContact(params.contactId);
        }

    *   Updating Data
        1. Form with post method
        2.  import EditContact from "./routes/edit";
        3.  {
                path: "contacts/:contactId/edit", // you can made url  over dynamic url.
                element: <EditContact />,
                loader: contactLoader,
                
            },
    *   redirect
        * import {
            redirect,
        } from "react-router-dom";

        return redirect(`/contacts/${params.contactId}`);
    *   as maontion we can get form data 
        export async function action({ request, params }) {
                const formData = await request.formData();

                const updates = Object.fromEntries(formData); // to make it form data into an object.

                await updateContact(params.contactId, updates); // update the data 

                return redirect(`/contacts/${params.contactId}`);
        }


    *   Active Link Styling
        to make link active 
        *   used 
        *   import {
  
                NavLink,
  
            } from "react-router-dom";

        *   <nav>
          {contacts.length ? (
            <ul>
              {contacts.map((contact) => (
                <li key={contact.id}>
                * <NavLink
                    to={`contacts/${contact.id}`}
                    className={({ isActive, isPending }) =>
                      isActive
                        ? "active"
                        : isPending
                        ? "pending"
                        : ""
                    }
                  >
                    {/* other code */}
                  </NavLink>
                </li>
              ))}
            </ul>
          ) : (
            <p>{/* other code */}</p>
          )}
        </nav>

    
    *   Global Pending UI
        *   useNavigation
            all
        *   import {
                // existing code
                useNavigation,
            } from "react-router-dom";  

        *   const navigation = useNavigation();

        *    <div
                id="detail"
                className={
                  navigation.state === "loading" ?      "loading" : ""
                }
             >
                <Outlet />
            </div>
    *   Deleting Records

        *   <Form
                method="post"
                action="destroy" ///
                onSubmit={(event) => {
                  if (
                    !confirm(
                      "Please confirm you want to delete            this record."
                    )
                  ) {
                    event.preventDefault();
                  }
                }}
            >
                <button type="submit">Delete</button>
            </Form>

        *   export async function action({ params }) {
            await deleteContact(params.contactId);
            return redirect("/");
        }

        *   import { action as destroyAction } from "./routes/destroy";

        * children: [
            /* existing routes */
        {
            path: "contacts/:contactId/destroy",
            action: destroyAction,
            errorElement: <div>Oops! There was an error.</div>,
        },
        ],  

    *   index route
        When a route has children, and you're at the parent route's path, the <Outlet> has nothing to render because no children match. You can think of index routes as the default child route to fill in that space.

        children: [
            { index: true, element: <Index /> },
            // when there is no child element. 
            /* existing routes */ 
        ],
    
    *   cancel button
        <button
          type="button"
          onClick={() => {
            navigate(-1); // that send one entry back
          }}
        >
          Cancel
        </button>


    *   GET Submissions with Client Side Routing
        *   <Form id="search-form" role="search">
            <input
              id="q"
              aria-label="Search contacts"
              placeholder="Search"
              type="search"
              name="q" // that take it as params key
            />
            <div id="search-spinner" aria-hidden        hidden={true} />
            <div className="sr-only"        aria-live="polite"></div>
        </Form>

        *   export async function loader({ request }) {
            const url = new URL(request.url);
            const q = url.searchParams.get("q"); // get value with key value.
            const contacts = await getContacts(q);
            return { contacts };
        }
        *   Synchronizing URLs to Form State
            *   form and input do not sync
            *   
                1.  If you click back after a search, the           form field still has the value you          entered even though the list is no          longer filtered.

                2.  If you refresh the page after           searching, the form field no longer has         the value in it, even though the list           is filtered
            *   return q 
                export async function loader({ request }) {
  
                    return { contacts, q };
                }
            *   set it to default value input value
                <input
                    id="q"
                    aria-label="Search contacts"
                    placeholder="Search"
                    type="search"
                    name="q"
                    defaultValue={q}//
                />
    *   useSubmit

            * import {
                // existing code
                useSubmit,
            } from "react-router-dom";

            *  const submit = useSubmit(); 
            *   <input
                    id="q"
                    aria-label="Search contacts"
                    placeholder="Search"
                    type="search"
                    name="q"
                    defaultValue={q}
                    onChange={(event) => {
                      submit(event.currentTarget.   form);
                    }}
                    //currentTarget is the DOM node the event is attached to
                    //  the currentTarget.form is the input's parent form node
            />
    
    *   Adding Search Spinner

        *    on search from database always show a lack on loading.
        *   const searching =

                navigation.location &&
                new URLSearchParams(navigation.location.            search).has(
                  "q"
            );
        *   <input
              id="q"
              className={searching ? "loading" : ""}
              // existing code
            />
        *   

    *   Managing the History Stack

        *    Use replace in submit
            // for searching queries 
            // save all search result.
            //We only want to replace search results

        *   <input
              id="q"
              // existing code
              onChange={(event) => {
                const isFirstSearch = q == null;
                submit(event.currentTarget.form, {
                  replace: !isFirstSearch,
                });
              }}
            />

    *   Mutations Without Navigation
        if we want to loaders and actions without causing a navigation.
        we should use useFetcher

        *   import {
              useLoaderData,
              Form,
              useFetcher,
            } from "react-router-dom";
        
        *   const fetcher = useFetcher();

        *   <fetcher.Form method="post">
              <button
                name="favorite"
                value={favorite ? "false" : "true"}
                aria-label={
                  favorite
                    ? "Remove from favorites"
                    : "Add to favorites"
                }
              >
                {favorite ? "★" : "☆"}
              </button>
            </fetcher.Form>

        *  export async function action({ request, params }) {
          let formData = await request.formData ();
          return updateContact(params.  contactId, {
            favorite: formData.get("favorite")  ===  "true",
          });
        } // update favorite start

        *   There is one key difference though, it's not a navigation--the URL doesn't change, the history stack is unaffected.

        *   fetcher.formData 
            * it show loading state on fetch-formData.
            *     let favorite = contact.favorite;

            if (fetcher.formData) {
              favorite = fetcher.formData.get ("favorite") === "true";
            }

    *   Not Found Data
        *     const contact = await getContact(params.contactId);
            if (!contact) {
              throw new Response("", {
                status: 404,
                statusText: "Not Found",
              });
            }

    *   Pathless Routes

        if data is not found.it is better to rendered inside the root outlet, , because use has many option 
        *   To do show we want to re-direct to the same page for all children.

        *   we wrap out all children in no oath url

        *   children: [
              {
                errorElement: <ErrorPage />,
                children: [
                  { index: true, element:   <Index /  > },
                  {
                    path: "contacts/:contactId",
                    element: <Contact />,
                    loader: contactLoader,
                    action: contactAction,
                  },
                  /* the rest of the routes */
                ],
              },
            ],
            *   When any errors are thrown in the child routes, our new pathless route will catch it and render, preserving the root route's UI!




        



* #redux 
  • Action
       File with export function
          export const actionName=(props)=>{
               return {
                    type: 'INCREMENT'
                    data: props
               }
          }
       
  • Reducer
        • root.js
               Import all reducerfile
               Import {combineReducers}
               
               const rootReducer = combineReducers({
                       users: Reducerfile1,
                       students: Reducerfile2
               export default rootReducer;
               
       • reducerHandler.js
              InitialState
              const reducerName = (state=initialState, 
              action) => {
                    Switch (action.type) {
                         case "typeValue1"
                             return stateValue;
                          case "typeValue2"
                               return stateResetValue; 
  • Store 
        import rootReducer from
        Import {createStore}
        
        const Store = createStore(rootReducer);
        
       export default Store;
       
       //Import store file and rep index.js file
       //Check store state
       
  • Provider
      Import {Provider}
      <Provider store={store}>
      //Wrap the components you want to 
      </Provider>
      
   • useSelector to fatch state 
   • useDispatch to call action.
        Const dispatch = useDispatch ();
        
        dispatch (incNumber(props));
    * connect components

      * const mapStateToProps = (state) => {
        return {
          user: state // that user as key for access current state value to App component.

        }
      }
      export default connect(mapStateToProps)(Apps) // high order function

      * const mapDispatchToProps = (dispatch) = >{
        return {
          change: (name) => {dispatch(type: "SET_NAME", payload: name)}
          change: () => { dispatch(updateName(name))} // if we have Action files.

        }
      }

      // export const updateName = (name) => {
        return {
         type: "SET_NAME", 
         payload: name
        }
      }

      // used in app my simply props.user, props.change

      export default connect(mapStateToProps, mapDispatchToProps)(Apps) // high order function

  * middleware and thunk
      * it is used when you need to fatch so data from API in reducer
      * npm i redux-thunk
      * import thunk from 'redux-thunk'
      * const store createStore(mainreducer, {common data} , applyMiddleware(thunk));
      * reducer function
        * allACTION
        * export const updateStudentId = (studentId) => {
          return (dispatch) => {
            // for get the data dispatch()
            var url ="apiurl",
            axios.get(url);
            .then (response => {
              dispatch({type: "SET_SID", playload: response.data.data[studentId].name});
            })
          }
        }
  * logger 
    * to get all log states(prevState, action, newState)
    * npm i redux-logger
    * import logger from "redux-logger"
    * ..... applyMiddleware(logger, thunk) 

  * react dev tool
    * npm i redux-devtools-extension
    * const store = createStore(mainreducer, commondata, commonwithDevTools(applyMiddleware(logger,thunk)))
  
  * useSelector & useDispatch
    * useSelector to fetch data
      const propsHook = useSelector(state => {
        return {
          users: state.users,
          student: state.students
        }
      })
    * const dispatch = useDispatch();
      * dispatch(updateStudentID('ttttt'));

  * react saga 
    * it similar to thunk work on async promise function
    * it use generator function 
      callback function to run next after other
    * npm i redux-saga
    * import createSagaMiddleware from 'redux-saga'
    * const sagaMiddleware = createSagaMiddleware()
    * rootsada.js file all saga file
      * rootsaga
      import {all} from 'redux-saga/effects'
      import StudentSgaga 
      import ageSaga

      export default function* rootSaga () {
          yield all([waitForFetchMarks()], [waitForFetchAges()] ) // it manage all waitForFetchMarks()
      }

      StudentSgaga.js 
      * import {takeEvery, takeLatest, call, put} from 'redux-saga/effect'
      import all action.js file


      * function* fetchMarks(params) {
        //params from component call
        try {
          yield put (doneMarks('75'));
          const data = yield call('api', firstParams, secondParams);
        } catch (e) {

        }
      }

      * export function* waitForFetchMarks(firstParams,secondParams) {
        yield takeEvery('Get_MARKS' , fetchMarks) // when it run fetchMarks() for every
        yield takeLatest('Get_MARKS' , fetchMarks) // it run one function at time, it cancel previous task
      }

      * in AllAction .js
          getMarks() //initial
          doneMarks() // after done
      * reducer for same also

      * in index.js 
        import createSagaMiddleware from 'redux-saga'
        import rootSaga from "./rootSaga'
        * const sagaMiddleware = createSagaMiddleware()
       const store = createStore(mainReducer, {commonData}, composeWithDevTools(applyMiddleware(sagaMiddleware)));

       sagaMiddleware.run(rootSaga);




* redux-toolkit
    * 

#contextAPI&Reducer 


#fetchAPI

* #Formik and Yup
  * Formik is use to form handling
    * import {useFormik} from "formik"
    * const Formik = useFormik(
      initialValues: initalValues,
      onSubmit: (values, action) => {
        ""
        values
        action.resetForm();
      }
    )
    * all handle need value
      * Formik.values.name
      * const {values , errors, touch handleChange , handleSubmit , handleBlur} = useFormik()
      * {errors.name && touched.name ? <p>errors.name</p> : null}

    * <element on
  * Yup for validation
    * import * as Yup from "yup"
    * export const signUpSchema = Yup.object({
      name: Yup.string().min(2).max(25).required("Please enter your name"),
      email: Yup.string().email().required("please enter your email"),
      password: Yup.string().min(6).required("please your password"),
      confirm_password: Yup.string().min(6).oneOf([Yup.ref("password"), null], "password not match"),

    })
    * const Formik = useFormik({
      // all code same 
      validationSchema: signUpSchema
    })

* #react-toastify
  * npm i react-toastify
  * import { ToastContainer , toast} from "react-toastify"
  * toast : for individual notification
  * import "react-toastify/dist/ReactToastify.css
  * <ToastContainer /> at the end 
  * style can be do in it playground that they providing
    * theme: "dark"

* # React propsType
   * it is used to check type of props passing 
   * it is just return all error in console.log
   * not stop render
   * npm i prop-types
   * it is use to give prop type to a component
   * for a component to apply prop type
      * import PropTypes from 'prop-types'
      * .... function component 
      * ComponentName.propTypes ={
         name : PropTypes.string
         age: PropTypes.number.isRequired
      }
      * PropTypes Variants
         * PropTypes.string
         * PropTypes.number
         * PropTypes.bool
         * PropTypes.func
         * PropTypes.object
         * PropTypes.array
         * PropTypes.node 
            * // it is used to check props is renderable or not 
            * like object is not renderable
            * string 
         * PropTypes.element 
            * it is used to check props type a react component or not
            * PropTypes.element.isRequired
         * PropTypes.elementType
            * it is used to check passing props is a type of react element
            * as: PropTypes.elementType
            * <component as={link} />
         * PropTypes.any.isRequired
            * 
         * PropTypes.oneOfType([PropTypes.string, PropTypes.number])
            * it is used check from set of type
         * PropTypes.oneOf(['loading', 'Ready'])
            * it is used to check value pass in is one of given et values
         * PropTypes.arrayOf(propsTypes.number)
            * it is used to check value type of array pass in
            * it is multiple check on combine 
            * it is PropTypes.oneOfType([PropTypes.number, PropTypes.string])
            * 
         * PropTypes.shape({
            name: PropTypes.string,
            age: PropTypes.number
            })
            * it is used to check shape of object 
            * it is option check 
         * PropTypes.exact({
            name: PropTypes.string,
            age: PropTypes.number
            })
            * it is used to check shape of object
            * it is eject match of given shape
         * 
* 
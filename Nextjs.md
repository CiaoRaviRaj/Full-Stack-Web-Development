# Next js 
* Introduction 
    * It is javascript framework for production.
    * It helps in SEO.
    * first landing page
    * advance load page in server 
    * static generator  
    * getRequest in data change
    * revalidate: 30 // generator html and js code chang data in every time interval.
    * styles with 
        * global
        * home.modules.css
            * use as style object .
    * _app.js : main landing page
    * every page have a default export function
    * [id].js dynamic route
        * import {useRouter} from 'next/router'
        * ... rest of code 
        * const { id } = router.query
        * 
    * api folder 
        * used for server-only routes
        * it used as back-end
    * data fetching 
        * SSG : Static generation
            * it generate html code on run build time
            * make storage bucket static 
            * getStaticProps({ paraps }) // provide fetch static data configuration to default export fucntion as props
            * <Head></Head> from 'next/head // to specify / optimism SEO for this route
            * getStaticPaths // that make a number of value of params value for route.
                // we map the path
                and return {
                    paths,
                    fallback: false
                } 
                // It generator pre-dev html file before touching js
            * SSR 
                * contain generate on server
                * getServerSideProps
    * round off features
        * file based routing
        * Pre rendering
        * api routes
        * Support for CSS modules
        * Authentication
        * dev and prod build system


* npx create-next-app folder
* npm start //error
    * npm run build // before npm start
* npm run dev // run both together

* pages and route
    * route
        * file home.js // small case like we do in route
        * blog 
            * add.js
            /blog/add // that run add file
        
    * dynamic route
        * article folder
            * index.js // /article
            * policy.js // statics 
            * [articleid].js //dynamic
                * next/router -> useRouter
                * const router = useRouter
                * const {id } = router.query

        * brand folder
            * [brandName] folder dynamic folder
                * model // statics folder
                    * [modelName].js dynamic
        /brand/[brandName]/model/[modelName]

* Linking 
    /info/bike/bajaj/discover...
    -> we want to call Info file always
    * info folder
        * index.js //default call on /info
        * [...infoType].js as take in params
            * console.log(router.query); //return all query in the form of array
            * const {infoType=[]} = router.query
            console.log(infoType);
            * if(infoType.length === 1) {
                return <h1> infoType[0]</h1>
            }
        * 
    * link as navigator in react
        * import Link from 'next/link'
        *   <link href="/home-data> behave like a button
                button name
            </link>

            <link href="/url" replace>
                name -> url -> newPage
                replace back url from history
                if we click browse back from newPage
                then it goes back to news(!not at /url)
            </link>

    * <link href={
        pathname:"/about',
        query: {name: 'dummy', id: {} ....}
    }>

    * <link href={
        pathname: 'blog/blockId',
        query: {blogId: 5}
    }>

    * <link href={"/about"} passHref > //it passHref value to children or ref to children
        <MyButton />
      <link>

        const MyButton = react.forwardRef( function fr (onClick, href), ref) {
            console.log(href)
            <a href={href} onClick={onClick} ref={ref}> Yes Click </a>
        }

    



* useRouter
    * 404 (not found page)
        * 404.js
            * notFound page function
            * if we get 404 status then it call that components

    *   auth check
        * auth ? router.push("/landingUrl") : <page>
    

    * shallow routing
        * <button  onClick={() => router.push('/home?page=3','/about',{shallow: true})}>
        it work on sample url, it want until page load the data

    * dynamic push
        <button onClick={() => {
        router.push({
            pathname: '/blog/[blogId],
            query: {blogId: 4 , id: 4...}
        })
    }}>
    * push back
     router.back()
    * Replace
        router.replace("/blog")
    * router.beforePopState(cb) 
        cb is a function run on incomming popstate
    * router event 
        useEffect(() => {
            const handleRouteChange = (url) => {
                log('ready to change',url)
            }
            router.events.on('routeChangeStart', handleRouteChange); // before url change
        })
        * routeChangeStart( url , {shallow})
        * routeChangeComplete (url , {shallow})
        * routeChangeError(err, url {shallow})
        * beforeHistoryChange(url , {shallow})
        * hashChangeStart(url, {shallow})
        * hashChangeComplete(url, {shallow})
        



* layout 
    * components
        * components
    * layout folder
        * layoutFilename.js
            layoutFilename({children})
            ...
            children
    * _app.js 
        return 
            <layoutFilename> 
                <Component {...pageProps} />
            </layoutFilename>
    * for specific layout 



*   styling 
    * globals.com // for global import into _app
    * home.module.css 
        style.class/id
    * 



* Pre Rendering
    * static Generation
        * without data 
        * with data
            * it get data from api on build

            * getStaticProps to get data from api in build
                * export async function getStaticProps(context) {
                    const res = await fetch("url");
                    const blogs = await res.json()
                    if(!blogs) {
                        return {
                            redirect: {
                                destination: "/about",
                                permanent: false
                            }
                        }
                    } 
                    if(!blog) {
                        return {
                            notFound: true // not found data
                        }
                    }
                    return {
                        props: {
                            blogData:  blogs
                            revalidate: 10 //Incremental Static Regeneration 
                        }
                    }
                }
                * export default const blog ({blogData}) {
                    return {
                        <div>
                            blogData.map((item) => {
                                return <Blog item={item}>
                            })
                            
                        </div>
                    }
                }

            * how to handle frequently change data in an api

                .....

                return {
                        props: {
                            blogData:  blogs
                            revalidate: 10 
                        }
                    }
                it make build it self after every 10 sec


        * getStaticPath
            * for some dynamic page ,we make build for fast serve
            * const async function getStaticPaths() {
                const paths = ['/page1','/page2', 'page3'];

                return {
                    paths, //it make module for these path on build
                    fallback: true // to get loading data state, if false it not run dynamic api call
                }
            }
            * fallback: true 
                // to get loading data state,
                // then after it make a build file.
            * fallback: false
                // false it not run dynamic api call
            * fallback: "blocking"
                // it not render page util its loading data not complete. it make and save build file of it 

            if(router.idFallback) {
                <h1>loading data</h1>
            }
            // it fetch on run time but on build html
            // to get data on build we used SSR

    * Server-side-rendering 
        export async function getServerSideProps({query}) {
            const {blogId} = query
            const blogs = fetch("url" +blogId);
            return {
                props: {
                    blogData: blogs
                }
                
            }
        }
        // it get data from server

* Authentication 
    * Authentication pattern
        * SGP : 
        * SSP : 

* Dynamic import
    import dynamic from "next/dynamic"
    * const Sidebar = dynamic(() => import("../path").then((module) => module.sidebar), {
        ssr: false,
        loading: () => <h1> loading</h1>
    });


* errors on build
    * dynamic import
        * component definition is missing
            * const Sidebar = dynamic(() => import("../path").then((module) => module.sidebar), {
                     ssr: false,
                        loading: () => <h1> loading</h1> // error
                });

        * it need a name to return 
        loading: function ld() {
            return <h1> loading ... </h1>
        }
* meta title
    * import Head from 'next/head,
        <Head>
        <meta property="og:title " contant>
         <title>hhh<title>
        </Head>

* custom app
    for layout
* custom document
    _document.js
    default page formate 
    if some page not contain tag

* custom server
    * api route 
        * pages
            * api
                * login.js
                    * export default function handler (req, req) {

                        if(req.method === 'GET') {
                            res.status[200].json({name: 'code improve' , message: 'success'})
                        }
                        if(req.method === 'POST') {
                            res.status[200].json({name: 'code improve' , message: 'success'})
                        }

                        res.status[200].json({name: 'code improve' , message: 'success'})
                    }
                * localhost:3000/api/login to fetch that data

            * api params
                * post 
                    * [postId].js
                        export default function handler (req, req) { 
                            const {postId} = req.query

                            res.status[200].json({name: 'code improve' , message: 'success'})
                        }
                    * [...typeInfo].js
                        export default function handler (req, req) { 
                            const { typeInfo=[]} = req.query;

                            res.status[200].json({name: 'code improve' , message: 'success'})
                        }


            
                * database
                    * npm i mysql
                    * var conn = mysql.createConnection({
                        host: 
                        user
                        password
                        database
                    })
                    conn.connect( function(err) {
                        if(err) {
                            log("error" + err)
                        } else {
                         log("Db connect")
                        }
                    })
                     export default function handler (req, req) { 
                        let result = await getUserData() 
                        res.status(200.json({name: result, message: "success"}))

                     }

                     async function getUserData() {
                        return new Promise((resolve, reject) => {
                            let sql = "select * from users"

                            conn.query(sql, function(error, results,field){
                                if(error) {reject(error)}
                                else {
                                    resolve(results)
                                }
                            })
                        })
                     }

                    
    * 

* next.config.js
    module.exports = {
        reactStrictMode: true
        env {
            mySite: "hhhh"
        }
        basePath: "/code test"
        async rewrites(){
            return [
                {
                    source: 'testing',
                    destination: 'blog/2'
                },
                {
                    source: '/dummy/:path',
                    destination: '/info/:path'
                }
            ]
        }

        async redirects() {
            return [
                {
                    source: "/mytesting',
                    destination: '/blog/4,
                    permanent: true
                }
            ]
        }

        async headers() {
            return {
                source: "/blog/:blogId
                Headers: [
                    {
                        key :"xyz",
                        value: 'yes code'

                    }
                ]
            }
        }

    }



* next js 13 
    * how to change next js 13
    * pages -> 
        app 
        * next.config.js {
            experimental : {
                appDir: true,
            }
        }
        * tailiwind.config {
            content: [
                './app/**/*.{js,jsx,tsx}'
            ]
        }
        app folder : pages
        * layout {

        }
        * page.tsx {

        }

         * layout hierarchy 
            * make a layout in folder 
                * then it only change this layout data rest is same

        * fetch (url , {cache: 'no-store' //SDR
                        cache: 'force-cache' //SSR
                        next: {
                            revalidate: 60 // ISR
                        }
                        })
        * export async function generateStaticParams() {
            // SGP : getStaticPaths 
            // not run in revalidation
            // run once in 
        }
        * conditional checkout on data 
            import {notFound} from "next/navigation"
            * not-found {
                if(!todo.id) {
                    return notFound() // 404 page
                }
            }
        * for components 
            'use client' // it is use in client side not on server side
            * it is not show change in server side page
                * to show change in server side , we used 
                    * const router = useRouter()
                    * call router.refresh() after components change the serve data. // it re fetch data from api only not all page refresh
            * 



    

    
     


    * link components change
    * turbo pack
    * fetching components data separate
        * default all function are SSR 
        * external data fetch just using normal function
        * loading.js // show on loading component on data fetch
        * backEnd not writeable in app
            * it is †

    * Data Fetching props
        * getStaticProps
            * import { use } from react
            * function pageName () {
                const data = use(getData());
                return data.map()...
            }
            * async function getData() {
                return await (await fetch ("url" , {cache: "force-cache" // Default})).json() // get data in build
            }
        * getServerSideProps
            * import {use} from react
            *  async function getData() {
                return await (await fetch ("url" , {cache : "no-store"})).json() // get data in build
            }
            * export default Serverpage () {
                const data = use(getData());
                return data
            }
        *   client side fetching
            * "use client"
            * import  third party data fetching app import useSWR "swr"
            * import Link from "next/link"
            * const fetcher = (path) => fetch(`url/${path`).then(res => res.json())
            * export default function clientSide() {
                const data = useSWR("urlPath",fetcher)

                return data...
            }
            * getStaticPaths
                * folder slug
                * async function getData() {
                    return await (await fetch("url")).json()
                }
                * export async function generatorStaticparams() {
                    const characters = await getData();
                    return charactors?.results.map ( c => {
                        slug: c?.name.replace(/\s+/g, "-").toLowerCase();

                    })
                }
                * export default function StaticPages ({params}) {
                    return (
                        <>
                            <h1>The charactor name is: {params.slug}</h1>
                        </>
                    )
                }


* Rendering patterns
    * static page
    * dynamic page
        * dynamic page 
        * server
            *  render one page and dynamic change data and render change data in browser like react do
            * It is not good for SEO , all contents not render for first time.
            * SSR (metaFrame )
                * it need serve to fetch all data 
            * SSG
                * 
                * it rebuild  all page in store in static server
                * it hybrids javascript after render and then it revaluate and request and server build new build file , and then it's re render //ISG
                * partial hydration
                    * dynamic import 
                    * island hydration
                        * static html 
                        * dynamic file only get js
                        // astro 
                    * Streaming SSR
                        * load components in multiple chucks

                    * Exclude hydration
                        * REASUMABLITY
                        * qwik
                        * event listener in sync 
                        * javascript in multiple chuck

* styling 
    * Global style
        * it is applicable'
        * import it on _app.js
        * all external style is also import here Like bootstrap

    * component style
        * Home.module.css
        * import style from "../styles/Home.module.css"
        * the style name colliding is not happened , all component same different instance of style object
    * scss style
        * similar like normal css file 
    *  CSS in-line-style js support
        * in line style
            * style={{color: "hhhh"}}
        * styled-component also used for in line style
        

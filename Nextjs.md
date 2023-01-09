l#Next js 
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
                            notFound: true
                        }
                    }
                    return {
                        props: {
                            blogData:  blogs
                            revalidate: 10
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

    

    
     




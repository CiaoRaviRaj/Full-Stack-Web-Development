# Sails

* introduction
    * MVC framework build over node js
    * any database like Mysql, MongoDB,Postgresql
    * auto - generated REST APIs
    * WebSoket Integration
    * File Handling
    * Frontend Agnostic 
* installation
    * npm i -g sails --no-frontend
    * sails new projectName
    * cd projectName
    * sails lift
* folder structure
    * api
        * controllers
            
        * helper
        * models

        * policies
            // for middleware
    * config
        // all config file
        * env
            * production.js
                * development related information in this file
        * blueprints.js
            * 
        * bootstrap.js
            * the very first file which is run on sails
        * custom.js
            * custom configuration setting 
            * api keys
        * datastores.js
            * dataStore config
        * globals.js
            * globals variable
            * globals requirement
        * http.js
            * all middleware write here
        * i18njs
        * local.js
        * log.js
        * models.js
        * policies.js
        * routes.js
            * all routes
        * security.js
            * cors
        * session.js
        * sockets.js
        * views.js


    * views

    * app.js
        * it run this file in first stage
        * rc = require('sails/accessible/rc');

* sails generate api articles
    * it generate api for articles
        * a new file added to your api > controllers folder 
            ArticlesController.js
        * a new file added to your api > models folder 
            Articles.js 
        
        * migrate once you added a api
            * auto migrate
            * to make auto 
                * config
                    * models.js
                        * migrate: 'alter'
            * all restfull api create by default true in blueprint
                * 'POST /article' : 'ArticlesController.create',
                * 'GET /article' : 'ArticlesController.create',
                * 'GET /article/:[id]' : 'ArticlesController.create',
        * all Local Db
            * .temp
                * localDiskDb
                    * articles.db
        
* config
    * blueprints.js
        * RestFull
            * rest: true // by default
        * shortcut Route
            * to create new record
                * 'Get '/todo/create?name=""?description=""'
                to create record
            * to fetch all record
                * 'GET '/todo/find
                * 'Get '/todo/find/1
            * to update record
                * it update only params value
                * 'Get '/todo/update/2?name=""
            * to delete record
                * 'GET '/todo/destroy/2

* database        
    * sails to connect mysql
        * config > 
            * datastore.js
                *   adaptor: 'sails-mysql', //npm i -s sails-mysql
                *   user: 'root',
                *   password: 'root',
                *   port: '3306'
                *   host: 'localhost'
                *   database: 'nameofDb' //set The db before
            * model

                migrate: 'alter'
        
    
    * sails to connect mongoDB
        * one terminal
            * mongod
        * second
            * mongo
                * use portal_db
        * datastore.js
            * mongodb: {
                *   adaptor: 'sails-mongo', //npm i -s sails-mongo
                *   user: 'root', //optional
                *   password: 'root', //optional
                *   port: '27017'
                *   host: 'localhost'
                *   database: 'nameofDb' //set The db before
            }
            
        * setup model for it
            * api
                * models
                    * Article.js
                        * model.exports = {
                            * attributes: {
                                // schema structure for database
                                title: {
                                    type: 'string'
                                },
                                description: {
                                    type: 'string'
                                }
                            },
                            * connection: 'mongodb' // we can use different database for different database
                        }

* migrate
    * alter
        * 
    * drop 
        * it drop the database and re-initialize all models every time
    * safe
        * it not migrate , do its with your hands
    
    
* jobPortal application
    * use Case
        * Each user can register many companies
        * Each company can post many jobs
        * many candidates can apply to many jobs
    
    * creating model
        *  api
            * models
                * Company.js
                    module.exports = {
                        attributes: {
                            name: {
                                type: 'string',
                                required: true
                            },
                            city: {
                                 type: 'string',
                            }
                            address: {
                                type: 'string'
                            }
                        }
                    }
    * creating controllers 
        * api
            * controllers
                * CompanyController.js
                    * module.exports = {
                        * create(req, res) {

                            * //Create a new record in company model
                                * //use create method from company model
                                * // it is possible because, it is a global variable, 
                                * // it is set in global.js
                                    * models: true
                            * get th name from the req params
                                * let params = req.allParams()
                                    * // It store all params value
                                
                                * Validate name input 
                                 * if (!params.name) {
                                    return res.badRequest({err : 'name is required field'})
                                    // it is validate name
                                    * // All  res pre- build method is define in
                                        * node_module
                                            * sails
                                                * lib
                                                    * hooks
                                                        * responses
                                                            * badRequest = 400
                                                            * negotiate = 500 
                                                            * serverError = 500
                                                            * ok = 200


                                }
                                * // create a new record
                                    * Company.create({
                                        name: params.name,
                                        city: params.city,
                                        address: params.address
                                    },(err, result) => {
                                        // Callback method
                                        if(err) {
                                            return res.serverError(err)
                                        }
                                        return res.ok(result);
                                    }
                                    )
                                    * promise method to check model result
                                        * Company.create({
                                        name: params.name,
                                        city: params.city,
                                        address: params.address
                                    }
                                    )
                                        .then (result => {
                                            return res.ok(result)
                                        })
                                        .catch(err => {
                                            return res.serverError(err)
                                        })
                                    * async and await
                                        * async create (req, res) 
                                            .... rest code
                                            * try {
                                                * const result = await Company.create({
                                                    name: params.name,
                                                    city: params.city,
                                                    address: params.address
                                                    }
                                                )
                                                return res.ok(results)
                                            } catch (err) {
                                                return res.serverError(err);
                                            }



                        },
                        * async find(req, res) {
                            //use the find method from company
                            // find all the companies
                            * try {
                                const companies = await Company.find();
                                return res.ok(companies)
                            } catch {
                                return res.serverError(err);
                            }
                            
                            //Create route

                        },
                        * async findOne(req, res) {
                            try {
                                const company = await Company.findOne({
                                    id: req.params.id
                                })
                                return res.ok(company)
                            } catch (err) {
                                return res.serverError(err)
                            }
                            //Create route
                        },
                        * async update(req, res) {

                            try {
                                let params = req.allParams();
                                let attributes = {}
                                if (params.name) {
                                    attributes.name = params.name;
                                }
                                if (params.city) {
                                    attributes.city = params.city;
                                }
                                if (params.address) {
                                    attributes.address = params.address;
                                }

                                const result = await Company.update({id: req.params.id}, attributes);
                                return res.ok(result)
                            } catch (err){
                                return res.serverError(err)
                            }
                            // create route for it
                        },
                        * async delete(req, res) {
                            try {
                                const result = await Company.destory({id: req.params.id})
                                return res.ok(result)
                            } catch (err) {
                                return res.serverError(err)
                            }
                            // create route

                        }
                    }
    * creating routes
        *   config
            * routes.js
                * all routes here
                * 'POST /companies' : 'CompanyController.create'
                * 'GET /companies : 'CompanyController.find'
                * 'GET /companies/:id : 'CompanyController.findOne'
                * 'PATCH /companies/:id : 'CompanyController.update'
                * 'DELETE /companies/:id : 'CompanyController.delete'

    
        

* docs concept
    * Action and Controllers
        * Actions file
            * it is special file which is going to run on a particular route res
                * action file and folder are in lowercase
                * example 
                    * 'GET /companies' : 'companies/find'
                        * it is going to run companies/find on this route request /companies.
            * there are two way to create action file
                *   modern way
                    * run sails generate action user/find // to create automatic file of action.
                    * it look like this
                        * module.exports ={
                            // it is not use res or req syntax , it is auto handle
                            friendlyName: 'Sign up',
                            description: '',
                            * inputs: {
                                // it take all incoming params value
                                // example
                                * userId: {
                                    description: "it is developer description detail"
                                    // it get  value from params
                                    * // it is similar to 
                                        * const userId = var userId = req.param('userId');
                                        // it fetch /user/:userId

                                    * type : "number"
                                    // it is type change for it ,
                                    // if it is not a number, then it return res.badRequest()

                                    * required: true
                                    // similarly it return res.badRequest(), it is not get that.
                                
                                }


                            },
                            * exits: {
                                // it is customs res response 
                                * success: {
                                    // view file
                                    responseType: 'view',
                                    // redirect path
                                    viewTemplatePath: 'pages/welcome'
                                }
                                * notFound: {
                                    * description: 'No user with the specified ID was found in the database.',
                                    * responseType: 'notFound'
                                }

                            },
                            fn: async function (inputs, exits) {
                                // it is operations function

                                // now we do not need to check type of userId here, it check before  
                                var user = await User.findOne({id : userId});
                                
                                if(!user) {
                                    throw 'notFound'
                                    //alternate way
                                    return exit.notFound()
                                    // we also pass data
                                        throw {notFound: ['', '']}
                                }

                                // res.success statement with data 
                                return {
                                    name : user.name
                                };

                            }

                        }

                * classic way  
                    *  run sails generate action user/signup --no-actions2 // to create action file in classic way
                    * it use classic req, res way 
                    *   it is look like this
                        * module.exports = async function signup(req, res) {

                            * // type check userId
                                *  var userId = req.param('userId');
                                * if(!_.isnumeric(userId)) {
                                    // it check required and type check
                                    return res.badRequest(new Error('not user ID specified));
                                }
                            * looking into database
                                * var user = await User.findOne({ id: userId });
                            * check user found status
                                * if (!user) {
                                    // user not found we want to redirect
                                    return res.redirect('/signup' );
                                }
                            * return the final res
                                * return res.view('welcome', {name: user.name});


                            sails.log.debug('TODO: implement');
                            return res.ok();

                        }; 
        * controllers
            * it is easier way to make multiple actions function into one single file
            * run sails generate controller UserControllers.js
            * it look like this
                * module.exports = {
                  login: function (req, res) { ... },
                  logout: function (req, res) { ... },
                  signup: function (req, res) { ... },
                };
                * it equal to (as we fallow action method)
                    * user
                        * login.js
                        * logout.js
                        * signup.js
                    * in route
                        * "Get /user" : "UserControllers.login"
                        * we just specified method to run that function on this route 
                * it BluePrint index route automatically
                    * /user auto res some Blueprint res data , if we not define route
        * routing action
            * binding a route to a controllers
            * config/routes.js
            * "GET /users" : "UserControllers.login" 
            * if you use actions methods way
                * "GET /user" : "users/login"
            * automatic routing
                * it automatic trigger controller function if route name same as action
                * example
                    * if you make a get request to /user/login
                        it automatically run UserController.login function
                * to activate this feature
                    * config/blueprints.js
                        * actions: true
    * Assets 
        * it is refer to static files (js,css,images ,etc)
        * on build it put that file in .tmp/public/ folder. it is pre - access things
        * it run  task/register/pipeline.js before run
            * it load all assets files
        * static middleware
            * it use serve-static middleware like express
            * it automatic run index.html file in a directory call
                * Eg: 
                    * /assets/foo/index.html and /assets/foo run index.html file automatically


            
    * Blueprints
        * automatically create route
        * Action Routes
            
            * action : true //default
            // automatically call controller action in route call
        * RESTFull route
            
            * rest : true //default
                * it is auto-routes for fetching data
                * GET /user => UserController.find
                * GET /user/:id : UserController.findOne
                * POST /user : UserController.create
                * PUT /user/:id : UserController.update
                * DELETE /user/:id : UserController.destroy
        * Shortcuts route
            * that enable crud method from browser
            * shortcut: true // default
            * find , create , update , destroy all these function can call by url 
            * Eg: 
                * GET /user/create?name="jdsjk"?.. // to create new record
                * GET /user/find // find all records
    * routes
        * it provides routes with controllers
        * config/routes.js
            * "/": {
                view: "homepage" // it can be change with your file
            }
    * configuration 
        * config/env
            * for all environment variable
        * config/local.js
            * for local environment set up
        * Setting sails.config values using command line arguments
            * 
        * custom configuration
        * bootstrap
            * it run as seed for your sails app. it run before sails app
            * some of application
                * setting up baseline data
                    * find or create an admin user
                * running sanity checks on the status of your database
                * seeding your database with stub data
        * 
    * Extending Sails
        * there are 3 ways extend sails
            * Adapters
                * it make easy way to communicated with database
                * it is dictionary with methods like find, create etc for database
                * available database 
                    * MySQL => sails-mysql
                    * PostgreSQL => sails-postgresql
                    * MongoDB => sails-mongo
                    * Localdisk/memory => build in
                * custom adapters
                    * 
            * custom response
                * api/response
                    * insufficientFunds.js
                        * module.exports = function insufficientFunds(err, extraInfo){

                              var req = this.req;
                              var res = this.res;
                              var sails = req._sails;

                              var newError = new Error('Insufficient funds');
                              newError.raw = err;
                              _.extend(newError, extraInfo);

                              sails.log.verbose('Sent "Insufficient funds" response.');

                              return res.badRequest(newError);

                            }
                        * similarly you can also override build in response
            * Generators
                * some sails cli code
                    * Commands that generate a new Sails app
                        * sails new name --fast/caviar
                        * sails new name --without=grunt
                        * sails new name --without=lodash,async,grunt,blueprints,i18n
                        * sails new name --no-frontend --without=sockets,lodash
                    * Generators for spitting out new files in an existing Sails app
                        * sails generate model identity
                        * sails generate action name
                        * sails generate page name
                        * sails generate helper name
                        * sails generate controller name
                        * sails generate api name
                        * sails generate hook name
                        * sails generate response name

                * custom generate
                    * sails generate awesome
                    * {
                          "generators": {
                            "modules": {
                                "awesome": "./my-project/awesome"
                            }
                          }
                        }
            * Hooks
                * There are three types of hooks available in Sails:
                    * Core hooks
                    * App-level hooks
                        * Event
                            * sails.on(eventName, eventHandlerFn) //on sails        state
                                * ready
                                * lifted
                                * lower
                                * hook:<hook identity>:loaded
                            * sails.after(eventName, eventHandlerFn)
                    
                    * Installable hooks
                    * Hook specification
                        * api/hooks/my-basic-hook
                            * index.js
                                * module.exports = function myBasicHook(sails)      {
                                   return {};
                                }
                            * sails lift --verbose // to load hook
                        * Hook features
                            * .defaults
                            * .configure()
                            * .initialize()
                            * .routes()
                            * .registerActions()
    * helper 
        * utilities functions
            * run sails generate helper name
            * it is look like this
                * module.exports = 
                  * friendlyName: 'Format welcome message'
                  * description: 'Return a personalized greeting based on the provided name.'
                  * inputs: {
                
                    name: {
                      type: 'string',
                      example: 'Ami',
                      description: 'The name of the person to greet.',
                      required: true
                    
                  },
                  * fn: async function (inputs, exits) {
                    const result = `Hello, ${inputs.name}!`;
                    return exits.success(result);
                   }
                }
    * Globals
        * it is global scop variable.
        * 
    * File uploads
        * in front 
            * from method action enctype="multipart/form-data"
                * input type="file" name="file"
        * req.file('file').upload({
            dirname: "path to upload"\
            maxBytes: 10000
        },
            function(err, file) {
                if(err) log(err);
                res.json({"status": "file upload successfully", "file" , file}); 
        })
        * by default it upload in tem/upload
        * Uploading to Mongo GridFS
            * req.file('avatar').upload({
              * adapter: require('skipper-gridfs'),
              * uri: 'mongodb://[username:password@]host1[:port1][/[database[.bucket]]'
            }, function (err, filesUploaded) {
              if (err) return res.serverError(err);
              return res.ok();
            });
    * middleware
        * it is function which take (req, res ,next) ,
        * it run next() function on place of next()
        * when next() all function executed then 
        * it return back to next() place and then it run rest of the code
        * Eg: 
            function logger (req, res, next) {
                log("before"); //it run first
                next() // it run all next function
                log("after") // it run after next() function done
            }
                        

    

            

             

                
                
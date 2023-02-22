* # JWT 
    * jwt -> jsonwebtoken
    * setup
        * npm i jsonwebtoken
    * require
        * const jwt = require("jsonwebtoken")
        
    * set as a middle ware module
        * app.use(express.json())
        * 
    * apply jwt
        * app.post("/login , (req,res) => {
            const username = req.body.username
            const user = { name : username}

            // serialize user
            * const accessToken = jwl.sign(user, process.env.ACCESS_TOKKEN_SECRET)

            * res.json({accessToken: accessToken})
        })
    * in middleware
        * function authenticateToken( req, res, next) {
            const authHeader = req.headers['authorization']
            * //Bearer TOKEN 
            const token = authHeader && authHeader.split(" ")[1]
            
            if(token == null) return res.sendStatus(401)
            * //badrequest

            jwt.verify(token, process.env.ACCESS_TOKKEN_SECRET, (err, user) => {
                if(err) return res.sendStatus(403)
                req.user = user
                next()
            })
            // now in route we can get req.user to get user auth
        }

* # lodash
    * setup
        * npm i lodash
        * import _ from "lodash"
    * Array
        * const number = [1,2,3,4,5,6,7,8];
            * _.first(number)
            * _.last(number)
            * _.head(number)
            * _.nth(number, 6)
            * _.chunk(number, 2) // it create array of array of 2 element
                * return [[1,2],[3,4],[5,6],[7,8]]
            * _.difference(number,[1,4,5])
                * it return difference elements
            * _.drop(number, 4) // it remove first 4 elements
            * _.take(number, 4) // it take value not remove the elements
            * _.fill(Array(3),2) // it fills array with a default value (2)
            * _.flatten(num) // it return one level flat array
                * _.flattenDeep(num) // it return all level flat array 
                * _.flattenDepth(num) // it return nth deep level flat array.

        * _.union(c,d) // it return all element from c and d array.
        * -.intersection(c,d) // it return all common element from c and d array
    * collection
        * _filter()
        * _.each([1,2], function(value) {
            _.each({a: 1, b: 2}, function(value) {

            })
        }) //for each
        * _.include(array, value)
        * _.every(array, conditions ) // for all that conditions to be ture then it return ture , otherwise it false
        * _.some(array, conditions)
        * _.sortBy(array,[field1 , field2])
        * _.countBy(employees,"gender") // it return categories of gender count .
        * _.groupBy(employees,"gender") // it return group of elements of employee based of categories of gender values
        * _.orderBy(employees,"salary","desc")
            * const maxSalary = _.first(_.orderBy(employees,"salary","desc"))
            * const top3 = _.take(_.orderBy(employees,"salary","desc"), 3)
        * _.map(employee, "first_name") //it return firstname only
        * _.reduce(employee, (prev, curr) => prev + curr.salary, 0); // it return total salary.
        * group by total salary
            * const grpBYGender = _groupBy(employees, 'gender') // it return in map formate (key , value)
            * const totalSalaryByGender = _.map(grpBYGender, (grp) => _.reduce(grp, (prev, curr) => prev + curr.salary, 0)) // it return total of each group 
    

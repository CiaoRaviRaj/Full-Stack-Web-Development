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
            })
        }


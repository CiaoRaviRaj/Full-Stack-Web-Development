- Programming language for a interactive website
- creating graphics animation 2D amd 3D.
- API
- javascript is automated in garbage collection
- • It use reachability/unreachability concept.
-

- Documents.querySelector("h1"
  •
- Variables

      * Let
      * const
      * ver

      * DataType
          * String
                 • String are immutable
                 •  let str = ' Hi ';
                 •  str[0] = 'h'; // error
                 •  to do so
                 •  let str = 'Hi';
                 •  str = 'h1' + str[1]; // correct
                 •
                 • " " vs ` `
                    ` able to work in multiple lines
                      Just enter its work
                 • \n for next line
                 • \r\n combine work as \n
                 • \t for tab
                 • \b for backspace
                 • \f for form feed
                 • \v for from vertical Tab
                 • \",\',\`,\\,

                 • accessing
                    str[0]
                    str.at[-1] can use - value
                 • changing case
                    • str.toUpperCase();
                    • str.toLowerCase();
                 • Searching for a substring
                    • str.indexOf(substr, pos); //pos : count:2
                 •
                 • includes, startsWith, endsWith
                      • str.includes('id', pos);
                      • str.startsWith("wid"));
                      • str.endsWith("get"));
                      •
                 • getting a substring
                      • str.slice(start [ , end ) ); // - value ok

                       • str.slice(6, 2) // empty string ""
                       • str.substring(6,2) // swap srt & end
                          value

                      • str.substr(start , length);

                   •  comparing string
                       • comparing position in UTF-16
                       • ('a' > 'Z') //true

                       • "Z".codePointAt(0); // to find position
                       • String.fromCodePoint(i); //to create
                          str

                       • comparing according to language
                           • str.localeCompare(str2); //0,1,-1
                      •
                      •
          * Number
          * Boolean
          * Array
                 • order collections with any type of data.

                  • let arr = new Array();
                  • let arr = [];

                  • let fruits = ["fruits", "","",{name}];
                  • fruits [2];
                  • fruits [1] = 'me';
                  • fruits [3].name; // anytype of data
                  • fruits [fruits.length - 1] or .at[-1]
                  • fruits.length
                 • pop/push and shift/unshift
                     • Queue: push / shift
                     • stack: push/pop
                 • iteration
                     • for .... of .. // return specific value ,not
                         index with all properties.
                         value
                     •  for ...in ... // Return index value. With
                         every thing
                 • multidimensional arrays
                     • let matrix = [
                          [],
                          [],
                     ];
                     matrix[1][1];
                 • toString
                    •
                 • comparing array with === not ==
                    • object convert to primitive if any
                       argument have primitive .
                 •
            • Object
            • map and set
                 • map.set(key, value)
                 • map.get(key)
                 • map.has(key)
                 • map.delete(key)
                 • map.clear() // everything
                 • map.size() // count of elements
                 • iteration
                     • map.keys()
                     • map.values()
                     • map.entries() // just map (same)
                     • for .... of ...
                     • map.forEach((value, key, map) => { }
                 • map can have arrays or object
                     • let map = new Map([ ///for array
                          ['1' : ""],
                        ]
                     • for object entries
                        let map = new
                         Map(Object.entries(obj...));

                     • from array to object entries
                         • give array it creat object from it.
                         let map = new
                         Map(Object.fromEntries([])

                     •
             • Set
                 • uquic value ( without key)
                 • in behid using arr.find() to check
                   duplicate
                 • new Set()
                 • set.add(value)
                 • set.delete(value)
                 • set.has(value)
                 • set.clear()
                 • set.size

                 • iterators
                     • for.... of ...
                     • forEach
                     • set.keys()
                     • set.values()
                     • set.entries()// set
                 •
             •
             • weak set and weak map
                 Deal with object only
                 • weakSet
                      • const ws = new WeakMap();
                      • Used to store only objects.
                      • not iterable
                      • ws.has(obj1);
                      • ws.delete(obj1);
                 • weakMap
                      • const wm = new WeakMap();
                      • Used to store only objects.
                      • not iterable
                      • wm.has(obj1);
                      • wm.delete(obj1);
                 •
            •
       •

  • Operators
  • +,-,\*,/
  • = ,===, !==
  •
  •

- Functions
  - function multiply(num1, num2) {
    let result = num1 \* num2;
    return result;
    }
  - multiply (2, 3);
  - Methods
    - fucntion.call() //function borrowing
      We can use function from other object
      Or we set this refer to a function .
      Function.call( objectname, argu );
    - Function.apply
      Same as call but it different in passing agru
      Function.apply(obj, ["array", "List"]);
    - Function.bind
      Let func = function.bind(obj,props, ,);
      It create copy of fucntion as fucnthat
      invoke later.
      now we can use
      fucn(); to run this fucntion
      • \* Events
      • .addEventListener("click", fucntion () {
      alert("alert! ");
      }
      • .setAttribute("src" , "....image.png");
- localStronge
  • getItem('name')
  • setItem('name', 'hhhh');
- objects

    - Object
    •
    • const person = {}
    • person {
    } on fetching
    • Object can have anytype of data
    • object reference and copy
    • Let a = {};
    • let b = a; // copy the reference of obj a.
    • cloning and merging //referencing
    • object.assign(user, obj1, obj2);
    • const obj = object.assign(obj2, obj3);
    • StructuredClone
    • //not reference (independent obj)
    • let clone = structuredClone(user);

        • Dot notation
             • To trace sub-childs

        • Bracket notation
              • Instead of Dot you can use bracket.
              •
        • Thi keyword
              •
        • object Contructor
              • it is used used to construct object of
                  same type.
              • fucntion car(brand, model, color) {
                     This .brand= brand;
                     This.model = model;
                     This.color = color;
              }
              • Var cardetail= new Car( 'maruti' , 'shift',
                   'white');
              • you can add extra features / method for
                 also.
               • Object.getprototypeOf(myObject);
               • Object.create(personPrototype);
               • Object.assign(person.prototype,
                   perosnPrototype);
               • Object.hasOwn(peroson, 'name')

    - Symbol ()
    • Uquic value always, no confilt , no
    override issues.
    • Id.toString()
    • id.description
    • Symbol (' label');// for debugging
    • const sym1 = Symbol ("cat");
    • used for identifier
    const idSym = Symbol ('id');
    user[idsym] = 1234678; uncomfilicting
    things.
    User = {
    [IdSym] = 2245950;
    }
    • it is not own propery of object.
    user
    user{... not idSym show}
    user.getOwnPropertySymbols(user)
    To get symbol.
    Symbol(id)

             • use for Symbol
                  const sym1 = symbol.for('cat');
                  Const sym2 = symbol.for('cat');
                  sym1 === sym2
                  True

        •

    - Object prototypes
    • it is use for inherit properties from other
    • it used to add extra **proto** object value
    of a object
    • Prototype is less like inheritance and more
    like delegation.
    • Delegation: it is programming patterns
    Inwhich an object can perform task
    itself or ask other object to perform
    tasks
    • Ex:
    • Car.prototype.modelNo = '2021'
    • we get data in **proto** { }
    • we also add some inherit fucntion into
    it.
    •
    •
    - Object-oriented programming
    •
    • class Person
    • Properties
    • Methods
    • Contructor
    • inheritance
    • class Professor extends Person {
    Contructors (name, teacher){
    super(name);

                    }
                }
        • Encapsulation
             • private let name
             • only access by components within the
                class only
             • We make getter and setter method to
                to Modified it.
             •
        • OOPS
            • Class and Object can have separate
               Contructors
            • Contructors and prototype cam be used
               to implement class-based OOPs pattern.
            •
         • Object to primitive conversion
            • Conversion rules
                • object -> true in a boolean mostly
                • numeric conversion -> object
                   subtracting object .
                • String conversion -> when we make
                   alert(obj)
                • Three version
                      • Object to string
                      • object to number
                      • default case
                • Symbol.toPrimitive
                     • var obj2 = {
                            [Symbol.toPrimitive](hint){
                                  if (hint == 'number')
                                      return 100;
                                  else if (hint == 'string') {
                                      return 'hello'
                                  } else
                                      return ture; //default type
                            }
                        };
                • obj[Symbol.toPrimitive](hint){ ... } //
                     //Exit condition
                • obj.toString(){... }  //Hint is string
                • obj.tovalueOf() { } // hint is No./Default

         •

    - Classes
    • Contructors
    • Ommitting Contructors
    •
    • Inheritance
    • class Professor extends Person {
    Contructors (name, teacher){
    super(name);
    }
    }
    • conts object = new Professor ('name',
    'science ');
    •
    • Encapsulation
    •
    •
    - Json
    • JSON text like javascript object
    • string with specified data format
    • Array as JSON
    • API fatching
    • requestedURL, Request , fetch () ,
    response , json
    • appendChild
    • parse(), stringify()
    •

- Data Type method
  • Primitive data type method
  • str.toUpperCase()
  • str.toLowerCase
  • n.toFixed(2) // round to 2 digits
  • typeof value
  • null/undefined.test// error it has no method
  •  
   • Number
  • let billion = 1000000000
  • let billion= 1_000_000_000 /seperator
  • let billion = 1e9 // e9 = 1000000000
  • let mcs = 1e-6 // 0.000001
  • hexadecimal: used for color
  • num.toString(base)
  base = 16 used for color
  Base = 2 used for debugging bitwise
  Base= 36 used for 0..9 or A..Z to convert
  a large screen  
   • Rounding
  • Math.floor:- round to lower value
  • Math.ceil :- round to larger value
  • Math.round :- round to near end
  • Math.trunc :- just remove decimal
  •
  • Imprecise
  • 64 bits : over
  • 1e500 overflow
  • fraction is used to tofixed (2) always
  Other it give error
  0.1 + 0.2 === 0.3 /// false
  (0.1 + 0.2).toFixed(2) === 0.3 // true

                •
           • isFinite / isNaN
                NaN
                • Conver it to num then compare to NaN
                • alert( NaN === NaN) / false

                • isFinite
                    Reguale num true
                    Else false on NaN/Infinity
                •
           • parseInt and parseFloat
           • Other fucntion
                • MATH.random()
                • Math.max/min(....)
                • Math.pow(2,10)
                •
           •

  • String

  • Arrays
  •
  •

- Iterables
  • It is inbuilt iteration(for loop) method
  • it is used build custom method for iterators
  • primitive method
  Symbol.iterator () // fucntion of obj arr iterator
  with only have one fucntion
  .next()
  • itfn.next();
  Done : false,
  Value: 1,
  • let Number [Symbol.iterator] = () => {
  let nextValue = 10;
  return {
  next: fucntion () {
  nextValue++;
  done: nextValue > 15 ? ture : false,
  Value: nextValue // custom value
  }
  }
  }
- object fresh / object.li

* Promises, async/await
    * callbacks
    * Promise
        * It is simple like promise in real life
        * you commit a promise 
            Either it
            * Resolve
            * Reject
        
        * let p = new Promise((resolve, reject) => {
            let a = 1 + 1
            if (a == 2) {
                //resolve fucntion run resolve
                resolve('success')
            } else {
                //resolve fucntion run reject
                reject('failed')
            }
        })
        * Most used formate
            * p.then ((message) => {
                //message value from resolve function
                console.log('this is resolved' + message);
            }).catch((message) => {
                //message value from reject function
                console.log('this is rejected' + message);
            })
        * Promise.all([
            //Run all promises and return all
            promise1,
            promise2,
            promise3
        ]).then((messages) => {

        }).catch((messages)=>{

        })

        * Promise.race([
            //Run all promises and return one which completed first.
            promise1,
            promise2,
            promise3
        ]).then((messages) => {

        }).catch((messages)=>{

        })


    * Promises chaining
    * Error handling with promises
    * Promise API
    * Promisification
    * Microtasks
    * Async/await
        *   make promise Better.
        1.  async A function need await 
                await api()
        *   to manage error
            *   try {
                All error 
            } catch (err) {
                all error detail
            }

* Fetch API
    *   fetch("APIUrl", {
            method: 'POST'
            headers: {
                'Content-Type': 'application/json'
            }
            body: JSON.stringify({
                name: 'user 1' 
            })
        })
            .then(res => {
                if(res.ok) {
                    res.json()
                } else {
                   console.log("unsuccessful) 
                }
                
            })
            .then(data => console.log(data));
            .catch(error => console.log('ERROR')) //Catch statement is going to run only fetch method get error(network error). It is not doing to anything about api status

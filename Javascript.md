# Javascript

## Introduction

- Programming language for an interactive website
- creating graphics animation 2D amd 3D.
- API
- javascript is automated in garbage collection
  - It use reachability/unreachability concept for garbage collection

## DOM

- Documents.querySelector("h1")

## Variables

- Let
- const
- var
  - var is access across the module but let and const are not access before it declaration.
  - var amd let can update their values . But const variables do not change their value.

## DataType

### String

- **String are immutable**
  - let str = ' Hi ';
  - str[0] = 'h'; // error
  - to do so
    - let str = 'Hi';
    - str = 'h' + str[1]; // correct
- " " vs ` `
  - ` ` able to work in multiple lines
    - Just enter its work
  - \n for next line
  - \r\n combine work as \n
  - \t for tab
  - \b for backspace
  - \f for form feed
  - \v for from vertical Tab
  - \",\',\`,\\,\* \* accessing
- **Access value by its index**
  - str[0]
  - str.at[-1] can use - value for access from back
- **To change case**
  - str.toUpperCase();
  - str.toLowerCase();
- **Searching for a substring**
  - str.indexOf(substr, pos); // pos : count:2
  - **includes, startsWith, endsWith**
    - str.includes('id', pos);
    - str.startsWith("wid"));
    - str.endsWith("get"));
- **getting a substring**
  - str.slice(start , end ); // - value ok
  - str.slice(6, 2) // empty string ""
  - str.substring(6,2) // swap srt & end value
  - str.substr(start , length);
- **comparing string**
  - comparing position according UTF-16
  - ('a' > 'Z') //true
  - "Z".codePointAt(0); // to find position
  - String.fromCodePoint(code1, code2); //to create str
  - comparing according to language
    - str.localeCompare(str2); //0,1,-1

### Number

### **Boolean**

### **Array**

- order collections with any type of data.
- **Declaration**
  - let arr = new Array();
  - let arr = [];
  - let arr = new Array(element1, element2);
  - let fruits = ["fruits", "","",{name}];
- **Access value and change**

  - fruits [2];
  - fruits [1] = 'me'; // change value at index 1
  - fruits [3].name;
  - fruits [fruits.length - 1] or .at[-1]
  - **pop/push and shift/unshift**
    - Queue: push / shift
    - stack: push/pop
  - I**teration**
    - for .... of .. // return specific value of that array
    - for … in // return key value from an object.
    - array.indexOf
  - **multidimensional arrays**

    ```jsx
    let matrix = [[], []];

    matrix[1][1];
    ```

  - toString
  - comparing array with === not ==
    - object convert to primitive if any argument have primitive .

### Object

### Map

- map.get(key)
- map.has(key)
- map.delete(key)
- map.clear() // everything
- map.size() // count of elements
- **iteration**
  - map.keys()
  - map.values()
  - map.entries() // just map (same)
  - for .... of ...
  - map.forEach((value, key, map) => { }
- **map can have arrays or object**
  - let map = new Map([ ///for array
    ['1' : ""],
    ]
  - for object entries
    - let map = new Map(Object.entries(obj...));
  - from array to object entries
    - give array it create object from it.
      - let map = new Map(Object.fromEntries([])

### **Set**

- uqunic value ( without key)
- in behid using arr.find() to check duplicate
- new Set()
- set.add(value)
- set.delete(value)
- set.has(value)
- set.clear()
- set.size
- **iterators**
  - for.... of ...
  - forEach
  - set.keys()
  - set.values()
  - set.entries() // set
  - weak set and weak map Deal with object only
    - weakSet
      - const ws = new WeakMap();
      - Used to store only objects.
      - not iterable
      - ws.has(obj1);
      - ws.delete(obj1);
    - weakMap
      - const wm = new WeakMap();
      - Used to store only objects.
      - not iterable
      - wm.has(obj1);
      - wm.delete(obj1);

### Objects

### Object

- const person = {}
- person {} on fetching
- Object can have any type of data
- Object reference and copy
- let a = {};
- let b = a; // copy the reference of obj a.
- Cloning and merging //referencing
  - object.assign(user, obj1, obj2);
  - const obj = object.assign(obj2, obj3);
- StructuredClone
  - //not reference (independent obj)
  - let clone = structuredClone(user);
    - Dot notation
      - To trace sub-childs
    - Bracket notation
      - Instead of Dot you can use bracket.
    - Thi keyword
- Object Contructor

  - it is used used to construct object of same type.

  ```jsx
  fucntion car(brand, model, color) {
    This .brand= brand;
    This.model = model;
    This.color = color;
  }

  ```

  - Var cardetail= new Car( 'maruti' , 'shift', 'white');
  - you can add extra features / method for also.
  - Object.getprototypeOf(myObject);
  - Object.create(personPrototype);
  - Object.assign(person.prototype, perosnPrototype);
  - Object.hasOwn(peroson, 'name')

### Symbol ()

- unique value always, no confilt , no override issues.
- Eg:

  ```jsx
  const sym1 = Symbol();
  const sym2 = Symbol("foo");
  const sym3 = Symbol("foo");

  Symbol("foo") === Symbol("foo"); // false

  const same1 = Symbol.for('cat')
  const same2 = Symbol.for('cat')

  same1 === same2 // true, it is added one at global scope

  user cases
  1. const user = {
  		id: 23355,
  		....
  	}
  	user[id]: 565655656565
  	// any one can change it any time
  	But if you have
  		const sym1  = Symbole('id')
  		const user = {
  			id:78956223
  			[sym1]: 4556665566
  		}

  		user[sym1] = 1233 // error


  ```

- Id.toString()
- id.description
- it is not own propery of object.
  - user{... not idSym show}
  - user.getOwnPropertySymbols(user)
- To get symbol.
  - Symbol(id)
- **Object prototypes**
  - it is use for inherit properties from other.
  - it used to add extra **proto** object value of a object.
  - Prototype is less like inheritance and more like delegation.
  - Delegation: it is programming patterns In which an object can perform task itself or ask other object to perform tasks.
    Ex:
  - Car.prototype.modelNo = '2021'
    - we get data in **proto** { }
    - we also add some inherit fucntion into it.

### Object-oriented programming

- class Person
- Contructor
  - inheritance
- **Properties**
- **Methods**
- Ex
  ```jsx
  class Professor extends Person {
  	super(name); // the name parameter is used for the parent class
  }
  ```
- **Encapsulation**
  - private let name
  - only access by components within the class only
  - We make getter and setter method to Modified it.
- OOPS
  - Class and Object can have separate Constructors
  - Constructors and prototype can be used to implement class-based OOPs pattern.
- Object to primitive conversion

  - Conversion rules

    - object -> true in a boolean mostly
    - numeric conversion -> object subtracting object
    - String conversion -> when we make alert(obj)
    - Three version
      - Object to string
      - object to number
      - default case
    - Symbol.toPrimitive

      ```jsx
      var obj2 = {
        [Symbol.toPrimitive](hint){
      		 if (hint == 'number') return 100;
      		 else if (hint == 'string') return 'hello'
           else return ture; //default type
        }
      };

      console.log(+obj2); // 10        — hint is "number"
      console.log(`${obj2}`); // "hello"   — hint is "string"
      console.log(obj2 + ""); // "true"    — hint is "default"

      obj.toString(){... }  //Hint is string
      obj.tovalueOf() { } // hint is No./Default
      ```

## Classes

- Constructors
- Ommitting Constructors
- Inheritance
- Eg:
  ```jsx
  class Professor extends Person {
    Constructors(name, teacher) {
      super(name);
    }
  }
  ```
  - const object = new Professor ('name', 'science ');
  - Encapsulation

## JSON

- JSON text like javascript object
- string with specified data format
- Array as JSON
- API fetching
- requestedURL, Request , fetch () ,response , json appendChild
- parse(), stringify()

### Data Type method

- Primitive data type method
- str.toUpperCase()
- str.toLowerCase()
- n.toFixed(2) // round to 2 digits
- typeof value
- null/undefined.test// error it has no method

### **Number**

- let billion = 1000000000
- let billion= 1_000_000_000 /seperator
- let billion = 1e9 // e9 = 1000000000
- let mcs = 1e-6 // 0.000001
- hexadecimal: used for color
- num.toString(base)
- Base = 16 used for color
- Base = 2 used for debugging bitwise
- Base= 36 used for 0..9 or A..Z to convert a large screen
- **Rounding**
  - Math.floor:- round to lower value
  - Math.ceil :- round to larger value
  - Math.round :- round to near end
  - Math.trunc :- just remove decimal
  - n.toFixed(2) // round to 2 digits
- **Imprecise**
  - 64 bits : over
  - 1e500 overflow
  - fraction is used to tofixed (2) always
  - Other type of error
    - 0.1 + 0.2 === 0.3 /// false
    - (0.1 + 0.2).toFixed(2) === 0.3 // true
  - isFinite / isNaN
    - NaN
      - Convert it to num then compare to NaN by using isNaN
      - alert( NaN === NaN) / false
    - isFinite
      - Regular num true
      - Else false on NaN/Infinity
  - parseInt and parseFloat
    - it is used to extract number from an integer
  - Other function
    - MATH.random()
    - Math.max/min(....)
    - Math.pow(2,10)

### String

### Arrays

### Functions

- **Declarative**
  - function multiply(num1, num2) {
    let result = num1 \* num2;
    return result;
    }
  -
- **Calling**
  - multiply (2, 3);
- **Methods**
  - function.call() //function borrowing
    - We can use function from other object Or we set this refer to a function .
    - Function.call( objectname, argu );
  - Function.apply
    - Same as call but it different in passing agru.
    - Function.apply(obj, ["array", "List"]);
  - Function.bind
    - Let func = function.bind(obj,props, ,);
    - now we can use
      - fucn(); to run this fucntion

### Events

- Query.addEventListener("click", fucntion () {
  alert("alert! ");
  Query.setAttribute("src" , "....image.png");
  }

### Operators

- - ,- ,\ ,\* , /
- = ,===, !==

### javascript Browser Storage

- **Cookies**
  - it available in all tab for a website
  - manually set expires
  - storage location Browser and Server
  - send with requests
  - To set
    - document.cookie = 'name=Kyle; expires=' + newData(9999,0,1).toUTCString()
  - To view
    - log(document.cookie)
- Local Storage
  - setItem('name', 'hhhh');
  - getItem('name')
- Session Storage
  - it available in only particular tab for a website.
  - expire is on tab close

### Intersection

### Promises, async/await

- callbacks
- **Promise**

  - It is simple like promise in real life
  - you commit a promise
    - Either it
      - Resolve
      - Reject

  ```jsx
  let p = new Promise((resolve, reject) => {
    let a = 1 + 1;
    if (a == 2) {
      //resolve fucntion run resolve
      resolve("success");
    } else {
      //resolve fucntion run reject
      reject("failed");
    }
  });

  p.then((message) => {
    //message value from resolve function
    console.log("this is resolved" + message);
  }).catch((message) => {
    //message value from reject function
    console.log("this is rejected" + message);
  });
  ```

  - **promise.all**
    ```jsx
    Promise.all([
      //Run all promises and return all
      promise1,
      promise2,
      promise3,
    ])
      .then((messages) => {})
      .catch((messages) => {});
    ```
  - **promise.race**
    ```jsx
    Promise.race([
      //Run all promises and return one which completed first.
      promise1,
      promise2,
      promise3,
    ])
      .then((messages) => {
        // it return response in the form of array
      })
      .catch((messages) => {});
    ```
  - Promises chaining
  - Error handling with promises
  - Promise API
  - Promisification
  - Microtasks
  - **Async/awai**t
    - make promise Better.
    - async A function need await
      - await api()
    - to manage error
      ```jsx
      try {
         All error occur here
      } catch (err) {
         all error detail manage error
      }
      ```

### DOM Manipulation

- A**dding element to a page**
  - const body = document.body
  - body.append("Hello World")
    - you can add string
    - it can pass multiple element
  - body.appendChild(node)
    - it one at one time
  - append a element
    - const dic = document.createElement("div")
      - it create a reference for a element
    - dic.innerText = "Hello World"
      - adding text inside div element
      - it return text like show in doc in DOC
    - dic.textContent = "Hello world2"
      - it preview total similar to indentation in code
    - body.append(dic)
- adding HTML TAG
  - div.innerHtml = "<strong>Hello world</strong>"
    - it security problem
    - anyone can manipulate doc
  - const strong = documentation.createElement("strong")
    - strong.innerText = "Hello world"
    - div.append(strong)
    - body.append(div)
- remove Html
  - dic.remove()
  - body.removeChild(dic) from parent
- attributes
  <span id="hi" title='title' data-test="it is test">
  - const spanHi = document.querySelect("#hi")
  - spanHi.getAttribute("id")
  - spanHi.id()
    - it also work
  - spanHi.setAttribute("id" , "hello")
  - spanHi.id = 'hello'
  - spanHi.removeAttribute("id")
  - spanHi.dataset()
    - it is return object of data set
    - spanHi.dataset.test()
      - return test data value
    - spanHi.dataset.test = "dddd"
      - to change value
- class
  - spanHi.classList.add("hi1")
  - spanHi.classList.remove("hi1")
  - spanH1.classList.toggle("hi1")
- style
  - spanHi.style.backgroundColor= "red"

### Fetch and api

```jsx
fetch("APIUrl", {
  method: 'POST'
  headers: {
     'Content-Type': 'application/json'
  },
  body: JSON.stringify({
       name: 'user 1'
  }),
})
.then(res => {
    if(res.ok) {
       res.json()
    } else {
        console.log("unsuccessful)
     }

})
.then(data => console.log(data));
.catch(error => console.log('ERROR', error)) //Catch statement is going to run only fetch method get error(network error). It is not doing to anything about api status

```

### WebRTC

- it is REAL TIME COMMUNICATION BETWEEN browsers.
- Data never touches server.
- WebSocket
  - real-time communication through the server.
- UDP policy to transfer data.
  - UDP is not a reliable protocol for transferring important data.
    - to receive data to the destination or not
  - No built-in signaling . we have to make connection then you connect with WebRTC.
  - SDPs
    - offer / answer
    - it is object contain address , media type , audio ..
  - ICE Candidate
    - it transfer public IP address and port for receiving data.
    - STUN SERVER to get its IP address and then it go to all STUN server user

# Notes

```markdown
- Iterables
  - It is inbuilt iteration(for loop) method
  - it is used build custom method for iterators
  - primitive method
  - Symbol.iterator () // fucntion of obj arr iterator with only have one fucntion
  - .next()
    • itfn.next();
    Done : false,
    Value: 1,
  - let Number [Symbol.iterator] = () => {
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
```

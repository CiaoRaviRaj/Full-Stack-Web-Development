What is design pattern ?
In software engineering, a software design pattern is a <i>general</i>, <i>reusable</i> solution to a commonly occurring problem within a given context in software design.
Design patterns are formalized best practices that the programmer can use to solve common problems when designing an application or system.

<h3>Null Object Pattern</h3>
    Usage
        It is going to use when we have a null object return.
        check if(null) every time every where
        To Avoid it
            1. Make Object/Class a similar properties named as NullObjectName/NullClass. (Eg. NullUser)
            2.  Inside fetching function
                function getUser (id) {
                    const user = users.find(user => user.id === id) ;
                    if (user == null) {
                        return new NullUser()
                    } else {
                        return user;
                    }
                }

- Builder Pattern

  - Usages
    It is use when we work with complex objects where so many inter depended elements, some are optional are going to combine to make a single object.
    example:
    class Address {
    constructor(zip, street) {
    this.zip = zip
    this.street = street
    }
    }
    class User {
    constructor(name, age, phone, address) {
    this.name = name
    this.age = age
    this.phone = phone
    this.address = address
    }
    }
    const user = new User('Bob', undefined, undefined, new Address('12345', 'Main St.'))
    // To set only address is so difficult to set
    Traditional Method

          //required field add in normal class
          class User {
              constructor(name) {
                  this.name = name
              }
          }
          // We are going to use UserBuild class to build user object.
          class UserBuilder {
              constructor(name) {
                  this.user = new User(name)
              }
              //Optional field is set by that field set function and then it return this to userBuildClass.
              setAge(age) {
                  this.user.age = age
                  return this
              }

              setPhone(phone) {
                  this.user.phone = phone
                  return this
              }

              setAddress(address) {
                  this.user.address = address
                  return this
              }

              build() {
                  return this.user
              }
          }

          const builder = new UserBuilder('Bob')
          const user = builder.setAddress(new Address('12345', 'Main St.')).build()

          Modern Method (Javascript Method)
              It is done by optional parameter passing technic

              class User {
                  //If user do not pass any optional field value then we pass {nullObject}
                  //we set default value by pass default value in params.

                  constructor(name, { age, phone = '123-456-7890', address } = {}) {
                      this.name = name
                      this.age = age
                      this.phone = phone
                      this.address = address

                  }
              }

              let user = new User('Bob', { address: new Address('12345', 'Main St.') })

- Singleton Pattern

  - Usage
    When we want to share an single instant among different child components
  - example
    export default class FancyLogger {
    constructor() {
    this.logs = []
    }

          log(message) {
              this.logs.push(message)
              console.log(`FANCY: ${message}`)
          }

          printLogCount() {
              console.log(`${this.logs.length} Logs`)
          }

    }

    //whenever child want to create a object of that class that object is totally different object among all instant.

    To fix we are going to use singleton pattern.

    class FancyLogger {
    constructor() {
    //FancyLogger is variable that use to count class instance.
    if (FancyLogger.instance == null) {
    this.logs = []
    FancyLogger.instance = this
    }
    return FancyLogger.instance
    }

          log(message) {
              this.logs.push(message)
              console.log(`FANCY: ${message}`)
          }

          printLogCount() {
              console.log(`${this.logs.length} Logs`)
          }

    }
    //That create the only instance of object.
    ////That we are going to pass among different component.

    const logger = new FancyLogger()

    //That restrict to change function and constructor structure or add something new .
    Object.freeze(logger)

    export default logger

    //After that we are going to import logger to child components.
    //And we are going to access or use single object instant among everyWhere

- Facade Pattern

  - It is going to useful when we have a section of code which is used in many place and deffer in some value .
    example : fetchApi
    function getUsers() {
    return fetch('https://jsonplaceholder.typicode.com/users', {
    method: "GET",
    headers: { "Content-Type": "application/json" }
    }).then(res => res.json())
    }

        function getUserPosts(userId) {
            return fetch(`https://jsonplaceholder.typicode.com/posts?userId=${userId}`, {
            method: "GET",
            headers: { "Content-Type": "application/json" }
            }).then(res => res.json())
        }

        getUsers().then(users => {
            users.forEach(user => {
                getUserPosts(user.id).then(posts => {
                    console.log(user.name)
                    console.log(posts.length)
                })
            })
        })

  - To avoid fetch repetition, we just make a function to do so using Facade pattern
    function getUsers() {
    return getFetch('https://jsonplaceholder.typicode.com/users')
    }

    function getUserPosts(userId) {
    return getFetch('https://jsonplaceholder.typicode.com/posts', {
    userId: userId
    })
    }

    getUsers().then(users => {
    users.forEach(user => {
    getUserPosts(user.id).then(posts => {
    console.log(user.name)
    console.log(posts.length)
    })
    })
    })

    // That getFetch manage all the fetch request

    // function getFetch(url, params = {}) {

    //Object.defineProperties(params)
    //{user: 1}
    //Object.entries(params) : return object as array.
    //[[userId, 1]]

    // const queryString = Object.entries(params).map (param => {
    // return `${param[0]}=${param[1]}`
    // }).join('&')
    // return fetch(`${url}?${queryString}`, {
    // method: "GET",
    // headers: { "Content-Type": "application/ json" }
    // }).then(res => res.json())
    // }

    //We just change the implementation by just doing this it change every where.
    function getFetch(url, params = {}) {
    return axios({
    url: url,
    method: "GET",
    params: params
    }).then(res => res.data)
    }

- Command Pattern

  - Usages
    When we have a set functions in a class,And then we are going to add undo feature and adding mix commands from it, then it is going to use.

  - Before
    //calculator app code
    class Calculator {
    constructor() {
    this.value = 0
    }

        add(valueToAdd) {
          this.value = this.value + valueToAdd
        }

        subtract(valueToSubtract) {
          this.value = this.value - valueToSubtract
        }

        multiply(valueToMultiply) {
          this.value = this.value * valueToMultiply
        }

        divide(valueToDivide) {
          this.value = this.value / valueToDivide
        }

    }
    // not reusable code
    // No undo feature
    // when ever we want to add and multiply next to it , then we wright new function. it is going to very easy to make combine command.

  - After

    class Calculator {
    constructor() {
    this.value = 0
    // previous calculation result used to undo
    this.history = []
    }

          // Given command executed with the value given to current value.

          executeCommand(command) {

              this.value = command.execute(this.value)

              //We push updated result in undo state array.
              this.history.push(command)
          }

          undo() {
              //Similarly for undo ,do pop from array. that delete and return latest command with value.
              const command = this.history.pop()

              //  Applied undo with that command and value to it.
              this.value = command.undo(this.value)
          }

    }

    // Reusable function for ADD
    class AddCommand {
    constructor(valueToAdd) {
    this.valueToAdd = valueToAdd
    }

        execute(currentValue) {
          return currentValue + this.valueToAdd
        }

        undo(currentValue) {
          return currentValue - this.valueToAdd
        }

    }

    // Reusable function for Subtraction
    class SubtractCommand {
    constructor(valueToSubtract) {
    this.valueToSubtract = valueToSubtract
    }

        execute(currentValue) {
          return currentValue - this.valueToSubtract
        }

        undo(currentValue) {
          return currentValue + this.valueToSubtract
        }

    }

    // Reusable function for Multiplication
    class MultiplyCommand {
    constructor(valueToMultiply) {
    this.valueToMultiply = valueToMultiply
    }

        execute(currentValue) {
          return currentValue * this.valueToMultiply
        }

        undo(currentValue) {
          return currentValue / this.valueToMultiply
        }

    }

    // Reusable function for Divide

    class DivideCommand {
    constructor(valueToDivide) {
    this.valueToDivide = valueToDivide
    }

        execute(currentValue) {
          return currentValue / this.valueToDivide
        }

        undo(currentValue) {
          return currentValue * this.valueToDivide
        }

    }

    // combine ADDthenMultiply
    // this is use in case like save , exit ,save and exit button.

    class AddThenMultiplyCommand {
    constructor(valueToAdd, valueToMultiply) {
    this.addCommand = new AddCommand(valueToAdd)
    this.multiplyCommand = new MultiplyCommand (valueToMultiply)
    }

        execute(currentValue) {
          const newValue = this.addCommand.execute        (currentValue)
          return this.multiplyCommand.execute(newValue)
        }

        undo(currentValue) {
          const newValue = this.multiplyCommand.undo      (currentValue)
          return this.addCommand.undo(newValue)
        }

    }

    const calculator = new Calculator();

    calculator.executeCommand(new AddCommand(10));

    calculator.executeCommand(new MultiplyCommand(10));

    calculator.undo()


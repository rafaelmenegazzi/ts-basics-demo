# ts-basics-demo
A quick hands-on guide to explore the basics concepts and uses of Typescript

## Step 1 - Project setup:

### Install typescript
```
# comand line
yarn init
yarn add -D typescript
```

### Add some project files
```
# command line
mkdir src
cd src
touch my-js.js
touch my-ts.ts
```

## Step 2: Compiler intro

### Using tsc
```
# my-js.js
console.log('oi from js')

# my-ts.ts
console.log('oi from ts')

# command line
tsc src/my-ts.ts
```

### Creating a tsconfig.json file
```
# comand line
tsc --init

# tsconfig.json
"compilerOptions.target": "es6",
"include": ["src"],
```

### Executing our code
```
# package.json
"scripts": {
    "run-js": "node src/my-js.js",
    "run-ts": "tsc && node src/my-ts.js"
  }

# command line
yarn run-js
yarn run-ts
```

## Setup 3: Exploring typescript features

### Type checking and intellisense
```
# my-ts.js

const z = 'Mene'
const greet = (name) => `Hi ${name}`
console.log(greet(z))
// z.toFixed()
// z.toUpperCase()

const x = 1  // play with 1 or '1'
const y = 2  // play with 2 or '2'
const add = (arg1, arg2) => arg1 + arg2
console.log(`${x} + ${y} = ${add(x, y)}`)
// x.toFixed()
// x.toUpperCase()

# my-ts.ts

const z : string = 'Mene'
const greet = (name : string) : string => `Hi ${name}`
console.log(greet(z))
// z.toFixed()
// z.toUpperCase()

const x : number = 1  // play with 1 or '1'
const y : number = 2  // play with 2 or '2'
const add = (arg1: number, arg2: number) : number => arg1 + arg2
console.log(`${x} + ${y} = ${add(x, y)}`)
// x.toFixed()
// x.toUpperCase()
```

### Type inference
```
# my-ts.ts

const z = 'Mene'
const greet = (name : string) => `Hi ${name}`
console.log(greet(z))
// z.toFixed()
// z.toUpperCase()

const x = 1  // play with 1 or '1'
const y = 2  // play with 2 or '2'
const add = (arg1: number, arg2: number) => arg1 + arg2
console.log(`${x} + ${y} = ${add(x, y)}`)
// x.toFixed()
// x.toUpperCase()
```

### Literal Types
```
# my-ts.ts

// Unions (and Intersection) Types
type Argument = number | string
let arg : Argument
arg = 10
arg = 'string'
// arg.toFixed()
// arg.toUpperCase()

type Product = 'flex' | 'food' | 'life'
let card : Product
// card = 'flex'
// card = 'go'
// card = 10

// Enum
enum CardTypes { flex = 180, food = 181, life = 182 }
let card2 : CardTypes
// card2 = CardTypes.flex

// Type Structure
type Person = {
  name: string, 
  age: number,
  greeting: () => string
}
let x : Person
x = {
  name: 'Mene',
  age: 20,
  greeting: () => 'Hi there',
}
// x.name

// Type Structure (Optional)
type Person2 = {
  name: string,
  age: number,
  greeting?: () => string
}
let y : Person2
y = {
  name: 'Mene',
  age: 20,
  // greeting: () => 'Hi there',
}
// y.name

// Type Structure (Readonly)
type Person3 = {
  readonly name: string,
  readonly age: number,
  readonly greeting: () => string
}
let z : Person3
z = {
  name: 'Mene',
  age: 20,
  greeting: () => 'Hi there'
}
// z.name = 'Não Mene'

// Type Function
type IGreet = (name: string) => string
const greet : IGreet = (name) => `${name}!`
```

### interfaces
```
# my-ts.ts

// Interface
type IGreeting = () => string

interface Person {
  readonly name: string,
  readonly age: number, 
  readonly greeting: IGreeting
}

class Employee implements Person {
  readonly name: string
  readonly age: number
  readonly greeting: IGreeting

  constructor(name: string, age: number, greeting: IGreeting) {
    this.name = name
    this.age = age
    this.greeting = greeting
  }
}

const x = new Employee('Mene', 30, () => `Bão!`)
// x.greeting()
// x.age = 31
```

## Setup 4: Using libraries with typescript

### Axios example
```
# command line
yarn add axios

# my-ts.ts

import axios, { AxiosRequestConfig } from 'axios'

const getPokemon = async (pokemon : string) => {
  const res = await axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
  // console.log(res)
  console.log(res.data)
}
// getPokemon(1234)
getPokemon('pikachu')

const getPokemon2 = async (pokemon : string, config? : AxiosRequestConfig ) => {
  const res = await axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemon}`, config)
  // console.log(res)
  console.log(res.data)
}
// getPokemon2('ditto', { name: '123' })
getPokemon2('ditto', {
  headers: { 'Content-Type': 'application/json' },
  timeout: 30000,
})
```


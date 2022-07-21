---
css: unocss
theme: geist

drawings:
  persist: true

highlighter: shiki
lineNumbers: false

layout: cover

info: |
  ## Software Design and Architecture
---

# Software Design and Architecture

Part II

Open slides here: https://sda.np-overflow.club

---

# Installation

Due to certain language limitations of Python, we'll be using ✨ Typescript ✨ for this workshop!

Please install the following:

1. [ ]  NodeJS & NPM [Install here](https://docs.volta.sh/guide/getting-started)
2. [ ]  Your favorite code editor [or VSCode](https://code.visualstudio.com)

---

# Tech support

* Don't panic, find help

<br/>

<v-click>
<div class="text-center text-blue-600 border-1 border-blue-500 rounded-sm font-semibold text-xl bg-blue-100">

Head over to `#tech-support` on our [Discord server](https://discord.gg/YB5925kr)

</div>
</v-click>


---

# Recap from last week

* Object-Oriented Programming (with Python 🐍)
* Creation patterns
  * Singleton
  * Abstract classes
* Structural patterns
  * Decorators
  * Bridges

<br/>

<v-click>
<div class="text-center text-red-600 border-1 border-red-500 rounded-sm font-semibold text-xl bg-red-100">

⁉ ️How can we use this in our code ⁉️

</div>
</v-click>

---

# Deep dive into OOP

* **SOLID** - 5 principles that compliments OOP
  * Also helps you write good code 👍 (maintainable, readable, understandable, flexible... developers good code)

| Character | Idea                            | Important |
|-----------|---------------------------------|-----------|
| S         | Single responsibility principle | ✅         |
| O         | Open closed principle           | ✅         |
| L         | Liskov substitution principle   | ✅         |
| I         | Interface segregation principle | ✅         |
| D         | Dependency inversion principle  | ✅         |

---

# Single responsibility principle

* Each class should only manage a **single** thing

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.ts`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `mouse.ts` 
```js
class Mouse {
    scroll() {
        console.log('wheeeeee')
    }
}
```

</div>
<div>

❌ `accessories.ts`
```js
class Accessories {
    type() {
        // ...
    }
    scroll() {
        // ...
    }
}
```

</div>
</div>

---

# Open closed principle

* Clases should be **open for *extension*** but **closed for *modification***

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.ts`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `rgb-keyboard.ts`
```js
class RGBKeyboard extends Keyboard {
    colors = ['red', 'green', 'blue']
    
    showFancyLights() {
        console.log(colors)
    }
}
```

</div>
<div>

❌ `keyboard.ts`
```js {all|2,7-9}
class Keyboard {
    colors = ['red', 'green', 'blue']
    
    type() {
        console.log('clang clang')
    }
    showRGB() {
        console.log('beep boop')
    }
}
```

</div>
</div>

---

# Liskov substitution principle

* If class `RGBKeyboard` is a subclass of `Keyboard`:
  * `RGBKeyboard` should be able to replace `Keyboard` without any side effects

<div grid="~ cols-2" gap="3">
<div>

`developer.ts`
```typescript
class Developer {
    keyboard: Keyboard
    constructor(keyboard: Keyboard) {
      this.keyboard = keyboard
    }
    
    writeCode() {
        this.keyboard.type()
    }
}
```

</div>
<div>

`main.ts`
```typescript {all|1-3|5-7}
const logitechKeyboard = new Keyboard()
const qinguan = new Developer(logitechKeyboard)
qinguan.writeCode() // Writes code with `Keyboard`

const razerKeyboard = new RGBKeyboard()
const jimmy = new Developer(razerKeyboard)
jimmy.writeCode() // Writes code with `RGBKeyboard`
```

</div>
</div>

---

# Interface segregation principle

* Interfaces (methods/properties of a class) should be split into their logical concerns
* For example, read vs writes to a database can be 2 interfaces, instead of a huge interface

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.ts`
```typescript
interface KeyboardDatabaseWriter {
    create(keyboard: Keyboard)
    update(keyboard: Keyboard)
    delete(keyboard: Keyboard)
}

interface KeybaordDatabaseReader {
  findByName(name: string)
  findByBrand(brand: string)
  findByPrice(price: string)
}
```

</div>
<div>

❌ `keyboard.ts`
```typescript
interface KeyboardDatabase {
  create(keyboard: Keyboard)
  findByName(name: string)
  findByBrand(brand: string)
  findByPrice(price: string)
  update(keyboard: Keyboard)
  delete(keyboard: Keyboard)
}
```

</div>
</div>

---

# Dependency inversion principle

* Dependencies should be on abstractions and not concretions
* Instead of depending on classes, which are "concrete" and contain implementation, use interfaces which only define methods & not implementation

<div grid="~ cols-2" gap="3">
<div>

`developer.ts`
```typescript
// Anything that I can type on is a keyboard!
interface Keyboard {
  type()
}
class Developer {
    keyboard: Keyboard // Depend on an interface
    constructor(keyboard: Keyboard) {
      this.keyboard = keyboard
    }
    writeCode() {
        this.keyboard.type()
    }
}
```

</div>
<div>

`main.ts`
```typescript
// Any class that has a `type()` method can be used

const logitechKeyboard = new Keyboard() 
const qinguan = new Developer(logitechKeyboard)
qinguan.writeCode() // Writes code with `Keyboard`

const razerKeyboard = new RGBKeyboard()
const jimmy = new Developer(razerKeyboard)
jimmy.writeCode() // Writes code with `RGBKeyboard`
```

</div>
</div>

---

# Applying SOLID with Clean Architecture

* Separate your program into layers
* Achieve a few objectives 
  * Independent of framework
  * Independent of user interface
  * Independent of database
  * Independent of external interfaces
  * Highly testable 

---

# Layers of Clean Architecture

| Layer                  | Purpose                                                |
|------------------------|--------------------------------------------------------|
| **Entity**             | Entities and their corresponding rules                 |
| **Use case**           | Service/business functions                             |
| **Interface adapter**  | Mapping/connecting our use cases to frameworks/drivers |
| **Frameworks/drivers** | Databases, HTTP handlers, user interfaces, etc         |

---
layout: iframe-right
url: https://app.sli.do/event/aBFgfQS8ZNRrYLJxxMzNhj/embed/polls/ae6f1842-b636-47fa-a5db-6e128bb8c492
---

# Activity time!

**Duration:** 10 minutes

**Task:** Find a real life application which you can apply Clean Architecture to

**Once done:** Submit to sli.do on the right!

---

# Practical time!

<v-clicks>

* Let's rewrite a program with Clean Architecture
* The program
  * [ ]  Has an HTTP API endpoint we can interact with
  * [ ]  Shows the keyboards in our collection
  * [ ]  When new keyboards arrive, add them to our collection
* Before we begin, we need a few things:
  1. Starter code [here](https://gitlab.com/-/snippets/2374405)
  2. API tester [here](https://hopp.sh/r/oBDUknNJGLrX)

</v-clicks>

<br/>

<v-click>
<div class="text-center text-green-600 border-1 border-green-500 rounded-sm font-semibold text-xl bg-green-100">

Open them on your laptop!

</div>
</v-click>

---
layout: center
---

# ⚠️ Demo on screen! ⚠️

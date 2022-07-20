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

✅ `keyboard.js`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `mouse.js` 
```js
class Mouse {
    scroll() {
        console.log('wheeeeee')
    }
}
```

</div>
<div>

❌ `accessories.js`
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

* Each class should only manage a **single** thing

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.js`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `mouse.js`
```js
class Mouse {
    scroll() {
        console.log('wheeeeee')
    }
}
```

</div>
<div>

❌ `accessories.js`
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

# Liskov substitution principle

* Each class should only manage a **single** thing

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.js`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `mouse.js`
```js
class Mouse {
    scroll() {
        console.log('wheeeeee')
    }
}
```

</div>
<div>

❌ `accessories.js`
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

# Interface segregation principle

* Each class should only manage a **single** thing

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.js`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `mouse.js`
```js
class Mouse {
    scroll() {
        console.log('wheeeeee')
    }
}
```

</div>
<div>

❌ `accessories.js`
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

# Dependency inversion principle

* Each class should only manage a **single** thing

<div grid="~ cols-2" gap="3">
<div>

✅ `keyboard.js`
```js
class Keyboard {
  type() {
    console.log('clang clang')
  }
}
```

✅ `mouse.js`
```js
class Mouse {
    scroll() {
        console.log('wheeeeee')
    }
}
```

</div>
<div>

❌ `accessories.js`
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


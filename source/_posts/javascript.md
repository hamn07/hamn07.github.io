title: javascript
date: 2017-03-26 06:08:39
tags: [js, javascript, dojo]

---

# ECMAScript

## delete object property immutably

```js
const {[businessToRemove.businessID]: _, ...updatedBusinesses} = savedBusinesses;
```

## compare array

# JSX

## 使用條件式產生Properties

```javascript
<KeyboardAvoidingView {...(Platform.OS === 'ios' && {behavior: 'padding'})}>
```

## 使用迴圈產生JSX elements

```javascript
<View style={tw`flex-1 justify-around`}>
  {notes.map(note => (
    <Text key={note.key}>{note.content}</Text>
  ))}
</View>
```

# Dojo Toolkit

> - with the 1.7 release Dojo adopted the **Asynchronous Module Definition (AMD)** format for its source code, allowing completely modular web application development.

> - `require` enables you to load modules and use them, while `define` allows you to define your own modules. A module is typically a single JavaScript source file.

## dojo/on

```js
require(["dojo/on"], function(on){
  on(target, "event", function(e){ /* who, "what", how */
    // handle the event
  });
});
```

## Closure

```js
define(function(){
    var privateValue = 0;
    return {
        increment: function(){
            privateValue++;
        },

        decrement: function(){
            privateValue--;
        },

        getValue: function(){
            return privateValue;
        }
    };
});
```

## Singleton

```js
define(function(){
    var privateValue = 0;
    return {
        increment: function(){
            privateValue++;
        },

        decrement: function(){
            privateValue--;
        },

        getValue: function(){
            return privateValue;
        }
    };
});
```

[Introduction to AMD Modules](https://dojotoolkit.org/documentation/tutorials/1.10/modules/)
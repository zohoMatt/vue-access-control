# v-access-control

## Introduction
`v-access-control` is an implementation of front-end access control on DOM/Component level. [Custom directive](https://vuejs.org/v2/guide/custom-directive.html) has been applied, in the form of v-access, to annotate accessible authorities on DOM/Component.
> On developing: access control of route level

## Install
`npm i v-access-control`  
or   
`yarn add v-access-control`

## Documentation
### Basic examples
#### Directive binding modifiers (shorthand)
``` html
<my-component v-access.AUTH1.AUTH2 {...otherProps}></my-component>
<div class="any-dom" v-access.AUTH1.AUTH2>
<!-- ... -->
</div>
```
By this annotation, this element will only display if user acquire AUTH1 **and** AUTH2.
#### Directive binding args (shorthand)
``` html
<my-component v-access:AUTH1|AUTH2 {...otherProps}></my-component>
<div class="any-dom" v-access:AUTH1|AUTH2>
<!-- ... -->
</div>
```
By this annotation, this element will only display if user acquire AUTH1 **or** AUTH2.

#### Value mode
In template:
```html
<my-component v-access="accessAllowed"></my-component>
<div class="any-dom" v-access="accessAllowed">
<!-- ... -->
</div>
```
In script:
```javascript
data() {
    return {
        accessAllowed: {
            access: ['AUTH1', 'AUTH2'],
            anyAccess: ['AUTH3', 'AUTH4']
        }
    }
}
```
Consequently, user who acquire AUTH1 and AUTH2 and **any one of** `AUTH3, AUTH4` will be allowed to observe this element.

### APIs
#### `options` in `Vue.use(VAccessControlPlugin, options)`
##### Type
```javascript
{
    // Use a factory function to return an array. In this way, userAuth is guaranteed to be up-to-date every time v-access lifecycle hooks are called.
    userAuthFactory: void => string[],
    router?: VueRouterObject
}
```
##### Example

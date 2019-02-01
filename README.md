# Coding guidelines for project

*A mostly reasonable approach to `JAVASCRIPT` and `React` and rules and that follow in `SARA`*

This style guide is mostly based on the standards that are currently prevalent in JavaScript and we have to follow 
in our project, although some conventions (i.e async/await, naming files)

## Table of Contents

1. [Basic Rules](#basic-rules)
1. [Naming](#naming)
1. [Decleration](#decleration)
1. [Alignment](#alignment)
1. [Spacing](#spacing)
1. [Quotes](#quotes)
1. [Props](#props)
1. [Refs](#refs)
1. [Parentheses](#parentheses)
1. [Callback Handlers](#callback-handlers)
1. [Methods](#methods)
1. [Common](#common)
1. [Create Routing](#create-routing)
1. [Creating Redux](#creating-redux)
1. [Seperate Form Comoponents](#seperate-form-components)
1. [Form Validators](#form-validators)


## Basic Rules

  - Only include one React component per file.
    - However, multiple [Stateless, or Pure, Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) 
    are allowed per file.
  - Always use JSX syntax In `React.JS` and use JS syntax in `React Native` for files, were using `.js` extension in `React     Native` if you want to enabled `.jsx` extension in react native make `rn-cli.config.js` inside of the root of your           project and place this code [See this](https://stackoverflow.com/questions/50311473/how-to-allow-react-native-to-enable-support-for-jsx-extension-files/53016425#53016425)
    ```
    module.exports = {
      /// @name Make ReactNative Great Again
      /// @description Allows you to enable support for JSX files, and `.mjs` files which is the new node standard
      /// @source http://www.fallingcanbedeadly.com/posts/enabling-react-native-jsx-extension
      /// @note One caveat, The `index.js` file in the root of your project has to be `.js`. 
      getSourceExts: () => [ 'jsx', 'mjs', 'js' ],
    }
    ```
    
## Naming

- **Extensions**: Use `.jsx` extension for React components in `React.JS` and use `.js` extension in `React Native`.
- **Filename**: Use `lisp-case` for filename . E.g., `login-container.jsx`.
- **Reference Naming**: Use `PascalCase` for React components and `camelCase` for their instances. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

    ```jsx
    // bad
    import loginContainer from './login-container';

    // good
    import LoginContainer from './login-container';

    // bad
    const LoginContainer = <LoginContainer />;

    // good
    const loginContainer = <LoginContainer />;
    ```
 - **variables**: Always use `camelCase` for defining varaible and its name must represent its value, and use let for          varaibles instead of var and use const for instant of components and and props that cannot be change.
    
    ```jsx
    // bad
    let obj = {
      firstName: 'Testing'
      lastName: 'user'
    }
    

    // good
    let userData = {
      firstName: 'Testing'
      lastName: 'user'
    }
    
    
    // bad
    let loginContainer = <LoginContainer />
    
   
    // good
    const loginContainer = <LoginContainer />
    ```
    
  - **Component Naming**: Use the filename as the component name. For example, `login-container.jsx` should have a                reference name of `LoginContainer`. However, for root components of a directory, use `index.jsx` as the filename            and use the directory name as the component name:

    ```jsx
    // bad
    import loginContainer from './Login/login-container.js';

    // bad
    import LoginContainer from './Login/index.js';

    // good (it will import index file in Login Folder)
    import LoginContainer from './Login';
    ```
    
  - **Props Naming**: Use `camelCase` when passing props to component and avoid using DOM component prop names for different      purposes.
     > Why? People expect props like `style` and `className` to mean one specific thing. Varying this API for a subset of your app makes the code less readable and less maintainable, and may cause bugs.
    
    ```jsx
    // bad
    <MyComponent style="fancy" />

    // bad
    <MyComponent className="fancy" />

    // good
    <MyComponent variant="fancy" />
    ```
    
## Decleration

   - Do not use `displayName` for naming components. Instead, name the component by reference and export component to last       lines of the files.
      > Why? when exporting component to seperate and last in the file it helps to bind component and to redux and other            libraries and it makes code more readable.
  
  
      ```jsx
      // bad
      export default React.createClass({
      displayName: 'ReservationCard',
      // stuff goes here
      });

      // bad
      export default class ReservationCard extends React.Component {
      }
    
    
      // good
      const ReservationCard = React.createClass({
        // stuff goes here
      });

      export defalut ReservationCard;

      // good
      class ReservationCard extends React.Component {
      }
    
      export defalut ReservationCard;
      ```
      
## Alignment

  - Follow these alignment styles for JSX syntax. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [`react/jsx-closing-tag-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)
  
  
  
    ```jsx
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // if props fit in one line then keep it on the same line
    <Foo bar="bar" />

    // children get indented normally
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>

    // bad
    {showButton &&
      <Button />
    }

    // bad
    {
      showButton &&
        <Button />
    }

    // good
    {showButton && (
      <Button />
    )}

    // good
    {showButton && <Button />}
    ```
    
    
    
## Quotes

  - Always use double quotes (`"`) for JSX attributes, but single quotes (`'`) for all other JS. eslint: [`jsx-quotes`](https://eslint.org/docs/rules/jsx-quotes)

    > Why? Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.

    ```jsx
    // bad
    <Foo bar='bar' />

    // good
    <Foo bar="bar" />

    // bad
    <Foo style={{ left: "20px" }} />

    // good
    <Foo style={{ left: '20px' }} />
    ```
    
    
## Spacing

  - Always include a single space in your self-closing tag. eslint: [`no-multi-spaces`](https://eslint.org/docs/rules/no-multi-spaces), [`react/jsx-tag-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)

    ```jsx
    // bad
    <Foo/>

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

  - Do not pad JSX curly braces with spaces. eslint: [`react/jsx-curly-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)

    ```jsx
    // bad
    <Foo bar={ baz } />

    // good
    <Foo bar={baz} />
    ```
    
    
## Props

  - Always use camelCase for prop names.

    ```jsx
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```
    
  - Omit the value of the prop when it is explicitly `true`. eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

    ```jsx
    // bad
    <Foo
      hidden={true}
    />

    // good
    <Foo
      hidden
    />

    // good
    <Foo hidden />
    ```
    
  - Always include an `alt` prop on `<img>` tags. If the image is presentational, `alt` can be an empty string or the            `<img>` must have `role="presentation"`. eslint: [`jsx-a11y/alt-text`](https://github.com/evcohen/eslint-plugin-jsx-         a11y/blob/master/docs/rules/alt-text.md)

     ```jsx
     // bad
     <img src="hello.jpg" />

     // good
     <img src="hello.jpg" alt="Me waving hello" />

     // good
     <img src="hello.jpg" alt="" />

     // good
     <img src="hello.jpg" role="presentation" />
     ```
 
 
   - Do not use words like "image", "photo", or "picture" in `<img>` `alt` props. eslint: [`jsx-a11y/img-redundant-alt`]         (https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-redundant-alt.md)
      > Why? Screenreaders already announce `img` elements as images, so there is no need to include this information in the        alt text.

      ```jsx
      // bad
      <img src="hello.jpg" alt="Picture of me waving hello" />

      // good
      <img src="hello.jpg" alt="Me waving hello" />
      ```
    
  - Avoid using an array index as `key` prop, prefer a stable ID. eslint: [`react/no-array-index-key`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-array-index-key.md)
    > Why? Not using a stable ID [is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-         e0349aece318) because it can negatively impact performance and cause issues with component state.

      We don’t recommend using indexes for keys if the order of items may change.

       ```jsx
       // bad
       {todos.map((todo, index) =>
         <Todo
           {...todo}
           key={index}
         />
       )}

       // good
       {todos.map(todo => (
         <Todo
           {...todo}
           key={todo.id}
         />
        ))}
       ```

## Refs

  - Always use ref callbacks. eslint: [`react/no-string-refs`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

       ```jsx
       // bad
       <Foo
       ref="myRef"
       />

       // good
       <Foo
       ref={(ref) => { this.myRef = ref; }}
       />
       ```

## Parentheses

  - Wrap JSX tags in parentheses when they span more than one line. eslint: [`react/jsx-wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-wrap-multilines.md)

       ```jsx
       // bad
       render() {
       return <MyComponent variant="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

       // good
       render() {
       return (
        <MyComponent variant="long body" foo="bar">
          <MyChild />
        </MyComponent>
       );
       }

       // good, when single line
       render() {
       const body = <div>hello</div>;
       return <MyComponent>{body}</MyComponent>;
       }
       ```


## Callback Handlers


  - **setState Callback**: Don't use setState callback as much as you can.
      > Why? setState callback fires after the rerender (just after componentDidUpdate) and shouldn't fire if the component         unmounts first.
      
  - **Defining Callbacks**: Don't call handler functions in callbacks of DOM functions (`onClick`, `onPress`) make your              handler your as callback function.
  
       ```jsx
       // bad       
       handlePress = () = {
        // handle press
       }
       
       <button onClick={()=> this.handlePress() }> Press Me </button>
      
       // good
       handlePress = () = {
        // handle press
       }
       
       <button onClick={this.handlePress}> Press Me </button>

## Methods

  - **Declearing Funcions**: Always decleare function handler with arrow pattern (`() => {}`)
      > Why? declearing a function without arrow pattern did'nt get the `this` scope then it should bind with `this` in             constructor 
    
       ```jsx
       // bad 
       class LoginContainer extends React.Component {
         constructor(props) {
         super(props);
        
         this.onLoginPress = this.onLoginPress.bind(this)
         }
        
         onLoginPress(){
           // login code
         }
       }
      
       // good
       class LoginContainer extends React.Component {
         constructor(props) {
           super(props);
         }
        
       onLoginPress = () => {
        // login code
       }
       }
       ```

  - **Decleare Methods Name**: Always declare methods name that it will represent its work
       ```jsx
       // bad
       login = () => {
        // login code
       }
       
       change = () =>{
       }
       
       modal = () => {
       }
       
       // good
       onLoginPress = () => {
       }
       
       handleChange = () => {
       }
       
       openModal = () => {
       }
       
## Common
  - Make all common components (`modals`,`dropdowns`,`drawer`) which can be use in more than one component in `common` >           `components` folder.
  
  - Place all the images in `common` > `assets` and require image in `images.js` file in variable and which can be used in       any components.
  
  - Make all helpers functions in `common` > `utils` > `helpers.js` which can be used in more than one component.
  
  

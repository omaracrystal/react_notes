##React.js BASICS

http://codepen.io/DevCoffee/pen/GZQaXb?editors=1010

https://www.youtube.com/watch?v=PGUMRVowdv8

### KEY TERMS:
* Babel, ES6, JSX
   
* HTML name element with id or class to render to ie: ``<div id=“app”></div>``

* React Component has:
    * **constructor**
        * ``super(props)`` = inheritance the parent object’s properties which is props 
        * ``this.state`` = contains all initial states of component
    * ``render()`` method has:
        * **props**
            * **destructoring** = ``var { name, age, bio, pic } = this.props;``
        * **state** = ``var { height } = this.state;``
        * Return 
            * ``this.methodName.bind(this)``
    * Custom **methods**
    * Then you render the React component with
        * ``ReactDOM.render()`` or ``React.render()``

EXAMPLE
```
class Profile extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      height: 100
    };
  }
  
  render() {
  
    var { name, age, bio, pic } = this.props;
    var { height } = this.state;
    
    return (
      <div className="profile-box">
        <h2>{name}</h2>
        <h4>Age: {age}</h4>
        <h4>Bio: {bio}</h4>
        <img src={pic} height={height} />
        <br />
        <button onClick={this.zoomPicOut.bind(this)}>-</button>
        <button onClick={this.zoomPicIn.bind(this)}>+</button>
      </div>
    );
  }
  
  zoomPicIn() {
    this.setState({height: this.state.height + 100});
  }
  
  zoomPicOut() {
    this.setState({height: this.state.height - 100});
  }
}

// props
// state
React.render(<Profile name="Chris Pena" age={24} bio="I like puppies." pic="http://goo.gl/qnbcXi" />, document.getElementById('app'));
```


### BREAKDOWN
1. JavaScript Preprocessor
    * Babel
    
1. React CDN
    * //cdnjs.cloudflare.com/ajax/libs/react/0.13.0/react.min.js

1. ES6
    * Class with inheritance
    * Class name followed by Component Name and extend React.Component
    * ``class Profile extends React.Component { }``
    * ``render()`` <- always needed to give a view - takes html - goes into above brackets

1. Needs a place to render - match up with id of HTML element
    * ``<div id=“app”></div>``

1. Use ReactDOM, with container you want to attach it to
    * ``React.render`` or ``ReactDom.render(<Profile/>, document.getElementById(‘app));``

1. How do you pass Data
    * **Props** = takes a KEY and a VALUE
    * ``React.render(<Profile name=“Crystal” age={30} bio=“I like puppies”/>, document.getElementById(‘app));``
    * What to put in Javascript? You need { } (see age)

1.  Where is the data at? Within the React Component
    * Try typing ``console.log(this)`` between the component’s ``render()`` function and ``return()`` function
    * Check it out in the inspector Console under Profile (component name) and find **“props”**
    * ``console.log(this.props.bio); = “I like puppies”``
    
1. **JSX** - markup for React - instead of **“class”** > **“className”**

1. **ES6** - pull out values (**destruction**) - It goes and finds that object and pulls out all the properties you ask for
    * ``var { name, age, bio } = this.props;``
    * ``{name}`` instead of ``{this.props.name}``
    
1. More Dynamic? 
    * Add a pic value to the Profile component like so
        * ``<Profile name=“Crystal” age={30} bio=“I like puppies” pic=“https://the-url-of-pic.com”/>``
    * Within render / return function
        * ``<img src={pic} height={100} />``
    
1. Add another Method?
    * ``Render()`` is a Method you can add one after this if you like!
    * Let’s add ``zoomPicIn()`` and ``zoomPicOut()``
        * add ``<button onClick={this.zoomPicIn.bind(this)}> + </button>`` for instance to the render function
        * You must **bind** the method to that component with ``.bind()``

1. Use React way = **“State” not jQuery** Way
    * There are **props** and **state**
        * **Props** = data, takes key and values
        * **State** = it determines the state of your component so if your state changes it re-renders a portion of your component that is relevant to the state

1. Define state with a **“constructor”** method (**ES6**) within the component
    * ``constructor(props) { super(props) }``
    * ``super(props)`` = inheritance the parent object’s properties which is props 
    * Now we can write state
        * ``constructor(props) { super(props); this.state = { }; }``
        * ``this.state`` is equal to an object
        * Within the object we are now going to define the different state attributes such as:
            * ``height = 100``
            * rename ``<img src={pic} height={this.state.height} />``
            * refactor further add above
                * ``var { height } = this.state;``
            * mutate (or change) state with a function
                * ``zoomPicIn() { this.setState({ height: this.state.height + 20}) }``
            
1. Side Notes
    * **All components need to be wrapped into one containing element tag**

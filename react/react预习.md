### css module

````css
// styles.css
// 使用css module引入时，会对每个类名生成唯一的hash串
.App{
    background-color: 'blue';
}
.border{
    border: 1px solid #ccc;
}
.logo{
    width: '100px';
    composes: border; // css 复合，只能用在有一层的css样式上
}
````



````js
import React from 'react'
import styles from './styles.css'
function App() {
    return <div className={styles.App}></div>
}
````



### setState

setState只有在合成事件或者生命周期中才是异步的，在setTimeout、原生事件中是同步的。这里异步指的是批量更新

````js
setState(partialState, callback) // callback会在页面重新渲染后执行
setState((state, props) => {
    // state、props是最新的
})
setTimeout(() => {
    this.setState(...) // 同步执行
    console.log(this.state.xxx) // 可以获取最新值
}, 0)
document.getElementById('test').addEventListener('click', function() {
    this.setState(...) // 同步执行
    console.log(this.state.xxx) // 可以获取最新值
})
````



### 组件复合(类似于slot)

主要是通过props.children来实现组件复合的功能。

````react
// 匿名插槽 ,在Dialog组件内部可以通过props.children拿到匿名组件
<Dialog>
	<p class="header">头部</p>
    <p class="content">内容</p>
</Dialog>
// 具名插槽, props.children第一个对象
<Dialog>
	{
        {
            header: <p class="header">头部</p>,
            content: <p class="content">内容</p>
        }
    }
</Dialog>
// 作用插槽，props.children可以是一个函数
<Dialog>
	{
        ({header, content}) => {
            return (
            	<div>
                	<p class="header">{header}</p>
                    <p class="content">{content}</p>
                </div>
            )
        }
    }
</Dialog>
````



### redux

1、当app中的状态很多很复杂，不利于维护时，可以考虑redux

2、通过状态提升将状态全部挂载到APP顶层已经无法满足要求时，可以考虑 redux

3、任意组件之间状态需要共享

使用步骤：

1、通过createStore创建store实例

2、store.getState()获取状态

3、store.dispatch({type: 'ADD'})派发action，执行reducer更新状态

4、store.subscribe()订阅状态变更

````react
// store.js
import {createStore} from 'redux'
const counterReducer = function(state = 0, action) {
    switch(action.type){
    	case: 'ADD':
            return state + 1
        default:
            return state
    }
}
export default createStore(counterReducer)
// ReduxPage.js

class ReduxPage extends React.Component{
    componentDidMount() {
        store.subscribe(() => {
            this.forceUpdate() // 手动更新组件
        })
    }
    render() {
        return <div>
        	<p>{store.getState()}</p>
            <button onClick={() => store.dispatch({type: 'ADD'})}>ADD</button>
        </div>
    }
}
````

### react-redux

1、解决redux中需要手动订阅状态变更，手动更新组件

2、使用到redux的组件都需要引入store实例，耦合性太强

使用步骤：

react-redux提供Provider、connect两个api

Provider：提供store实例，在所有子组件中都可以使用

connect：将状态、action映射到组件的属性上，状态变化时自动更新组件

````react
// App.js根组件
import {Provider} from 'react-redux'
ReactDom.render(<Provider store={store}><App/></Provider>, document.getElementById('app'))

// CounterPage.js
const mapStateToProps = state => ({num: state})
const mapDispatchToProps = {
    add: () => ({type: 'ADD'}),
    minus: () => ({type: 'MINUS'})
}
export default class connect(mapStateToProps, mapDispatchToProps)(CounterPage) extends Component{
    render() {
        const { num, add, minus } = this.props
        return (
        	<div>
            	<p>{num}</p>
                <button onClick={add}>add</button>
                <button onClick={minus}>minus</button>
            </div>
        )
    }
}
````

### 生命周期

componentWillMount、componentWillUpdate、componentWillReceiverProps三个钩子函数可能被废弃

新出现的钩子函数

**static getDerivedStateFromProps** // 在render方法之前调用，在初始化以及后续更新都会调用。它应该返回一个对象来更新state，如果返回null则不更新任何内容 。与componentWillReceiverProps 对比，父组件重新渲染时才会触发，而不是在内部调用setState时

**getSnapshotBeforeUpdate**

![image-20200902114530122](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200902114530122.png)

### Hooks

解决函数组件没有状态：

**useState**、**useEffect**

````react
function HooksPage() {
    const [num, setNum] = useState(0)
    useEffect(() => {
        // count发生变化时，会执行这个回调函数
    }, [count])
    return (<div>
    	<p>{num}</p>
        <button onClick={() => setNum(num + 1)}></button>
    </div>)
}
````

**自定义Hook**

````react
function useClock() {
    const [date, setDate] = useState(new Date())
    useEffect(() => {
        const timer = setInterval(() => {
            setDate(new Date())
        }, 1000)
        return () => {
            clearInterval(timer)
        }
    }, [])
}
````

**useMemo**  返回一个memorized值

// 把“创建”函数和依赖项数组传给useMemo，它仅会在某个依赖项改变时重新计算memorized值。这种优化有助于避免在每次渲染都进行高开销的计算

````react

const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

````

**useCallback** 返回一个memorized函数

把内联回调函数及依赖项数组作为参数传递给useCallback，它将返回该回调函数的memorized版本，该回调函数仅在某个依赖项发生变化时才会更新。

当你把回调函数传递给经过优化的并使用引用相等去避免不必要的渲染(如：shouldComponentUpdate)的子组件时，他将非常有用

````react
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
````



# Context

跨层级组件通信

- **React.createContext**
- **Context.Provider**
- **Class.contextType**
- **Context.Consumer**
- **useContext**


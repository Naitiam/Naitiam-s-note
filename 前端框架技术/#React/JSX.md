```js
import './app.css';
//1.识别常规的变量
//2.原生js方法调用
//3.三元运算符
const name = '柴柴老师'
const getAge = ()=>{
  return 18
}
// const flag = true

//列表渲染
//map
//也需要一个类型为number/string不可重复的key
//key仅仅在内部使用，不会出现在真实的dom结构中
const songs = [
  { id: 1,name: 'aaaa'},
  { id: 2,name: 'bbbb'},
  { id: 3,name: 'cccc'}
]

//条件渲染
//三元表达式（常用） 逻辑&&运算
const flag = true

//精简原则：逻辑不要写在语法糖里
const getHtag = (type) => { 
  if(type === 1){
    return <h1>this is h1</h1>
  }
  if(type === 2){
    return <h2>this is h2</h2>
  }
  if(type === 3){
    return <h3>this is h3</h3>
  }
 }

//样式控制
//行内样式，元素绑定style属性
const style = {
  color:'red',
  fontSize:'25px'
}
//类型样式，元素绑定className属性
//动态控制active类名
const activeFlag  = false

function App() {
  return (
    <div className="App">
      <div>
        { name }
        { getAge() }
        { flag ? '真棒':'真菜' }
      </div>
      <div>
        <ul>
          { songs.map(song => <li key={song.id}>{song.name}</li>) }
        </ul>
      </div>
      <div>
        { flag ? (
          <div>
            <span>this is span</span>
          </div>):null
        }
        { false && <span>this is span</span> }
      </div>
      <div>
        { getHtag(1) }
        { getHtag(2) }
      </div>
      <div>
        <span style={{color:'red',fontSize:'25px'}}>this is span1</span>
        <span style={style}>this is span1</span>
        <span className='active'>测试类名样式</span>
        <span className={activeFlag?'active':''}>测试类名样式</span>
      </div>
    </div>
  );
}

// export default App;
```


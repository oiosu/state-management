```react
const MyContext = React.createContext(defaultValue);
```

Context 객체를 만든다, 리액트가 이 Context 객체를 구독하는 구성 요소를 렌더링 할 때 트리에서 그 위에  가장 근접하게 일치하는 Provider에서 현재 컨텍스트 값을 읽는다. 

`defaultValue` 인수는 트리에서 구성 요소 위에 일치하는 공급자가 없는 경우에만 사용한다. 

![image-20240522223020977](https://raw.githubusercontent.com/oiosu/image_repo/master/img/image-20240522223020977.png)



Context.Provider

```react
<MyContext.Provider value={/* some value */}>
```

모든 Context 객체에는 Consumer Component가 컨텍스트 변경 사항을 구독할 수 있도록 하는 Provider React 구성요소가 함께 제공됩니다. 

```react
<MyContext.Provider value={/* some value */}>
    <AComponent />
    <BComponent />
    <CComponent />
<MyContext.Provider>
```

A,B,C Component 모두 다 Context를 구독중 그래서 Context value에 변경 사항이  생기면 컴포넌트를 다시 렌더링 한다. 

변경사항은 Object.is와 동일한 알고리즘을 사용하여 새 값과 이전 값을 비교하여 결정된다. 

만약 createContext 를 할때 defaultValue를 `{userName: "John"}` 이라고 했더라도 Context.Prokvider value props에서 `{userName: "Han"}` 이라고 전달해주면 두번째 value가 Consumer Component들에 전달 된다. (Provider 사용으로 Context 의 Value를 변경해 줄 수 있다.)

```react
const MyContext = React.createContext({ userName: "John"});
```

```react
<MyContext.provider value={{ userName: "Han" }}>
```



Class.contextType 

```react
class MyClass extends React.Component {
    componentDidMount() {
        let value = this.context;
        /* perform a side-effect at mout using the value of MyContext*/
    }
    componentDidSUpdate(){
        let value = this.context;
         /*...*/
    }
    componentWillUnmount(){
        let value = this.context;
         /*...*/
    }
    render(){
        let value = this.context;
         /*render somthing based on the value of MyContext*/
    }
}
MyClass.contextType = MyContext;
```

클래스의 contextType 속성에는 `React.createContext()` 에 의해 생성된 context 객체가 할당될 수 있다. 이 속성을 사용하면 this.context 를 사용하여 해당 컨텍스트 유형의 가장 가까운 현재 value를 사용하 ㄹ수 있따. 렌더링 기능을 포함한 모드 ㄴ수명 주기 메서드에서 이를 참조 할 수 있다. 
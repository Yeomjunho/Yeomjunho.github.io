---
title: "State관리 라이브러리 (Mobx, Context API, Redux)"
date: 2019-05-09 15:17:00 -0400
categories: react
---

요즘 react, redux, mobx, Context API 이런거 보느라.. 휴..
흰머리만 늘고있다..


---

- State관리 라이브러리
  Mobx, Context API, Redux

  <h3>[MobX]</h3>
  observer()가 observable 값이 변할 때 컴포넌트의 forceUpdate 를 호출하게 함으로써 자동으로 변화가 화면에 반영됩니다
  생각보다 간단하긴하다
  
  데이터가 변하는걸 변수: observable로 정의하면 끝나는거니깐..
  
  
  //사용법
  ```
  import { decorate, observable, action } from 'mobx';
  import { observer } from 'mobx-react';
  
  class AAA extends Component{
    number = 0;
    action1 = () => {}
    action2 = () => {}
  }
  
  decorate(AAA, {
    number: observable,
    action1: action,
    action2: action
  })

  export default observer(AAA);
  
  ```
  
  //데이터 흐름
  ```
  AA.findAllDeliveries (호출)-> [ AA.deliveries <-> ajax Data] (렌더링)-> AA.deliveries
  
  @observable
  @inject('BB')
  ```
  
  <br/><br/>
  <hr/>
  <br/><br/>
  
  <h3>[MobX + Decorator]</h3>
  아..
  확실이 편하긴 하다..
  MobX를 사용할거면 Decorator는 무조건이구나..
  @observer로 정의해두면 어디에서든 import없이 
  @inject()로 사용가능한것 같다..
  세상에나.. 이건좀 신기방기하네? 
  
  
  ```
  import { observable, action } from 'mobx';
  import { observer } from 'mobx-react';
  
  @observer
  class AAA extends Component{
    @observable number = 0;
    @action action1 = () => {}
    @action action2 = () => {}
  }
  export default AAA;
  ```
  
  //데이터 사용 1
  ```
  import { Provider } from 'mobx-react'; // MobX 에서 사용하는 Provider
  import AAA from ',.fileName';
  
  const aaa = new AAA(); // 스토어 인스턴스를 만들고
  
  ...
  
  <Provider counter={aaa}>
    {/* Provider 에 props 로 넣어줍니다. */}
    <App />
  </Provider>
  ```
  
  //데이터 사용 2
  ```
  import { observer, inject } from 'mobx-react';
  
  @inject('AAA')
  /* 필요한 것만 가져와서 사용가능
  @inject(stores => ({
    number: stores.AAA.number,
    action1: stores.AAA.action1,
    action2: stores.AAA.action2,
  }))
  */
  @observer
  class BBB extends Component {
    render() {
      const { AAA } = this.props;
      /*
      const { number, action1, action2 } = this.props;
      */
      return (
        <div>
          <h1>{AAA.number}</h1>
          <button onClick={AAA.action1}></button>
          <button onClick={AAA.action2}></button>
        </div>
      );
    }
  }
  ```
  
  * [blog-link3]
  
  <br/><br/>
  <hr/>
  <br/><br/>
  
  <h3>[Context API]</h3>
  생각보다 간단하다
  쓰고싶은 곳에서 import후 <AA></AA> 감싸서 사용하면 데이터 가져와서 사용이 가능하다
  이건좀 간단하긴 하지만 지저분할수도..ㅎㅎ
  Redux 보다는 편리한듯..
  
  
   <AA.Provider />
   <AA.Consumer />
   
   //데이터 정의
   ```
   import React, { Component, createContext } from 'react';

   const Context = createContext();
   const { Provider, Consumer: CounterConsumer } = Context;
   // 내보내줍니다.
   export { CounterProvider, CounterConsumer };
  ```
  
  //데이터 사용
  ```
  import { CounterProvider } from './fileName';
  <CounterProvider>
  ...
  ...
  </CounterProvider>
  ```
  
  
  * [blog-link1]
  * [blog-link2]
  




[jun-docs][jun-gh]

[jun-docs]: https://Yeomjunho.com/docs/home
[jun-gh]:   https://github.com/Yeomjunho

[blog-link1]: http://woowabros.github.io/experience/2019/01/02/kimcj-react-mobx.html
[blog-link2]: https://medium.com/lunit-engineering/context-api%EA%B0%80-redux%EB%A5%BC-%EB%8C%80%EC%B2%B4%ED%95%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C%EC%9A%94-76a6209b369b
[blog-link3]: https://velog.io/@velopert/MobX-2-%EB%A6%AC%EC%95%A1%ED%8A%B8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90%EC%84%9C-MobX-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-oejltas52z

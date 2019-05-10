---
title: "State관리 라이브러리 (Mobx, Context API, Redux)"
date: 2019-05-10 14:57:00 -0400
categories: react
---

오늘은 회사일이 그닥 많지 않아 공부를 하고 있다
리엑트로 리뉴얼을 계획중이라..
하나두 모르는 사람 5명이 머리 싸매고 해보고 있다..ㅎㅎ



---


<h3>[Babel 7]</h3>
먼가로 감싸야 한다는게 항상 별로였는데.
귀찮지만 이제는 이렇게 감싸면 된다


```
return(
  <>
    ...
    ...
  </>
);
```

<br/><br/>
<hr/>
<br/><br/>

<h3>TypeScript</h3>
  + tsconfig: 환경 설정 파일 
  + tslint: 코드 가독선, 오류 검사
  
  * [link_tsconfig]
    [link_tslint]
  
  
<br/><br/>
<hr/>
<br/><br/>

<h3>React</h3>
  조금, 아주~ 조금 공부를 하고 접하다 보니
  이걸 먼저 알아야 할것 같습니다.
  흐름(life cycle), 데이터 랜더링이 되는 흐름 중간중간 어떤함수를 쓰면 되는지 알아야 할것 같습니다.
  

  [흐름]
  컴포넌트를 생성 할 때는 constructor -> componentWillMount -> render -> componentDidMount 순으로 진행됩니다.
  컴포넌트를 제거 할 때는 componentWillUnmount 메소드만 실행됩니다.
  컴포넌트의 prop이 변경될 때엔 componentWillReceiveProps -> shouldComponentUpdate -> componentWillUpdate-> render -> componentDidUpdate 순으로 진행됩니다.

  //Mounting
  - constructor -> componentWillMount -> render -> componentDidMount
  
  //Updating
    - Props Change
      componentWillReceiveProps -> shouldComponentUpdate -> componentWillUpdate
      -> render -> componentDidUpdate
    - State Change
      shouldComponentUpdate -> componentWillUpdate
      -> render -> componentDidUpdate
    - Unmounting 
      componentWillUnmount
  

  ```
  //component지정
  class AA extends React.Component<{aa: string}, {bb: number}>{
    ...
  }
  ```
  
  
  * [link_React1]
    [link_React2]
  
  
  
  [link_tsconfig]: https://basarat.gitbooks.io/typescript/content/docs/project/tsconfig.html
  [link_tslint]: https://github.com/palantir/tslint
  [link_React1]: https://reactjs-kr.firebaseapp.com/docs/installation.html
  [link_React2]: https://jaeyeophan.github.io/2018/01/01/React-4-Component-Life-Cycle/

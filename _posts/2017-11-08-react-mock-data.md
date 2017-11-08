---
layout: post
title: "reactjs 임시 화면 보여주기"
excerpt: ""
categories: "dev"
comments: false
---

```javascript
export default class ViewUserList extends Component {
    constructor(props) {
        super(props);

        this.state = {
            isFirst: true,
        }
    }

    componentWillMount() {
        this.setState({
            isFirst: false,
        });
    }

    render() {
        return (
            {this.state.isFirst ? 'Mock data' : 'Original data'}
        )
    }
}
```

- new class는 한번 일어난다.
- 그러므로 constructor 내용은 한번만 실행된다.
- this.state 로컬 변수(store에 있는 data는 전역변수)
- componentWillMount를 만나서 setState를 큐에 담는다.
- "Mock data" 텍스트를 출력한다.
- 큐에 담았던 setState 값을 비교한다.
- isFirst 값을 비교하여 true 에서 false로 바뀌었으므로 
- render를 다시 그린다.
- 다시 처음부터 실행된다.
- componentWillMount에서 setState 값이
- false 값으로 변동되지 않아 멈춘다.
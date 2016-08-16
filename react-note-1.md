#React学习笔记（一）
*代码示例全部使用es6标准*
####ReactDOM.findDOMNode
获取真实dom，必须在render后调用，一般在componentDidMount方法中调用，也可在事件的回调函数中调用，使用方法：
```JavaScript
render() {
    return (
        <Message ref="message" onClick={this.onClick.bind(this)} />
    );
}

// 在ComponentDidMount方法中调用
componentDidMount() {
    let dom = ReactDom.findDOMNode(this);
    let message = ReactDom.findDOMNode(this.refs.message);
}

// 在onClick事件中调用，需要绑定this
onClick(e) {
    let dom = ReactDom.findDOMNode(this);
    let message = ReactDom.findDOMNode(this.refs.message);
}
```
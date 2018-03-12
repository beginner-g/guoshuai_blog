---
title: ES5 和 ES6 的区别
categories:
  - Others
date: 2018-01-12 14:16:49
tags: [ES5,ES6]
cover_picture: http://img1.imgtn.bdimg.com/it/u=80834248,2473924617&fm=27&gp=0.jpg
---

### 我们来讨论下Es5和Es6到底有什么区别呢？

#### 系统库的引用
- ES5中的引用需要先使用require导入React包，成为对象，再去进行真正引用
~~~ js
//ES5
var React = require("react");
var {
    Component,
    PropTypes
} = React;  //引用React抽象组件
~~~
- ES6里，可以使用import方法来直接实现系统库引用，不需要额外制作一个类库对象
~~~ js
//ES6
import React, { 
    Component,
    PropTypes,
} from 'react'
~~~
#### 导出及引用单个类
- ES5中要导出一个类给别的模块用，一般通过module.exports来实现。引用时，则依然通过require方法来获取
~~~ js
//ES5导入
var MyComponent = React.createClass({
    ...
});
module.exports = MyComponent;

//ES5导入
var MyComponent = require('./MyComponent')
~~~
- ES6中，则可以使用用export default来实现相同的功能，使用import方法来实现导入。
注意:ES5和ES6的导入导出方法是成对出现的，不可以混用。
比如：使用export default来导出，只能通过import 来导入。若使用require来导入，编译将不能通过。
~~~ js
//ES6导出(一般都继承于Component类)
export default class MyComponent extends Component{
    ...
}

//ES6导入
import MyComponent from './MyComponent';
~~~
#### 定义组件
- ES5中，组件类的定义通过React.createClass实现。
注意;ES5中React.createClass后面是需要小括号的，且结尾必须有分号。
~~~ js
//ES5
var Photo = React.createClass({
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});
~~~ 
- 在ES6里，让组件类去继承React.Component类就可以了。
注意：这里结尾时不会出现小括号，也不需要添加分号。
~~~ js
//ES6
class Photo extends React.Component {
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}
~~~
#### 组件内部定义方法
- ES5中采用的是 ###:function()的形式，方法大括号末尾需要添加逗号
~~~ js
//ES5 
var Photo = React.createClass({
    componentWillMount: function(){

    },
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});
~~~
- ES6中省略了【: function】这一段，并且结尾不需要加逗号来实现分隔。
注意:使用ES6定义的规则的话，外层必须用【class #### extend React.Component】的方式来申明这个类，否则会报错。
~~~ js
/ES6
class Photo extends React.Component {
    componentWillMount() {

    }
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}
~~~
#### 定义组件的属性类型和默认属性
- 在ES5里，属性类型和默认属性分别通过propTypes成员和getDefaultProps方法来实现(这两个方法应该是固定名称的)
~~~ js
//ES5 
var Video = React.createClass({
    getDefaultProps: function() {
        return {
            autoPlay: false,
            maxLoops: 10,
        };
    },
    propTypes: {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    },
    render: function() {
        return (
            <View />
        );
    },
});
~~~
- 在ES6里，统一使用static成员来实现
~~~ js
//ES6
class Video extends React.Component {
    static defaultProps = {
        autoPlay: false,
        maxLoops: 10,
    };  // 注意这里有分号
    static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    };  // 注意这里有分号
    render() {
        return (
            <View />
        );
    } // 注意这里既没有分号也没有逗号
}
~~~
- ES6中也可以在组件类声明完成后追加其静态方法。虽不推荐，但写法上也没问题
~~~ js
//ES6
class Video extends React.Component {
    render() {
        return (
            <View />
        );
    }
}
Video.defaultProps = {
    autoPlay: false,
    maxLoops: 10,
};
Video.propTypes = {
    autoPlay: React.PropTypes.bool.isRequired,
    maxLoops: React.PropTypes.number.isRequired,
    posterFrameSrc: React.PropTypes.string.isRequired,
    videoSrc: React.PropTypes.string.isRequired,
};
~~~
#### 初始化STATE
- 在ES5中，初始化state的方法是固定的getInitialState
~~~ js
//ES5 
var Video = React.createClass({
    getInitialState: function() {
        return {
            loopsRemaining: this.props.maxLoops,
        };
    },
})
~~~
- ES6中存在两种写法
 - 第一种，直接构造state函数
 ~~~ js
 class Video extends React.Component {
    state = {
        loopsRemaining: this.props.maxLoops,
    }
}
~~~ js
 - 第二种，相当于OC中的方法重写，重写constructor方法

class Video extends React.Component {
    constructor(props){
        super(props);
        this.state = {
            loopsRemaining: this.props.maxLoops,
        };
    }
}
~~~

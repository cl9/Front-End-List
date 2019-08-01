# 注册前端实现
## 需求分析
1. 包括 手机号输入框、验证码输入框、验证码倒计时组件、注册按钮 四个组件
2. 验证码倒计时组件
    * loadash.throttle 节流
    * classnames 优化依赖props或state的css classname
```
import React from 'react';
import classnames from 'classnames';
import './index.scss';
import lodash from 'lodash';

function noop() {}

export default class sendCode extends React.Component{
  constructor(props) {
    super(props);
    this.state = {
      codeMsg: '获取验证码',
      codeActive: true
    }
  }

  static defaultProps = {
    timeout: 60,
    onClick: noop,
  }

  clearTime = () => {
    if (this.timer) {
      clearInterval(this.timer);
      this.timer = null;
      this.setState({
        codeMsg: '获取验证码'
      });
      this.setState({
        codeActive: true
      })
    }
  }

  count = () => {
    if (this.timer) {
      return null;
    }

    console.log('倒计时')

    this.setState({
      codeActive: false
    })

    const { timeout } = this.props;
    let count = timeout;

    this.props.onClick();
    
    this.timer = setInterval(() => {
      this.setState({
        codeMsg: `${--count}s后重新获取`
      })
      if(count == 1){
        this.clearTime();
      }
    },1000)
  }

  onCodeClick = lodash.throttle(
    e => {
      e.stopPropagation();
      this.state.codeActive && !this.timer && this.count();
    },
    2000,
    { 'trailing': false }
  )

  render() {
    const { codeMsg,codeActive } = this.state;
    const btnCls = classnames({
      'btn': !codeActive,
      'btn-active': codeActive
    })

    return (
      <div className='send-code'>
        <div className={btnCls} onClick={this.onCodeClick}>
          {codeMsg}
        </div>
      </div>
    )
  }
}
```


3. 输入框清空功能
4. 调用后端获取短信验证码和注册接口
    + 请求参数验证
    + 请求参数加密



# 注册后端实现
## 需求分析
### 短信验证码接口
1. 请求参数解密
2. 后端请求参数验证
3. 验证用户名(手机号)是否已经注册
4. 短信验证码接口的安全防护,可参考[Java后端防止获取短信验证码接口被恶意调用的代码实现](https://blog.csdn.net/weixin_42023666/article/details/89680342)
    + 使用安全的图片验证码
    + 单IP对验证码短信接口的请求次数限定
    + 单用户请求间隔时长限制

### 注册接口
1. 请求参数解密
2. 后端请求参数验证
3. 验证用户名(手机号)是否已经注册
4. 验证短信验证码
5. 注册成功录入数据库


<img src="http://yuml.me/diagram/scruffy/activity/(start)->[descrypt req]->(validate req)->(end)" >
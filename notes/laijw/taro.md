# Taro Snippets

记录 Taro 开发中的常用代码片段

```js
import Taro, { Component } from '@tarojs/taro'
import { View, Text, Radio, Button } from '@tarojs/components'
import { connect } from '@tarojs/redux'
import {AtIcon, AtTabs, AtTabsPane, AtFloatLayout, AtAvatar, AtAtList, AtListItem} from "taro-ui"
```

## Redux Connect

```js
@connect(
  ({ my: { member_history_get_list_data } }) => ({ member_history_get_list_data }),
  dispatch => ({
    ...dispatch.my
  })
)
```

## 常用 Method

```js
constructor(props) {
  super(props);
  this.state = {
    current: 0,
  }
}

componentDidMount() {
  this.props.dispatch({
    type: 'my/member_fullback_get_list',
    payload: {uid: '123'}
  })
}

gotoDetail(path) {
  Taro.navigateTo({
    url: path,
    payload: {uid: '123'}
  })
}

handleClick(value) {
  this.setState({
    current: value
  })
}
```

## 顶部 Tab 导航

```js
const tabList = [
  {title: '全部'},
  {title: '待付款'},
  {title: '待发货'},
  {title: '待收货'},
  {title: '待评价'},
  {title: '退换货'},
]

<AtTabs
  current={this.state.current}
  tabList={tabList}
  className='my-tabs'
  onClick={this.handleClick.bind(this)}
>
  <AtTabsPane current={this.state.current} index={0}>
  </AtTabsPane>
  <AtTabsPane current={this.state.current} index={1}>
  </AtTabsPane>
</AtTabs>
```

## List 遍历

```js
const list1 = []

const listItem1 = list1.map((item,i) => {
  return (
    <View taroKey={String(i)}></View>
  )
})
```

```js
{list1 && list1.length ? (
  <View className='column'>{listItem1}</View>
) : (
  <View><Text>暂无数据</Text></View>
)}
```

## 底部提交按钮

```js
<View className="column flex-center py-8">
  <Button className="bg-primary my-4 text-white" style="width: 60vw" onClick={this.gotoDetail.bind(this, '/pages/my/income/bank/list')}>提现</Button>
</View>
```

## List 链接

```js
<View className="bg-white">
  <AtList>
    <AtListItem title='提现到银行卡' onClick={this.gotoDetail.bind(this, '/pages/my/income/bank/list')} arrow='right'/>
  </AtList>
  <AtList>
    <AtListItem title='绑定银行卡' onClick={this.gotoDetail.bind(this, '/pages/my/income/bank/add')} arrow='right'/>
  </AtList>
</View>
```

```js
purchase() {
  Taro.showModal({
    title: '支付确认',
    content: '是否报名蔡徐坤篮球课堂',
    confirmColor: '#ff4451',
  })
    .then(res => {
      console.log(res.confirm)
    })
}
```

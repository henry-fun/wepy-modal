# wepy-modal
基于wepy框架开发的微信小程序modal组件

## 使用
### 1、安装 ###
```bash
  npm install wepy-modal -S
```
### 2、引入 ###
```html
<template>
  <view class="container">
    <modal/>
  </view>
</template>

<script>
  import wepy from 'wepy'
  import modal from 'wepy-modal'

  export default class extends wepy.page {
    components = {
      modal
    }
  }
</script>

```
### 3、使用方法 ###
#### 3.1、通过invoke调用 ####
```javascript
  this.$invoke('modal', 'showModal', {
    title: 'modal标题'
  });
```
#### 3.2 通过props参数控制
```html
<template>
  <view class="container">
    <modal
      :visible.sync="modalVisible"
    >
    </modal>
  </view>
</template>

<script>
  import wepy from 'wepy';
  import modal from 'wepy-modal';

  export default class ModalStudy extends wepy.page {
    data = {
      modalVisible: false
    }

    components = {
      modal
    }

    methods = {
      showModal() {
        this.modalVisible = true;
      }
    }
  }
</script>
```
### 4、参数说明 ###
#### 4.1 代码演示 ####
```html
<template>
  <view class="container">
    <modal
      title="modal测试"
      :cancelTxt.sync="cancelTxt"
      :okTxt.sync="okTxt"
      :visible.sync="modalVisible"
      :showOk.sync="showOk"
      :showCancel.sync="showCancel"
      :actionMode.sync="actionMode"
      :actions="actions"
      @onClickItem.user="handleClickItem"
      @onClickOk.user="handleClickOk"
      @onClickCancel.user="handleClickCancel"
    >
      <view slot="body">
        <view>body内容填充区</view>
      </view>
    </modal>
  </view>
</template>

<script>
  import wepy from 'wepy';
  import modal from 'wepy-modal';

  export default class ModalStudy extends wepy.page {
    data = {
      modalVisible: false,
      cancelTxt: '关闭',
      okTxt: '确定',
      showOk: true,
      showCancel: true,
      actionMode: '',
      actions: [{
        name: '操作一',
        color: 'red',
      }, {
        name: '操作二',
        color: 'blue'

      }, {
        name: '操作三',
        color: '#f60'
      }]
    }

    methods = {
      handleClickItem (index, action) {
        this.visible = false;
        this.$emit('onClickItem', index, action);
      },
      handleClickOk () {
        this.visible = false;
        this.$emit('onOk');
      },
      handleClickCancel () {
        this.visible = false;
        this.$emit('onCancel');
      }
    }
  }
</script>
```
#### 4.2 参数配置说明 ####
| 属性/方法   | 说明    |  类型  |默认值|
| --------   | -----   | ---- |---- |
| visible | modal的显示与隐藏      |   Boolean |false|
| title | modal的标题文字(没有则不显示title)      |   String |''|
| cancelTxt | 取消按钮自定义文字      |   String |取消|
| okTxt | 确定按钮自定义文字      |   String |确定|
| showOk | 是否展示【确定】按钮      |   Boolean |true|
| showCancel | 是否展示【取消】按钮      |   Boolean |true|
| actions | 自定义的操作按钮,样例：[{name: '按钮一', color: 'red'}], name: 按钮名称，color：按钮颜色(css的颜色即可)      |   Array |[]|
| actionMode | 横列或竖列展示自定义操作按钮(默认横排)      |   String |''|
| onClickItem | 当点击自定义的操作按钮时触发，参数index为点击按钮的索引，参数action为点击按钮的配置项      |   function(index, action) |无|
| onClickOk | 当点击确定按钮时触发      |   function |无|
| onClickCancel | 当点击取消按钮时触发      |   function |无|
#### 4.3 modal的body内容自定义 ####
为了更好的自定义modal的body内容，使用了[slot插槽技术](https://tencent.github.io/wepy/document.html#/?id=slot-%E7%BB%84%E4%BB%B6%E5%86%85%E5%AE%B9%E5%88%86%E5%8F%91%E6%8F%92%E6%A7%BD)，可以使用wepy的slot技术来自定义modal的body内容。
```html
<template>
  <view class="container">
    
    <modal
      title="modal测试"
      :cancelTxt.sync="cancelTxt"
      :okTxt.sync="okTxt"
      :visible.sync="modalVisible"
      :showOk.sync="showOk"
      :showCancel.sync="showCancel"
      :actionMode.sync="actionMode"
      :actions="actions"
      @onClickItem.user="handleClickItem"
      @onClickOk.user="handleClickOk"
      @onClickCancel.user="handleClickCancel"
    >
      <view slot="body">
        <view>自定义body内容填充区</view>
      </view>
    </modal>
  </view>
</template>
```

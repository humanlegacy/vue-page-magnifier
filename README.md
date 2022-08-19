### 页面放大镜
```bash
npm i vue-page-magnifier
```

```js
import Magnifier from 'vue-page-magnifier'
export default {
  components: { Magnifier }
}
```
```html
  <Magnifier :scale='2' width='150px' height='150px'>
    <!-- 
      将需要被放大的内容添加到此处
      scale:2  需要被放大的倍数
      width:150px,height:150px 放大镜镜片大小
    -->

  </Magnifier>
```


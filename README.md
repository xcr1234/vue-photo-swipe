# PhotoSwipe Vue 2.0插件

[demo](https://xcr1234.github.io/vue-photo-swipe/#/)



# 环境

Vue 2.0


# 安装

[下载](https://github.com/xcr1234/vue-photo-swipe/archive/master.zip)

直接把src/photo-swipe放到你项目的src中，然后在main.js中引入：

```javascript
import Vue from 'vue'
import PhotoSwipe from './photo-swipe';

Vue.use(PhotoSwipe);
```


# 使用

具体例子，可以参考`HelloWorld.vue`

```vue
<template>
  <photo-swipe :data="data"></photo-swipe>
</template>
<script>
  import PhotoSwipe from "../photo-swipe/photo-swipe.vue";
  export default {
    components: {PhotoSwipe},
      name: 'HelloWorld',
      data(){
          return {
              data : [
                    {
                         //指定图片的宽度、高度
                         src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94201.jpg",
                         width : 1920,
                         height : 1080
                     },
                    {
                         //自动计算图片的宽度、高度
                         src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94200.jpg",
                         autoSize : true
                     },
                     {
                        loader(callback){
                          //异步加载图片，指定宽度，高度
                          setTimeout(()=>{
                            callback("http://old.bz55.com/uploads/allimg/140717/1-140GF94203-50.jpg",1920,1080);
                          },2000);
                        }
                     },
                     {
                       loader(callback){
                         //异步加载图片，自动计算图片的宽度、高度
                         setTimeout(()=>{
                              callback("http://old.bz55.com/uploads/allimg/140717/1-140GF94204.jpg");
                          },2000);
                       }
                     }
              ]
          }
     }
  }
</script>
```

# 参考

参考PhotoSwipe文档：

http://photoswipe.com/


<template>
  <div id="app">
    <!--
      cols:瀑布流布局的列数
      imgList:图片列表，注意：src必须是服务器的地址，本地不行（本地打包会找不到图片的路径）
      reachBottom:当滑动到底端时被触发
    -->
    <WaterFall :cols="cols" :imgList="imgList" @reachBottom="getMoreImg"></WaterFall>
  </div>
</template>

<script>
import WaterFall from "./components/waterFall.vue"
export default {
  name: 'App',
  components: {
    WaterFall
  },
  data(){
    return {
      cols:4,
      imgWidth:230,
      imgList:[
        {
          "src": "http://10.1.2.158:3000/image/1.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":322
        },
        {
          "src": "http://10.1.2.158:3000/image/2.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":322
        },
        {
          "src": "http://10.1.2.158:3000/image/3.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":452
        },
        {
          "src": "http://10.1.2.158:3000/image/4.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":171
        },
        {
          "src": "http://10.1.2.158:3000/image/5.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":223
        },
        {
          "src": "http://10.1.2.158:3000/image/6.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":167
        },
        {
          "src": "http://10.1.2.158:3000/image/7.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":308
        },
        {
          "src": "http://10.1.2.158:3000/image/8.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":302
        },
        {
          "src": "http://10.1.2.158:3000/image/9.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":160
        },
        {
          "src": "http://10.1.2.158:3000/image/10.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":322
        },
        {
          "src": "http://10.1.2.158:3000/image/11.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":255
        },
        {
          "src": "http://10.1.2.158:3000/image/12.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":269
        },
        {
          "src": "http://10.1.2.158:3000/image/13.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":182
        },
        {
          "src": "http://10.1.2.158:3000/image/14.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":353
        },
        {
          "src": "http://10.1.2.158:3000/image/15.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":249
        },
        {
          "src": "http://10.1.2.158:3000/image/16.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":309
        },
        {
          "src": "http://10.1.2.158:3000/image/17.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":240
        },
        {
          "src": "http://10.1.2.158:3000/image/18.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":334
        },
        {
          "src": "http://10.1.2.158:3000/image/19.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":322
        },
        {
          "src": "http://10.1.2.158:3000/image/20.jpg",
          "href": "https://www.baidu.com",
          "info": "一些图片描述文字",
          "_height":322
        }
      ]
    }
  },
  methods:{
    getMoreImg(){
      this.imgList.push(...this.imgList);
    }
  }
}
</script>

<style lang="scss" scoped>
  #app{
    width:975px;
    margin:0 auto;
  }
</style>

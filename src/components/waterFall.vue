<template>
  <div class="water-fall">
    <div class="col-item" v-for="(imgList,index) in imgListSort" :key="index">
      <div class="img-wrap" v-for="(imgListItem,index) in imgList" :key="index">
        <img :src="imgListItem">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'waterFall',
  props:{
    imgList:{
      type:Array,
      default:()=>{
        return []
      }
    },
    cols:{
      type:Number,
      required:true
    }
  },
  data(){
    return {
      imgListSort:{

      },
      heightDiv:[],
      startFor:0,
      containerElement:null
    }
  },
  watch:{
    cols:{
      handler(cols){
        for(let i=0;i<cols;i++){
         let key=`col_item_${i}`;
         this.$set(this.imgListSort,key,[])
          //this.imgListSort[key]=[];//vue不会对新增加的属性进行监听
        }
      },
      immediate:true
    },
    imgList(){
      this.appendImage();
    }
  },
  mounted () {
    //每列高度用数组缓存起来
    this.initHeightDiv();
    //把图片插到高度最小的一列
    this.appendImage();
    //当滑动到低端时触发事件
    this.watchScroll();
  },
  methods:{
    initHeightDiv(){
      let col_item=document.querySelectorAll(".col-item");
      col_item.forEach((node)=>{
        this.heightDiv.push(node.offsetHeight);
      })
    },
    //计算出高度最小的那一列
    minHeightDiv(){
      return this.indexOfSmallest(this.heightDiv);
    },
    indexOfSmallest(arr) {
      return arr.reduce(function(lowest, next, index) {
          return next < arr[ lowest ]?index:lowest
        }, 0);
    },
    appendImage(){
      for(let i=this.startFor;i<this.imgList.length;i++){
        let index=this.minHeightDiv();
        let key=`col_item_${index}`;
        this.imgListSort[key].push(this.imgList[i].src);
        this.heightDiv[index]=this.heightDiv[index]+this.imgList[i]._height;
      }
      this.startFor=this.imgList.length;
    },
    //监听滚动事件
    watchScroll(){
      window.addEventListener("scroll",()=>{
        let scrollHeight=document.documentElement.scrollHeight;
        let scrollTop=document.documentElement.scrollTop;
        let clientHeight=document.documentElement.clientHeight;
        if(scrollHeight-scrollTop==clientHeight){
          this.$emit("reachBottom")
        }
      })
    }
  }
}
</script>

<style scoped lang="scss">
  .water-fall{
    width:100%;
    display: flex;
    justify-content: flex-start;
    & > .col-item{
      flex:1;
      &:not(:first-child){
        margin-left:5px;
      }
      img{
        padding:5px;
        box-sizing: border-box;
        background:greenyellow;
      }
    }
  }
</style>

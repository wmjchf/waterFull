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
      imgSrc:"http://10.1.2.158:3000/image/1.jpg"
    }
  },
  watch:{
    cols:{
      handler(cols){
        for(let i=0;i<cols;i++){
         let key=`col_item_${i}`;
         this.$set(this.imgListSort,key,[])
          //this.imgListSort[key]=[];
        }
      },
      immediate:true
    }
  },
  mounted () {
    this.initHeightDiv();
    this.appendImage();
  },
  methods:{
    initHeightDiv(){
      let col_item=document.querySelectorAll(".col-item");
      col_item.forEach((node)=>{
        this.heightDiv.push(node.offsetHeight);
      })
      this.heightDiv[0]=10;
      this.heightDiv[1]=15;
      this.heightDiv[2]=14;
      this.heightDiv[3]=13;
    },
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
        console.log(this.heightDiv);
      }
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

<template>
  <div class="parts">
      <div class="partsHeader">
            <span class="i-wrap" @click="parts">
                <i class="iconfont icon-552cc14536532"></i>
            </span>
            <span>吱音品牌简介</span>
        </div>
      <div class="partsMain">
        <img src="https://img.alicdn.com/imgextra/i4/1753596474/T2Cb9uXtJXXXXXXXXX_!!1753596474.png" alt="">
      </div>
  </div>
</template>

<script>
import { Navbar, TabItem } from 'mint-ui';
export default {
    data(){
        return{
            selected:"tab-container1",
            list:[],
            charger:[],
            protect:[],
            headset:[]
        }
    },
    mounted:function(){
        this.getData(),
        this.chargerData(),
        this.protectData(),
        this.HeadsetData()
    },
    methods:{
        getData:function(){
            var _this=this;
            this.$http.get("http://shop.ziinlife.com/web/static/parts.json").then(function(res){
              for(var i=0,len=res.body.list.length;i<len;i++){
                  var selData=res.body.list[i];
                  var part=res.body.list[i].name;
                  _this.list.push(selData)
              }
          })
        },

        chargerData:function(){
            var _this=this;
            this.$http.get("http://shop.ziinlife.com/web/static/parts.json").then(function(res){
              for(var i=0,len=res.body.charger.length;i<len;i++){
                  var selData=res.body.charger[i];
                  var part=res.body.charger[i].name;
                  _this.charger.push(selData)
              }
          })
        },

        protectData:function(){
            var _this=this;
            this.$http.get("http://shop.ziinlife.com/web/static/parts.json").then(function(res){
              for(var i=0,len=res.body.protect.length;i<len;i++){
                  var selData=res.body.protect[i];
                  var part=res.body.protect[i].name;
                  _this.protect.push(selData)
              }
          })
        },

        HeadsetData:function(){
            var _this=this;
            this.$http.get("http://shop.ziinlife.com/web/static/parts.json").then(function(res){
              for(var i=0,len=res.body.headset.length;i<len;i++){
                  var selData=res.body.headset[i];
                  var part=res.body.headset[i].name;
                  _this.headset.push(selData)
              }
          })
        },
        parts:function(){
            this.$router.go(-1)
        },
        open:function(id){
            this.$router.push({path:"goodDetail",query:{id:id}})
        },
    }
}
</script>


<style>
.parts{
    position: absolute;
    background: white;
    width: 100%;
    height: 100%;
    top: 0;
    bottom: 0;
    z-index: 999;
}
.partsHeader{
    width: 100%;
    z-index: 1;
    height: 1.3rem;
    line-height: 1.3rem;
    font-size: 12px;
    background: white;
    position: fixed;
    -webkit-box-shadow: 0 0 10px #cecece;
    box-shadow: 0 0 10px #cecece;
    text-align: center;
    font-size: 0.41rem;
}
.partsHeader i{
    display: block;
    float: left;
    height: 50px;
    padding-left: 0.3rem;
    font-size: 0.71rem;
    color: black;
}
.partsHeader .i-wrap{
  position: absolute;
  left:0;
}
.partsMain{
    margin-top: 1.32rem;
}
.partsMain img{
  width:100%;
}

</style>

<template>
  <div class="choose">
        <div class="_choose_header">
            <span class="i-wrap" @click="back">
                <i class="iconfont icon-552cc14536532"></i>
            </span>
            <span>ziinlife</span>
        </div>
        <div class="_choose_twoMain">
            <mt-navbar v-model="selected" >
                <mt-tab-item id="tab-container1">全部</mt-tab-item>
                <mt-tab-item id="tab-container2">沙发椅凳</mt-tab-item>
                <mt-tab-item id="tab-container3">桌几</mt-tab-item>
                <mt-tab-item id="tab-container4">橱柜</mt-tab-item>
                <mt-tab-item id="tab-container5">床榻</mt-tab-item>
            </mt-navbar>

            <mt-tab-container v-model="selected" swipeable>
                <mt-tab-container-item id="tab-container1">
                    <ul style="margin-top: 2px;">
                        <li class="_chooseList" v-for="(choose,index) in chooses" :id="choose.id" @click="open(choose.id)">
                            <img v-bind:src="choose.ImageOne" alt="图片">
                            <p>{{choose.name}}</p>
                            <p style="font-size: 0.3rem;">{{choose.nametwo}}</p>
                            <div>￥{{choose.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <mt-tab-container-item id="tab-container2">
                    <ul style="margin-top: 2px;">
                        <li class="_chooseList" v-for="(choose,index) in chair" :id="choose.id" @click="open(choose.id)">
                            <img v-bind:src="choose.ImageOne" alt="图片">
                            <p>{{choose.name}}</p>
                            <p style="font-size: 0.3rem;">{{choose.nametwo}}</p>
                            <div>￥{{choose.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <mt-tab-container-item id="tab-container3">
                     <ul style="margin-top: 2px;">
                        <li class="_chooseList" v-for="(choose,index) in table" :id="choose.id" @click="open(choose.id)">
                            <img v-bind:src="choose.ImageOne" alt="图片">
                            <p>{{choose.name}}</p>
                            <p style="font-size: 0.3rem;">{{choose.nametwo}}</p>
                            <div>￥{{choose.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <mt-tab-container-item id="tab-container4">
                    <ul style="margin-top: 2px;">
                        <li class="_chooseList" v-for="(choose,index) in cabenit" :id="choose.id" @click="open(choose.id)">
                            <img v-bind:src="choose.ImageOne" alt="图片">
                            <p>{{choose.name}}</p>
                            <p style="font-size: 0.3rem;">{{choose.nametwo}}</p>
                            <div>￥{{choose.Price}}</div>
                        </li>
                    </ul>
                </mt-tab-container-item>
                <mt-tab-container-item id="tab-container5">
                  <ul style="margin-top: 2px;">
                    <li class="_chooseList" v-for="(choose,index) in bed" :id="choose.id" @click="open(choose.id)">
                      <img v-bind:src="choose.ImageOne" alt="图片">
                      <p>{{choose.name}}</p>
                      <p style="font-size: 0.3rem;">{{choose.nametwo}}</p>
                      <div>￥{{choose.Price}}</div>
                    </li>
                  </ul>
                </mt-tab-container-item>
            </mt-tab-container>

        </div>
  </div>
</template>


<script>
import { Navbar, TabItem } from 'mint-ui';
export default {
  name:"choose",
  data(){
      return{
          selected:"tab-container1",
          chooses:[],
          chair:[],
          table:[],
          cabenit:[],
          bed:[],
      }
  },
  mounted:function(){
      this.getData()
      this.getChair()
      this.getTable()
      this.getCabenit()
      this.getBed()
  },
  methods:{
      getData:function(){
          var _this=this;
          this.$http.get("http://shop.ziinlife.com/web/static/choose.json").then(function(res){
              for(var i=0,len=res.body.chooses.length;i<len;i++){
                  var selData=res.body.chooses[i];
                  var part=res.body.chooses[i].name;
                  _this.chooses.push(selData)
              }
          })
      },
       getChair:function(){
          var _this=this;
          this.$http.get("http://shop.ziinlife.com/web/static/choose.json").then(function(res){
              for(var i=0,len=res.body.chair.length;i<len;i++){
                  var selData=res.body.chair[i];
                  var part=res.body.chair[i].name;
                  _this.chair.push(selData)
              }
          })
      },
      getTable:function(){
          var _this=this;
          this.$http.get("http://shop.ziinlife.com/web/static/choose.json").then(function(res){
              for(var i=0,len=res.body.table.length;i<len;i++){
                  var selData=res.body.table[i];
                  var part=res.body.table[i].name;
                  _this.table.push(selData)
              }
          })
      },
      getCabenit:function(){
          var _this=this;
          this.$http.get("http://shop.ziinlife.com/web/static/choose.json").then(function(res){
              for(var i=0,len=res.body.cabenit.length;i<len;i++){
                  var selData=res.body.cabenit[i];
                  var part=res.body.cabenit[i].name;
                  _this.cabenit.push(selData)
              }
          })
      },
      getBed:function(){
        var _this=this;
        this.$http.get("http://shop.ziinlife.com/web/static/choose.json").then(function(res){
          for(var i=0,len=res.body.bed.length;i<len;i++){
            var selData=res.body.bed[i];
            var part=res.body.bed[i].name;
            _this.bed.push(selData)
          }
        })
      },
      open:function(id){
          this.$router.push({path:"goodDetail",query:{id:id}})
      },
      back:function(){
          this.$router.go(-1)
      },
  }
}
</script>

<style>
.choose{
    position: absolute;
    background: white;
    width: 100%;
    height: 100%;
    top: 0;
    bottom: 0;
    z-index:999;
}
._choose_header{
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
._choose_header .i-wrap{
  position: absolute;
  left: 0;
}
._choose_header i{
    display: block;
    float: left;
    height: 50px;
    padding-left: 0.3rem;
    font-size: 0.71rem;
    color: black;
}
._choose_twoMain{
    margin-top: 1.32rem;
}
._chooseList{
    height: 6.6rem;
    background: white;
    float: left;
    box-sizing: border-box;
    width: 50%;
    border-right: 1px solid #F4F4F4;
    border-bottom: 1px solid #F4F4F4;
    float: left;
    margin-top: 1px;
    list-style: none;
}
._chooseList p{
    width: 94%;
    overflow: hidden;
    text-overflow: ellipsis;
    margin: auto;
    font-size: 0.35rem;
    text-align: center;
}
._chooseList div{
    text-align: center;
    color: red;
    margin-top: 10px;
  font-size:0.33rem;
}
._chooseList img{
    height: 4rem;
    width: 4rem;
    display: block;
    margin: auto;
    padding: 0.5rem;
}
</style>

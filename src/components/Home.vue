<template>
  <div class="Home">
      <div class="Homeheader"><div class="Homeheader-inner"><img src="http://shop.ziinlife.com/web/static/img/header_logo.png" alt="logo"></div></div>
      <div class="swipe">
        <mt-swipe :auto="4000">
          <!--<mt-swipe-item><router-link to="goodDetail?id=4"><img src="http://shop.ziinlife.com/web/static/img/index1.jpg" alt="轮播图"></router-link></mt-swipe-item>-->
          <mt-swipe-item><router-link to="choose"><img src="http://shop.ziinlife.com/web/static/img/index1.jpg" alt="轮播图"></router-link></mt-swipe-item>
          <mt-swipe-item><router-link to="choose"><img src="http://shop.ziinlife.com/web/static/img/index2.jpg" alt="轮播图"></router-link></mt-swipe-item>
        </mt-swipe>
      </div>
      <div class="HomeList">
        <ul >
          <li><div @click="xuangou"><img src="http://shop.ziinlife.com/web/static/img/product.png" alt="所有產品"></div><span>所有商品</span></li>
          <li><div @click="store"><img src="http://shop.ziinlife.com/web/static/img/shops.png" alt="门店信息"></div><span>门店信息</span></li>
          <li><div @click="parts"><img src="http://shop.ziinlife.com/web/static/img/headphone.png" alt="品牌介绍"></div><span>品牌介绍</span></li>
        </ul>
      </div>
      <div class="main">
        <div class="main_box">
          <ul><!-- <img src="../assets/list1.jpg" alt="商品"> -->
            <li v-for="(todo,index) in todos" :id="todo.id"  @click="open(todo.id)" class="list">
                <div class="image">
                  <img v-bind:src="todo.img" alt="图片">
                </div>
                <div class="name">{{todo.name}}</div>
                <div class="Price">￥{{todo.Price}}</div>
            </li>
          </ul>
        </div>
      </div>
  </div>
  </div>
</div>

</template>

<script>
import { mapState,mapMutations,mapGetters  } from 'vuex';
import { Swipe, SwipeItem } from 'mint-ui';
import { MessageBox } from 'mint-ui';
export default {
  name:"Home",
  data(){
    return{
      todos:[]
    }
  },
  mounted:function(){
    this.getData();
  },
  methods:{
    getData:function(){
      var _this=this;
      this.$http.get("http://shop.ziinlife.com/web/static/Home.json").then(function(res) {
        for (var i = 0, len = res.body.todos.length; i < len; i++) {
          var selData = res.body.todos[i];
          var part = res.body.todos[i].name;
          _this.todos.push(selData);
        }
      })
    },
    open:function(id){
    this.$router.push({path:"goodDetail",query:{id:id}})
    },
    xuangou:function(){
      this.$router.push({path:"choose"})
    },
    store:function () {
      this.$router.push({path:"storeInfo"})
    },
    parts:function(){
      this.$router.push({path:"parts"})
    }
  },
}
</script>

<style>
  .Home{
    border-bottom: 10px;
  }
  .Homeheader img{
    display:block;
    width:3.5rem;
    /*vertical-align:middle;*/
  }
  .Homeheader-inner{
    display:table-cell;
    vertical-align:middle;
    text-align:center;
    height: 1.3rem;
    width: 100%;
  }
   .Homeheader{
     position: fixed;
     width: 100%;
     top: 0;
     z-index: 1;
     height: 1.3rem;
     padding-left: 0.4rem;
     background: white;
   }
   .swipe{
     height: 4.7rem;
     margin-top: 1.3rem;
   }
   .swipe img{
      width: 100%;
      /*height: 4.5rem;*/
  }
  .main_box{
    /* margin-bottom: 34px;  */
    height: 339px;

  }
  .main span{
    display: block;
    height: 1.3rem;
    background: white;
    font-size: 0.35rem;
    line-height: 1.3rem;
    padding-left: 0.3rem;
  }
  .list {
    height: 6.6rem;
    background: white;
    float: left;
    box-sizing:border-box;
    width:50%;
    border-right: 1px solid #F4F4F4;
    border-top: 1px solid #F4F4F4;
  }
  .list span{
    display: block;
    color: red;
    padding-left: 0.5rem;
    padding-top: 0.1rem;
  }
  .main_box ul{
      overflow: hidden;
      margin-bottom: 1.5rem;
  }
  ul li{
    list-style: none;
  }
  .name{
    width: 80%;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    margin: auto;
    font-size: 0.37rem;
    padding-top: 0.8rem;
    font-weight: 800;
    text-align: center;
  }
    .nametwo{
      font-size: 0.01rem;
      text-align: center;
      padding-top: 0.15rem;
      font-family: "微软雅黑"
    }
    .Price{
      font-size: 0.33rem;
      color: red;
      margin: auto;
      text-align: center;
      padding-top: 0.28rem;
    }
    .image{
      width: 100%;
      height: 4rem;
      background: white;
    }
    .image img{
      height: 3.3rem;
      width: 3.5rem;
      display: block;
      margin: auto;
      padding-top: 0.9rem;
    }
    .HomeList{
      width: 100%;
      height: 2rem;
      background: white;
      padding:0.3rem 0;
    }
    .HomeList>ul>li{
      width: 33.3%;
      text-align: center;
      float: left;
      margin: auto;
    }
    .HomeList>ul>li div{
      width: 1.1rem;
      margin:0 auto;
      padding:0.2rem 0;
    }
    .HomeList>ul>li img{
      display: block;
      width: 1.1rem;
    }
</style>


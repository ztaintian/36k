<template>
  <div id="app">
    <!--<router-view></router-view>-->
    <hello  :news='item' v-for="item in items"></hello>
    <div class='loading' v-if='hasmore'>加载中......</div>
  </div>
</template>

<script>
import Hello from './components/hello'
import $ from 'jquery'
export default {
  name: 'app',
  components: {
    Hello
  },
  data() {
    return {
      allitems:'',
      items: '',
      num:0,
      hasmore:true,
    };
  },
  mounted() {
    var that = this;
    var YqlUrl='http://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20xml%20where%20url%3D"'+'http://36kr.com/feed'+'"&format=json&diagnostics=true&callback=?';
    $.getJSON(YqlUrl,function(data){
      console.log(data)
      that.allitems = data.query.results.rss.channel.item;
      that.items = that.allitems.slice(that.num,that.num+10);
      that.num +=10;
      document.body.scrollTop = 0;
    })
    this.loadMore();
  },
  methods:{
      loadMore: function(){
        var that = this;
        window.onscroll = function(){
          if(document.body.scrollTop+window.screen.height+200 > document.body.clientHeight){
            if(that.allitems.slice(that.num,that.num+10).length>0){
              var tempArr = that.allitems.slice(that.num,that.num+10);
              for(var i = 0; i < tempArr.length; i++){
                that.items.push(tempArr[i]);
              }
              that.num +=10;
            }else{
              that.hasmore = false;
            }
          }
        }
    }
  }
}
</script>

<style>
.loading{
  height: 30px;
  text-align: center;
  color:#888;
  line-height: 30px;
}
</style>

<template>
  <div class="hello">
    <div class='title'><p>{{news.title}}</p></div>
    <div class='author'><span class='writer'>{{news.author}}</span><span class='sort'>{{news.category}}</span><span class='date'>{{news.pubDate}}</span></div>
    <div  @click="onclick(news)" class='content'><img src="" alt=""><p>{{news.description}}</p></div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
    }
  },
  props:{
    news: {
      type: Object , // 类型按需求
    }
  },
  methods:{
    onclick: function(data){
      // console.log(data.link)
      window.location.assign(data.link);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  padding:0 5%;
}
.title p{
  font:22px/1.2 '微软雅黑';
  margin: 15px 0;
  overflow : hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
.author{
  position:relative;
  height: 30px;
}
.writer, .sort, .date{
  float: left;
  border-radius: 3px;
  color:#fff;
}
.writer{
  background: #5190cc;
}
.sort{
  margin-left: 5%;
  background: #eef4f2;
  color:#c69493;
}
.date{
  float: right;
  color:#fff;
  background: #98989a;
  height: 16px;
  width:100px;
  overflow: hidden;
}
.content{
  padding: 15px 0;
  border-bottom:2px solid #888;
  overflow: hidden;
}
.content p{
  width: 65%;
  font:14px/1.5 '微软雅黑';
  color:#666;
  overflow : hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  word-break: normal;
}
.content img{
  height: 100px;
  width: 100px;
  float: right;
}
</style>

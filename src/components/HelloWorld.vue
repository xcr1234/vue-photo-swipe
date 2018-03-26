<template>
  <div class="hello">
    <photo-swipe :data="data"></photo-swipe>
  </div>
</template>

<script>


import PhotoSwipe from "../photo-swipe/photo-swipe.vue";

export default {
  components: {PhotoSwipe},
  name: 'HelloWorld',

  data () {
    return {
      data:[
        {
          //src : "https://diycode.b0.upaiyun.com/photo/2017/fc7727985fd40e43f6b5bd6192dc23b7.jpeg",
          loader(callback){
            setTimeout(()=>{
              callback('https://diycode.b0.upaiyun.com/photo/2017/fc7727985fd40e43f6b5bd6192dc23b7.jpeg')
            },2000);
          }
        },
        {
          src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94201.jpg",
          width : 1920,
          height : 1080
        },
        {
          src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94200.jpg",
          width : 1920,
          height : 1080
        }
        ,
        {
          src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94203-50.jpg",
          width : 1920,
          height : 1080,
          loader(callback){
            setTimeout(()=>{
              callback("http://old.bz55.com/uploads/allimg/140717/1-140GF94203-50.jpg",1920,1080)
            },2000);
          }
        }
        ,
        {
          src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94204.jpg",
          width : 1920,
          height : 1080
        }
        ,
        {
          src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94205.jpg",
          width : 1920,
          height : 1080
        },
        {
          src : "http://old.bz55.com/uploads/allimg/140717/1-140GF94206-50.jpg",
          width : 1920,
          height : 1080
        }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

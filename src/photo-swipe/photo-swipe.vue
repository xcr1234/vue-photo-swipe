<template>
  <!-- Root element of PhotoSwipe. Must have class pswp. -->
  <div class="pswp" tabindex="-1" role="dialog" aria-hidden="true" ref="el">

    <!-- Background of PhotoSwipe.
         It's a separate element as animating opacity is faster than rgba(). -->
    <div class="pswp__bg"></div>

    <!-- Slides wrapper with overflow:hidden. -->
    <div class="pswp__scroll-wrap">

      <!-- Container that holds slides.
          PhotoSwipe keeps only 3 of them in the DOM to save memory.
          Don't modify these 3 pswp__item elements, data is added later on. -->
      <div class="pswp__container">
        <div class="pswp__item"></div>
        <div class="pswp__item"></div>
        <div class="pswp__item"></div>
      </div>

      <!-- Default (PhotoSwipeUI_Default) interface on top of sliding area. Can be changed. -->
      <div class="pswp__ui pswp__ui--hidden">

        <div class="pswp__top-bar">

          <!--  Controls are self-explanatory. Order can be changed. -->

          <div class="pswp__counter"></div>

          <!--<button class="pswp__button pswp__button&#45;&#45;close" title="Close (Esc)"></button>

          <button class="pswp__button pswp__button&#45;&#45;share" title="Share"></button>

          <button class="pswp__button pswp__button&#45;&#45;fs" title="Toggle fullscreen"></button>

          <button class="pswp__button pswp__button&#45;&#45;zoom" title="Zoom in/out"></button>-->

          <!-- Preloader demo http://codepen.io/dimsemenov/pen/yyBWoR -->
          <!-- element will get class pswp__preloader--active when preloader is running -->
          <div class="pswp__preloader">
            <div class="pswp__preloader__icn">
              <div class="pswp__preloader__cut">
                <div class="pswp__preloader__donut"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="pswp__share-modal pswp__share-modal--hidden pswp__single-tap">
          <div class="pswp__share-tooltip"></div>
        </div>

        <button class="pswp__button pswp__button--arrow--left" title="Previous (arrow left)">
        </button>

        <button class="pswp__button pswp__button--arrow--right" title="Next (arrow right)">
        </button>

        <div class="pswp__caption">
          <div class="pswp__caption__center"></div>
        </div>

      </div>

    </div>

  </div>

</template>

<script>

  function wrapItem(data) {
    const item = Object.assign({},data);
    if(data.autoSize || data.loader){
      item.w = 0;
      item.h = 0;
    }else{
      item.w = data.width;
      item.h = data.height;
    }
    return item;
  }

  export default {
    name : "photo-swipe",
    mounted(){
      this.update();
    },
    updated(){
      this.update();
    },
    props:{
      data : Array,
      options : Object,
    },
    data(){
      return {
      }
    },
    computed:{
      items(){
        if(!this.data){
          return [];
        }
        const items = [];
        this.data.forEach(data=>{
          items.push(wrapItem(data));
        });
        return items;
      },
      pwsp(){
        return this.$refs.el.$pwsp;
      }
    },
    destroyed(){
      this.$refs.el.$pwsp.close();
    },
    methods:{
      update(){
        if(this.$refs.el.$pwsp){
          this.$refs.el.$pwsp.close();
        }
        const options = Object.assign({},this.$PhotoSwipe.OPTIONS,this.options);
        const pswp = new this.$PhotoSwipe(this.$refs.el,this.$PhotoSwipe.UI,this.items,options);
        pswp.listen("gettingData",(index,item)=>{
          const data = this.data[index];
          if(data.autoSize && item.w < 1 && item.h < 1){
            var img = new Image();
            img.onload = function() { // will get size after load
              item.w = img.width; // set image width
              item.h = img.height; // set image height
              pswp.invalidateCurrItems(); // reinit Items
              pswp.updateSize(true); // reinit Items
            };
            img.src = data.src;
          }
          if(data.loader && item.w < 1 && item.h < 1){
            item.src = null;
            if(!item.loading){
                item.loading = true;
                data.loader((src,width,height)=>{
                    if(width && height){
                        item.src = src;
                        item.w= width;
                        item.h = height;
                        pswp.invalidateCurrItems(); // reinit Items
                        pswp.updateSize(true); // reinit Items
                    }else{
                        const img = new Image();
                        img.onload = function() { // will get size after load
                            item.src = src;
                            item.w = img.width; // set image width
                            item.h = img.height; // set image height
                            pswp.invalidateCurrItems(); // reinit Items
                            pswp.updateSize(true); // reinit Items
                        };
                        img.src= src;
                    }
                    item.loading = false;
                });
            }
          }
        });
        pswp.init();
        this.$refs.el.$pwsp = pswp;
      }
    }
  }
</script>

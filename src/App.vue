<template>
  <div id="app">
      <v-header :seller="seller"></v-header>
      <div class="tab border-1px">
          <div class="tab-item">
            <router-link to="/goods">商品 </router-link>
          </div>
          <div class="tab-item">
             <router-link to="/ratings">评论</router-link>
          </div>
          <div class="tab-item">
           <router-link to="/seller">商家</router-link>

          </div>
      </div>
      <keep-alive>
       <router-view :seller="seller"></router-view>
      </keep-alive>
  </div>
</template>

<script>
    import header from './components/header/header.vue';
    import {urlParse} from './common/js/util.js';
    const ERR_OK=0;
    export default {
         data:function() {
            return{
              seller:{
                id:(()=>{
                  let queryParam=urlParse();
                  console.log(queryParam);
                  return queryParam.id;
                })()
              }
            };
         },
         created(){
          // GET /someUrl
            this.$http.get('/api/seller?id='+this.seller.id).then(response => {
              // get body data
              response = response.body;
              if(response.errno === ERR_OK) {
               // this.seller = response.data;
                this.seller = Object.assign({}, this.seller, response.data);
                // console.log(this.seller.id)
              }
            });
         },
        components:{
            'v-header':header
        }
    };
</script>

<style lang="stylus">
 @import "./common/stylus/index.styl";
  .tab
    display:flex
    width:100%
    height:40px
    line-height:40px
    .tab-item
      flex:1
      text-align:center
      border-1px(rgba(7,17,27,0.1))
      & > a
        display:block
        font-size:14px;
        color:rgb(77,85,93)
        &.active
          color:#f01414

</style>

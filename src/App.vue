<template>
  <div id="app">
       <v-header :seller="seller"></v-header>
    <div class="tab">
        <div class="tab-item">
           <router-link to="/goods">商品</router-link>
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
const ERR_OK = 0;
export default {
  data(){
    return{
      seller:{}
    }
  },
  created() {
    this.$axios.get('http://localhost:8080/api/seller').then((res) =>{
        //  console.log(res.data.data)
      if (res.data.errno === ERR_OK) {
          this.seller =  res.data.data;
      }
    })
  },
  components: {
    'v-header':header,
  }
}
</script>

<style lang="scss" rel="stylesheet/scss" scope>
    @import "common/scss/mixins";

 .tab {
        display: flex;
        width: 100%;
        height: 40px;
        line-height: 40px;
        @include border-1px(rgba(7, 17, 27, 0.1));

        .tab-item {
            flex: 1;
            text-align: center;

            & > a {
                display: block;
                font-size: 14px;
                color: rgb(75, 112, 150);

                &.active {
                    color: rgb(247, 2, 2)
                }
            }
        }
    }
</style>

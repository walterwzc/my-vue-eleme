<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
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
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from 'components/header/header.vue';

  const ERR_OK = 0;

  export default {
    data() {
      return {
        seller: null
      };
    },
    components: {
      'v-header': header
    },
    created() {
      this.$http.get('/api/seller').then((response) => {
        console.log(response.body);
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = response.data;
        }
      });
    },
    mounted() {
      document.setTitle = function(t) {
        document.title = t;
        var i = document.createElement('iframe');
        i.style.display = 'none';
        i.onload = function () {
          setTimeout(function() {
            i.remove();
          }, 10);
        };
        document.body.appendChild(i);
      };

      document.setTitle('hello');
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"

  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7, 17, 27, 0.1))
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77, 85, 93)
        &.active
          color: rgb(240, 20, 20)
</style>

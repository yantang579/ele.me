<template>
  <div class="seller">
    <div class="overview">
      <h1 class="name">{{seller.name}}</h1>
      <div class="desc">
        <star :size="36" :score="seller.score"></star>
        <span class="content">({{seller.ratingCount}})</span>
        <span class="content">月售{{seller.sellCount}}单</span>
      </div>
      <div class="mark">
        <div class="icon"></div>
        <div class="content">已收藏</div>
      </div>
      <ul>
        <li>
          <h2 class="title">起送价</h2>
          <div class="content">
            <span class="stress">{{seller.minPrice}}</span>元
          </div>
        </li>
        <li>
          <h2 class="title">商家配送</h2>
          <div class="content">
            <span class="stress">{{seller.deliveryPrice}}</span>元
          </div>
        </li>
        <li>
          <h2 class="title">平均配送时间</h2>
          <div class="content">
            <span class="stress">{{seller.diliveryTime}}</span>分钟
          </div>
        </li>
      </ul>
    </div>
    <div class="bulletin"></div>
    <div class="pics"></div>
    <div class="info"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import '../star/star.vue';

  export default {
    props: {
      seller: {
        type: Object
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">

</style>

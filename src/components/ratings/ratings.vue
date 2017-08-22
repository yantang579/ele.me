<template>
  <div class="ratings">
    <div class="overview">
      <div class="overview-left">
        <div class="score">{{seller.score}}</div>
        <div class="title">综合评分</div>
        <div class="rank">
          <span class="text">高于周边商家</span>
          <span class="rankRate">{{seller.rankRate}}%</span>
        </div>
      </div>
      <div class="overview-right">
        <div class="score-wrapper">
          <span class="title">服务态度</span>
          <star :size="36" :score="seller.serviceScore"></star>
          <span class="score">{{seller.serviceScore}}</span>
        </div>
        <div class="score-wrapper">
          <span class="title">商品评分</span>
          <star :size="36" :score="seller.foodScore"></star>
          <span class="score">{{seller.foodScore}}</span>
        </div>
        <div class="delivery-wrapper">
          <span class="title">送达时间</span>
          <span class="score">{{seller.deliveryTime}}分钟</span>
        </div>
      </div>
    </div>
    <split></split>
    <ratingselect :ratings="ratings"></ratingselect>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from '../star/star.vue';
  import split from '../split/split.vue';
  import ratingselect from '../ratingselect/ratingselect.vue';

  const ERR_OK = 0;

  export default {
    data() {
      return {
        ratings: []
      };
    },
    props: {
      seller: {
        type: Object
      }
    },
    created() {
      this.$http.get('/api/ratings').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.ratings = response.data;
        }
        console.log(this.ratings);
      });
    },
    components: {
      star,
      split,
      ratingselect
    }
  }
  ;
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .ratings
    position: absolute
    top: 174px
    left: 0
    width: 100%
    overflow: hidden
    .overview
      display: flex
      margin: 18px 0
      .overview-left
        display: 0 0 137px
        width: 137px
        text-align: center
        border-right: 1px solid rgba(7, 17, 27, 0.1)
        .score
          font-size: 24px
          color: rgb(255, 153, 0)
          line-height: 28px
          padding-bottom: 6px
        .title
          font-size: 12px
          color: rgb(7, 17, 27)
          line-height: 12px
          padding-bottom: 8px
        .rank
          font-size: 10px
          color: rgb(147, 153, 159)
          padding-bottom: 6px

      .overview-right
        padding: 6px 0 6px 24px
        flex: 1
        .score-wrapper
          margin-bottom: 8px
          font-size: 0
          .title
            display: inline-block
            margin-right: 12px
            font-size: 12px
            color: rgb(7, 17, 27)
            line-height: 18px
          .star
            display: inline-block
            vertical-align: top
            margin-right: 12px
          .score
            display: inline-block
            font-size: 12px
            color: rgb(255, 153, 0)
            line-height: 18px
        .delivery-wrapper
          .title
            display: inline-block
            margin-right: 12px
            font-size: 12px
            color: rgb(7, 17, 27)
            line-height: 18px
          .score
            font-size: 12px
            color: rgb(157, 153, 159)
            line-height: 18px


</style>

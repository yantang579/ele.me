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
    <ratingselect v-on:selectTypeKey="theSelectType" v-on:toggleContentKey="IsonlyContent"
                  :ratings="ratings"></ratingselect>
    <div class="rating-wrapper">
      <ul>
        <li class="rating-item border-1px" v-for="rating in ratings" v-show="needShow(rating.rateType, rating.text)">
          <div class="avatar">
            <img width="28px" height="28px" :src="rating.avatar">
          </div>
          <div class="content">
            <h1 class="name">{{rating.username}}</h1>
            <div class="star-wrapper">
              <star :size="24" :score="rating.score"></star>
              <span class="delivery" v-show="rating.deliveryTime">{{rating.deliveryTime}}分钟送达</span>
            </div>
            <p class="text">{{rating.text}}</p>
            <div class="recommend" v-show="rating.recommend && rating.recommend.length">
              <span class="icon-thumb_up"></span>
              <span class="item" v-for="item in rating.recommend">{{item}}</span>
            </div>
            <div class="time">{{rating.rateTime}}</div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from '../star/star.vue';
  import split from '../split/split.vue';
  import ratingselect from '../ratingselect/ratingselect.vue';

  const ERR_OK = 0;
  const ALL = 0;
  const POSITIVE = 1;
  const NEGATIVE = 2;
  export default {
    data() {
      return {
        ratings: [],
        ratingType: 0,
        onlyContent: false
      };
    },
    props: {
      seller: {
        type: Object
      }
    },
    methods: {
      theSelectType: function (type) {
        this.ratingType = type;
      },
      IsonlyContent: function (onlyContent) {
        this.onlyContent = onlyContent;
      },
      needShow(type, text) {
        if (this.onlyContent && !text) {
          return false;
        }
        if (this.ratingType === ALL) {
          return true;
        } else {
          return this.ratingType === type;
        }
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
  @import "../../common/stylus/mixin.styl";

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

    .rating-wrapper
      padding: 0 18px
      .rating-item
        display: flex
        padding: 18px 0
        font-size: 0px
        border-1px(rgba(7, 17, 27, 0.1))
        .avatar
          height: 28px
          width: 28px
          flex: 0 0 28px
          margin-right: 12px
          .img
            border-radius: 50%
        .content
          flex: 1
          .name
            font-size: 10px
            line-height: 12px
            color: rgb(7, 17, 27)
            padding-bottom: 4px
          .star-wrapper
            padding-bottom: 6px
            .star
              display: inline-block
              vertical-align: top
              padding-right: 6px
            .delivery
              display: inline-block
              vertical-align: top
              font-size: 10px
              color: rgb(147, 153, 159)
              line-height: 12px
          .text
            padding-bottom: 8px
            font-size: 12px
            line-height: 18px
            color: rgb(7, 17, 27)
          .recommend
            line-height: 16px
            font-size: 0
            .icon-thumb_up
              display: inline-block
              vertical-align: top
              font-size: 12px
              color: rgb(0, 160, 220)
              padding-right: 6px
            .item
              display: inline-block
              padding: 0 6px
              margin-right: 8px
              overflow: hidden
              border: 1px solid rgba(7, 17, 27, 0.1)
              border-radius: 1px
              font-size: 9px
              color: rgb(147, 153, 159)
          .time
            position: absolute
            top: 18px
            right: 0px
            font-size: 10px
            color: rgb(147, 153, 159)
            line-height: 12px

</style>

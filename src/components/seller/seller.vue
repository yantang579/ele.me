<template>
  <div class="seller">
    <div class="overview">
      <h1 class="name">{{seller.name}}</h1>
      <div class="desc border-1px">
        <star :size="36" :score="seller.score"></star>
        <span class="content">({{seller.ratingCount}})</span>
        <span class="content">月售{{seller.sellCount}}单</span>
      </div>
      <div class="favorite">
        <div class="icon-favorite" :class="{'active':favorite}"></div>
        <div class="content">{{IsMarked}}</div>
      </div>
      <ul class="remark">
        <li class="block">
          <h2 class="title">起送价</h2>
          <div class="content">
            <span class="stress">{{seller.minPrice}}</span>元
          </div>
        </li>
        <li class="block">
          <h2 class="title">商家配送</h2>
          <div class="content">
            <span class="stress">{{seller.deliveryPrice}}</span>元
          </div>
        </li>
        <li class="block">
          <h2 class="title">平均配送时间</h2>
          <div class="content">
            <span class="stress">{{seller.deliveryTime}}</span>分钟
          </div>
        </li>
      </ul>
    </div>
<<<<<<< HEAD
    <split></split>
=======
>>>>>>> 660e63c296318d4dea73c952d1ceb9080b31bda7
    <div class="bulletin">
      <h1 class="title">公告与活动</h1>
      <div class="content border-1px">{{seller.bulletin}}</div>
      <ul class="supports" v-if="seller.supports">
        <li class="item border-1px" v-for="(item,index) in seller.supports">
          <span class="icon" :class="classMap[seller.supports[index].type]"></span>
          <span class="text">{{seller.supports[index].description}}</span>
        </li>
      </ul>
    </div>
<<<<<<< HEAD
    <split></split>
=======
>>>>>>> 660e63c296318d4dea73c952d1ceb9080b31bda7
    <div class="pics">
      <h1 class="title">商家实景</h1>
      <div class="pics-wrapper">
        <ul class="pics-list">
          <li class="pic-item" v-for="pic in seller.pics">
            <img :src="pic" width="120px" height="90px">
          </li>
        </ul>
      </div>
    </div>
<<<<<<< HEAD
    <split></split>
=======
>>>>>>> 660e63c296318d4dea73c952d1ceb9080b31bda7
    <div class="info">
      <h1 class="title border-1px">商家信息</h1>
      <div class="content">
        <ul class="info-list">
          <li class="info-item border-1px" v-for="item in seller.infos">{{item}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import star from '../star/star.vue';
<<<<<<< HEAD
  import split from '../split/split.vue';
=======
>>>>>>> 660e63c296318d4dea73c952d1ceb9080b31bda7

  export default {
    created() {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
    },
    data() {
      return {
        favorite: true
      };
    },
    props: {
      seller: {
        type: Object
      }
    },
    computed: {
      IsMarked() {
        return this.favorite ? '已收藏' : '收藏';
      }
    },
    components: {
<<<<<<< HEAD
      star,
      split
=======
      star
>>>>>>> 660e63c296318d4dea73c952d1ceb9080b31bda7
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .seller
    position: absolute
    top: 174px
<<<<<<< HEAD
    bottom: 0
=======
>>>>>>> 660e63c296318d4dea73c952d1ceb9080b31bda7
    left: 0
    width: 100%
    overflow: hidden
    .overview
      position: relative
      padding: 18px
      .name
        font-size: 14px
        color: rgb(7, 17, 27)
        line-height: 14px
        padding-bottom: 8px
      .desc
        font-size: 0px
        color: rgb(77, 85, 93)
        line-height: 18px
        padding-bottom: 18px
        border-1px(rgba(7, 17, 27, 0.1))
        .star
          margin-right: 8px
          display: inline-block
          vertical-align: top
        .content
          padding-right: 12px
          font-size: 10px
          vertical-align: top
      .favorite
        position: absolute
        top: 20px
        right: 18px
        text-align: center
        .icon-favorite
          font-size: 24px
          line-height: 24px
          color: #d4d6d9
          &.active
            color: rgb(240, 20, 20)
        .content
          margin-top: 4px
          font-size: 10px
          line-height: 10px
          color: rgb(77, 85, 93)

      .remark
        display: flex
        padding: 18px
        .block
          flex: 1px
          text-align: center
          border-right: 1px solid rgba(7, 17, 27, 0.1)
          &:last-child
            border: none
          .title
            padding-bottom: 4px
            font-size: 10px
            line-height: 10px
            color: rgb(147, 153, 159)
          .content
            font-size: 10px
            line-height: 24px
            color: rgb(7, 17, 27)
            .stress
              font-size: 24px
    .bulletin
      position: relative
      padding: 18px 18px 16px 18px
      .title
        font-size: 14px
        color: rgb(7, 17, 27)
        line-height: 14px
        padding-bottom: 8px
      .content
        font-size: 12px
        font-weight: 200
        color: rgb(240, 20, 20)
        line-height: 24px
        padding-bottom: 16px
        margin: 0 12px
        border-1px(rgba(7, 17, 27, 0.1))

      .supports
        .item
          padding: 16px 12px
          border-1px(rgba(7, 17, 27, 0.1))
          font-size: 0
          .icon
            display: inline-block
            vertical-align: top
            width: 16px
            height: 16px
            -webkit-background-size: 16px 16px
            background-size: 16px 16px
            margin-right: 6px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_4')
            &.discount
              bg-image('discount_4')
            &.guarantee
              bg-image('guarantee_4')
            &.invoice
              bg-image('invoice_4')
            &.special
              bg-image('special_4')
          .text
            font-size: 12px
            line-height: 16px
            font-weight: 200
            color: rgb(7, 17, 27)

    .pics
      padding: 18px
      .title
        font-size: 14px
        color: rgb(7, 17, 27)
        line-height: 14px
        padding-bottom: 12px
      .pics-wrapper
        width: 100%
        overflow: hidden
        white-space: nowrap
        .pics-list
          font-size: 0
          .pic-item
            display: inline-block
            margin-right: 6px
            width: 120px
            height: 90px
            &.last-child
              margin: 0



    .info
      padding:18px
      .title
        font-size: 14px
        color: rgb(7, 17, 27)
        line-height: 14px
        padding-bottom: 12px
        border-1px(rgba(7,17,27,0.1))
      .content
        .info-list
          .info-item
            border-1px(rgba(7,17,27,0.1))
            padding:16px 12px
            font-size: 12px
            line-height: 16px
            font-weight: 200
            color: rgb(7,17,27)

</style>

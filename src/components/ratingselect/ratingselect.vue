<template>
  <div class="ratingSelect">
    <div class="ratingType border-1px">
      <span @click="select(0,$event)" class="block positive" :class="{'active':selectType===0}">{{desc.all}}<span
        class="count">{{ratings.length}}</span></span>
      <span @click="select(1,$event)" class="block positive" :class="{'active':selectType===1}">{{desc.positive}}<span
        class="count">{{positives.length}}</span></span>
      <span @click="select(2,$event)" class="block negative" :class="{'active':selectType===2}">{{desc.negative}}<span
        class="count">{{negatives.length}}</span></span>
    </div>
    <div @click="toggleContent" class="onlyContent" :class="{'on':onlyContent}">
      <span class="icon-check_circle"></span>
      <span class="text">只看有内容的评价</span>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  const ALL = 0;
  const POSITIVE = 1;
  const NEGATIVE = 2;

  export default {
    data() {
      return {
        desc: {
          all: '全部',
          positive: '满意',
          negative: '不满意'
        },
        selectType: ALL,
        onlyContent: false
      };
    },
    props: {
      ratings: {
        type: Array,
        default() {
          return [];
        }
      }
    },
    computed: {
      //  计算满意的评论个数，返回的是rateType为positive的评论集合，计算positive.length得到个数
      positives() {
        return this.ratings.filter((rating) => {
          return rating.rateType === POSITIVE;
        });
      },
      //  计算不满意的评论个数
      negatives() {
        return this.ratings.filter((rating) => {
          return rating.rateType === NEGATIVE;
        });
      }
    },
    methods: {
      select(type, event) {
        this.selectType = type;
        this.$emit('selectTypeKey', type);
      },
      toggleContent(event) {
        this.onlyContent = !this.onlyContent;
        this.$emit('toggleContentKey', this.onlyContent);
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .ratingSelect
    .ratingType
      margin: 0 24px
      padding: 18px 0px
      border-1px(rgba(7, 17, 27, 0.1))
      font-size: 0
      .block
        display: inline-block
        padding: 8px 12px
        margin-right: 8px
        line-height: 16px
        border-radius: 1px
        font-size: 12px
        color: rgb(77, 85, 93)
        .count
          margin-left: 2px
          font-size: 8px
        &.active
          color: #fff
        &.positive
          background-color: rgba(0, 160, 220, 0.2)
          &.active
            background: rgb(0, 160, 220)
        &.negative
          background-color: rgba(77, 85, 93, 0.2)
          &.active
            background-color: rgb(77, 85, 93)
    .onlyContent
      padding: 12px 18px
      line-height: 24px
      border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      color: rgb(147, 153, 159)
      font-size: 0
      &.on
        .icon-check_circle
          color: #00c850
      .icon-check_circle
        display: inline-block
        margin-right: 4px
        vertical-align: top
        font-size: 24px
      .text
        display: inline-block
        vertical-align: top
        font-size: 12px
</style>

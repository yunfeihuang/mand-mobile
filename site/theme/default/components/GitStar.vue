<template>
  <div class="mfe-git-star">
    <a
      href="https://github.com/didi/mand-mobile"
      target="_blank"
      class="mfe-git-star-button"
      v-tooltip.right="{
        content: number,
        classes: 'mfe-git-star-number',
        show: number > 0,
        trigger: 'manual',
        offset: 5
      }"
    >
      <em></em>
      <span>Star</span>
    </a>
  </div>
</template>

<script>
export default {
  data () {
    return {
      number: 0,
    }
  },
  mounted () {
    setTimeout(() => {
      this.getNumber()
    }, 500)
  },
  methods: {
    getNumber () {
      $.get('https://api.github.com/repos/didi/mand-mobile', (data) => {
        if (data) {
          this.number = data.stargazers_count
        }
      })
    }
  }
}
</script>

<style lang="stylus">
.mfe-git-star
  display flex
  height 45px
  align-items center
  .mfe-git-star-button
    display flex
    width 68px
    height 28px
    line-height 28px
    padding 0 5px
    border-radius 2px
    border 1px solid #d1d2d3
    background-color #eff3f6
    background-image linear-gradient(to bottom, #fafbfc, #e4ebf0)
    transition all .3s
    box-sizing border-box
    text-decoration none
    justify-content center
    &:hover
      background-image linear-gradient(to bottom, #f0f3f6, #dce3ec)
    em
      display inline-block
      width 20px
      height 20px
      margin-top 4px
      background url('../assets/images/github.png') no-repeat
      background-size contain
    span
      margin-left 4px
      color #333
      font-size 12px
      font-weight bold
.mfe-git-star-number
  .tooltip-arrow
    left -3px !important
</style>

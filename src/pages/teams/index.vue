<template>
  <div>
    <i-panel title="球队阵容">
      <view>
        <i-card i-class="split" v-for="item in recommand" :key="item" :extra="item.name" :thumb="item.img">
            <view slot="content">场均得分：{{item.score}}  篮板：{{item.rebotes}}  助攻:{{item.assist}}</view>
        </i-card>
      </view>
    </i-panel>
  </div>
</template>

<script>
export default {
  data () {
    return {
      recommand: []
    }
  },
  onLoad (option) {
    console.log(option.type)
    this.recommand = require('@/data/' + option.type + '.json')
  },
  created () {
  }
}
</script>
<style scoped>
</style>
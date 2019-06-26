<template>
  <div>
    <i-panel title="东部排名">
      <view>
        <i-card i-class="split" v-for="item in recommand" :key="item" :extra="item.name" :thumb="item.img">
            <view slot="content">胜场：{{item.win}}  败场：{{item.lose}}</view>
            <view slot="footer">排名：{{item.Ranking}}</view>
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
div >>> .split {
  margin-bottom: 10pt;
}
</style>
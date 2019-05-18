<template>
  <div>
    
    <i-tabs :current="current" color="#2b85e" bindchange="handleChange">
     <i-tab key="tab1" title="赛事"></i-tab>
     <i-tab key="tab2" title="我的球队"></i-tab>
    </i-tabs>
    
    <i-notice-bar v-if='show' icon="systemprompt" loop>
     {{notice}}
    </i-notice-bar>

    <view v-for="item in basketballteams" :key='item' class="top-padding">
      <i-card :title="item.name" :extra="item.score" thumb="cloud://southafrica.736f-southafrica/rocket.jpg">
        <view slot="content">{{item.introduction}}</view>
      </i-card>
    </view>
    <div>
     <view class="img" style="background-image: url(/static/tabs/1.png)"></view>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'
export default {
  data () {
    return {
      current: 'tab1',
      notice: '2018-2019季后赛',
      grids: ['赛程', '我的球队'],
      basketballteams: [],
      show: true
    }
  },
  components: {
    card
  },
  methods: {
    handleChange ({ detail }) {
      this.setData({
        current: detail.key
      })
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },
  created () {
    const db = wx.cloud.database({ env: 'southafrica' })
    db.collection('basketballteams').get().then(
      res => {
        console.log(res.data)
        this.basketballteams = res.data
      }
    )
  }
}
</script>

<style scoped>
div >>> .no-border {
  border-width: 0pt;
}
div >>> .top-padding {
  padding-top: 10px;
}
</style>
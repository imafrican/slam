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
    <view class="img" style="background-image: url(/static/tabs/1.png)"></view>
    <i-panel title="标题">
    <view style="padding: 15px;"><img src="cloud://southafrica.736f-southafrica/rocket.jpg" style="width:50px;height:50px"><img src="cloud://southafrica.736f-southafrica/rocket.jpg" style="width:50px;height:50px"></view>
    </i-panel>
    <rich-text :nodes="nodes" bindtap="tap"></rich-text>
  </div>
</template>

<script>
import card from '@/components/card'
export default {
  data () {
    return {
      nodes: [{
        name: 'div',
        attrs: {
          class: 'div_class',
          style: 'line-height: 60px; color: red;'
        },
        children: [{
          type: 'text',
          img: 'cloud://southafrica.736f-southafrica/rocket.jpg" style="width:50px;height:50px',
          text: '    &emsp;&emsp;Hello&emsp;World!'
        }]
      }],
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
    tap () {
      console.log('tap')
    },
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
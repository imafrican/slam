<template>
  <div>
    
    <i-notice-bar v-if='show' icon="systemprompt" loop>
     {{notice}}
    </i-notice-bar>
    
    <swiper
      :indicator-dots="indicatorDots"
      :autoplay="autoplay"
      :interval="interval"
      :duration="duration"
      style="height:200px"
    >
    <block v-for="item in imgUrls" :key="item">
      <swiper-item>
        <image :src="item" style="width:100%;height:100%;" />
      </swiper-item>
    </block>
    </swiper>

    <i-grid>
      <i-grid-item @click="goList(item.url)" v-for="item in grids" :key="item">
         <i-grid-icon>
              <image :src="item.img" />
          </i-grid-icon>
          <i-grid-label >{{item.type}}</i-grid-label>
      </i-grid-item>
  </i-grid>

    <view v-for="item in basketballteams" :key='item' class="top-padding">
      <i-card :title="item.name" :extra="item.score" thumb="cloud://southafrica.736f-southafrica/rocket.jpg">
        <view slot="content">{{item.introduction}}</view>
      </i-card>
    </view>
   
  </div>
</template>

<script>
import card from '@/components/card'
export default {
  data () {
    return {
      notice: '2018-2019季后赛',
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000,
      imgUrls: [
        'cloud://southafrica.736f-southafrica/3.jpg',
        'cloud://southafrica.736f-southafrica/2.jpg',
        'cloud://southafrica.736f-southafrica/4.jpg'
      ],
      grids: [
        {type: '东部球队', img: 'cloud://southafrica.736f-southafrica/east.jpg', url: '../east/main?type=1'},
        {type: '西部球队', img: 'cloud://southafrica.736f-southafrica/west.png', url: '../west/main?type=2'}
      ],
      basketballteams: [],
      show: true
    }
  },
  components: {
    card
  },
  methods: {
    goList (url) {
      mpvue.navigateTo({ url })
    },
    goType (type) {
      let url = '../east/main?type=' + type
      mpvue.navigateTo({ url })
    },
    tap () {
      console.log('tap')
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
<template>
  <div @click="clickHandle">
    <i-notice-bar v-if='show' icon="systemprompt" loop>
     {{notice}}
    </i-notice-bar>
    <i-grid i-class="no-border">
     <i-grid-item v-for="item in grids" :key="item" >
     <i-grid-label>{{item}}</i-grid-label>
     </i-grid-item>
    </i-grid>
    
    <i-grid i-class="no-border">
     <i-grid-item i-class="no-border">
        <i-grid-icon>
         <image src="/static/tabs/1.png" />
        </i-grid-icon>
       <i-grid-label>1</i-grid-label>
      </i-grid-item>
      <i-grid-item i-class="no-border">
        <i-grid-icon>
         <image src="/static/tabs/2.png" />
        </i-grid-icon>
        <i-grid-label>2</i-grid-label>
      </i-grid-item>
      <i-grid-item i-class="no-border">
        <i-grid-icon>
         <image src="/static/tabs/3.png" />
        </i-grid-icon>
        <i-grid-label>3</i-grid-label>
      </i-grid-item>
      <i-grid-item i-class="no-border">
       <i-grid-icon>
         <image src="/static/tabs/4.png" />
       </i-grid-icon>
       <i-grid-label>4</i-grid-label>
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
      grids: ['赛程', '我的球队'],
      basketballteams: [],
      show: true
    }
  },
  components: {
    card
  },
  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
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
  padding-top: 50px;
}
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}
.userinfo-nickname {
  color: #aaa;
}
.usermotto {
  margin-top: 150px;
}
.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}
.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}
</style>
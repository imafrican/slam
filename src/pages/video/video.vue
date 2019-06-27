<template>
  <div>
  <i-card>
  <view slot="content"><video style="width: 100%;height=400px;margin:1px;" src="cloud://southafrica.736f-southafrica/video/dear basketball.mp4" binderror="videoErrorCallback"></video></view>
</i-card>
<i-card >
  <view @click="go(url)" slot="content"><img style="width:100%;height:200px" src="cloud://southafrica.736f-southafrica/klay.jpg"></view>
        <view slot="content">汤普森本周将与勇士会面 寻求顶薪合同</view>
</i-card>

   
  </div>
</template>
<script>
import card from '@/components/card'
export default {
  data () {
    return {
      url: 'http://nbachina.qq.com/a/20190627/002202.htm?pageShare=true?from=app&type=news&column=banner&articleId=20190627002312kind=0',
      components: {
        card
      },
      methods: {
        go (url) {
          window.location.href = url
        }
      },
      tap () {
        console.log('tap')
      }
    }
  }
}
</script>
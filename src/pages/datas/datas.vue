<template>
  <div>
    <swiper
      :indicator-dots="indicatorDots"
      :autoplay="autoplay"
      :interval="interval"
      :duration="duration"
      style="height:150px"
    >
    <block v-for="item in imgUrls" :key="item">
      <swiper-item>
        <image :src="item" style="width:100%;height:100%;" />
      </swiper-item>
    </block>
    </swiper>


    <i-tabs :current="current" color="#f759ab" bindchange="handleChange">
     <i-tab key="tab1" title="东部赛区"></i-tab>
     <i-tab key="tab2" title="西部赛区"></i-tab>
    </i-tabs>
  </div>
</template>

<script>
export default {
  components: {
  },
  data () {
    return {
      current: 'tab1',
      imgUrls: [
        'cloud://southafrica.736f-southafrica/2.jpg',
        'cloud://southafrica.736f-southafrica/3.jpg',
        'cloud://southafrica.736f-southafrica/4.jpg'
      ],
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000
    }
  },
  methods: {
    handleChange ({ detail }) {
      this.setData({
        current: detail.key
      })
    }
  },
  created () {
  }
}
</script>

<style>

</style>
<template>
    <div>
        <i-row>
    <i-col span="8" i-class="col-class">col-8</i-col>
    <i-col span="8" i-class="col-class">col-8</i-col>
    <i-col span="8" i-class="col-class">col-8</i-col>
       </i-row>
    </div>
</template>

<script>

export default {
  methods: {
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    }
  },

  created () {
    wx.cloud.callFunction({ name: 'me' }).then(
      res => {
        console.log(res)
      }
    )
  }
}
</script>

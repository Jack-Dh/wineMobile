<template>
  <div class="home">

  <div style="width: 100%;height: 40%">
    <img style="width: 100%;height: auto" :src="parameter">
  </div>



  </div>
</template>

<script>


  export default {
    name: 'home',
    data() {
      return {
        parameter: '',//图片地址
      }
    },
    methods:{
      imgLoad(){
        let url = window.location.href
        let a = url.indexOf('=')
        this.parameter = url.substring(a + 1)

        this.$axios.get('http://qrcode.jiajiachuang.cn/qrcode/qrcode/selectById', {
          params: {
            id: this.parameter
          }
        }).then(res => {
          this.parameter = `http://${res.data.data.imageUrl}`
        })
      }
    },
    created: function () {
      this.imgLoad()
    }
  };
</script>

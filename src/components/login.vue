<template>
  <div>
    <div class="non">
      <div class = "Logo"></div>
      <div class = "index">불법 스포트도박 사이트 URL</div>
      <button type="button" v-on:click="onexport" class="btn">Excel download</button>
    </div>
  </div>
</template>
<script>
// import Vue from 'vue'
import axios from 'axios'
import XLSX from 'xlsx'

export default {
  name: 'login',
  data: () => ({
    Datas: {
      'sites': [
      ]
    }
  }),
  methods: {
    async onexport () {
      var result = await axios.post('http://soylatte.kr:3000/image/excel', {
        some: 'data'
      }).catch((response) => {
        alert('연동 실패!')
        return 0
      })
      result = result.data
      for (var i = 0; result[i] != null; i++) {
        let data = result[i]
        this.Datas.sites.push(data)
      }
      var site = XLSX.utils.json_to_sheet(this.Datas.sites)
      var siteWS = XLSX.utils.book_new()
      XLSX.utils.book_append_sheet(siteWS, site, 'sites')
      XLSX.writeFile(siteWS, 'site.xlsx')
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body{
  margin : 0;
}
.btn {
  width: 20vw;
  height: 15vh;
  color: #fff;
  background: #77c043;
  border: 1px solid #e2e2e2;
  margin-left: 40vw;
  margin-top: calc(24vh - 1vw);
  box-sizing: border-box;
  font-size: 4.5vh;
  border-radius: 0.3em;
}
.Logo {
  width: 15vh;
  height: 15vh;
  margin-left: 1.5vw;
  margin-top: 1vw;
  background-image: url('../assets/logo.png');
  background-size: contain;
  background-repeat: no-repeat;
}
.index {
  width: 40vw;
  margin-left: 30vw;
  text-align: center;
  margin-top: 15vh;
  color: #fff;
  font-size: 6vh;
}
</style>

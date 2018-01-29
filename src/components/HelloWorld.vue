<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="box">
      <img :src="headerImg" alt="" srcset="">
    </div>
    <input type="text" v-model="valInp">
    <button @click="hashImg">hash</button>
  </div>
</template>

<script>
  import Identicon from 'identicon.js'
  import crypto from 'crypto'
  export default {
    name: 'HelloWorld',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        valInp: '',
        headerImg:''
      }
    },
    methods: {
      hashImg() {
        if (this.valInp) {
          let hash = crypto.createHash('md5');
          hash.update(this.valInp);
          var options = {   //配置项
            foreground: [   //前景色，为了使得产生的图片颜色不同，随机产生三个0-255的数字
              parseInt(Math.random() * 255),
              parseInt(Math.random() * 255),
              parseInt(Math.random() * 255),
              255
            ],
            background: [240, 240, 240, 255],
            margin: 0.1,
            size: 400,
            format: 'svg'
          };
          var data = new Identicon(hash.digest('hex'), options).toString();
          this.headerImg = "data:image/svg+xml;base64," + data;
        }

      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1,
  h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
.box{
  widows: 400px;
  height: 400px;
  margin-bottom: 20px;
}
</style>

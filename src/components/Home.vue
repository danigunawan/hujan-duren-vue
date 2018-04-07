<template>
  <div class="container">
    <div class="playboard">
      <div class="duren" :style="{ 'margin-left': marginLeftDuren + '%', 'top': 'calc(' + marginTopDuren + '% - 20px)'  }"></div>
    </div>
    <div class="controller">
      <div class="bucket"  :style="{ 'margin-left': marginLeft + '%', 'margin-top': marginTopBucket + '%'}">
      </div>
      <button v-shortkey="['arrowleft']" @shortkey="moveLeft" @click="moveLeft"class="button">Kiri</button>
      <button v-shortkey="['arrowright']" @shortkey="moveRight" @click="moveRight " class="button">Kanan</button>
      <h3>Point: {{point}}</h3>
      <p><b>* Bisa gunakan arrow key left atau right di keyboard untuk menggerakan bucket </b> </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      point: 0,
      marginLeft: 49,
      marginTopBucket: 40,
      marginLeftDuren: 49,
      marginTopDuren: 0
    }
  },
  mounted () {
    this.durianPosition()
    this.durianFall()
  },
  methods: {
    moveLeft () {
      this.marginLeft -= 2
    },
    moveRight () {
      this.marginLeft += 2
    },
    durianPosition () {
      const position = Math.random() * 70
      this.marginLeftDuren = position
    },
    getDuren () {
      let toleransiKiri = this.marginLeft - 4
      let toleransiKanan = this.marginLeft + 8
      if (this.marginTopDuren === 100 && (this.marginLeftDuren === this.marginLeft || (this.marginLeftDuren >= toleransiKiri && this.marginLeftDuren <= toleransiKanan))) {
        this.point++
      }
    },
    durianFall () {
      const app = this
      let fall = setInterval(function () {
        app.marginTopDuren += 2
        app.getDuren()
        if (app.marginTopDuren === 100) {
          clearInterval(fall)
          app.marginTopDuren = 0
          app.durianPosition()
          app.durianFall()
        }
      }, 30)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1, h2 {
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

.bucket {
  background-color: black;
  width: 100px;
  height: 30px;
  margin-right: auto;
  margin-bottom: 2%;
}

.duren {
  background-color: orange;
  width: 30px;
  height: 30px;
  margin-right: auto;
  position: absolute;

}
.playboard {
  height: calc(100vh - 259px);
  position: relative;
}
.controller {
  width: 100%;
  position: fixed;
  bottom: 0;
}

a {
  color: #35495E;
}
.button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
}
</style>

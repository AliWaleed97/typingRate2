<template>
  <div class="clientsAdmin" align="left">
    <!-- Clients Admin -->
    <section id="four" class="wrapper style1 special fade-up">
      <div class="container">
        <header class="major">
          <h2>Entry</h2>
          <br>
          <br>
          <button class="button special" v-on:click="Start()">Start</button>
          <br>
          <input type="text" class="form-control" placeholder="Text" v-model="text">
          <br>
          <button class="button special" v-on:click="Stop()">Stop</button>
          <br>
          <br>
          <button class="button special" v-on:click="Open()">Download</button>
        </header>
      </div>
    </section>
  </div>
</template>
<script>
import env from '../env'
import auth from '../auth'
export default {
  name: 'clientsAdmin',
  data() {
    return {
      text: '',
      duration: '',
      startTime: '',
      endTime: '',
      url: '',
      boolean: false
    }
  },
  methods: {
    Open: function() {
      URL = env.URL.concat('/uploads/typingRate.csv')
      console.log(URL)
      window.open(URL)
    },
    Start: function() {
      this.startTime = new Date()
      this.startTime = this.startTime.getTime()

    },
    Stop: function() {
      this.endTime = new Date()
      this.endTime = this.endTime.getTime()
      var elapsedTime = (this.endTime - this.startTime) / 1000
      console.log(elapsedTime)
      this.$http.post(env.URL + '/admin/sendEntry', {
        "text": this.text,
        "time": elapsedTime,

      }).catch((error) => {
        console.log(error)
      })

    }
  },
  created() {
    this.url = env.URL
  }

}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#scroll {
  position: fixed;
  bottom: 100px;
  right: 50px;
}

img {
  height: auto;
}

img {
  max-width: 100%;
  border: none;
}

@media (min-width: 768px) .col-sm-12 {
  width: 100%;
}

</style>

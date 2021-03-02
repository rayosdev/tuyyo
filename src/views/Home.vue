<template>
  <div>
  <h1>Sueno es fantastico</h1>
  <div class="home">
    <div class="claudia card">
      <div class="claudia-img"></div>
      <div class="wrapper">
        <h2>Claudia Jimena Montero Pino</h2>
        <h3>Peru</h3>
        <h3>{{peru}}</h3>
        <button 
          @click="peruConvertOpen = !peruConvertOpen" 
          :class="{'active': peruConvertOpen}"
        >time converter</button>
        <div 
          class="convert-container" 
          :class="{'open': peruConvertOpen}"
        >
          <div>
            Peru: <input v-model="convertPeru" type="time"> 
          </div>
          <div>
            Norway: <span>{{convertedToNorway | invalidTime}}</span> 
          </div>
        </div>
      </div>
    </div>
    <div class="jared card">
      <div class="jared-img"></div>
      <div class="wrapper">
        <h2>Jared Anders Isaksen</h2>
        <h3>Norway</h3>
        <h3>{{norway}}</h3>
        <button 
          @click="norwayConvertOpen = !norwayConvertOpen" 
          :class="{'active': norwayConvertOpen}"
        >time converter</button>
        <div 
          class="convert-container" 
          :class="{'open': norwayConvertOpen}"
        >
          <div>
            Norway: <input v-model="convertNorway" type="time"> 
          </div>
          <div>
            Peru: <span>{{convertedToPeru | invalidTime}}</span> 
          </div>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import moment from 'moment-timezone'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data() {
    return {
        peru: moment.tz('America/Lima').format(),
        norway: moment.tz('Europe/Oslo').format(),
        convertPeru: '00:00',
        convertNorway: '00:00',
        convertedToPeru: '00:00',
        convertedToNorway: '00:00',
        peruConvertOpen: false,
        norwayConvertOpen: false,
      }
  },
  mounted() {
    setInterval(() => {
      this.peru = moment.tz('America/Lima').format('HH:mm:ss')
      this.norway = moment.tz('Europe/Oslo').format('HH:mm:ss')
    }, 100)
  },
  watch: {
    convertNorway(value){
      this.convertedToPeru = moment(value, 'HH:mm').tz('Europe/Oslo').tz('America/Lima').format('HH:mm')
    },
    convertPeru(value){
      this.convertedToNorway = moment(value, 'HH:mm').add(6, 'hours').format('HH:mm')
    }
  },
  filters: {
    invalidTime: value => {
      if(value != 'Invalid date') return value
      return '00:00'
    }
  }
}
</script>
<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Dancing+Script&family=Shadows+Into+Light&family=Syncopate&display=swap');

  body {
    background: linear-gradient(304.7deg, #405a7b 0%, #00285a 100%);
    font-family: 'Ballet', cursive;
    display: grid;
    justify-content: center;
    align-content: center;
    /* height: 100vh; */
  }
  h1 {
    color: rgb(126, 21, 175);
  }

  .home {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    color: #FFF;
    margin-top: 2rem;
  }

  .card {
    transition: all .4s;
    padding: 0 2rem;

    .wrapper {
      height: 280px;
    }
  }

  h2 {
    font-family: 'Dancing Script', cursive;
  }

  .jared h2 {
    font-family: 'Shadows Into Light', cursive;
    line-height: 1;
  }

  .card {
    margin: 0 1rem;
    max-width: 90%;
    display: grid;
    justify-items: center;
  }

  .claudia-img,
  .jared-img {
    width: 150px;
    height: 150px;
    background-size: 150px;
    border-radius: 50%;
    border: solid #162a43 15px;
  }

  .claudia-img {
    background-image: url(../assets/claudia.jpg);
  }
  .jared-img {
    background-image: url(../assets/jared.jpg);
  }

  .wrapper button {
    cursor: pointer;
    margin-bottom: 1rem;
    padding: 10px 15px;
    background: #162a43;
    color: #fff;
    transition: all .2s;
    font-weight: 800;
    border: none;

    &.active {
      transition: all .2s;
      background: #fff;
      color: #162a43;
    }
  }

  .convert-container {
    background: #203855;
    overflow: hidden;
    height: 0px;
    transition: all .2s;

    &.open {
      transition: all .2s;
      padding: 10px;
      height: 90px;
    }
    
    & > :nth-child(1) {
      margin-bottom: 1em;

      & input {
        padding: 5px 10px;
      }
    }
  }

</style>

<template lang="pug">
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Gogo</h1>
    ul
      li(v-for="artist in artists") {{artist.name}}
    ul
      artist(v-for="artist in artists" v-bind:artist="artist")
    h1 Tablas
    table
      th Nombre
      th Edad
      tr
      td Emiliano
      td 38
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template>
<template lang="pug">
  <div id="app">
    <img src="./assets/logo.png">
    h1 Album Music
    select 
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name}}
      select(v-model="selectedCountry")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid") 
    
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>
<script>
export default {
  name: 'app',
  data () {
    return {
      artists:[
      {name:'David Bowie'},
      {name:'Mana'},

      ]
    }
  }
}
</script>
<script>
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[]
    }
  },
  mounted: function (){
    const self = this
    getArtists()
      .then(function (artists) {
        self.artists = artists
      })

  }
}
</script>
<script>
import Artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[]
    }
  },
  components:{
    Artist
  },
  mounted: function (){
    const self = this
    getArtists()
      .then(function (artists) {
        self.artists = artists
      })

  }
}
</script>
<script>
import Artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
      { name:'Mexico',value:'mexico'},
      { name:'Argentina',value:'argentina'},
      { name:'Colombia',value:'colombia'},
      ]
    }
  },
  components:{
    Artist
  },
  mounted: function (){
    const self = this
    getArtists()
      .then(function (artists) {
        self.artists = artists
      })

  }
}
</script>
<script>
import Artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
      { name:'Mexico',value:'mexico'},
      { name:'Argentina',value:'argentina'},
      { name:'Colombia',value:'colombia'},
      { name:'España',value:'spain'},
      ],
      selectedCountry: 'mexico'
    }
  },
  components:{
    Artist
  },
  methods:{
    refreshArtists(){
      const self = this
    getArtists(this.selectedCountry)
      .then(function (artists) {
        self.artists = artists
      })

    }
  },
  mounted(){
    this.refreshArtists()
  },
  watch: {
    selectedCountry(){
      this.refreshArtists()

    }
  }
}
</script>

<style lang="stylus">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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

a {
  color: #42b983;
}
table, th, td, tr
  border: 2px solid green;
</style>

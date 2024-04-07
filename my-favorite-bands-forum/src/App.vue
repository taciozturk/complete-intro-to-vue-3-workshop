<script>
  export default {
    data() {
          return {
            band: {
              name: '',
              genre:[],
            },
            bands: [
              {
                name:"Opeth",
                genre:['Progressive','Death'],
              }, 
              {
                name:"Tool",
                genre:['Progressive','Alternative'],
              },
              {
                name:"Gojira",
                genre:['Progressive','Death']
              },
              {
                name:"Deftones",
                genre:['Alternative','Nu'],
              },
              {
                name:"Behemoth",
                genre:['Black', 'Death'],
              },
            ],
            favorites: [],
          };
        },
    computed: {
      bandStatistics() {
        const genres = ['Progressive','Alternative','Death','Black','Nu']
        const statistics = {
          Progressive:0,
          Alternative:0,
          Death:0,
          Black:0,
          Nu:0,
        }

        this.bands.forEach(band => {
          genres.forEach(genre => {
            if(band.genre.indexOf(genre) > -1) {
              statistics[genre] += 1
            }
          })
        })
        return statistics
      }
    },
    methods: {
      addBand() {
        this.bands.push(this.band)
      },
      addToFavorites(band) {
        this.favorites.push(band)
      }
    }
  }
</script>

<template>
  <h2>Statistics</h2>
  <ul>
    <li v-for="(value, key) in bandStatistics"
      :key="`value-${key}`">
      {{key}}: {{value}}
    </li>
  </ul>
  <h1>My Favorite Bands</h1>
  <ul v-if="favorites.length > 0">
    <li v-for="(fav,index) in favorites" 
      :key="`fav-${index}`">
      <p> {{ fav.name }} </p>
    </li>
  </ul>
  <p v-else>No favorite band yet!</p>
  <hr>
  <h2>New Band</h2>
  <div>
    <label>Band Name:</label>
    <input type="text" v-model="band.name"/>
  </div>
  <button v-on:click="addBand">Add Band</button>
  <hr>
  <h1>List of Rock/Metal Bands</h1>
  <ul>
      <li v-for="(band,index) in bands"
        :key="`band-${index}`">
        <p>{{band.name}}</p>
        <button @click="addToFavorites(band)">⭐Favorite</button>
      </li>
      
  </ul>
</template>



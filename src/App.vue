<template>
  <button @click="showFilm" class="addFilm" v-on:click="addFilms" :disabled="numFilms>= films.length">Add Film</button> Liked: {{ likes }} Disliked: {{ dislikes }}
  <ul>
    <li v-for="film in displayedFilms">
      <Film :film="film" @close="removeFilm(film)"></Film>
      <hr>
    </li>
  </ul>
</template>

<script>
  import Film from './components/Film.vue'
  export default {
    name: 'App',
    components: {
      Film
    },
    data() {
      return {
        numFilms: 3,
        films: [{title: "Star Wars (1977)", actors: ["Mark Hamill", "Harrison Ford", "Carrie Fisher", "R2D2", "C3P0"], like: 0},
                {title: "Toys Story (1955)", actors: ["Tom Hanks", "Tim Allen", "Don Rickles", "Woody", "Buzz Lightyear"], like: 0},
                {title: "X-Men", actors: ["Michael", "Fassbender", "James Macavoy", "Jennifer Lawrence"], like: 0},
                {title: "Avengers", actors: ["Mark Ruffalo", "Robert Downey Jr", "Chris Hemsworth", "Chris Evans", "Scarlett Johanson"], like: 0},
                {title: "Men In Black", actors: ["Will Smith", "Tommy Lee Jones", "Random Actor", "Random Actor2"], like: 0},
                {title: "Random Movie", actors: ["Random Actor 1", "Random Actor 2", "Random Actor 3", "Random Actor 4"], like: 0}
              ]
      }
    },
    methods: {
      removeFilm(film) {
            const index = this.films.indexOf(film)
            this.films.splice(index, 1)
            this.numFilms -= 1
        }
    },
    computed: {
      addFilms() {
        this.numFilms += 1
      },
      displayedFilms() {
        return this.films.slice(0, this.numFilms)
      },
      likes() {
        return this.films.filter((film)=>film.like===1).length
      },
      dislikes() {
        return this.films.filter((film)=>film.like===-1).length
      }
    }
  }
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: left;
  color: #000000;
  margin-top: 2rem;
  margin-left: 1rem;
}
button {
        padding: 0.5rem 3rem;
        background-color: white;
        border-color: rgb(101, 141, 155);
        border-style: solid;
        margin-right: 1rem;
    }
ul {
  .box {
        padding: 100px 0;
        width: 400px;
        text-align: center;
        background: #ddd;
        margin: 20px;
        display: inline-block;
    }
    li {
        list-style-type: none;
    }
    li.fav {
        background: #ff9ed2;
        color: white;
    }
    .addFilm {
      padding: 10rem;
    }
}
</style>

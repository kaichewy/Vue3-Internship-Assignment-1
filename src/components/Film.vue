<template>
    <div :class="{'liked': film.like===1, 'disliked': film.like===-1}">
        <button @click="closeFilm">Delete</button> {{film.title}} ({{ film.year }})<button class="like" @click="like" :disabled="film.like==-1">{{film.like==1 ? "Liked" : "Like" }}</button> <button class="dislike" @click="dislike" :disabled="film.like==1">{{film.like==-1 ? "Disliked" : "Dislike" }}</button>
        <ul>
            <li v-for="actor in displayedActors">
                <button @click="removeActor(actor)">Delete</button> {{ actor }}
            </li>
            <li v-if="this.numActors < this.film.actors.length">
                <button class="addActor" @click="addActors">Add Actor</button>
            </li>
        </ul>
    </div>
</template>

<script>
  export default {
    data() {
        return {
            numActors: 3,
        }
    },
    props: ['film'],
    methods: {
        closeFilm() {
            this.$emit('close')
        },
        addActors() {
            this.numActors += 1
        },
        removeActor(actor) {
            const index = this.film.actors.indexOf(actor)
            this.film.actors.splice(index, 1)
            this.numActors -= 1
        },
        like() {
            if (this.film.like==1) {
                this.film.like = 0
            } else {
                this.film.like = 1
            }
        },
        dislike() {
            if (this.film.like==-1) {
                this.film.like = 0
            } else {
                this.film.like = -1
            }
        }
    },
    computed: {
        displayedActors() {
            return this.film.actors.slice(0, this.numActors)
        }
    }
}
</script>


<style scoped>
    button {
        padding: 0.5rem;
        background-color: white;
        border-color: rgb(101, 141, 155);
        border-style: solid;
    }
    .addActor {
        padding: 0.5rem 3rem;
    }
    li {
        margin: 1rem 0.25rem;
    }
    .like, .dislike button{
        margin: 0rem 2rem;
        padding: 0.5rem 1rem;
    }
    .liked {
        background-color: aqua;
    }
    .disliked {
        background-color: orange;
    }
    div {
        padding: 2rem;
    }
</style>
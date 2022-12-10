<template>
    <header>
        <h1>Movies list</h1>
    </header>
    <section>
        <h2>Choose movie</h2>
        <ul>
            <SingleMovie v-for="movie in movies" :movie="movie" :key="movie" :toggle="toogleShowMovie" :idToShow="idMovieToShow" />
        </ul>
    </section>
</template>

<script>
    import SingleMovie from './SingleMovie.vue';

    export default {
        components: {
            SingleMovie
        },
        data() {
            return {
                movies: [{title: 'movie 1', src: './movie1.mp4', duration: '15 sec'}, {title: 'movie 2', src: './movie2.mp4', duration: '32 sec'}, {title: 'movie 3', src: './movie3.mp4', duration: '9 sec'}, {title: 'movie 4', src: './movie4.mp4', duration: '17 sec'}],
                idMovieToShow: null
            }
        },
        methods: {
            toogleShowMovie(id) {
                this.idMovieToShow = this.idMovieToShow === id ? null : id;
            }
        }
    }
</script>

<style lang="scss">
    body {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 0 auto;
        @media only screen and (max-width: 720px) {
            max-width: 100%;
        }
    }
    #app {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 50rem;
        @media only screen and (max-width: 720px) {
            max-width: 100%;
        }
        header {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 10rem;
            width: 100%;
            background-color: #3385ff;
            border-radius: 0.25rem;
            box-shadow: 0px 0px 4px 1px #3385ff;
            margin-bottom: 0.5rem;
            h1 {
                font-size: 3rem;
                color: #ffffff;
                font-style: italic;
                text-transform: uppercase;
            }
        }
        ul {
            list-style: none;
            padding: 0;
            padding: 0.5rem;
        }
    }
</style>
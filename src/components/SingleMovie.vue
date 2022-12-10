<template>
    <li class="movie-item">
        <div>
            <h3>Title: {{movie.title}}</h3>
            <h4>Duration: {{movie.duration}}</h4>
            <button @click="toggle(movie.title)">{{setBtnText}}</button>
        </div>
        <video ref="videoRef" :src="movie.src" :class="toShow(movie.title)" @timeupdate="showStartOrHalfTime" @ended="showEndVideo" controls></video>
    </li>
</template>

<script>



export default {
    props: {
        movie: Object,
        toggle: Function,
        idToShow: String
    },
    data() {
        return {
            isShowed: false,
            isStartVideo: false,
            isHalfTimeVideo: false
        }
    },
    methods: {
        toShow(id){
            this.isShowed = id === this.idToShow;
            return this.isShowed ? 'collapsed' : ''
        },
        showStartOrHalfTime() {
            if(!this.isStartVideo) {
                console.log('start of video')
                this.isStartVideo = true;
            }
            if(!this.isHalfTimeVideo && this.$refs.videoRef.currentTime >= this.$refs.videoRef.duration/2) {
                console.log('half time of video');
                this.isHalfTimeVideo = true;
            }
            
        },
        showEndVideo() {
            console.log('end of video');
            this.isStartVideo = false;
            this.isHalfTimeVideo = false;

        }
    },
    computed: {
        setBtnText() {
            return this.isShowed ? 'hide' : 'show'
        }
    }
}
</script>

<style lang="scss">
    #app {
        section {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
            height: 100vh;
            background-color: #def0ff;
            box-shadow: 0px 0px 4px 1px #def0ff;
            border-radius: 0.25rem;
            h2 {
                font-size: 2rem;
            }
        }
        .movie-item {
            div {
                display: flex;
                justify-content: space-between;
                align-items: center;
                button {
                    background-color: #3385ff;
                    border: 0.125rem solid #3385ff;
                    border-radius: 0.25rem;
                    color: #ffffff;
                    font-weight: bolder;
                    height: 2rem;
                    width: 4rem;
                    &:active {
                        background-color: #33CCFF;
                        border: 0.125rem solid #33CCFF;
                    }
                }
            }
            video {
                width: 30rem;
                height: 0;
                opacity: 0;
                transition: opacity 1.2s 0s;
                &.collapsed {
                    height: 20rem;
                    opacity: 1;
                }
                @media only screen and (max-width: 720px) {
                    max-width: 100%;
                }
            }
        }
    }
</style>
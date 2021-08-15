<template>
    <div class="block" v-if="showBlock" @click="stopTimer">
        Click Me!
    </div>    
</template>


<script>
export default {
    props: ['delay'],
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0,
        }
    },
    methods:
    {
        startTimer(){
            this.timer = setInterval(() => {
                this.reactionTime += 10
            }, 10)
        },
        stopTimer(){
            clearInterval(this.timer)
            console.log(this.reactionTime)
            // emitting event up
            this.$emit('end', this.reactionTime)
        }
    },
    mounted() {
        console.log('Component mounted')
        setTimeout(() => {
            this.showBlock = true
            this.startTimer()
            console.log(this.delay)
        }, this.delay)
    },
    updated() {
        console.log('Component updated')
    },
    unmounted(){ // good for working with the vue router...
        console.log('Unmounted')
    },
}
</script>'

<style scoped>
    .block {
        width: 400px;
        border-radius: 20px;
        background: #0faf87;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>
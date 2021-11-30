<template>
  <div class="duck">
      <img src="../assets/duck.png" alt="duck"\
      v-if="isVisible"
      :style="{top: topValue +'%', left: leftValue + '%'} "
      @click="hit"
    >
  </div>
</template>

<script>
export default {
    name: "Duck",
    props: {
        delay: Number

    },
    data() {
        return {
            topValue: 4,
            leftValue: 40,
            isVisible: false,
            startTime: null

        };
    },
    methods: {
        hit(){
            this.isVisible = false;
            const endTime = Date.now();
            const responseTime = this.endTime - this.startTime;

            this.$emit("hit", responseTime);
        },

        showDuck() {
            this.topValue = Math.random()*85+5;
            this.leftValue = Math.random()*85+5;
            this.isVisible = true;
            this.startTime = Date.now();

        },
    },
    mounted () {
        this.showDuck();

        setInterval( ()=>{
            this.showDuck();
        } , this.delay);
        
    }
}
</script>

<style scoped>

.duck {
    position: absolute;
    width: 80px;
    left: 50px;
    top: 30px;
    cursor: crosshair;
}

img {
    width: 100%;
}

</style>
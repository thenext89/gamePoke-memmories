<script>
export default {
  props: {
    time: {
      type: Number,
      required: true,
    },
  },
  methods:{
    onstartAgain(){
      this.$emit("onstartAgain");
    }
  }
};
</script>
<template lang="">
  <div class="screen">
    <h1>results</h1>
    <h2>Time: {{ Math.round(time / 1000) }}</h2>
    <button @click="onstartAgain">Start Again</button>
  </div>
</template>
<style scoped>
.screen{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}
h1{
  font-size: 5rem;
  color: #fff;
}
h2{
  font-size: 2rem;
  color: #fff;
}
button{
  font-family: var(--font-text);
  width: 8rem;
  height: 3rem;
  font-size: 1.6rem;
  border-radius: 1.5rem;
  margin-top: 1rem;
  cursor: pointer;
}</style>

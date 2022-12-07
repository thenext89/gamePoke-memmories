<script>
export default {
  name: "MainScreen",
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>
<template>
  <div class="screen">
    <h1>POKEMON</h1>
    <h3>select mode game</h3>
    <div class="action">
      <button @click="onStart(16)">
        <span>4X4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6X6</span>
        <span>simple</span>
      </button>
      <button @click="onStart(64)">
        <span>8X8</span>
        <span>medium</span>
      </button>
      <button @click="onStart(100)">
        <span>10X10</span>
        <span>hard</span>
      </button>
    </div>
  </div>
</template>
<style scoped lang="css">

.screen{
  height: 100vh;
  color:#fff;
  position: relative;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
h1{
  font-size: 5rem;
}
h3{
  font-size: 2rem;
}
.action{
  margin-top: 3rem;
}
.action button{
  background-color: transparent;
  color: var(--light);
  border: .3rem solid #fff;
  width: 10rem;
  height: 10rem;
  margin: 0 2rem;
  /* display: flex;
  justify-content: center;
  align-items: center; */
  border-radius: 2rem;
  cursor: pointer;

  box-shadow: .3rem .3rem 1rem rgb(190, 26, 26);
}
.action button:focus{
  border: .5rem solid red;
}
.action button:nth-child(2){
  box-shadow: .3rem .3rem 1rem rgb(26, 53, 190);
}
.action button:nth-child(3){
  box-shadow: .3rem .3rem 1rem rgb(190, 135, 26);
}
.action button:nth-child(1){
  box-shadow: .3rem .3rem 1rem rgb(37, 190, 26);
}
button span{
  display: block;
  margin-top: .5rem;

}
</style>

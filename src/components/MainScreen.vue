<template>
  <div class="screen">
    <h1>POKEMON CARDS MEMORIES GAME</h1>
    <h3>Select mode to start game</h3>
    <div class="modes">
      <button @click="onStart(4)">
        <span>2x2</span>
        <span>Super Easy</span></button
      ><button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>Asian</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background-color: var(--dark);
  color: var(--light);
}
.screen h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}
.screen p {
  font-size: 2rem;
}
.modes {
  display: flex;
  margin-top: 2rem;
}
.modes button {
  font: var(--font);
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}
.modes button:hover {
  background-color: var(--light);
  color: var(--dark);
}
.modes button span:first-child {
  font-size: 2rem;
}
.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
@media only screen and (max-width: 720px) {
  .screen {
    width: 100vw;
    justify-content: flex-start;
    padding: 40px;
  }
  .screen h1 {
    font-size: 4rem;
    text-align: center;
  }
  .modes {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  .modes button {
    margin: 10px;
    width: 100px;
    height: 100px;
  }
}
</style>

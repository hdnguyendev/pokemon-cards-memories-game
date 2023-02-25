<template>
  <div class="screen">
    <div class="btn__back">
      <button @click="onStartAgain">
        <span>👈</span>
        <span>Back</span>
      </button>
    </div>
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((heightScreen - 16 * 4) / Math.sqrt(cardsContext.length) - 16) *
            3) /
            4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        :rules="rules"
        :widthScreen="widthScreen"
        :heightScreen="heightScreen"
        @onFlip="checkRule($event)"
      ></card-flip>
    </div>
  </div>
</template>
<script>
import CardFlip from "./CardFlip.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
      count: 0,
      widthScreen: window.innerWidth,
      heightScreen: window.innerHeight,
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length >= 2) {
        return false;
      }
      this.rules.push(card);
      console.log(card);
      console.log(this.rules);
      if (this.rules.length === 2) {
        if (this.rules[0].index != this.rules[1].index)
          if (this.rules[0].value === this.rules[1].value) {
            console.log("Right");
            this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMode();
            this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMode();
            this.count += 1;
            if (this.count === this.$props.cardsContext.length / 2) {
              setTimeout(() => {
                this.$emit("onFinish");
              }, 920);
            }
            this.rules = [];
            // reset rules
          } else if (this.rules[0].value !== this.rules[1].value) {
            console.log("Wrong");
            setTimeout(() => {
              this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
              this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
              this.rules = [];
              console.log(this.rules);
            }, 800);
          } else {
            this.rules = [];
          }
      }
    },
    onStartAgain() {
      console.log(this.rules);
      this.$emit("onStartAgain");
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
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
.screen .btn__back button {
  position: absolute;
  top: 0;
  left: 0;
  font: var(--font);
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  margin: 1rem;
  padding: 1rem 1.25rem;
  border-radius: 0.5rem;
  font-size: 1.25rem;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}
.screen .btn__back button:hover {
  background-color: var(--light);
  color: var(--dark);
}

@media only screen and (max-width: 720px) {
  .screen {
    max-width: 100vw;
    overflow-x: hidden;
  }
  .screen__inner {
    max-width: 100vw;
    display: flex;
    justify-content: center;
  }
  .screen .btn__back button {
    position: fixed;
    left: auto;
    top: auto;
    right: 0;
    bottom: 10px;
    z-index: 100;
  }
}
</style>

<template>
  <div class="container text-center w-25 mt-2 px-0" :style="diceShow">
    <!-- eslint-disable-next-line -->
    <span id="dice" v-for="(die, index) in dice" :key="index" v-html="getHexCodeDice(die)"></span>
  </div>
</template>

<script>
export default {
  props: {
    dice: {
      type: Array,
      required: true
    }
  },
  data() {
    return {};
  },
  computed: {
    diceShow() {
      return {
        height: "153px",
        background: "white",
        opacity: this.dice.length ? 0.9 : 0
      };
    }
  },
  methods: {
    getHexCodeDice(die) {
      return `&#x268${die - 1};`;
    }
  }
};
</script>

<style>
.diceshow {
  opacity: 0.9;
}

.visibleDice {
  opacity: 0.9;
}
.invisibleDice {
  opacity: 0;
}

#dice {
  font-size: 6rem;
}
</style>
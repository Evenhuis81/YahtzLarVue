<template>
  <div class="container text-center w-25 mt-2 px-0" :style="diceShow">
    <!-- eslint-disable-next-line -->
    <span
      class="rolledDice"
      id="dice"
      v-for="(die, index) in dice"
      :key="index"
      v-html="getHexCodeDice(die)"
      @click="setDice(index)"
      :style="settedDice(index)"
    ></span>
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
    return {
      diceOnHold: []
    };
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
    },
    settedDice(index) {
      if (this.diceOnHold.includes(index)) {
        return { color: "green" };
      } else {
        return { color: "black" };
      }
    },
    setDice(index) {
      if (this.diceOnHold.includes(index)) {
        for (let i = 0; i < this.diceOnHold.length; i++) {
          if (this.diceOnHold[i] === index) {
            this.diceOnHold.splice(i, 1);
          }
        }
      } else {
        this.diceOnHold.push(index);
      }
      if (this.diceOnHold.length) {
        this.$emit("settedDiceToParent", this.diceOnHold);
      }
    }
  },
  watch: {
    dice: function(old) {
      if (!this.dice.length) {
        this.diceOnHold = [];
      }
    }
  }
};
</script>

<style>
.rolledDice:hover {
  border: 2px solid red;
}
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

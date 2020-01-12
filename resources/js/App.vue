<template>
  <div>
    <results-table :dice="diceData"></results-table>
    <show-dices :dice="diceData" v-on:settedDiceToParent="onSetDice"></show-dices>
    <roll-button v-on:diceToParent="onRollDice" :settedDice="settedDice"></roll-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      settedDice: [],
      diceData: []
    };
  },
  methods: {
    onRollDice(value) {
      if (!value.length) {
        this.settedDice = [];
      }

      this.diceData = value;
    },
    onSetDice(value) {
      this.settedDice = value;
    }
  }
};
</script>

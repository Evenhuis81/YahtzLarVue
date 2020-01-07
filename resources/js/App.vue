<template>
  <div>
    <results-table :dice="diceData"></results-table>
    <show-dices :dice="diceData"></show-dices>
    <roll-button v-on:diceToParent="onRollDice"></roll-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      diceData: []
    };
  },
  methods: {
    onRollDice(value) {
      this.diceData = value;
    }
  }
};
</script>
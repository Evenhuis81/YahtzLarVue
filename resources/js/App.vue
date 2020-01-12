<template>
  <div>
    <results-table :dice="diceData" v-on:valueSetted="onSetValue"></results-table>
    <show-dices :dice="diceData" v-on:settedDiceToParent="onSetDice"></show-dices>
    <roll-button
      v-on:diceToParent="onRollDice"
      :settedDice="settedDice"
      :settedValue="settedValue"
      v-on:unsetValue="onUnsetValue"
    ></roll-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      settedValue: 0,
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
    },
    onSetValue() {
      this.settedValue = 1;
    },
    onUnsetValue() {
      this.settedValue = 0;
    }
  }
};
</script>

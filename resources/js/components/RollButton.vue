<template>
  <div class="container-fluid text-center w-100 mt-3">
    <button
      class="btn btn-primary w-25"
      @click="rollDice"
      :disabled="rollButtonIsDisabled"
      v-bind:class="{ disabledButton: rollButtonIsDisabled }"
      ref="button"
    >
      <pre class="mb-0" style="color:white; font-weight:600;">ROLL [<span style="color: red;">{{ rollnr >= 1 ? 'X' : ' ' }}</span>] [<span style="color: red;">{{ rollnr >= 2 ? 'X' : ' ' }}</span>] [<span style="color: red;">{{ rollnr == 3 ? 'X' : ' ' }}</span>]</pre>
    </button>
    <br />
    <button class="btn btn-danger w-25 mt-3" @click="playAgain" v-show="rollnr == 3">
      <pre class="mb-0" style="color:white; font-weight:600;">PLAY AGAIN!</pre>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      diceData: [],
      rollButtonIsDisabled: false,
      rollnr: 0
    };
  },
  methods: {
    rollDice() {
      this.diceData = [];
      this.rollnr++;
      if (this.rollnr == 3) {
        this.rollButtonIsDisabled = true;
      }
      for (let index = 0; index < 5; index++) {
        const facevalue = Math.ceil(Math.random() * 6);
        this.diceData.push(facevalue);
      }
      this.$emit("diceToParent", this.diceData);
      this.$refs.button.blur();
    },
    playAgain() {
      this.diceData = [];
      this.rollnr = 0;
      this.rollButtonIsDisabled = false;
      this.$emit("diceToParent", this.diceData);
    }
  }
};
</script>

<style scoped>
.disabledButton {
  opacity: 0.9;
}

button {
  border: 5px solid black;
  font-size: 2rem;
}
</style>

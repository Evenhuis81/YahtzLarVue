<template>
  <div class="container-fluid text-center w-100 mt-3">
    <button
      :style="buttonStyling"
      class="btn btn-primary w-25"
      @click="rollDice"
      :disabled="rollButtonIsDisabled"
      v-bind:class="{ disabledButton: rollButtonIsDisabled }"
      ref="button"
    >
      <pre class="mb-0" :style="rollButtonTextStyle">ROLL [<span style="color: red;">{{ rollnr >= 1 ? 'X' : ' ' }}</span>] [<span style="color: red;">{{ rollnr >= 2 ? 'X' : ' ' }}</span>] [<span style="color: red;">{{ rollnr == 3 ? 'X' : ' ' }}</span>]</pre>
    </button>
    <br />
    <button
      :style="buttonStyling2"
      class="btn btn-danger w-25 mt-3"
      @click="playAgain"
      v-show="rollnr == 3"
      :disabled="playAgainButtonIsDisabled"
    >
      <pre class="mb-0" :style="playAgainButtonTextStyle">{{ againBtnTxt }}</pre>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    placingValue: Number,
    settedDice: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      againBtnTxt: "Place Value",
      buttonStyles: {
        border: "5px solid black",
        fontSize: "2rem",
        color: "white",
        fontWeight: 600
      },
      diceData: [],
      rollButtonIsDisabled: this.rollnr === 3,
      playAgainButtonIsDisabled: this.placingValue,
      rollnr: 0
    };
  },
  methods: {
    rollDice2() {
      this.diceData = [];
      this.diceData.push(2, 5, 1, 3, 4);
      this.$emit("diceToParent", this.diceData);
    },
    rollDice() {
      const arr = [...this.diceData];
      this.diceData = [];
      this.rollnr++;
      //   if (this.rollnr == 3) {
      //     this.rollButtonIsDisabled = true;
      //   }
      for (let index = 0; index < 5; index++) {
        if (this.settedDice.includes(index)) {
          this.diceData.push(arr[index]);
        } else {
          const facevalue = Math.ceil(Math.random() * 6);
          this.diceData.push(facevalue);
        }
      }
      this.$emit("diceToParent", this.diceData);
      this.$refs.button.blur();
    },
    playAgain() {
      this.diceData = [];
      this.rollnr = 0;
      //   this.rollButtonIsDisabled = false;
      this.$emit("diceToParent", this.diceData);
    }
  },
  computed: {
    buttonStyling() {
      return {
        fontSize: this.buttonStyles.fontSize,
        cursor: this.rollnr === 3 ? "default" : "pointer",
        border:
          this.rollnr === 3 ? "5px dotted black" : this.buttonStyles.border
      };
    },
    buttonStyling2() {
      return {
        border: this.buttonStyles.border,
        fontSize: this.buttonStyles.fontSize
        // cursor: this.rollnr === 3 ? "default" : "pointer"
      };
    },
    playAgainButtonTextStyle() {
      return {
        color: "white",
        fontweight: 600
      };
    },
    rollButtonTextStyle() {
      return {
        color: this.rollnr === 3 ? "black" : "white",
        fontweight: 600
      };
    }
  }
};
</script>

<style scoped>
.disabledButton {
  opacity: 0.9;
}
</style>

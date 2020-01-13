<template>
  <div class="container-fluid text-center w-100 mt-3">
    <button
      :style="buttonStyling"
      class="btn btn-primary w-25"
      @click="rollDice"
      :disabled="rollnr === 3 || settedValue === 1"
      v-bind:class="{ disabledButton: rollnr === 3 }"
      ref="button"
    >
      <pre class="mb-0" :style="rollButtonTextStyle">ROLL [<span style="color: red;">{{ rollnr >= 1 ? 'X' : ' ' }}</span>] [<span style="color: red;">{{ rollnr >= 2 ? 'X' : ' ' }}</span>] [<span style="color: red;">{{ rollnr == 3 ? 'X' : ' ' }}</span>]</pre>
    </button>
    <br />
    <button
      :style="buttonStyling2"
      class="btn btn-danger w-25 mt-3"
      @click="playAgain"
      v-show="rollnr === 3 || settedValue === 1"
      :disabled="playAgainButtonIsDisabled"
    >
      <pre class="mb-0" :style="playAgainButtonTextStyle">{{ settedValue === 1 ? againBtnTxt : placeBtnTxt }}</pre>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    settedValue: Number,
    settedDice: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      againBtnTxt: "Next Round!",
      placeBtnTxt: "Set Value",
      buttonStyles: {
        border: "5px solid black",
        fontSize: "2rem",
        color: "white",
        fontWeight: 600
      },
      diceData: [],
      playAgainButtonIsDisabled: true,
      rollnr: 0
    };
  },
  methods: {
    // For testing
    rollDice2() {
      this.diceData = [];
      this.diceData.push(4, 3, 2, 2, 1);
      this.$emit("diceToParent", this.diceData);
    },
    rollDice() {
      const arr = [...this.diceData];
      this.diceData = [];
      this.rollnr++;
      for (let index = 0; index < 5; index++) {
        if (this.settedDice.includes(index)) {
          this.diceData.push(arr[index]);
        } else {
          const facevalue = Math.ceil(Math.random() * 6);
          this.diceData.push(facevalue);
        }
      }
      this.$emit("diceToParent", this.diceData);
    },
    playAgain() {
      this.diceData = [];
      this.rollnr = 0;
      this.$emit("diceToParent", this.diceData);
      this.$emit("unsetValue");
    }
  },
  computed: {
    buttonStyling() {
      return {
        fontSize: this.buttonStyles.fontSize,
        cursor:
          this.rollnr === 3 || this.settedValue === 1 ? "default" : "pointer",
        border:
          this.rollnr === 3 ? "5px dotted black" : this.buttonStyles.border
      };
    },
    buttonStyling2() {
      return {
        border: this.buttonStyles.border,
        fontSize: this.buttonStyles.fontSize,
        cursor: this.playAgainButtonIsDisabled ? "default" : "pointer"
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
  },
  watch: {
    settedValue: function(newValue) {
      if (newValue === 1) {
        this.playAgainButtonIsDisabled = false;
      } else {
        this.playAgainButtonIsDisabled = true;
      }
    }
  }
};
</script>

<style scoped>
.disabledButton {
  opacity: 0.9;
}
</style>

<template>
  <div class="container h-100 w-50 content mt-5 px-0">
    <div class="row align-items-end">
      <div class="col-6">
        <h5 class="mb-0 text-center font-weight-bold">Player 1</h5>
      </div>
      <div class="col-6">
        <h5 class="mb-0 text-center font-weight-bold">Player 2/Computer</h5>
      </div>
    </div>
    <hr class="hr my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Ones</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ counter[1] || '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">3-of-a-kind</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ dice.length ? threeOfAKind : '' }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Twos</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ counter[2] * 2 || '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">4-of-a-kind</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Threes</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ counter[3] * 3 || '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Full House</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Fours</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ counter[4] * 4 || '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Small Street</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Fives</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ counter[5] * 5 || '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Large Street</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Sixes</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ counter[6] * 6 || '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Yahtzee</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ this.counter }}</p>
      </div>
    </div>
    <hr class="hr3 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Section Bonus (+35%)</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ '.' }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Chance</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">{{ dice.length ? chance : '' }}</p>
      </div>
    </div>
    <hr class="hr3 my-0" />
    <div class="row align-items-center" style="border-bottom: 3px solid black;">
      <div class="col-3"></div>
      <div class="col-3">
        <h4 class="mb-0 text-center" style="border-right: 3px solid red;">Total</h4>
      </div>
      <div class="col-3">
        <h4 class="mb-0 text-center" style="border-left: 3px solid red;">{{ '.' }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    dice: {
      required: true,
      type: Array
    }
  },
  data() {
    return {};
  },
  computed: {
    counter() {
      return this.dice.reduce((acc, die) => {
        if (!acc[die]) acc[die] = 0;
        acc[die]++;
        return acc;
      }, {});
    },
    threeOfAKind() {
      // var counts = Array(6).fill(0);
      // this.dice.forEach(dice => {
      //   counts[dice - 1]++;
      // });
      for (let key in this.counter) {
        if (this.counter[key] >= 3) {
          return this.chance;
        }
      }
      return "";

      // couts.forEach((count, index) => {
      // for (let index = 0; index < diceLength; index++) {
      //   if (this.counter[index] >= 3) {
      //     alert(counter[index]);
      // z = [index + 1] * this.counter[index];
      // }
      // }
    },
    fourOfAKind() {},
    fullHouse() {},
    smallStreet() {},
    largeStreet() {},
    yahtzee() {},
    chance() {
      return this.dice.reduce((acc, die) => acc + die);
    }
  }
};
</script>

<style scoped>
.content {
  background: green;
  opacity: 0.9;
}
.brdr {
  border-right: 3px solid black;
}
.brdl {
  border-left: 3px solid black;
}
.row {
  height: 2rem;
}
.bgrz {
  background: #ffcccb;
}
.hr {
  background: black;
  height: 3px;
}
.hr2 {
  background: black;
  height: 1px;
}
.hr3 {
  background: black;
  height: 2px;
}
h4 {
  color: red;
}
h5 {
  border-right: 2px solid black;
  border-left: 2px solid black;
}
</style>
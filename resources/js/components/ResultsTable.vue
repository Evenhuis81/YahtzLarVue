<template>
  <div class="container h-100 w-50 content mt-5 px-0">
    <div class="row align-items-end">
      <div class="col-6">
        <h5 class="mb-0 text-center font-weight-bold">Player 1</h5>
      </div>
      <!-- speler 2 bestaat niet? -->
      <div class="col-6">
        <h5 class="mb-0 text-center font-weight-bold">Player 2/Computer</h5>
      </div>
    </div>
    <hr class="hr my-0" />
    <div class="row align-items-center bgrz">
      <!-- <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Ones</p>
      </div> -->
      <!-- stop alle combinatietypes (ones, twos, etc.) in een array van objecten. Elk object heeft bijv. de properties name en score. Itereer met v-for
        door dit array. Dit scheelt veel code! -->
      <div v-for="(combination, index) in combinations" :key="index" class="col-3" style="background-color: white">
        <p 
          class="mb-0 text-center font-weight-bold brdr" 
          @click="lockCombination(combination)"
          :class="{ combinationLocked: combination.locked }">
            {{ combination.name }}: {{ combination.toString() }}
        </p>
        <hr class="hr2 my-0" />
      </div>
      
      <!-- <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold brdr"
          :class="{ hoverme: !yahtzeeObject['Ones'] && !settedValue }"
          :style="setColor('Ones')"
          @click="yahtzeeObject['Ones'] || settedValue ? null : setVal('Ones')"
          @mouseover="yahtzeeObject['Ones'] ? null : counter[1] ? counter[1] : hoverOnes='0'"
          @mouseleave="hoverOnes=''"
        >{{ hoverOnes ? hoverOnes : yahtzeeObject['Ones'] ? yahtzeeObject['Ones'] : counter[1] ? counter[1] : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">3-of-a-kind</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Three of a Kind'] && !settedValue }"
          :style="setColor('Three of a Kind')"
          @click="yahtzeeObject['Three of a Kind'] || settedValue ? null : setVal('Three of a Kind')"
          @mouseover="yahtzeeObject['Three of a Kind'] ? null : threeOfAKind ? threeOfAKind : hoverThreeOfAKind='0'"
          @mouseleave="hoverThreeOfAKind=''"
        >{{ hoverThreeOfAKind ? hoverThreeOfAKind : yahtzeeObject['Three of a Kind'] ? yahtzeeObject['Three of a Kind'] : threeOfAKind ? threeOfAKind : "." }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Twos</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold brdr"
          :class="{ hoverme: !yahtzeeObject['Twos'] && !settedValue }"
          :style="setColor('Twos')"
          @click="yahtzeeObject['Twos'] || settedValue ? null : setVal('Twos')"
          @mouseover="yahtzeeObject['Twos'] ? null : counter[2] ? counter[2] * 2 : hoverTwos='0'"
          @mouseleave="hoverTwos=''"
        >{{ hoverTwos ? hoverTwos : yahtzeeObject['Twos'] ? yahtzeeObject['Twos'] : counter[2] ? counter[2] * 2 : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">4-of-a-kind</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Four of a Kind'] && !settedValue }"
          :style="setColor('Four of a Kind')"
          @click="yahtzeeObject['Four of a Kind'] || settedValue ? null : setVal('Four of a Kind')"
          @mouseover="yahtzeeObject['Four of a Kind'] ? null : fourOfAKind ? fourOfAKind : hoverFourOfAKind='0'"
          @mouseleave="hoverFourOfAKind=''"
        >{{ hoverFourOfAKind ? hoverFourOfAKind : yahtzeeObject['Four of a Kind'] ? yahtzeeObject['Four of a Kind'] : fourOfAKind ? fourOfAKind : "." }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Threes</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold brdr"
          :class="{ hoverme: !yahtzeeObject['Threes'] && !settedValue }"
          :style="setColor('Threes')"
          @click="yahtzeeObject['Threes'] || settedValue ? null : setVal('Threes')"
          @mouseover="yahtzeeObject['Threes'] ? null : counter[3] ? counter[3] * 3 : hoverThrees='0'"
          @mouseleave="hoverThrees=''"
        >{{ hoverThrees ? hoverThrees : yahtzeeObject['Threes'] ? yahtzeeObject['Threes'] : counter[3] ? counter[3] * 3 : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Full House</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Full House'] && !settedValue }"
          :style="setColor('Full House')"
          @click="yahtzeeObject['Full House'] || settedValue ? null : setVal('Full House')"
          @mouseover="yahtzeeObject['Full House'] ? null : fullHouse ? fullHouse : hoverFullHouse='0'"
          @mouseleave="hoverFullHouse=''"
        >{{ hoverFullHouse ? hoverFullHouse : yahtzeeObject['Full House'] ? yahtzeeObject['Full House'] : fullHouse ? fullHouse : "." }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Fours</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold brdr"
          :class="{ hoverme: !yahtzeeObject['Fours'] && !settedValue }"
          :style="setColor('Fours')"
          @click="yahtzeeObject['Fours'] || settedValue ? null : setVal('Fours')"
          @mouseover="yahtzeeObject['Fours'] ? null : counter[4] ? counter[4] * 4 : hoverFours='0'"
          @mouseleave="hoverFours=''"
        >{{ hoverFours ? hoverFours : yahtzeeObject['Fours'] ? yahtzeeObject['Fours'] : counter[4] ? counter[4] * 4 : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Small Street</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Small Street'] && !settedValue }"
          :style="setColor('Small Street')"
          @click="yahtzeeObject['Small Street'] || settedValue ? null : setVal('Small Street')"
          @mouseover="yahtzeeObject['Small Street'] ? null : street >= 3 ? 30 : hoverSmallStreet='0'"
          @mouseleave="hoverSmallStreet=''"
        >{{ hoverSmallStreet ? hoverSmallStreet : yahtzeeObject['Small Street'] ? yahtzeeObject['Small Street'] : street >=3 ? 30 : "." }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Fives</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold brdr"
          :class="{ hoverme: !yahtzeeObject['Fives'] && !settedValue }"
          :style="setColor('Fives')"
          @click="yahtzeeObject['Fives'] || settedValue ? null : setVal('Fives')"
          @mouseover="yahtzeeObject['Fives'] ? null : counter[5] ? counter[5] * 5 : hoverFives='0'"
          @mouseleave="hoverFives=''"
        >{{ hoverFives ? hoverFives : yahtzeeObject['Fives'] ? yahtzeeObject['Fives'] : counter[5] ? counter[5] * 5 : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Large Street</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Large Street'] && !settedValue }"
          :style="setColor('Large Street')"
          @click="yahtzeeObject['Large Street'] || settedValue ? null : setVal('Large Street')"
          @mouseover="yahtzeeObject['Large Street'] ? null : street >= 4 ? 40 : hoverLargeStreet='0'"
          @mouseleave="hoverLargeStreet=''"
        >{{ hoverLargeStreet ? hoverLargeStreet : yahtzeeObject['Large Street'] ? yahtzeeObject['Large Street'] : street >=4 ? 40 : "." }}</p>
      </div>
    </div>
    <hr class="hr2 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Sixes</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold brdr"
          :class="{ hoverme: !yahtzeeObject['Sixes'] && !settedValue }"
          :style="setColor('Sixes')"
          @click="yahtzeeObject['Sixes'] || settedValue ? null : setVal('Sixes')"
          @mouseover="yahtzeeObject['Sixes'] ? null : counter[6] ? counter[6] * 6 : hoverSixes='0'"
          @mouseleave="hoverSixes=''"
        >{{ hoverSixes ? hoverSixes : yahtzeeObject['Sixes'] ? yahtzeeObject['Sixes'] : counter[6] ? counter[6] * 6 : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Yahtzee</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Yahtzee'] && !settedValue }"
          :style="setColor('Yahtzee')"
          @click="yahtzeeObject['Yahtzee'] || settedValue ? null : setVal('Yahtzee')"
          @mouseover="yahtzeeObject['Yahtzee'] ? null : yahtzee ? yahtzee : hoverYahtzee='0'"
          @mouseleave="hoverYahtzee=''"
        >{{ hoverYahtzee ? hoverYahtzee : yahtzeeObject['Yahtzee'] ? yahtzeeObject['Yahtzee'] : yahtzee ? yahtzee : "." }}</p>
      </div>
    </div>
    <hr class="hr3 my-0" />
    <div class="row align-items-center bgrz">
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold">Section Bonus (+35%)</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdr">{{ sectionBonus ? sectionBonus : "." }}</p>
      </div>
      <div class="col-3">
        <p class="mb-0 text-center font-weight-bold brdl">Chance</p>
      </div>
      <div class="col-3">
        <p
          class="mb-0 text-center font-weight-bold"
          :class="{ hoverme: !yahtzeeObject['Chance'] && !settedValue }"
          :style="setColor('Chance')"
          @click="yahtzeeObject['Chance'] || settedValue ? null : setVal('Chance')"
        >{{ yahtzeeObject['Chance'] ? yahtzeeObject['Chance'] : chance ? chance : "." }}</p>
      </div>
    </div>
    <hr class="hr3 my-0" />
    <div class="row align-items-center" style="border-bottom: 3px solid black;">
      <div class="col-6">
        <h4 class="mb-0 text-center" style="border-right: 3px solid red;">Total</h4>
      </div>
      <div class="col-6">
        <h4
          class="mb-0 text-center"
          style="color: white; border-left: 3px solid red;"
        {{ totalSettedValue ? totalSettedValue : "." }}</h4> -->
        <!-- if roundnr != 0 then show 0 instead of . -->
      <!--</div> -->
    </div>
  </div>
</template>

<script>

class Combination {
  constructor(name, currentScore) {
    this.name = name;
    this.score = 0;
    this.locked = false;
    this.currentScore = currentScore;
  }

  toString() {
    return this.locked ? this.score : this.currentScore();
  }
}

export default {
  props: {
    dice: {
      required: true,
      type: Array
    }
  },
  data() {
    return {
      settedValue: false,
      // hoverYahtzee: "",
      // hoverThreeOfAKind: "",
      // hoverFourOfAKind: "",
      // hoverFullHouse: "",
      // hoverSmallStreet: "",
      // hoverLargeStreet: "",
      // hoverSixes: "",
      // hoverFives: "",
      // hoverFours: "",
      // hoverThrees: "",
      // hoverTwos: "",
      // hoverOnes: "",
      combinations: [],
      // yahtzeeArray: [
      //   "Ones",
      //   "Twos",
      //   "Threes",
      //   "Fours",
      //   "Fives",
      //   "Sixes",
      //   "Three of a Kind",
      //   "Four of a Kind",
      //   "Full House",
      //   "Small Street",
      //   "Large Street",
      //   "Yahtzee",
      //   "Chance",
      //   "Section Bonus (+35%)"
      // ],
      // yahtzeeObject: {},
      // settedColor: "black",
      // defaultColor: "red"
    };
  },
  computed: {
    sectionBonus() {
      let sectionTotal = 0;
      const sectionKeys = Object.keys(this.yahtzeeObject);
      // alert(sectionKeys);
      for (let index = 0; index < 6; index++) {
        if (this.yahtzeeObject[sectionKeys[index]] != "0") {
          sectionTotal += this.yahtzeeObject[sectionKeys[index]];
        }
      }
      return sectionTotal;
    },
    totalSettedValue() {
      let total = 0;
      Object.keys(this.yahtzeeObject).forEach(key => {
        if (this.yahtzeeObject[key] != "0") {
          total += this.yahtzeeObject[key];
        }
      });
      return total;
    },
    createY() {
      return this.yahtzeeArray.reduce((acc, elem) => {
        acc[elem] = null;
        return acc;
      }, {});
    },
    counter() {
      return this.dice.reduce((acc, die) => {
        if (!acc[die]) acc[die] = 0;
        acc[die]++;
        return acc;
      }, {});
    },
    threeOfAKind() {
      for (let key in this.counter) {
        if (this.counter[key] >= 3) {
          return this.chance;
        }
      }
      return null;
    },
    fourOfAKind() {
      for (let key in this.counter) {
        if (this.counter[key] >= 4) {
          return this.chance;
        }
      }
      return null;
    },
    yahtzee() {
      for (let key in this.counter) {
        if (this.counter[key] === 5) {
          return true;
        }
      }
      return null;
    },
    fullHouse() {
      for (let key in this.counter) {
        if (this.counter[key] === 3) {
          for (let key in this.counter) {
            if (this.counter[key] === 2) {
              return 25;
            }
          }
        }
      }
      return null;
    },
    street() {
      let maxS = 0;
      const arr = [...this.dice].sort();
      let sorted = [...new Set(arr)];
      for (let i = 0; i < sorted.length - 1; i++) {
        const firstDie = sorted[i];
        const secondDie = sorted[i + 1];
        if (firstDie === secondDie - 1) {
          maxS++;
        }
      }
      return maxS;
    },
    chance() {
      if (this.dice.length) {
        return this.dice.reduce((acc, die) => acc + die);
      } else {
        return null;
      }
    }
  },
  methods: {
    // setColor(para) {
    //   return {
    //     color: this.yahtzeeObject[para] ? this.settedColor : this.defaultColor
    //   };
    // },
    lockCombination(combination) {
      if(!combination.locked) {
        combination.score = combination.currentScore();
        combination.locked = true;

        this.settedValue = true;
        this.$emit("valueSetted");
      }
    },

    // kies duidelijke:
    // * functienaam. 'setVal' is een erg algemene naam. Suggestie: lockCombination
    // * parameter naam. 'para' zegt niets over inhoud parameter. Suggestie: combination
    // setVal(para) {
    //   // kan ook in switch blok i.p.v. if/else
    //   if (para == "Chance") {
    //     this.chance
    //       ? (this.yahtzeeObject[para] = this.chance)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Yahtzee") {
    //     this.yahtzee
    //       ? (this.yahtzeeObject[para] = 50)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Sixes") {
    //     this.counter[6]
    //       ? (this.yahtzeeObject[para] = this.counter[6] * 6)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Fives") {
    //     this.counter[5]
    //       ? (this.yahtzeeObject[para] = this.counter[5] * 5)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Fours") {
    //     this.counter[4]
    //       ? (this.yahtzeeObject[para] = this.counter[4] * 4)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Threes") {
    //     this.counter[3]
    //       ? (this.yahtzeeObject[para] = this.counter[3] * 3)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Twos") {
    //     this.counter[2]
    //       ? (this.yahtzeeObject[para] = this.counter[2] * 2)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Ones") {
    //     this.counter[1]
    //       ? (this.yahtzeeObject[para] = this.counter[1])
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Three of a Kind") {
    //     this.threeOfAKind
    //       ? (this.yahtzeeObject[para] = this.threeOfAKind)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Large Street") {
    //     this.street >= 4
    //       ? (this.yahtzeeObject[para] = 40)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Small Street") {
    //     this.street >= 3
    //       ? (this.yahtzeeObject[para] = 30)
    //       : (this.yahtzeeObject[para] = "0");
    //   } else if (para == "Full House") {
    //     this.fullHouse
    //       ? (this.yahtzeeObject[para] = this.fullHouse)
    //       : (this.yahtzeeObject[para] = "0");
    //   }

    //   this.settedValue = true;
    //   this.$emit("valueSetted");
    //   // alert(this.hover + para);
    // }
  },
  mounted() {
    //this.yahtzeeObject = this.createY;
    this.combinations.push(new Combination("Ones", () => { return this.dice.filter(x => x==1).length }));
    this.combinations.push(new Combination("Twos", () => { return this.dice.filter(x => x==2).length*2 }));
    this.combinations.push(new Combination("Threes", () => { return this.dice.filter(x => x==3).length*3 }));
    this.combinations.push(new Combination("Fours", () => { return this.dice.filter(x => x==4).length*4 }));
    this.combinations.push(new Combination("Fives", () => { return this.dice.filter(x => x==5).length*5 }));
    this.combinations.push(new Combination("Sixes", () => { return this.dice.filter(x => x==6).length*6 }));
    this.combinations.push(new Combination("Sixes", () => { return this.dice.filter(x => x==6).length*6 }));
    this.combinations.push(new Combination("Three of a Kind", () => { return this.threeOfAKind }));
    // voeg overige combinaties zelf verder toe ...
  },
  watch: {
    dice: function(newValue) {
      this.dice.length ? (this.settedValue = false) : (this.settedValue = true);
    }
  }
};
</script>

<style scoped>
.combinationLocked {
  color: red;
}

.hoverme:hover {
  border: 2px solid black;
  cursor: pointer;
}
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

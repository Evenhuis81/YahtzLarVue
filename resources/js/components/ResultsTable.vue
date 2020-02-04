<template>
<div>
    <div class="container h-100 w-50 content mt-2 px-0">
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

            <!-- stop alle combinatietypes (ones, twos, etc.) in een array van objecten. Elk object heeft bijv. de properties name en score. Itereer met v-for
      door dit array. Dit scheelt veel code!-->
            <!-- <p class="mb-0 text-center font-weight-bold" :class="{ hoverme: !yahtzeeObject['Large Street'] && !settedValue }" :style="setColor('Large Street')" @click="yahtzeeObject['Large Street'] || settedValue ? null : setVal('Large Street')" @mouseover="yahtzeeObject['Large Street'] ? null : street >= 4 ? 40 : hoverLargeStreet='0'" @mouseleave="hoverLargeStreet=''">{{ hoverLargeStreet ? hoverLargeStreet : yahtzeeObject['Large Street'] ? yahtzeeObject['Large Street'] : street >=4 ? 40 : "." }}</p>
        <hr class="hr2 my-0" /> -->

        <!-- if roundnr != 0 then show 0 instead of . -->

        <div v-for="(combination, index) in combinations" :key="index" class="col-3" style="background-color: white">
            <p class="mb-0 text-center font-weight-bold brdr" @click="clickActive(combination)" :class="buttonStyles(combination)">{{ combination.name }}: <span :style="showGreen(combination)">{{ combination.toString() }}</span></p>
            <hr class="hr2 my-0" />
        </div>
        </div>
    </div>
</div>
</template>

<script>
class Combination {
    constructor(name, currentScore, clickable, locked) {
        this.name = name;
        this.score = 0;
        this.locked = !!locked;
        this.currentScore = currentScore;
        this.clickable = !clickable;
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
            unsettedScoreStyle: {
                color: "green"
            },
            settedValue: true,
            combinations: []
        };
    },
    computed: {
      sectionBonus() {
          let sectionTotal = 0;
          const sectionKeys = Object.keys(this.combinations);
          // alert(sectionKeys);
          for (let index = 0; index < 6; index++) {
                  sectionTotal += this.combinations[sectionKeys[index]];
              }
              // console.log(sectionTotal)
          return sectionTotal > 62 ? 35 : 0;
      },
      totalSettedValue() {
          let total = 0;
          Object.keys(this.combinations).forEach(key => {
                  total += this.combinations[key].score;
          });
          return total;
      },
      // createY() {
      //   return this.yahtzeeArray.reduce((acc, elem) => {
      //     acc[elem] = null;
      //     return acc;
      //   }, {});
      // },
      counter() {
          return this.dice.reduce((acc, die) => {
              if (!acc[die]) acc[die] = 0;
              acc[die]++;
              return acc;
          }, {});
      },
      chance() {
          if (this.dice.length) {
              return this.dice.reduce((acc, die) => acc + die);
          } else {
              return 0;
          }
      },
      streets() {
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
      }
    },
    methods: {
      buttonStyles(combination) {
         return { combinationLocked: this.showLockedCombination(combination), onHoverCombination: this.showLockedCombinationOnHover(combination) }
         },
        clickActive(combination) {
          if (combination.name === 'Section Bonus' || combination.name === 'Total Score') {
            return;
          } 
          this.lockCombination(combination)
            // console.log('true')
            // return true;
          
        },
        showLockedCombination(combination) {
          if (combination.locked && combination.clickable) {
            return true;
          } else {
            return false;
          }
        },
        showLockedCombinationOnHover(combination) {
          return !combination.locked && !this.settedValue
        },
        // combination.locked && combination.clickable, onHoverCombination : !combination.locked && !settedValue
        showGreen(combination) {
          if (combination.currentScore() && !combination.locked && !this.settedValue ) {
            return this.unsettedScoreStyle;
          }
          return ''
          // combination.currentScore() && !combination.locked && !settedValue ? unsettedScoreStyle : ''
        },
        lockCombination(combination) {
            if (!combination.locked) {
                combination.score = combination.currentScore();
                combination.locked = true;
                this.settedValue = true;
                this.$emit("valueSetted");
            }
        }
    },
    mounted() {
        this.combinations.push(
            new Combination("Ones", () => {
                return this.dice.filter(x => x == 1).length;
            })
        );
        this.combinations.push(
            new Combination("Twos", () => {
                return this.dice.filter(x => x == 2).length * 2;
            })
        );
        this.combinations.push(
            new Combination("Threes", () => {
                return this.dice.filter(x => x == 3).length * 3;
            })
        );
        this.combinations.push(
            new Combination("Fours", () => {
                return this.dice.filter(x => x == 4).length * 4;
            })
        );
        this.combinations.push(
            new Combination("Fives", () => {
                return this.dice.filter(x => x == 5).length * 5;
            })
        );
        this.combinations.push(
            new Combination("Sixes", () => {
                return this.dice.filter(x => x == 6).length * 6;
            })
        );
        this.combinations.push(
            new Combination("Three of a Kind", () => {
                for (let key in this.counter) {
                    if (this.counter[key] >= 3) {
                        return this.chance;
                    }
                }
                return 0;
            })
        );
        this.combinations.push(
            new Combination("Four of a Kind", () => {
                for (let key in this.counter) {
                    if (this.counter[key] >= 4) {
                        return this.chance;
                    }
                }
                return 0;
            })
        );
        this.combinations.push(
            new Combination("Yahtzee", () => {
                for (let key in this.counter) {
                    if (this.counter[key] === 5) {
                        return 50;
                    }
                }
                return 0;
            })
        );
        this.combinations.push(
            new Combination("Full House", () => {
                for (let key in this.counter) {
                    if (this.counter[key] === 3) {
                        for (let key in this.counter) {
                            if (this.counter[key] === 2) {
                                return 25;
                            }
                        }
                    }
              }
                return 0;
            })
        );
        this.combinations.push(
            new Combination("Small Street", () => {
                return this.streets >= 3 ? 30 : 0;
            })
        );
        this.combinations.push(
            new Combination("Large Street", () => {
                return this.streets >= 4 ? 40 : 0;
            })
        );
        this.combinations.push(
            new Combination("Chance", () => {
                return this.chance;
            })
        );
        this.combinations.push(
            new Combination("Section Bonus", () => {
              return this.sectionBonus;
              // make non interactive
            }, true, true)
        );
        this.combinations.push(
          new Combination("Total Score", () => {
            return this.totalSettedValue
            // make non interactive
          }, true, true)
        );
        // voeg overige combinaties zelf verder toe ...
    },
    watch: {
        dice: function (newValue) {
            this.dice.length ? (this.settedValue = false) : (this.settedValue = true);
        }
    }
};
</script>

<style scoped>
.combinationLocked {
    color: red;
}
.onHoverCombination:hover {
  color: green;
  cursor: pointer;
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

<template>
  <div class="calculator">
    <div class="display">{{ display }}</div>
    <p>CEILIDH ASHCROFT VC-2023</p>
    <div class="buttons">
      <button class="memory" @click="addToMemory()">M+</button>
      <button class="memory" @click="subtractFromMemory()">M-</button>
      <button class="memory" @click="recallMemory()">MR</button>
      <button class="memory" @click="clearMemory()">MC</button>
      <button class="memory" @click="clearDisplay()">C</button>
      <button class="memory" @click="clearLastCharacter()">CE</button>
      <button class="operator" @click="prependToDisplay('-')">+/-</button>
      <button class="operator" @click="setOperator('%')">%</button>
      <button class="number" @click="appendToDisplay('7')">7</button>
      <button class="number" @click="appendToDisplay('8')">8</button>
      <button class="number" @click="appendToDisplay('9')">9</button>
      <button class="operator" @click="setOperator('/')">÷</button>
      <button class="number" @click="appendToDisplay('4')">4</button>
      <button class="number" @click="appendToDisplay('5')">5</button>
      <button class="number" @click="appendToDisplay('6')">6</button>
      <button class="operator" @click="setOperator('*')">x</button>
      <button class="number" @click="appendToDisplay('1')">1</button>
      <button class="number" @click="appendToDisplay('2')">2</button>
      <button class="number" @click="appendToDisplay('3')">3</button>
      <button class="operator" @click="setOperator('-')">-</button>
      <button class="number" @click="appendToDisplay('0')">0</button>
      <button class="number" @click="appendToDisplay('.')">.</button>
      <button class="operator" @click="setOperator('+')">+</button>
      <button class="equals" @click="calculate()">=</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: '',
      operator: null,
      memory: 0,
    };
  },
  methods: {
    appendToDisplay(value) {
      this.display += value;
    },
    clearDisplay() {
      this.display = '';
    },
    setOperator(operator) {
      this.operator = operator;
      if (this.display) {
        //this.memory = parseFloat(this.display);
        this.clearDisplay();
      }
    },
    calculate() {
      const currentValue = parseFloat(this.display);
      let result = null;
      switch (this.operator) {
        case '+':
          result = this.memory + currentValue;
          break;
        case '-':
          result = this.memory - currentValue;
          break;
        case '*':
          result = this.memory * currentValue;
          break;
        case '/':
          result = this.memory / currentValue;
          break;
      }
      if (result !== null) {
        //this.memory = result;
        this.display = result.toString();
      }
      this.operator = null;
    },
    addToMemory() {
      if (this.display) {
        this.memory += parseFloat(this.display);
      }
    },
    subtractFromMemory() {
      if (this.display) {
        this.memory -= parseFloat(this.display);
      }
    },
    recallMemory() {
      this.display = this.memory.toString();
    },
    clearMemory() {
      this.memory = 0;
    },
    clearLastCharacter() {
      this.display = this.display.slice(0, -1);
    },

    prependToDisplay(value) {
      if (this.display[0] === '-') {
        this.display = this.display.slice(1);
      } else {
        this.display = value + this.display;
      }
    },
  },
};
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  padding: 20px;
  min-width: 400px;
  background-color: #160064;
  border-radius: 10px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3);
  font-size: 24px;
  text-align: right;
  overflow: hidden;
}

.display {
  margin-bottom: 20px;
  padding: 3rem;
  height: 2rem;
  color: black;
  background-color: #dfdfdf;
  border-radius: 5px;
  align-self: center;
  align-items: center;
  font-size: 2rem;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}

button {
  padding: 1rem;
  border: none;
  border-radius: 5px;
  background-color: #fff;
  color: #160064;
  font-size: 24px;
  cursor: pointer;
  box-shadow: 0 3px 0 rgba(0, 0, 0, 0.788) inset;
}

.equals {
  background-color: #8d0000;
  color: #fff;
}

.memory {
  background-color: #8d0000;
  color: #fff;
}

.operator {
  background-color: #8d0000;
  color: #fff;
}

.number {
  background-color: #fff;
  color: #160064;
}

</style>
```
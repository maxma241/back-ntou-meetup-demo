<template>
<div class="demo1">
  <div>
    <div>
      <h1>style binding</h1>
      <div>
        <div>Red<input type="number" v-model.number="RGB.r" /> <input type="range" v-model="RGB.r" :min="0" :max="255"> </div>
        <div>Green <input type="number" v-model.number="RGB.g" /> <input type="range" v-model="RGB.g" :min="0" :max="255"> </div>
        <div>Blue <input type="number" v-model.number="RGB.b" /> <input type="range" v-model="RGB.b" :min="0" :max="255"> </div>
      </div>
      {{ rgbStyleValue }}
      <div class="color-field" :style="{ backgroundColor: rgbStyleValue }"></div>
    </div>

    <div>
      <h1>origin sample data:</h1>
      <div>{{ sample }}</div>
    </div>
    <h1>input and computed</h1>
    <div>
      sample.testInput: <input type="number" @input="validateNumber" v-model.number="sample.testInput" />
      <div>
        <button @click="addTestInput">+ 1</button>
        <button @click="minusTestInput">- 1</button>
      </div>
    </div>
    <div>origin number: {{ sample.testInput }}</div>
    <div>double number: {{ doubleNumber }}</div>
    <div>Array({{ sample.testInput }}) sno: {{ snoArrayOftestInput }}</div>
    <div>{{ sample.testInput }}內的質數: {{ primeData }}</div>
  </div>
</div>
</template>

<script>

export default {
  data: () => ({
    sample: {
      testInput: 10,
      // testPoint: [0,0],
      // testArray: [0,1,2,3,4],
    },
    RGB: {
      r: 0,
      g: 0,
      b: 0,
    },
  }),
  computed: {
    rgbStyleValue() {
      const { r, g, b } = this.RGB;
      return `rgb(${r}, ${g}, ${b})`;
    },
    isInputNaN() {
      return isNaN(+this.sample.testInput)
    },
    doubleNumber() {
      return this.isInputNaN ? 0 : this.sample.testInput * 2;
    },
    snoArrayOftestInput() {
      let length = this.sample.testInput;
      if (this.sample.testInput > 100) {
        length = 100;
      }
      return this.isInputNaN ? [] : Array(length).fill(0).map((_zero, index) => index + 1)
    },
    primeData() {
      if (this.isInputNaN) {
        return [];
      }
      const n = this.sample.testInput > 100 ? 500 : this.sample.testInput;
      return this.generatePrimeData(n);
    },
  },
  methods: {
    addTestInput() {
      this.sample.testInput += 1;
    },
    minusTestInput() {
      this.sample.testInput -= 1;
    },
    validateNumber() {
      if (this.sample.testInput > 500) {
        this.sample.testInput = 500;
      }
    },
    isPrime(n){
      for (let i = 2; i < n; ++i) {
        if(n % i == 0) {
          return false;
        }
      }
      return true;
    },
    generatePrimeData(n) {
      const arr = [];
      for (let i = 2; i <= n; ++i) {
        if (this.isPrime(i)) {
          arr.push(i);
        }
      }
      return arr;
    },
  }
}
</script>

<style lang="scss">
.demo1 {
  text-align: left;
}
.color-field {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  background-color: #fff;
}
.rgb-input {
  width: 30%;
  display: flex;
  justify-content: space-around;
}
</style>
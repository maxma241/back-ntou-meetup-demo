<template>
<div class="demo1">
  <div>
    <h1>origin sample data:</h1>
    <div>{{ sample }}</div>
  </div>
  <div>
    <div>
      sample.testInput: <input type="number" min="2" max="500" v-model="sample.testInput" />
    </div>
    <div>origin number: {{ sample.testInput }}</div>
    <div>double number: {{ doubleNumber }}</div>
    <div>Array({{ sample.testInput }}) sno: {{ snoArrayOftestInput }}</div>
      <div>{{ sample.testInput }}內的質數: {{ primeData }}</div>
    <div v-for="n in snoArrayOftestInput" :key="n">
      <div>{{ n }}內的質數: {{ generatePrimeData(n) }}</div>
    </div>
  </div>
</div>
</template>

<script>

export default {
  data: () => ({
    sample: {
      testInput: 10,
      testPoint: [0,0],
      testArray: [0,1,2,3,4],
    },
  }),
  computed: {
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

<style>
.demo1 {
  text-align: left;
}
</style>
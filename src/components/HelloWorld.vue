<template>
  <div class="container">
    <div class="equation-area">
        <div class="fraction">
          <input type="text" v-model="numeratorArray[0]">
          <div class="divider" />
          <input type="text" v-model="denominatorArray[0]">
        </div>
        <div class="plus">+</div>
        <div class="fraction">
          <input type="text" v-model="numeratorArray[1]">
          <div class="divider" />
          <input type="text" v-model="denominatorArray[1]">
        </div>
        <div class="section" v-for="(item, index) in FractionElementArray" :key='index'>
          <div class="plus">+</div>
          <div class="fraction">
            <input type="text" v-model="numeratorArray[item]">
            <div class="divider" />
            <input type="text" v-model="denominatorArray[item]">
          </div>
        </div>
        <button class="button button1" v-on:click="add">新增分數</button>
    </div>
    <div class="reslut-area">
      <div class="equal"> = </div>
      <div class="fraction">
        <input type="text" v-model="resultArray[0]">
        <div class="divider" />
        <input type="text" v-model="resultArray[1]">
      </div>
      <button class="button button2" v-on:click="calculate">運算</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data() {
    return {
      counter: 2,
      FractionElementArray: [],
      numeratorArray: [], 
      denominatorArray: [],
      resultArray: [],
    }
  },
  methods: {
    add: function() {
      this.FractionElementArray.push(this.counter++)
    },
    reductionTo: function(m ,n) {
      var arr = [];
      var a = m;
      var b = n;
      (a >= b) ? (a = m, b = n) : (a = n, b = m);
      if (m != 1 && n != 1) {
          for (var i = b; i >= 2; i--) {
              if (m % i == 0 && n % i == 0) {
                  m = m / i;
                  n = n / i;
              }
          }
      }
      arr[0] = m;
      arr[1] = n;
      return arr;
    },
    calculate: function() {
      const denominator = this.denominatorArray.reduce((previousValue, currentValue) => previousValue * currentValue)
      const numeratorMap = this.numeratorArray.map(( numerator, index )=>{
          return numerator * denominator / this.denominatorArray[index]
      })
      const numerator = numeratorMap.reduce((previousValue, currentValue) => previousValue + currentValue)
      this.resultArray = this.reductionTo(numerator, denominator)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.container{
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 50px;
  .equation-area{
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-items: center;
    .plus{
      font-size: 30px;
      margin: 0px 30px;
    }
  }
  .reslut-area{
    display: flex;
    justify-content: flex-start;
    align-items: center;
    margin-top: 50px;
    .equal{
      font-size: 30px;
      margin-right: 30px;
    }
  }
}

.section{
  display: flex;
  justify-content: center;
  align-items: center;
}

.fraction{
  margin-top: 20px;
  width: 150px;
  height: 100px;
  display: flex;
  flex-direction: column;
  justify-content: center;

  .divider{
    height: 1px;
    width: 100%;
    border-top: 1px solid #000000;
    margin: 15px 0px;
  }

  input {
    font-size: 20px;
    height: 30px;
  }
}
.button {
  margin: 20px 30px;
  border: none;
  color: white;
  padding: 8px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 18px;
  transition-duration: 0.4s;
  border-radius: 5px;
  cursor: pointer;
}

.button1 {
  background-color: white; 
  color: #4CAF50; 
  border: 2px solid #4CAF50;
}

.button1:hover {
  background-color: #4CAF50;
  color: white;
}

.button2 {
  background-color: white; 
  color: #008CBA; 
  border: 2px solid #008CBA;
}

.button2:hover {
  background-color: #008CBA;
  color: white;
}

.button3 {
  background-color: white; 
  color: #f44336; 
  border: 2px solid #f44336;
}

.button3:hover {
  background-color: #f44336;
  color: white;
}

.button4 {
  background-color: white;
  color: #e7e7e7;
  border: 2px solid #e7e7e7;
}

.button4:hover {background-color: #e7e7e7;}

.button5 {
  background-color: white;
  color: #555555;
  border: 2px solid #555555;
}

.button5:hover {
  background-color: #555555;
  color: white;
}
</style>

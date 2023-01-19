<template>
<h1> Vue </h1>
  <div class="calculator-result p-3"> 
    <div class="w-full rounded m-1 p-3 text-end lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorValue || 0 }}
    </div>
      <div class="row g-0">
        <div class="col-3" v-for="calculatorElement in calculatorElements" :key="calculatorElement">
          <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class" 
                      @click="calculateInput(calculatorElement)">
            {{ calculatorElement }}
          </div>
        </div>
      </div>
    
  </div>
</template>

<script>
  export default {
    data() {
      return {
        calculatorValue: "",
        calculatorElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
        operator: null,
      }
    },

    methods: {
      calculateInput(calculatorElement){
        if(!isNaN(calculatorElement) || calculatorElement === '.'){
            this.calculatorValue += calculatorElement;
        }

        if(calculatorElement == 'C'){
            this.calculatorValue= '';
        }

        if(calculatorElement == '%'){
            this.calculatorValue = this.calculatorValue/100;
        }

        if(['/','*','+','-'].includes(calculatorElement)){
          this.operator = calculatorElement;
          this.calculatorValue +=' ' + this.operator + ' ';
        }

        if(calculatorElement === '='){
          this.calculatorValue = eval(this.calculatorValue);
        }
        
      }
    }
  }
</script>

<style scoped>
  .calculator-result {
    max-width: 400px;
    margin: 50px auto;
    background-color: #234;
  }

  .bg-vue-dark {
    background-color: #31475e;
  }

  .hover-class:hover {
    cursor: pointer;
    background-color: #3D5875;
    transition: 0.5s;
  }
</style>

<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn operator">C</div>
    <div @click="rad" class="btn operator">rad</div>
    <div @click="append('Math.sqrt(')" class="btn operator">root</div>
    <div @click="append('(')" class="btn operator">(</div>
    <div @click="append(')')" class="btn operator">)</div>
    <div @click="percent" class="btn operator">%</div>
    <div @click="append('/')" class="btn operator">÷</div>
    <div @click="append('Math.sin(')" class="btn operator">sin</div>
    <div @click="append('Math.cos(')" class="btn operator">cos</div>
    <div @click="append('Math.tan(')" class="btn operator">tan</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="append('*')" class="btn operator">x</div>
    <div @click="append('Math.log(')" class="btn operator">ln</div>
    <div @click="append('Math.log10(')" class="btn operator">log</div>
    <div @click="xdivide" class="btn operator">1/x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="append('-')" class="btn operator">-</div>
    <div @click="append('Math.exp(')" class="btn operator">e^x</div>
    <div @click="xtpow" class="btn operator">x^2</div>
    <div @click="xypow" class="btn operator">x^y</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="append('+')" class="btn operator">+</div>
    <div @click="abs" class="btn operator">|x|</div>
    <div @click="piyo" class="btn operator">PI</div>
    <div @click="juste" class="btn operator">e</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="append('0')" class="btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      scurrent: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
      this.scurrent ='';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
        
      this.scurrent = this.scurrent.charAt(0) === '-' ? 
        this.scurrent.slice(1) : `-${this.scurrent}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
      
      if (this.operatorClicked) {
        this.scurrent = '';
        this.operatorClicked = false;
      }
      this.scurrent = `${this.scurrent}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    equal() {
      this.current = eval(this.current);
      this.previous = null;
    },
    pequal() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
    },
    piyo() {
      this.operator = (a) => Math.PI * a;
      this.setPrevious();
      this.equal();
    },
    rad(){
      this.operator = (a) => a * 180 / Math.PI;
      this.setPrevious();
      this.pequal();
    },
    xdivide() {
      this.operator = (a) => 1/a;
      this.setPrevious();
      this.pequal();
    },
    xtpow(){
      this.operator = (a) => Math.pow(a, 2);
      this.setPrevious();
      this.pequal();
    },
    xypow() {
      this.operator = (a,b) => Math.pow(b, a);
      this.setPrevious();
    },
    abs() {
      this.operator = (a) => Math.abs(a);
      this.setPrevious();
      this.pequal();
    },
    juste() {
      this.operator = (a) => a * Math.E;
      this.setPrevious();
      this.pequal();
    }
  }
}
</script>

<style scoped>
.calculator {
  font-size: 40px;
  display: grid;
  grid-auto-rows: minmax(80px, auto);
}
.display {
  grid-column: 1 / 8;
  background-color: #333;
  color: white;
}
.sdisplay {
  grid-column: 1 / 8;
  background-color: rgb(32, 201, 142);
  color: white;
}
.btn {
  background-color: #F2F2F2;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
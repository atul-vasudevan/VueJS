<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn misc">C</div>
    <div @click="sign" class="btn misc">+/-</div>
    <div @click="percent" class="btn misc">%</div>
    <div @click="sqrt" class="btn operator">√</div>
    <div @click="power" class="btn misc">^</div>
    <div @click="pi" class="btn misc">π</div>
    <div @click="log" class="btn misc">log</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="plus" class ="btn operator">+</div>
    <div @click="append(0)" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn equal">=</div>
  </div>
</template>

<script> 
export default {
  data(){
    return {
      previous:null,
      current:'',
      operator:null,
      operatorClicked:false,
    }
  },
  methods: {
    clear(){
      this.current = ''
    },
    sign(){
      this.current = this.current.charAt(0) === '-'? this.current.slice(1): `-${this.current}`; 
    },
    percent(){
      this.current = `${parseFloat(this.current)/100}`;
    },
    append(number){
      if (this.operatorClicked){
        this.current='';
        this.operatorClicked=false;

      }
      if(this.current.length <=12){
        this.current = `${this.current}${number}`;
      }

      // this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.')=== -1){
        this.append('.')
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      // this.operator = (a,b) => b/a;
      this.operator = (a,b) => {
        var result = b/a;
        return result.toFixed(2)
      }
      this.setPrevious();
    },
    times(){
      this.operator = (a,b) => a*b;
      this.setPrevious();
    },
    minus(){
      // this.operator = function(a,b){
      //   return parseFloat(a)-parseFloat(b) <0 ? `-${parseFloat(a)-parseFloat(b)}`: parseFloat(a)-parseFloat(b);
      // } 
      this.operator = (a,b) => b-a;
      this.setPrevious();
    },
    plus(){
      this.operator = (a,b) => a+b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}`;
      this.previous=null;
      this.setPrevious();
      
    },
    sqrt(){
      this.current = Math.sqrt(this.current);
    },
    power(){
      this.operator =(a,b) => Math.pow(b,a);
      this.setPrevious();
    },
    pi(){
      this.current=Math.PI;
    },
    log(){
      this.current = Math.log10(this.current);
      this.setPrevious();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* * {
  background: white;
} */

.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  font-family:'Courier New', Courier, monospace;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(auto, auto);
  border: 10px groove lightgray;
}

.display {
  grid-column: 1/5;
  background-color: black;
  color: greenyellow;
  padding: 20px;
  text-align: right;
  overflow: hidden;
  text-overflow: ellipsis;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #eee;
  /* border: 1px solid #999; */
  border: 1px solid rgb(22, 22, 22);
  background: linear-gradient(#fafafa, lightgrey);
  cursor: pointer;
}
.btn:hover{
  border: 1px solid rgb(252, 240, 240);
  background-color: darken(linear-gradient(#fafafa, lightgrey),100%);
}
.btn:active{
  background: #777;
  color: whitesmoke;
}

.operator {
  color: black;
  background: linear-gradient(rgb(247, 180, 56), orange);
  /* background: linear-gradient(rgb(31, 177, 177), rgb(1, 160, 160)); */
  /* color: rgb(119, 118, 118); */
}
.equal {
  color: black;
  background: linear-gradient(red, rgb(189, 3, 3));
}
.misc {
  color: black;
  background: linear-gradient(rgb(196, 195, 195), rgb(156, 156, 156));
}
</style>

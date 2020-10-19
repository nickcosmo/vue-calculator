<template>
  <div class="calc">
    <div class="disp">{{ outputValue }}</div>
    <div class="btn" @click="clearAll">C</div>
    <div class="btn" @click="clearCurrent">CE</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="divide">/</div>
    <div class="btn" @click="appendNum('7')">7</div>
    <div class="btn" @click="appendNum('8')">8</div>
    <div class="btn" @click="appendNum('9')">9</div>
    <div class="btn" @click="multiply">*</div>
    <div class="btn" @click="appendNum('4')">4</div>
    <div class="btn" @click="appendNum('5')">5</div>
    <div class="btn" @click="appendNum('6')">6</div>
    <div class="btn" @click="minus">-</div>
    <div class="btn" @click="appendNum('1')">1</div>
    <div class="btn" @click="appendNum('2')">2</div>
    <div class="btn" @click="appendNum('3')">3</div>
    <div class="btn" @click="add">+</div>
    <div class="zero btn" @click="appendNum('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn" @click="equal">=</div>
  </div>
  <div>{{finalAnswer}}</div>
  <div>{{values}}</div>
</template>

<script>
export default {
  data() {
    return {
      values: [],
      valueIndex: 0,
      turn: false,
      finalAnswer: null,
    }
  },
  computed: {
    outputValue() {
      if(this.finalAnswer === null) {
        return this.values[this.valueIndex] || 0;
      } else {
        return this.finalAnswer;
      }
    }
  },
  methods: {
    clearCurrent() {
      this.values[this.valueIndex] = '';
    },
    clearAll() {
      this.values = [];
      this.finalAnswer = null;
    },
    sign() {
      if(this.turn === true) {
        this.values[this.valueIndex] = this.values[this.valueIndex].charAt(0) === '-' ? this.values[this.valueIndex].slice(1) : `-${this.values[this.valueIndex]}`;
      }
    },
    appendNum(number) {
      this.turn = true;
      if(this.values[this.valueIndex] === undefined) {
        this.values[this.valueIndex] = number;
      } else {
        this.values[this.valueIndex] = this.values[this.valueIndex] + number;
      }
    },
    dot() {
      if(this.turn === true) {
        if(this.values[this.valueIndex].indexOf('.') === -1) {
          this.appendNum('.');
        }
      }
    },
    divide() {
      if(this.turn === true) {
        this.values.push('/');
        this.valueIndex = this.valueIndex + 2;
      }
      this.turn = false;
    },
    multiply() {
      if(this.turn === true) {
        this.values.push('*');
        this.valueIndex = this.valueIndex + 2;
      }
      this.turn = false;
    },
    minus() {
      if(this.turn === true) {
        this.values.push('-');
        this.valueIndex = this.valueIndex + 2;
      }
      this.turn = false;
    },
    add() {
      if(this.turn === true) {
        this.values.push('+');
        this.valueIndex = this.valueIndex + 2;
      }
      this.turn = false;
    },
    equal() {
      if(this.turn === true) {
        for(let i=0; i<this.values.length; i++) {
          this.finalAnswer = eval(this.values.join(" "));
        }
        console.log(this.finalAnswer);
        this.turn = false;
        this.valueIndex = 0;
        this.values = [];
        return this.finalAnswer;
      }
    }
  }
}
</script>

<style scoped>
.calc {
    display: grid;
    grid-template-columns: auto auto auto auto;
    grid-auto-rows: minmax(50px, auto);
    font-size: 30px;
    text-align: center;
    animation: loadit 1s ease-in;
}

.disp {
  grid-column: 1 / 5;
  background-color: white;
  border: solid 1px black;
  padding-top: 6px;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  cursor: pointer;
  border: solid 1px black;
  background-color: #EFEFEF;
  padding-top: 6px;
}

.btn:hover {
  opacity: 85%;
}

@keyframes loadit {
    0% {
        opacity: 0%;
        transform: translateY(40px);
    }
    100% {
        opacity: 100%;
        transform: translateY(0);
    }
}

</style>
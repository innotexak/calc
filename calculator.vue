<template>
  <div class="calculator">
    <div class="display">{{current || 0 }}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="times" class="btn operator">*</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
    <div @click="square" class="btn operator">Sqrt</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      clicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.clicked) {
        this.current = "";
        this.clicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if ((this.current = this.current.indexOf(".") === -1)) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.clicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    square() {
      this.operator = a => a * a;
      this.setPrevious();
      // this.current = `${this.current}${this.current}`;
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 40%;
  margin: 0 auto;
  display: grid;
  font-size: 2em;
  background: #889;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1/5;
  background: black;
  color: white;
  text-align: right;
}
.btn {
  border: 2px solid #999;
}

.operator {
  background: orange;
  color: white;
}
.operator:hover {
  background: white;
  color: orange;
  font-size: 1.2em;
}
</style>

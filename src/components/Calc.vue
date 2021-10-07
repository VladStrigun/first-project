<template>
  <div class="calc">
    <div class="main">
      <input v-model="op1" type="number" />
      <input v-model="op2" type="number" />
      <br />
      = {{ result }}
      <br />
      = {{ fibResult }}
    </div>
    <div class="error" v-if="error">Ошибка: {{ error }}</div>
    <!-- В конце всегда должно быть v-else -->
    <div class="massage">
      <template v-if="result < 0">Получилось отрицательное число</template>
      <template v-else-if="result < 100">Результат в первой сотне</template>
      <template v-else>Просто условие</template>
    </div>
    <div class="keyboard">
      <button
        v-for="operand in operands"
        :key="operand"
        :title="operand"
        @click="calculate(operand)"
        :disabled="operand === '/' && op2 === 0"
      >
        {{ operand }}
      </button>
      <!--<button @click="calculate('+')">+</button>
      <button @click="calculate('-')">-</button>
      <button @click="calculate('/')">/</button>
      <button @click="calculate('*')">*</button>
      <button @click="calculate('**')">**</button>
      <button @click="calculate('//')">//</button> -->
    </div>
    <div class="logs">
      <div v-for="(log, id) in logs" :key="id">
        {{ log }}
      </div>
    </div>
    <div>
      <input
        type="checkbox"
        id="checkbox"
        v-model="buttonVisibility"
        @click="buttonVisibility = !buttonVisibility"
      />
      <label for="checkbox">Отображать экранную клавиатуру</label>
      <div class="button_numbers" v-show="buttonVisibility">
        <button
          v-for="value in keyBoards"
          :key="value"
          :value="value"
          @click="setValue(value)"
        >
          {{ value }}
        </button>
        <button @click="deleteLastChar()">del</button>
        <div class="radio">
          <input
            v-model="selectOp"
            id="one"
            value="op1"
            type="radio"
            name="checedRadio"
          />
          <label for="one">Первое поле</label>
          <input
            v-model="selectOp"
            id="two"
            value="op2"
            type="radio"
            name="checedRadio"
          />
          <label for="two">Второе поле</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      op1: "",
      op2: "",
      error: "",
      operands: ["+", "-", "/", "*", "**", "//"],
      result: 0,
      fibResult: 0,
      selectOp: "op1",
      myCollection: [1, 2, 3, 4, 5, 6, 7],
      logs: {},
      buttonVisibility: true,
      keyBoards: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    };
  },
  methods: {
    setValue(value) {
      const currentOp = this.selectOp;
      const prevValue = currentOp === "op1" ? this.op1 : this.op2;

      this[currentOp] = prevValue + value;
      console.log(this.selectOp);
    },

    deleteLastChar() {
      const currentOp = this.selectOp;
      const value = currentOp === "op1" ? this.op1 : this.op2;

      this[currentOp] = value.slice(0, -1);
    },

    fib(n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
    },
    calculate(operation = "+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.sub();
          break;
        case "/":
          this.div();
          break;
        case "*":
          this.multi();
          break;
        case "**":
          this.degree();
          break;
        case "//":
          this.id();
          break;
      }
      //   this.logs[
      //     Date.now()
      //   ] = `${this.op1}${operation}${this.op2} = ${this.result}`;
      const key = Date.now();
      const value = `${this.op1}${operation}${this.op2} = ${this.result}`;
      //   Vue.set(Object, propertyName, value) or;
      this.$set(this.logs, key, value);
    },
    add() {
      const { op1, op2 } = this;
      this.result = op1 + op2;
      this.fibResult = this.fib1 + this.fib2;
    },
    sub() {
      const { op1, op2 } = this;
      this.result = op1 - op2;
      this.fibResult = this.fib1 - this.fib2;
    },
    div() {
      const { op1, op2 } = this;
      if (op2 === 0) {
        this.error = "Делить на 0 нельзя!";
        return;
      }
      this.result = op1 / op2;
    },
    multi() {
      const { op1, op2 } = this;
      this.result = op1 * op2;
    },
    degree() {
      const { op1, op2 } = this;
      this.result = Math.pow(op1, op2);
    },
    id() {
      const { op1 } = this;
      this.result = Math.trunc(op1);
    },
  },
  computed: {
    fib1() {
      return this.fib(this.op1);
    },

    fib2() {
      return this.fib(this.op2);
    },
    arryFilter() {
      return this.myCollection.filter((i) => i > 5);
    },
  },
};
</script>
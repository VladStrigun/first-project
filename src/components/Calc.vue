<template>
  <div class="calc">
    <div class="main">
      <input v-model="op1" type="number" />
      <input v-model="op2" type="number" />
      = {{ result }}
    </div>
    <div class="keyboard">
      <button @click="result = op1 + op2">+</button>
      <button @click="sub(op1, op2)">-</button>
      <button @click="div">/</button>
      <button @click="multi">*</button>
      <button @click="degree">**</button>
      <button @click="id">//</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      op1: 0,
      op2: 0,
      result: 0,
    };
  },
  methods: {
    sub(op1, op2) {
      this.result = op1 - op2;
    },
    div() {
      const { op1, op2 } = this;
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
};
</script>
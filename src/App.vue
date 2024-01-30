<script setup>
import { ref } from 'vue'

const msg = ref('Hello World!')
</script>



<template>
  <div id="app" style="background-color: aliceblue;">
    <h1>Calculator</h1>
    <p>Enter a mathematical expression in the textbox or click the corresponding buttons, then click the '=' button to calculate</p>
    <div class="calculator" style="background-color: lightslategray">
      <input type="text" v-model="expression" @input="handleInput" />
      <div class="number-pad" style="background-color: whitesmoke;">
        <div v-for="row in 4" :key="row" class="button-row">
          <button
            v-for="button in buttons.slice((row - 1) * 4, row * 4)"
            :key="button"
            @click="appendToExpression(button)"
          >
            {{ button }}
          </button>
        </div>
      </div>
      <div class="extra-buttons">
        <button @click="calculateResult" class="equals-button">=</button>
        <button @click="clearExpression" class="clear-button">C</button>
      </div>
    </div>

    <div class="result">
      <p>{{ result }}</p>
    </div>
    <footer>Author: Mason Inman | inmanmason@gmail.com <br>Purpose: Introduction to Vue.js</footer>
  </div>
</template>


<script>
export default {
  data() {
    return {
      expression: "",
      result: "",
    };
  },
  computed: {
    buttons() {
      return ["7", "8", "9", "/", "4", "5", "6", "*", "1", "2", "3", "-", "0", ".", "+"];
    },
  },
  methods: {
    appendToExpression(value) {
      this.expression += value;
    },
    handleInput() {
      // Validate input if needed
    },
    calculateResult() {
      try {
        this.result = eval(this.expression);
      } catch (error) {
        this.result = "Error";
      }
    },
    clearExpression() {
      this.expression = "";
      this.result = "";
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
  margin-top: 50px;
}

.calculator {
  display: inline-block;
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
}

.calculator input {
  width: 90%;
  margin-bottom: 10px;
  padding: 5px;
  font-size: 16px;
}

.calculator button {
  width: 50px;
  height: 50px;
  margin: 5px;
  font-size: 16px;
  cursor: pointer;
  background-color: gainsboro;
}

.result p {
  font-size: 20px;
  font-weight: bold;
}

</style>

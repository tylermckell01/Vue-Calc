<template>
  <div class="border">
    <div class="screen">
      {{ onDisplay !== "" ? onDisplay : "0" }}
    </div>
    <div class="buttons">
      <div class="row1">
        <button @click="handleInputNumber(7)">7</button>
        <button @click="handleInputNumber(8)">8</button>
        <button @click="handleInputNumber(9)">9</button>
        <button @click="selectedOperation('/')">/</button>
      </div>
      <div class="row2">
        <button @click="handleInputNumber(4)">4</button>
        <button @click="handleInputNumber(5)">5</button>
        <button @click="handleInputNumber(6)">6</button>
        <button @click="selectedOperation('*')">x</button>
      </div>
      <div class="row3">
        <button @click="handleInputNumber(3)">3</button>
        <button @click="handleInputNumber(2)">2</button>
        <button @click="handleInputNumber(1)">1</button>
        <button @click="selectedOperation('-')">-</button>
      </div>
      <div class="row4">
        <button @click="handleInputNumber(0)">0</button>
        <button @click="inputDecimal('.')">.</button>
        <button @click="performOperation()">=</button>
        <button @click="selectedOperation('+')">+</button>
      </div>
      <div class="reset"><button @click="reset()">reset</button></div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "CalculatorApp",

  setup() {
    const firstNumber = ref("");
    const secondNumber = ref("");
    const currentOperation = ref("");
    const onDisplay = ref("");

    const handleInputNumber = (num) => {
      if (!currentOperation.value) {
        firstNumber.value += num;
        onDisplay.value = firstNumber.value;
      } else {
        secondNumber.value += num;
        onDisplay.value = `${firstNumber.value} ${currentOperation.value} ${secondNumber.value}`;
      }
    };

    const inputDecimal = () => {
      if (!currentOperation.value) {
        if (!firstNumber.value.includes(".")) {
          firstNumber.value += ".";
          onDisplay.value = `${firstNumber.value} ${currentOperation.value} ${secondNumber.value}`;
        }
      } else if (!secondNumber.value.includes(".")) {
        secondNumber.value += ".";
        onDisplay.value = `${firstNumber.value} ${currentOperation.value} ${secondNumber.value}`;
      }
    };

    const selectedOperation = (operation) => {
      if (firstNumber.value) {
        currentOperation.value = operation;

        onDisplay.value = `${onDisplay.value} ${operation}`;
      } else {
        onDisplay.value = "must select number first";
      }
    };

    const performOperation = () => {
      const num1 = parseFloat(firstNumber.value);
      const num2 = parseFloat(secondNumber.value);
      let result = 0;

      if (currentOperation.value == "+") {
        result = firstNumber.value = (num1 + num2).toString();
      } else if (currentOperation.value == "-") {
        result = firstNumber.value = (num1 - num2).toString();
      } else if (currentOperation.value == "*") {
        result = firstNumber.value = (num1 * num2).toString();
      } else if (currentOperation.value == "/") {
        result = firstNumber.value = (num1 / num2).toString();
      } else {
        secondNumber.value == "";
        currentOperation.value == "";
      }
      onDisplay.value = result;
      firstNumber.value = result;
      secondNumber.value = "";
      currentOperation.value = "";
    };

    const reset = () => {
      onDisplay.value = "";
      firstNumber.value = "";
      secondNumber.value = "";
      currentOperation.value = "";
    };

    return {
      firstNumber,
      secondNumber,
      currentOperation,
      onDisplay,
      handleInputNumber,
      inputDecimal,
      selectedOperation,
      performOperation,
      reset,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.border {
  justify-self: center;
  width: 400px;
  height: 500px;
  background-color: gray;
}
</style>

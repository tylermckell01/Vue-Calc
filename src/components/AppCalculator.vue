<template>
  <div class="border">
    <div class="screen">
      {{ onDisplay !== "" ? onDisplay : "0" }}
    </div>
    <div class="buttons">
      <div class="row 1">
        <button @click="handleInputNumber(7)">7</button>
        <button @click="handleInputNumber(8)">8</button>
        <button @click="handleInputNumber(9)">9</button>
        <button @click="selectedOperation('/')">/</button>
        <button @click="selectedOperation('sqr')">√</button>
      </div>
      <div class="row 2">
        <button @click="handleInputNumber(4)">4</button>
        <button @click="handleInputNumber(5)">5</button>
        <button @click="handleInputNumber(6)">6</button>
        <button @click="selectedOperation('*')">x</button>
        <button @click="selectedOperation('sqr')">√</button>
      </div>
      <div class="row 3">
        <button @click="handleInputNumber(3)">3</button>
        <button @click="handleInputNumber(2)">2</button>
        <button @click="handleInputNumber(1)">1</button>
        <button @click="selectedOperation('-')">-</button>
        <button @click="selectedOperation('sqr')">√</button>
      </div>
      <div class="row 4">
        <button @click="handleInputNumber(0)">0</button>
        <button @click="inputDecimal('.')">.</button>
        <button @click="performOperation()">=</button>
        <button @click="selectedOperation('+')">+</button>
        <button @click="selectedOperation('sqr')">√</button>
      </div>
      <div class="row reset"><button @click="reset()">reset</button></div>
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
        if (currentOperation.value == "sqr") {
          performOperation();
        }
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
      } else if (currentOperation.value == "sqr") {
        result = firstNumber.value = Math.sqrt(num1).toString();
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
<style scoped lang="scss">
.border {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 25px;
  // width: 300px;
  // height: 400px;
  padding: 15px;
  background-color: rgb(0, 89, 114);
  border-radius: 10px;

  .screen {
    // width: 100%;
    background-color: rgb(173, 203, 95);
    border-radius: 10px;
    padding: 10px 110px;
    font-size: 24px;
  }

  .buttons {
    width: 80%;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;

    .row {
      width: 100%;
      display: flex;
      justify-content: space-around;
      gap: 30px;

      button {
        width: 60px;
        height: 50px;
        border: none;
        border-radius: 5px;

        &:hover {
          cursor: pointer;
          background-color: rgba(152, 152, 152, 0.7);
          border-radius: 10px;
        }
      }
    }

    .reset {
      button {
        width: 100px;
        height: 35px;
      }
    }
  }
}
</style>

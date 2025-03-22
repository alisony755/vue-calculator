<template>
  <div class="calculator-container">
    <div class="calculator">
      <div class="display">
        <div class="previous-operand">{{ previousOperand }} {{ operation }}</div>
        <div class="current-operand">{{ currentOperand || '0' }}</div>
      </div>
      <button @click="clear" class="span-two">AC</button>
      <button @click="deleteNumber">DEL</button>
      <button @click="chooseOperation('÷')" class="operation">÷</button>
      <button @click="appendNumber('7')">7</button>
      <button @click="appendNumber('8')">8</button>
      <button @click="appendNumber('9')">9</button>
      <button @click="chooseOperation('×')" class="operation">×</button>
      <button @click="appendNumber('4')">4</button>
      <button @click="appendNumber('5')">5</button>
      <button @click="appendNumber('6')">6</button>
      <button @click="chooseOperation('−')" class="operation">−</button>
      <button @click="appendNumber('1')">1</button>
      <button @click="appendNumber('2')">2</button>
      <button @click="appendNumber('3')">3</button>
      <button @click="chooseOperation('+')" class="operation">+</button>
      <button @click="appendNumber('0')" class="span-two">0</button>
      <button @click="appendNumber('.')">.</button>
      <button @click="compute" class="operation equals">=</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const currentOperand = ref('');
const previousOperand = ref('');
const operation = ref('');
const shouldResetScreen = ref(false);

function clear() {
  currentOperand.value = '';
  previousOperand.value = '';
  operation.value = '';
}

function deleteNumber() {
  currentOperand.value = currentOperand.value.toString().slice(0, -1);
}

function appendNumber(number) {
  if (number === '.' && currentOperand.value.includes('.')) return;
  if (shouldResetScreen.value) {
    currentOperand.value = '';
    shouldResetScreen.value = false;
  }
  currentOperand.value = currentOperand.value.toString() + number.toString();
}

function chooseOperation(op) {
  if (currentOperand.value === '') return;
  if (previousOperand.value !== '') {
    compute();
  }
  operation.value = op;
  previousOperand.value = currentOperand.value;
  shouldResetScreen.value = true;
}

function compute() {
  let computation;
  const prev = parseFloat(previousOperand.value);
  const current = parseFloat(currentOperand.value);
  if (isNaN(prev) || isNaN(current)) return;

  switch (operation.value) {
    case '+':
      computation = prev + current;
      break;
    case '−':
      computation = prev - current;
      break;
    case '×':
      computation = prev * current;
      break;
    case '÷':
      computation = prev / current;
      break;
    default:
      return;
  }

  currentOperand.value = computation;
  operation.value = '';
  previousOperand.value = '';
}
</script>

<style scoped>
.calculator-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 1rem;
  background-color: #f5f5f5;
}

.calculator {
  width: 100%;
  max-width: 400px;
  background-color: #f0f0f0;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 1px;
  padding: 1px;
}

.display {
  grid-column: 1 / -1;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: space-around;
  padding: 10px;
  word-wrap: break-word;
  word-break: break-all;
  min-height: 100px;
}

.display .previous-operand {
  color: rgba(255, 255, 255, 0.75);
  font-size: 1.5rem;
}

.display .current-operand {
  color: white;
  font-size: 2.5rem;
}

button {
  cursor: pointer;
  font-size: 1.5rem;
  border: none;
  outline: none;
  background-color: white;
  padding: 1rem;
  transition: background-color 0.15s ease;
}

button:hover {
  background-color: rgba(255, 255, 255, 0.9);
}

.operation {
  background-color: #f8a51d;
  color: white;
}

.operation:hover {
  background-color: #da9016;
}

.equals {
  background-color: #2196f3;
}

.equals:hover {
  background-color: #0d8aee;
}

.span-two {
  grid-column: span 2;
}

@media (max-width: 500px) {
  button {
    padding: 0.75rem;
    font-size: 1.25rem;
  }
  
  .display {
    min-height: 80px;
  }
  
  .display .previous-operand {
    font-size: 1.25rem;
  }
  
  .display .current-operand {
    font-size: 2rem;
  }
}
</style>
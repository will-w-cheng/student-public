---
toc: true
comments: true
layout: post
title: Java Calculator
description: Cool javascript calculator thing I guess
type: hacks
courses: { csse: {week: 0}, csp: {week: 2}, csa: {week: 0} }
---

# Calculator

<div id="calculator" style="background-image: url('background.jpg'); background-size: cover; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0;">
  <div style="background-color: rgba(255, 255, 255, 0.8); border-radius: 10px; padding: 20px; box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);">
    <input type="text" id="display" readonly style="margin-bottom: 10px;">
    <div id="buttons" style="display: grid; grid-template-columns: repeat(4, 1fr); grid-gap: 5px;">
      <button onclick="appendToDisplay('7')">7</button>
      <button onclick="appendToDisplay('8')">8</button>
      <button onclick="appendToDisplay('9')">9</button>
      <button onclick="appendToDisplay('/')">/</button>
      <button onclick="appendToDisplay('4')">4</button>
      <button onclick="appendToDisplay('5')">5</button>
      <button onclick="appendToDisplay('6')">6</button>
      <button onclick="appendToDisplay('*')">*</button>
      <button onclick="appendToDisplay('1')">1</button>
      <button onclick="appendToDisplay('2')">2</button>
      <button onclick="appendToDisplay('3')">3</button>
      <button onclick="appendToDisplay('-')">-</button>
      <button onclick="appendToDisplay('0')">0</button>
      <button onclick="appendToDisplay('.')">.</button>
      <button onclick="clearDisplay()">C</button>
      <button onclick="appendToDisplay('+')">+</button>
      <button onclick="calculate()" style="grid-column: span 2;">=</button>
    </div>
  </div>
</div>

<script>
  const display = document.getElementById('display');

  function appendToDisplay(value) {
    display.value += value;
  }

  function clearDisplay() {
    display.value = '';
  }

  function calculate() {
    try {
      display.value = eval(display.value);
    } catch (error) {
      display.value = 'Error';
    }
  }
</script>

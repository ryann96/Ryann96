---
toc: true
comments: false
layout: post
title: Calculator
description: Calculator
type: hacks
courses: { compsci: {week: 2} }
---


<html>
<head>
    <title>Simple Calculator</title>
</head>
<body>
    <h1>Simple Calculator</h1>
    
    <input type="text" id="display" readonly>
    
    <table>
        <tr>
            <td><button onclick="appendToDisplay('7')">7</button></td>
            <td><button onclick="appendToDisplay('8')">8</button></td>
            <td><button onclick="appendToDisplay('9')">9</button></td>
            <td><button onclick="appendToDisplay('+')">+</button></td>
        </tr>
        <tr>
            <td><button onclick="appendToDisplay('4')">4</button></td>
            <td><button onclick="appendToDisplay('5')">5</button></td>
            <td><button onclick="appendToDisplay('6')">6</button></td>
            <td><button onclick="appendToDisplay('-')">-</button></td>
        </tr>
        <tr>
            <td><button onclick="appendToDisplay('1')">1</button></td>
            <td><button onclick="appendToDisplay('2')">2</button></td>
            <td><button onclick="appendToDisplay('3')">3</button></td>
            <td><button onclick="appendToDisplay('*')">*</button></td>
        </tr>
        <tr>
            <td><button onclick="clearDisplay()">C</button></td>
            <td><button onclick="appendToDisplay('0')">0</button></td>
            <td><button onclick="calculateResult()">=</button></td>
            <td><button onclick="appendToDisplay('/')">/</button></td>
        </tr>
    </table>

    <script>
        function appendToDisplay(value) {
            document.getElementById('display').value += value;
        }

        function clearDisplay() {
            document.getElementById('display').value = '';
        }

        function calculateResult() {
            try {
                const result = eval(document.getElementById('display').value);
                document.getElementById('display').value = result;
            } catch (error) {
                document.getElementById('display').value = 'Error';
            }
        }
    </script>
</body>
</html>
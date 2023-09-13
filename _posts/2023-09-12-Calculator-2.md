---
toc: true
comments: false
layout: post
title: Calculator 2
description: Calculator V2
type: hacks
courses: { compsci: {week: 4} }
---

<html>
<head>
    <title>Score Calculator</title>
    <style>
        /* Add your CSS styles here */
        input[type="number"] {
            text-align: right;
            width: 5em;
        }
    </style>
</head>
<body>
    <h3>Input scores and press "Tab" to add each new number.</h3>
    
 <div id="scores">
        <!-- JavaScript-generated inputs go here -->
    </div>
    
<script>
        // Function to create a new input line
        function createInputLine(index) {
            const label = document.createElement('label');
            label.htmlFor = `score-${index}`;
            label.textContent = `${index + 1}. `;
            
            const input = document.createElement('input');
            input.id = `score-${index}`;
            input.type = 'number';
            input.name = 'score';
            
            const br = document.createElement('br');
            
            document.getElementById('scores').appendChild(label);
            document.getElementById('scores').appendChild(input);
            document.getElementById('scores').appendChild(br);
            
            input.focus();
        }
        
        // Function to handle the calculator logic
        function calculator(event) {
            const eventKey = event.key;
            
            if (eventKey === 'Tab' || eventKey === 'Enter') {
                event.preventDefault();
                
                const scoreInputs = document.getElementsByName('score');
                let total = 0;
                let count = 0;
                
                for (const input of scoreInputs) {
                    const value = parseFloat(input.value);
                    if (!isNaN(value)) {
                        total += value;
                        count++;
                    }
                }
                
                const totalElement = document.getElementById('total');
                const countElement = document.getElementById('count');
                const averageElement = document.getElementById('average');
                
                totalElement.textContent = total.toFixed(2);
                countElement.textContent = count;
                averageElement.textContent = (count > 0) ? (total / count).toFixed(2) : '0.0';
                
                if (count === scoreInputs.length) {
                    createInputLine(count);
                }
            }
        }
        
        // Attach the event handler to the document body
        document.body.addEventListener('keydown', calculator);
        
        // Create the first input line
        createInputLine(0);
    </script>
</body>
</html>
# Ex04 Simple Calculator - React Project
## Date:24-05-2026
## Reg No:212224220123

## AIM
To  develop a Simple Calculator using React.js with clean and responsive design, ensuring a smooth user experience across different screen sizes.

## ALGORITHM
### STEP 1
Create a React App.

### STEP 2
Open a terminal and run:
  <ul><li>npx create-react-app simple-calculator</li>
  <li>cd simple-calculator</li>
  <li>npm start</li></ul>

### STEP 3
Inside the src/ folder, create a new file Calculator.js and define the basic structure.

### STEP 4
Plan the UI: Display screen, number buttons (0-9), operators (+, -, *, /), clear (C), and equal (=).

### STEP 5
Create a new file Calculator.css in src/ and add the styling.

### STEP 6
Open src/App.js and modify it.

### STEP 7
Start the development server.
  npm start

### STEP 8
Open http://localhost:3000/ in the browser.

### STEP 9
Test the calculator by entering numbers and operations.

### STEP 10
Fix styling issues and refine content placement.

### STEP 11
Deploy the website.

### STEP 12
Upload to GitHub Pages for free hosting.

## PROGRAM
## Calculator.js:
```
import React, { useState } from 'react';
import './Calculator.css';

const Calculator = () => {
    const [input, setInput] = useState("");
    const [result, setResult] = useState("");

    const handleClick = (value) => {
        setInput((prev) => prev + value);
    };

    const handleClear = () => {
        setInput("");
        setResult("");
    };

    const handleBackspace = () => {
        setInput((prev) => prev.slice(0, -1));
    };

    const handleCalculate = () => {
        try {
            if (!input.trim()) return;
            // Safe mathematical evaluation
            // eslint-disable-next-line no-new-func
            const sanitizedResult = new Function(`return ${input}`)();
            
            if (sanitizedResult === Infinity || isNaN(sanitizedResult)) {
                setResult("Error");
            } else {
                setResult(Number(sanitizedResult.toFixed(4)).toString());
            }
        } catch (error) {
            setResult("Error");
        }
    };

    return (
        <div className="calc-wrapper">
            <div className="calc-card">
                {/* Brand Header */}
                <div className="calc-header">
                    <span className="brand-name">Yashova <span>Smart Calc</span></span>
                    <div className="status-indicator"></div>
                </div>

                {/* Professional Screen Layout */}
                <div className="calc-screen">
                    <div className="history-display">{input || "0"}</div>
                    <div className="main-display">{result || "0"}</div>
                </div>

                {/* Grid Layout */}
                <div className="calc-grid">
                    <button onClick={handleClear} className="key action-key">C</button>
                    <button onClick={handleBackspace} className="key action-key">&#x232b;</button>
                    <button onClick={() => handleClick("/")} className="key math-key">&divide;</button>
                    <button onClick={() => handleClick("*")} className="key math-key">&times;</button>

                    <button onClick={() => handleClick("7")} className="key num-key">7</button>
                    <button onClick={() => handleClick("8")} className="key num-key">8</button>
                    <button onClick={() => handleClick("9")} className="key num-key">9</button>
                    <button onClick={() => handleClick("-")} className="key math-key">&minus;</button>

                    <button onClick={() => handleClick("4")} className="key num-key">4</button>
                    <button onClick={() => handleClick("5")} className="key num-key">5</button>
                    <button onClick={() => handleClick("6")} className="key num-key">6</button>
                    <button onClick={() => handleClick("+")} className="key math-key">+</button>

                    <button onClick={() => handleClick("1")} className="key num-key">1</button>
                    <button onClick={() => handleClick("2")} className="key num-key">2</button>
                    <button onClick={() => handleClick("3")} className="key num-key">3</button>
                    
                    {/* Equals spans two positions vertically */}
                    <button onClick={handleCalculate} className="key total-key">=</button>

                    <button onClick={() => handleClick("0")} className="key num-key zero-key">0</button>
                    <button onClick={() => handleClick(".")} className="key num-key">.</button>
                </div>
            </div>
        </div>
    );
};

export default Calculator;
```
## Calculator.css:
```
/* Centered layout canvas background */
.calc-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: radial-gradient(circle at center, #1e293b 0%, #0f172a 100%);
    padding: 20px;
}

/* Premium Dashboard Case Frame */
.calc-card {
    background: #111827;
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 24px;
    padding: 24px;
    width: 100%;
    max-width: 350px;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.7);
    position: relative;
}

/* Application Header branding bar */
.calc-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 18px;
    padding: 0 4px;
}

.brand-name {
    font-size: 0.85rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    color: #9ca3af;
}

.brand-name span {
    color: #3b82f6;
    font-weight: 400;
}

.status-indicator {
    width: 8px;
    height: 8px;
    background-color: #10b981;
    border-radius: 50%;
    box-shadow: 0 0 8px #10b981;
}

/* Integrated Matte-finish Screen module */
.calc-screen {
    background: #030712;
    border: 1px solid rgba(255, 255, 255, 0.03);
    border-radius: 16px;
    padding: 20px;
    text-align: right;
    min-height: 110px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-bottom: 24px;
}

.history-display {
    color: #6b7280;
    font-size: 1rem;
    letter-spacing: 0.5px;
    min-height: 1.5rem;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.main-display {
    color: #f9fafb;
    font-size: 2.4rem;
    font-weight: 500;
    line-height: 1;
    overflow-x: auto;
    white-space: nowrap;
}

/* Micro-scroll behavior custom scrollbar */
.main-display::-webkit-scrollbar {
    height: 3px;
}
.main-display::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 2px;
}

/* Structured Keypad Configuration */
.calc-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
}

/* Universal Button Element properties */
.key {
    border: none;
    outline: none;
    padding: 16px;
    font-size: 1.25rem;
    font-weight: 500;
    border-radius: 14px;
    cursor: pointer;
    transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);
    display: flex;
    justify-content: center;
    align-items: center;
}

.key:active {
    transform: scale(0.95);
}

/* Numeric Input Key styling */
.num-key {
    background: #1f2937;
    color: #f3f4f6;
}

.num-key:hover {
    background: #374151;
}

/* Operation controls functional layout adjustments */
.action-key {
    background: rgba(239, 68, 68, 0.1);
    color: #f87171;
}

.action-key:hover {
    background: rgba(239, 68, 68, 0.2);
}

/* Mathematical Operator modifiers */
.math-key {
    background: rgba(59, 130, 246, 0.1);
    color: #60a5fa;
    font-size: 1.4rem;
}

.math-key:hover {
    background: rgba(59, 130, 246, 0.2);
}

/* Execution/Equals Key highlighting */
.total-key {
    grid-row: span 2;
    background: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
    color: #ffffff;
    box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
}

.total-key:hover {
    box-shadow: 0 6px 20px rgba(59, 130, 246, 0.4);
    filter: brightness(1.1);
}

/* Spanning adjustment modifier for standard double cell keys */
.zero-key {
    grid-column: span 2;
}

/* Mobile viewport adjustments formatting response */
@media (max-width: 360px) {
    .calc-card {
        padding: 16px;
    }
    .key {
        padding: 14px;
        font-size: 1.15rem;
    }
}
```

## OUTPUT
<img width="1911" height="1083" alt="image" src="https://github.com/user-attachments/assets/9ad0c30e-7346-4fca-80a2-027b07f3f85f" />
<img width="1896" height="948" alt="image" src="https://github.com/user-attachments/assets/2740210c-7b5d-4fe0-b929-3c1b57ba2769" />


## RESULT
The program for developing a simple calculator in React.js is executed successfully.

# Ex04 Simple Calculator - React Project
## Date:14-03-2026
## Name : Aadhithya V
## Reg No :21222504002

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

## app.jsx
```
import { useState } from "react";
import "./App.css";

function App() {
  const [input, setInput] = useState("");
  const [result, setResult] = useState("");

  const handleClick = (value) => {
    if (value === "=") {
      calculate();
    } else if (value === "AC") {
      setInput("");
      setResult("");
    } else if (value === "DEL") {
      setInput((prev) => prev.slice(0, -1));
    } else {
      setInput((prev) => prev + value);
      setResult("");
    }
  };

  const calculate = () => {
    try {
      if (!input) return;

      const answer = eval(input);

      setResult(answer);
    } catch {
      setResult("Error");
    }
  };

  const buttons = [
    "AC", "DEL", "%", "/",
    "7", "8", "9", "*",
    "4", "5", "6", "-",
    "1", "2", "3", "+",
    "0", ".", "="
  ];

  return (
    <div className="app">

      <div className="calculator">

        <div className="calculator-header">
          <span className="brand">NOVA</span>
          <span className="mini-text">CALCULATOR</span>
        </div>

        <div className="display">

          <div className="expression">
            {input || "0"}
          </div>

          <div className="answer">
            {result !== "" ? `= ${result}` : ""}
          </div>

        </div>

        <div className="buttons">

          {buttons.map((button) => (

            <button
              key={button}
              onClick={() => handleClick(button)}
              className={`
                ${button === "=" ? "equals" : ""}
                ${["+", "-", "*", "/", "%"].includes(button)
                  ? "operator"
                  : ""}
                ${["AC", "DEL"].includes(button)
                  ? "special"
                  : ""}
                ${button === "0" ? "zero" : ""}
              `}
            >
              {button}
            </button>

          ))}

        </div>

        <div className="footer">
          React • Nova Calculator
        </div>

      </div>

    </div>
  );
}

export default App;
```

## app.css
```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Segoe UI", Arial, sans-serif;
}

/* MAIN BACKGROUND */

.app {
  min-height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;

  padding: 20px;

  background:
    radial-gradient(circle at 20% 20%, #5b21b6 0%, transparent 30%),
    radial-gradient(circle at 80% 80%, #0ea5e9 0%, transparent 30%),
    linear-gradient(135deg, #020617, #0f172a, #111827);

  position: relative;
  overflow: hidden;
}

/* Decorative glowing circles */

.app::before {
  content: "";

  position: absolute;

  width: 300px;
  height: 300px;

  border-radius: 50%;

  background: #8b5cf6;

  filter: blur(120px);

  opacity: 0.25;

  top: -100px;
  left: -100px;

  animation: float 6s ease-in-out infinite;
}

.app::after {
  content: "";

  position: absolute;

  width: 300px;
  height: 300px;

  border-radius: 50%;

  background: #06b6d4;

  filter: blur(120px);

  opacity: 0.25;

  bottom: -100px;
  right: -100px;

  animation: float 7s ease-in-out infinite reverse;
}

/* CALCULATOR */

.calculator {
  position: relative;

  z-index: 2;

  width: 370px;

  padding: 25px;

  border-radius: 30px;

  background: rgba(15, 23, 42, 0.72);

  backdrop-filter: blur(25px);

  border: 1px solid rgba(255, 255, 255, 0.12);

  box-shadow:
    0 25px 70px rgba(0, 0, 0, 0.55),
    inset 0 1px 1px rgba(255, 255, 255, 0.08);

  animation: appear 0.6s ease;
}

/* HEADER */

.calculator-header {
  display: flex;

  justify-content: space-between;

  align-items: center;

  margin-bottom: 20px;
}

.brand {
  font-size: 18px;

  font-weight: 800;

  letter-spacing: 4px;

  color: #a78bfa;
}

.mini-text {
  font-size: 10px;

  letter-spacing: 2px;

  color: #64748b;
}

/* DISPLAY */

.display {
  min-height: 125px;

  padding: 20px;

  margin-bottom: 20px;

  border-radius: 20px;

  background: rgba(2, 6, 23, 0.75);

  border: 1px solid rgba(255, 255, 255, 0.06);

  box-shadow:
    inset 0 0 25px rgba(0, 0, 0, 0.4);

  display: flex;

  flex-direction: column;

  justify-content: center;

  align-items: flex-end;

  overflow: hidden;
}

.expression {
  width: 100%;

  text-align: right;

  color: #cbd5e1;

  font-size: 25px;

  min-height: 35px;

  overflow-x: auto;

  white-space: nowrap;
}

.answer {
  color: #a78bfa;

  font-size: 34px;

  font-weight: 700;

  margin-top: 8px;

  min-height: 42px;

  text-shadow:
    0 0 15px rgba(167, 139, 250, 0.6);
}

/* BUTTON GRID */

.buttons {
  display: grid;

  grid-template-columns: repeat(4, 1fr);

  gap: 12px;
}

/* BUTTON */

button {
  height: 62px;

  border: none;

  border-radius: 18px;

  font-size: 19px;

  font-weight: 600;

  color: #e2e8f0;

  background: rgba(255, 255, 255, 0.07);

  border: 1px solid rgba(255, 255, 255, 0.05);

  cursor: pointer;

  transition:
    transform 0.15s,
    box-shadow 0.15s,
    background 0.15s;

  box-shadow:
    0 5px 15px rgba(0, 0, 0, 0.2);
}

button:hover {
  transform: translateY(-3px);

  background: rgba(255, 255, 255, 0.13);

  box-shadow:
    0 8px 20px rgba(0, 0, 0, 0.3);
}

button:active {
  transform: scale(0.92);
}

/* OPERATORS */

.operator {
  color: #38bdf8;

  background: rgba(14, 165, 233, 0.12);

  border-color: rgba(56, 189, 248, 0.2);
}

.operator:hover {
  background: rgba(14, 165, 233, 0.25);

  box-shadow:
    0 0 20px rgba(56, 189, 248, 0.2);
}

/* AC & DELETE */

.special {
  color: #fb7185;

  background: rgba(244, 63, 94, 0.12);

  border-color: rgba(244, 63, 94, 0.2);
}

.special:hover {
  background: rgba(244, 63, 94, 0.25);

  box-shadow:
    0 0 20px rgba(244, 63, 94, 0.2);
}

/* EQUAL */

.equals {
  grid-column: span 2;

  color: white;

  background:
    linear-gradient(
      135deg,
      #8b5cf6,
      #6366f1
    );

  box-shadow:
    0 0 20px rgba(139, 92, 246, 0.35);
}

.equals:hover {
  background:
    linear-gradient(
      135deg,
      #a78bfa,
      #818cf8
    );

  box-shadow:
    0 0 30px rgba(139, 92, 246, 0.6);
}

/* ZERO */

.zero {
  grid-column: span 2;
}

/* FOOTER */

.footer {
  text-align: center;

  margin-top: 20px;

  font-size: 10px;

  letter-spacing: 2px;

  color: #475569;
}

/* ANIMATIONS */

@keyframes appear {

  from {
    opacity: 0;
    transform: translateY(30px) scale(0.95);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }

}

@keyframes float {

  0%,
  100% {
    transform: translate(0, 0);
  }

  50% {
    transform: translate(30px, 30px);
  }

}

/* MOBILE */

@media (max-width: 450px) {

  .calculator {
    width: 100%;

    max-width: 370px;

    padding: 18px;
  }

  button {
    height: 58px;
  }

  .display {
    min-height: 110px;
  }

  .expression {
    font-size: 21px;
  }

  .answer {
    font-size: 29px;
  }

}
```
## main.jsx

```
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./App.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
## OUTPUT

<img width="1465" height="782" alt="643344859-420857f0-5e1b-40ac-8f51-39a07cab9abb" src="https://github.com/user-attachments/assets/08be1112-2751-417d-94ca-442f011e0581" />


## RESULT
The program for developing a simple calculator in React.js is executed successfully.

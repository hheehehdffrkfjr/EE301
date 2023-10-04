

# I. Introduction
This blog I will illustrate some details about how to construct a web calculator achieved by HTML, CSS and JS.
 
 This type of calculator has some basic functions such as addition, subtraction, multiplication, division, clearing and this calculator can support the trigonometric operation, power operation and logarithm operation.


---



# II. Student's information
The Link Your Class    |  [https://bbs.csdn.net/forums/ssynkqtd-04](https://bbs.csdn.net/forums/ssynkqtd-04)
-------- | -----
The Link of Requirement of This Assignment | [https://bbs.csdn.net/topics/617332156](https://bbs.csdn.net/topics/617332156)
The Aim of This Assignment  | Create a calculator with a visual interface.
MU STU ID and FZU STU ID  | 21125376_832102230
---
# III. PSP
| **Personal Software Process Stages**    | Estimated Time（minutes） | Actual Time（minutes） |
| :-------------------------------------- | :------------------------ | :--------------------- |
| Planning                                |                        |                        |
| • Estimate                              |                 30          |               35         |
| Development                             |                           |                        |
| • Analysis                              |           40                |                50        |
| • Design Spec                           |               60            |              90          |
| • Design Review                         |                 60          |           80             |
| • Coding Standard                       |                90           |               100         |
| • Design                                |                120           |                 125       |
| • Coding                                |                  120         |                 150       |
| • Code Review                           |               60            |             70           |
| • Test                                  |                   20        |                   35    |
| Reporting                               |                           |                        |
| • Test Repor                            |           13                |         15               |
| • Size Measurement                      |          5               |              5       |
| • Postmortem & Process Improvement Plan |                   24        |             40           |
| **Sum**                                 |         642                  |            795            |
---
# IV. Some problem-solving ideas before creating the calculator
As we all know, there are lots of software can help us making the visual infereface such as Android studio, Unity and so on. But basing on my limit computer programming skill and some other factors, I choose to use the **HTML, CSS and JS** to create a simple calculator to finish this task on the **Vscode** which is a popular software to investigate front end, followed by some reasons:
- Vscode will use less memory to help me creating a web page and the complexitiy of **HTML, CSS and JS** is simple for me.
- Vscode have various types of plug-in to debug our code (such as **Live Server**, it can modify the result automatically according to the newest code.) These additional functions can reduce the difficulty of finishing the task.

After that, because I haven't ever gotten in touch with how to create a web calculator, so firstly I searched some useful related information from some special websites such as **Youtube, bilibili, CSDN** and so on. Besides, I learnt how to design my own calculator's apparance, I learnt how to add the button to my web, how to achieve the additional function and so on.

# V. Design and implementation process
## 1. Page Layout
First and foremost, I focused on creating the user interface (UI) for the calculator. The goal was to design an intuitive and visually appealing layout, allowing users to input expressions and view results easily. I chose to use **HTML and CSS** to construct the page layout, ensuring responsiveness and user-friendliness. Here's a key part of the page layout:

```javascript
<div id="calculator">
        <input type="text" id="display">
        <div class="row">
            <button value="7" onclick="appendToDisplay('7')">7</button>
            <button value="8" onclick="appendToDisplay('8')">8</button>
            <button value="9" onclick="appendToDisplay('9')">9</button>
            <button value="/" onclick="appendToDisplay('/')">/</button>
        </div>
        <div class="row">
            <button value="4" onclick="appendToDisplay('4')">4</button>
            <button value="5" onclick="appendToDisplay('5')">5</button>
            <button value="6" onclick="appendToDisplay('6')">6</button>
            <button value="-" onclick="appendToDisplay('-')">-</button>
        </div>
        <div class="row">
            <button value="1" onclick="appendToDisplay('1')">1</button>
            <button value="2" onclick="appendToDisplay('2')">2</button>
            <button value="3" onclick="appendToDisplay('3')">3</button>
            <button value="+" onclick="appendToDisplay('+')">+</button>
        </div>
        <div class="row">
            <button value="0" onclick="appendToDisplay('0')">0</button>
            <button value="." onclick="appendToDisplay('.')">.</button>
            <button value="=" onclick="getResult()">=</button>
            <button value="C" onclick="clearAll()">C</button>
        </div>
        <div class="row">
            <button value="sin" onclick="Sin()">sin()</button>
            <button value="cos" onclick="Cos()">cos()</button>
            <button value="tan" onclick="Tan()">tan()</button>
            <button value="√" onclick="Sqrt()">√</button>
        </div>
        <div class="row">
            <button value="*" onclick="appendToDisplay('*')">*</button>
            <button value="^" onclick="appendToDisplay('**')">^</button>
            <button value="log" onclick="Log()">log()</button>
            <button value="←" onclick="moveCursor()">&#8592;</button> 
        </div>
    </div>
```
This is the code for **CSS**:
```javascript
<style>
        /* CSS styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            /* Horizontally center align */
            align-items: center;
            /* Vertically center align */
            height: 100vh;
            /* Make the entire page fill the viewport height */
            margin: 0;
        }

        #calculator {
            width: 300px;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #display {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 2px solid #ccc;
            /* Bold border */
            border-radius: 5px;
            font-size: 18px;
            max-width: 100%;
            /* Max width */
            text-align: right;
            /* Right-align text */
            box-sizing: border-box;
            /* Prevent border from adding to width */
        }

        .row {
            display: flex;
        }

        .row button {
            flex: 1;
            padding: 10px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            background-color: #337ab7;
            color: #fff;
            font-size: 18px;
            cursor: pointer;
        }

        .row button:hover {
            background-color: #23527c;
        }
    </style>
```

## 2. Button Functionality
To make the calculator interactive, I added onclick event handlers to each button. These handlers enable users to input numbers and operators by clicking buttons, displaying them on the calculator's display screen. The aim was to ensure reliable and user-friendly button functionality.
```javascript
function appendToDisplay(value) {
            // Append the user's input value to the display
            const display = document.getElementById('display');
            const startPos = display.selectionStart;
            const endPos = display.selectionEnd;
            const currentValue = display.value;
            const newValue = currentValue.substring(0, startPos) + value + currentValue.substring(endPos);
            display.value = newValue;
            display.setSelectionRange(startPos + value.length, startPos + value.length);
            display.focus();
        }
```
## 3.  Calculation Logic
The heart of the project lies in implementing the calculation logic. I utilized JavaScript to handle user-input mathematical expressions and compute results. This encompassed basic arithmetic operations such as addition, subtraction, multiplication, and division, along with advanced mathematical operations like trigonometric functions (e.g., sin, cos, tan), square roots, logarithms, and more. My focus was on maintaining code readability and performance to ensure accurate calculations.When the user clicks the equals (=) button, I retrieve the expression string from the display screen and use JavaScript's eval function to compute the result. If an error occurs during evaluation, I display an error message on the screen. 

```javascript
function getResult() {
            try {
                // Calculate the user's input expression and display the result
                const expression = document.getElementById('display').value;
                const result = eval(expression);
                document.getElementById('display').value = result;
            } catch (error) {
                // Display an error message if an error occurs during calculation
                document.getElementById('display').value = 'Error';
            }
        }
```

```javascript
function Sin() {
            // Calculate sine value
            const angle = parseFloat(document.getElementById('display').value);
            const radians = (angle * Math.PI) / 180;
            const sinValue = Math.sin(radians);
            document.getElementById('display').value = sinValue.toFixed(8); // Round to 8 decimal places
        }

        function Cos() {
            // Calculate cosine value
            const angle = parseFloat(document.getElementById('display').value);
            const radians = (angle * Math.PI) / 180;
            const cosValue = Math.cos(radians);
            document.getElementById('display').value = cosValue.toFixed(8); // Round to 8 decimal places
        }

        function Tan() {
            // Calculate tangent value
            const angle = parseFloat(document.getElementById('display').value);
            const radians = (angle * Math.PI) / 180;
            const tanValue = Math.tan(radians);
            document.getElementById('display').value = tanValue.toFixed(8); // Round to 8 decimal places
        }

        function Sqrt() {
            // Calculate square root
            const value = parseFloat(document.getElementById('display').value);
            const sqrtValue = Math.sqrt(value);
            document.getElementById('display').value = sqrtValue.toFixed(8); // Round to 8 decimal places
        }

        function Log() {
            // Calculate base 10 logarithm
            const value = parseFloat(document.getElementById('display').value);
            const logValue = Math.log10(value);
            document.getElementById('display').value = logValue.toFixed(8); // Round to 8 decimal places
        }

        function moveCursor() {
            // Move the cursor one position to the left
            const display = document.getElementById('display');
            const currentPosition = display.selectionStart;
            if (currentPosition > 0) {
                display.setSelectionRange(currentPosition - 1, currentPosition - 1);
                display.focus();
            }
        }
```
## 4. Cursor Control
While cursor control is an additional feature, it greatly enhances the user input experience. I added a dedicated "←" button to allow users to move the cursor within the input box. This feature empowers users to easily edit their input.
```javascript
function moveCursor() {
            // Move the cursor one position to the left
            const display = document.getElementById('display');
            const currentPosition = display.selectionStart;
            if (currentPosition > 0) {
                display.setSelectionRange(currentPosition - 1, currentPosition - 1);
                display.focus();
            }
        }
```

## 5. Clear function
When user press the button "C", the result will be cleared and the user can calculate again.
```javascript
function clearAll() {
            // Clear the display
            document.getElementById('display').value = '';
        }
```
## 6. Page Styling
Lastly, I dedicated time to enhance the visual appeal of the page. Using CSS styles, I set background colors, button styles, input box borders, and other elements to improve the overall appearance and user experience.

## 7. The flow chart
![在这里插入图片描述](https://img-blog.csdnimg.cn/284e80c687494b69a0647862fad5db0a.png#pic_center)


# VI. Code Description

This is the whole code:
```javascript
<!DOCTYPE html>
<html>

<head>
    <title>Calculator</title>
    <style>
        /* CSS styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            /* Horizontally center align */
            align-items: center;
            /* Vertically center align */
            height: 100vh;
            /* Make the entire page fill the viewport height */
            margin: 0;
        }

        #calculator {
            width: 300px;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #display {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 2px solid #ccc;
            /* Bold border */
            border-radius: 5px;
            font-size: 18px;
            max-width: 100%;
            /* Max width */
            text-align: right;
            /* Right-align text */
            box-sizing: border-box;
            /* Prevent border from adding to width */
        }

        .row {
            display: flex;
        }

        .row button {
            flex: 1;
            padding: 10px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            background-color: #337ab7;
            color: #fff;
            font-size: 18px;
            cursor: pointer;
        }

        .row button:hover {
            background-color: #23527c;
        }
    </style>
</head>

<body>
    <div id="calculator">
        <input type="text" id="display">
        <div class="row">
            <button value="7" onclick="appendToDisplay('7')">7</button>
            <button value="8" onclick="appendToDisplay('8')">8</button>
            <button value="9" onclick="appendToDisplay('9')">9</button>
            <button value="/" onclick="appendToDisplay('/')">/</button>
        </div>
        <div class="row">
            <button value="4" onclick="appendToDisplay('4')">4</button>
            <button value="5" onclick="appendToDisplay('5')">5</button>
            <button value="6" onclick="appendToDisplay('6')">6</button>
            <button value="-" onclick="appendToDisplay('-')">-</button>
        </div>
        <div class="row">
            <button value="1" onclick="appendToDisplay('1')">1</button>
            <button value="2" onclick="appendToDisplay('2')">2</button>
            <button value="3" onclick="appendToDisplay('3')">3</button>
            <button value="+" onclick="appendToDisplay('+')">+</button>
        </div>
        <div class="row">
            <button value="0" onclick="appendToDisplay('0')">0</button>
            <button value="." onclick="appendToDisplay('.')">.</button>
            <button value="=" onclick="getResult()">=</button>
            <button value="C" onclick="clearAll()">C</button>
        </div>
        <div class="row">
            <button value="sin" onclick="Sin()">sin()</button>
            <button value="cos" onclick="Cos()">cos()</button>
            <button value="tan" onclick="Tan()">tan()</button>
            <button value="√" onclick="Sqrt()">√</button>
        </div>
        <div class="row">
            <button value="*" onclick="appendToDisplay('*')">*</button>
            <button value="^" onclick="appendToDisplay('**')">^</button>
            <button value="log" onclick="Log()">log()</button>
            <button value="←" onclick="moveCursor()">&#8592;</button> <!-- New button to move cursor left -->
        </div>
    </div>

    <script>
        // JavaScript code
        function appendToDisplay(value) {
            // Append the user's input value to the display
            const display = document.getElementById('display');
            const startPos = display.selectionStart;
            const endPos = display.selectionEnd;
            const currentValue = display.value;
            const newValue = currentValue.substring(0, startPos) + value + currentValue.substring(endPos);
            display.value = newValue;
            display.setSelectionRange(startPos + value.length, startPos + value.length);
            display.focus();
        }

        function clearAll() {
            // Clear the display
            document.getElementById('display').value = '';
        }

        function getResult() {
            try {
                // Calculate the user's input expression and display the result
                const expression = document.getElementById('display').value;
                const result = eval(expression);
                document.getElementById('display').value = result;
            } catch (error) {
                // Display an error message if an error occurs during calculation
                document.getElementById('display').value = 'Error';
            }
        }

        function Sin() {
            // Calculate sine value
            const angle = parseFloat(document.getElementById('display').value);
            const radians = (angle * Math.PI) / 180;
            const sinValue = Math.sin(radians);
            document.getElementById('display').value = sinValue.toFixed(8); // Round to 8 decimal places
        }

        function Cos() {
            // Calculate cosine value
            const angle = parseFloat(document.getElementById('display').value);
            const radians = (angle * Math.PI) / 180;
            const cosValue = Math.cos(radians);
            document.getElementById('display').value = cosValue.toFixed(8); // Round to 8 decimal places
        }

        function Tan() {
            // Calculate tangent value
            const angle = parseFloat(document.getElementById('display').value);
            const radians = (angle * Math.PI) / 180;
            const tanValue = Math.tan(radians);
            document.getElementById('display').value = tanValue.toFixed(8); // Round to 8 decimal places
        }

        function Sqrt() {
            // Calculate square root
            const value = parseFloat(document.getElementById('display').value);
            const sqrtValue = Math.sqrt(value);
            document.getElementById('display').value = sqrtValue.toFixed(8); // Round to 8 decimal places
        }

        function Log() {
            // Calculate base 10 logarithm
            const value = parseFloat(document.getElementById('display').value);
            const logValue = Math.log10(value);
            document.getElementById('display').value = logValue.toFixed(8); // Round to 8 decimal places
        }

        function moveCursor() {
            // Move the cursor one position to the left
            const display = document.getElementById('display');
            const currentPosition = display.selectionStart;
            if (currentPosition > 0) {
                display.setSelectionRange(currentPosition - 1, currentPosition - 1);
                display.focus();
            }
        }
    </script>
</body>

</html>
```

# VII. Dynamic presentation of output results

[video(video-xxdYmuLY-1696409281565)(type-csdn)(url-https://live.csdn.net/v/embed/332441)(image-https://video-community.csdnimg.cn/vod-84deb4/6e651530625371ee9fba6732b78e0102/snapshots/797c962a32914afd8b1100f5f7160bdd-00005.jpg?auth_key=4849982103-0-0-cbf9827fca3e5f6576f7293c3077fda4)(title-Result Display)]





---

# VIII. Summary
Through this project, I successfully created a web-based calculator with basic mathematical operations and cursor control functionality. This endeavor familiarized me with fundamental **HTML, CSS, and JS** concepts and honed my problem-solving skills. It also taught me how to apply the Personal Software Process (**PSP**) for planning and tracking work time in practical projects.

This calculator project provided valuable experience, not only strengthening my front-end development skills but also enhancing my user interface design capabilities. I look forward to applying this knowledge in future projects.At the same time, this calculator still has many shortcomings such as not meeting the standards of scientific calculators, and will participate in more in-depth research in the future.
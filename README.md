# BIC21203 Lab 4a - Client-Side Scripting (JavaScript)

**Name:** Amirul Adnin
**Student ID:** CI250111

## About
This lab contains three small web pages built with plain HTML5, CSS and JavaScript (no libraries). Each page practises a core client-side scripting skill: selecting elements, handling events, validating input and generating content dynamically.

| Folder | Task | Key concepts |
| --- | --- | --- |
| `q1/` | Interactive Text Changer | DOM selection, function, `addEventListener` |
| `q2/` | Smart Number Validator | input validation, `if...else if...else` |
| `q3/` | Dynamic Number Generator | `for` loop, `createElement`, `textContent` |

## Q1: Interactive Text Changer

### What it does
The page shows the paragraph "Welcome to my website!" and a **Change Message** button. When the button is clicked, the paragraph text changes to "Hello there!".

### How it works
1. `document.getElementById("message")` selects the paragraph, and `document.getElementById("changeBtn")` selects the button.
2. The function `changeMessage()` sets `message.textContent = "Hello there!"`.
3. `changeBtn.addEventListener("click", changeMessage)` runs the function when the button is clicked.

### Design choices
- I used `textContent` instead of `innerHTML` because the text is plain text, and this avoids inserting unwanted HTML.
- I passed `changeMessage` to `addEventListener` without brackets, because adding `()` would run the function immediately when the page loads.
- The script is loaded with `defer`, so it runs only after the HTML elements exist.

### Test
| Action | Expected result |
| --- | --- |
| Open the page | Shows "Welcome to my website!" |
| Click **Change Message** | Shows "Hello there!" |

## Q2: Smart Number Validator

### What it does
The user types a value into a text box and clicks **Check**. The page decides whether the input is a valid number and, if it is, compares it with 10.

### How it works
1. `userInput.value.trim()` reads the input and removes leading and trailing spaces.
2. If the trimmed text is empty (`""`), the page shows "Please enter a valid number!" and stops using `return`.
3. `Number(text)` converts the text to a number. `Number.isFinite()` then rejects `NaN` (for example "abc") and `Infinity`.
4. An `if...else if...else` chain compares the number with 10:
   - below 10: "The number is lower than 10"
   - above 10: "The number is higher than 10"
   - exactly 10: "The number is equal to 10"
5. The result is written to the `#result` paragraph with `textContent`.
6. `checkBtn.addEventListener("click", checkInput)` runs the validation on click.

### Design choices
- `trim()` runs before `Number()` because `Number("")` and `Number("   ")` both return `0`, which would wrongly be treated as valid.
- Decimals such as 10.5 are accepted, because `Number()` handles decimal values.
- The result paragraph uses `role="status"` and `aria-live="polite"` so screen readers announce the message.

### Test cases
| Input | Expected result |
| --- | --- |
| `5` | The number is lower than 10 |
| `10` | The number is equal to 10 |
| `15` | The number is higher than 10 |
| `10.5` | The number is higher than 10 |
| `abc` | Please enter a valid number! |
| (empty) | Please enter a valid number! |
| (spaces only) | Please enter a valid number! |

## Q3: Dynamic Number Generator

### What it does
The page has a **Generate** button and an empty ordered list. Clicking the button fills the list with five items: "The number is 1" to "The number is 5".

### How it works
1. `numberList.textContent = ""` clears the list first.
2. A `for` loop runs from `i = 1` to `i <= 5`.
3. In each loop, `document.createElement("li")` creates a list item, `textContent` sets its text, and `appendChild` adds it to the `<ol>`.
4. `generateBtn.addEventListener("click", generateNumbers)` runs the function on click.

### Design choices
- Clearing the list before the loop prevents duplicates, so clicking the button many times always shows exactly five items.
- Creating elements with `createElement` and `textContent` builds the list safely, without writing HTML strings.
- The `<ol>` element numbers the items automatically.

### Test
| Action | Expected result |
| --- | --- |
| Open the page | The list is empty |
| Click **Generate** once | Five items, from "The number is 1" to "The number is 5" |
| Click **Generate** several times | Still exactly five items, with no duplicates |

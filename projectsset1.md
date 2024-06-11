# Project related to DOM

## Poject Link
[Click here](https://stackblitz.com/edit/dom-project-chaiaurcode-ekqzjk?file=index.html)

# Solution Code

## Project 1 (Background Color Changer)

```javascript

const buttons = document.querySelectorAll('.button')
console.log(buttons);

const body = document.querySelector('body')

buttons.forEach( function (button) {
  console.log(button)
  button.addEventListener( 'click', function (e) {
    console.log(e);
    console.log(e.target);
    
    if(e.target.id === 'grey') {
    //body.style.backgroundColor = "grey"
            //OR
    body.style.backgroundColor = e.target.id // best practice.
  }

  if(e.target.id === 'white') {
    body.style.backgroundColor = e.target.id
  }
  if(e.target.id === 'blue') {
    body.style.backgroundColor = e.target.id
  }
  if(e.target.id === 'yellow') {
    body.style.backgroundColor = e.target.id
  }
  })
});

```

## Project 1 Optimize Solution (Background Color Changer)

```javascript

const buttons = document.querySelectorAll('.button')
console.log(buttons)

const body = document.querySelector('body')

buttons.forEach( (button) => {
  console.log(button)
  button.addEventListener('click', (e) => {
    console.log(e)
    console.log(e.target)

    const color = e.target.id

    if( ["grey", 'white', 'blue', 'yellow'].includes(color) ){
      body.style.backgroundColor = color
    }
  })
})

```

## Projcet 2 solution (BMI Calculator)

```javascript

const form = document.querySelector('form')

// this usecase will give you empty value
// const height = parseInt(document.querySelector('#height').value)

form.addEventListener('submit', function(e){
  e.preventDefault()

  const height = parseInt(document.querySelector('#height').value);
  const weight = parseInt(document.querySelector('#weight').value);
  const results = document.querySelector('#results');

  // Check if height is not a number or is less than or equal to 0
  if (height === '' || height < 0 || isNaN(height)) {
    results.innerHTML = `Please give a valid height ${height}`;
    
  } else if (weight === '' || weight < 0 || isNaN(weight)) {
    results.innerHTML = `Please give a valid weight ${weight}`;
  } else {
    const bmi = ( weight / ((height * height) / 10000)).toFixed(2);

    // show the result
    results.innerHTML = `<span>${bmi}</span>`;
    if(bmi <= 18.6){
      results.innerHTML = `Under Weight ${bmi}`
    } else if (bmi >= 18.6 && bmi <= 24.9 ) {
      results.innerHTML = `Normal Range ${bmi}`
    } else if (bmi > 24.9){
      results.innerHTML = `Over Weight ${bmi}`
    }
  }
});

```

## Project 3 (Digital Clock)

```javascript
const clock = document.querySelector('#clock')

// `setInterval` is a function in JavaScript used to repeatedly execute a given function at a specified interval, in milliseconds. It continues to call the function until clearInterval is called or the page is unloaded.

setInterval(function () {
  let date = new Date()
  // console.log(date.toLocaleTimeString());
  clock.innerHTML = date.toLocaleTimeString()
}, 1000)
```

## Project 4 (Guessing the number)

```javascript
let randomNumber = parseInt(Math.random() * 100 + 1);

const submit = document.querySelector('#subt');
const userInput = document.querySelector('#guessField');
const guessSlot = document.querySelector('.guesses');
const remaining = document.querySelector('.lastResult');
const lowOrHi = document.querySelector('.lowOrHi');
const startOver = document.querySelector('.resultParas');

const p = document.createElement('p');
console.log(p);

let prevGuess = [];
let numGuess = 1;

let playGame = true;

if (playGame) {
  submit.addEventListener('click', function (e) {
    e.preventDefault()
    const guess = parseInt(userInput.value)
    console.log(guess);
    validateGuess(guess);
  });
}

function validateGuess(guess) {
  if(isNaN(guess)) {
    alert('please enter a valid number')
  } else if(guess < 1) {
    alert('please enter a number between 1 to 100')
  } else if(guess > 100) {
    alert('please enter a number between 1 to 100')
  } else{
    prevGuess.push(guess)
    if(numGuess === 10) {
      displayGuess(guess)
      displayMessage(`Game Over. Random number was ${randomNumber}`)
      endGame()
    } else {
      displayGuess(guess)
      checkGuess(guess)
    }
  }
}

function checkGuess(guess) {
  if(guess === randomNumber) {
    displayMessage(`You guessed it right`)
    endGame()
  } else if (guess < randomNumber) {
    displayMessage('Number is TOO low')
  }  else if (guess > randomNumber) {
    displayMessage('Number is TOO high')
  }
}

function displayGuess(guess) {
  userInput.value = ''
  guessSlot.innerHTML += `${guess}  `
  numGuess++;
  remaining.innerHTML = `${11 - numGuess}`
}

function displayMessage(message) {
  lowOrHi.innerHTML = `<h2>${message}</h2>`
}

function endGame() {
  userInput.value = '';
  userInput.setAttribute('disabled', '')
  p.classList.add('button')
  p.innerHTML = `<h2 id="newGame" style="cursor: pointer;">Start new Game</h2>`
  startOver.appendChild(p)
  playGame = false
  newGame()
}

// // `input.setAttribute`: This method is used to set an attribute on the `input` element.
// `'disabled'`: This is the name of the attribute being set. The disabled attribute is a standard attribute in HTML used to `disable` input elements.
// `''`: This is the value assigned to the `disabled` attribute. For boolean attributes like `disabled`, the value is often an empty string, but the presence of the attribute itself is what matters. Any non-empty value will have the same effect, but the convention is to use an empty string.
// }

// # Effect of `setAttribute('disabled', '')`
// - When the `disabled` attribute is set on an `<input>` element, the input field becomes disabled. This means:
// - The user cannot interact with the input field (i.e., they cannot type into it).
// - The input field typically appears grayed out in the browser.
// - The field's value will not be submitted with the form if the form is submitted while the field is disabled.

function newGame() {
  const newGameButton = document.querySelector('#newGame');
  newGameButton.addEventListener('click', function(e) {
    randomNumber = parseInt(Math.random() * 100 + 1);
    prevGuess = []
    numGuess = 1
    guessSlot.innerHTML = ''
    remaining.innerHTML = `${11 - numGuess}`
    userInput.removeAttribute('disabled')
    startOver.removeChild(p)

    playGame = true
  })
}
```

## Project 5 (keyboard check)

```javascript
const insert = document.getElementById('insert');

window.addEventListener('keydown', (e) => {
  insert.innerHTML = `
  <table>
  <tr>
    <th>Key</th>
    <th>Keycode</th>
    <th>Code</th>
  </tr>
  <tr>
    <td>${e.key === " " ? "Space": e.key}</td>
    <td>${e.keyCode}</td>
    <td>${e.code}</td>
  </tr>
</table>
  `
});
```

## Project 6 (unlimited colors)

```javascript
// generate a random color

// The hexadecimal ranges are 0-9 and A-F.

const randomColor = function () {
  const hex = '0123456789ABCDEF'
  let color = '#'
  for(let i = 0; i < 6; i++) {
   color += hex[ Math.floor(Math.random() * 16)]
  }
  return color
};
let intervalId;

const startChangingColor = function () {
  if(!intervalId){
    intervalId = setInterval(changeBGColor, 1000);
  }

  function changeBGColor(){
    document.body.style.backgroundColor = randomColor()
}
};

const stopChangingColor = function () {
  clearInterval(intervalId);
  intervalId = null;
};

document.querySelector('#start').addEventListener('click', startChangingColor);
document.querySelector('#stop').addEventListener('click', stopChangingColor);
```
## Explanation of project 6 Code:

[Click here](JavaScript_Code_Explanation.md)
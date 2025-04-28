## Project 4 Source Code.

## HTML
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guess The Number</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="wrapper">
        <h1>Number Guessing Game</h1>
        <p>Try and guess a number between 1 and 100</p>
        <p>You have 10 attemts to guess the right number.</p>
        <br>
        <form class="form">
            <label for="guessField" id="guess" >Guess a number</label>
            <input type="text" id="guessField" class="guessField" placeholder="Enter The Number" >
            <input type="submit" id="submit" value="Submit guess" class="guessSubmit" >
        </form>
        <div class="resultParas">
            <p>Previous guess: <span class="guesses"></span></p>
            <p>Remaining guesses: <span class="lastResult">10</span></p>
            <p class="lowerHigh"></p>
        </div>
    </div>
    
</body>
<script src="script.js"></script>
</html>
```

## CSS
```
#wrapper{
    padding: 40px;
    width: 60%;
    display:block;
    margin: auto;
    align-items: center;
    background-color:#212121;
    color: white;
}
::placeholder{
    color: rgb(41, 39, 39);
} 
```
## SCRIPT

```
// sabse phele random numbers genrate krwaenge

let randomNumber = (parseInt(Math.random() * 100 + 1));
const submit = document.querySelector('#submit')
const userInput = document.querySelector('#guessField')
const guessSlot = document.querySelector('.guesses')
const remaining = document.querySelector('.lastResult')
const LowHigh = document.querySelector('.lowerHigh')
const startOver = document.querySelector('.resultParas')

const p = document.createElement('p')

// previouse woh joh guess krr chuka hai woh ek array ke through dikhane ke liye
// ek array banayenge

let prevGuess = [];
// to see number of attempts
let numGuess = 1;

let playGame = true;

if (playGame) {
    submit.addEventListener('click', (event) => {
        event.preventDefault();// taki value post ya get pe nhy jaye ruk jaye..
        // value lenge user ne jha input diya wha se..
        const guess = parseInt(userInput.value);
        // ab ish value ko next function ko pass krr denge 
        // console.log(guess); // ishe pata chal jayega ki number ja rha hai ya nhy

        validateGuess(guess);
    })
}

// functions

function validateGuess(guess) {
    // cheak karenge ki ushne number diya woh shai bhi hai ya nhy kahi woh abc de de.. woh to galt hoga na..
    if (isNaN(guess)) {
        alert('Please Enter A Valid Number')
    } else if (guess < 1) {
        alert('Please Enter A Number More Then 1')
    } else if (guess > 100) {
        alert('Please Enter A Number Less Then 100')
    } else {
        // number right hai ab ishko array me push krr denge 
        prevGuess.push(guess)
        // ab cheak karenge kahi ushke attempts to finish nhy hue hai 
        if (numGuess === 11) {
            displayGuess();
            displayMessage(`Game Over. Random Number was ${randomNumber}`)
            endGame();
        } else {
            displayGuess(guess)
            // ab cheak karenge ush guess se woh jitaa ya hara..ya value higher hai ya lower hai..
            cheakGuess(guess)
        }
    }

}

function cheakGuess(guess) {
    // cheak the guess is higher/ lower / or euqal 
    if (guess === randomNumber) {
        displayMessage(`You Guessed it right`)
        endGame();
    } else if (guess < randomNumber) {
        displayMessage(`Number is too low`)
    }
    else if (guess > randomNumber) {
        displayMessage(`Number is too high`)
    }

}

function displayGuess(guess) {
    // user input ki value ko update karenge empty string se 
    // cleanUP
    userInput.value = "";
    guessSlot.innerHTML += `${guess}, `
    numGuess++;
    remaining.innerHTML = `${11 - numGuess}`


}

function displayMessage(message) {
    // user ki input value ko empty kr denge html me guess add krenge or number reduce kr denge attempts
    // lowerhigh me msg pass krenge
    LowHigh.innerHTML = `<h2>${message}</h2>`

}

function endGame() {
    userInput.value = '';
    // taki values show nhy ho
    userInput.setAttribute('disabled', '')
    // last wale peragramph ko id denge 
    p.classList('button')
    p.innerHTML = `</h2 id="newGame"></h2>`;
    startOver.appendChild('p')
    playGame = false;
    newGame();


}

function newGame() {
    const newGameButton = document.querySelector('#newGame')
    newGameButton.addEventListener('click', (event) => {
        randomNumber = (parseInt(Math.random() * 100 + 1)); // wps new random number generate honge
        prevGuess = []; // prev guess ko khali krr denge
        numGuess = 1;
        guessSlot.innerHTML = "";
        remaining.innerHTML = `${11 - numGuess}`
        userInput.removeAttribute('disabled')
        startOver.removeChild(p)
        playGame = true;
    })
}

```
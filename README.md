# week-9- 
// 01 - Basic input
//
// The simplest possible use of `readline`: read ONE line that the user types
// in the terminal, then print it back and exit.

// 1. Import the readline module that comes built-in with Node.js.
const readline = require('node:readline');

// 2. Create an "interface" that connects to the terminal:
//      - input : where the keystrokes come from (process.stdin)
//      - output: where prompts/echo go (process.stdout)
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

// 3. Ask the user a question. The callback runs once they press Enter.
rl.question('What is your name? ', (name) => {
  console.log(`Hello, ${name}! Welcome to Node.js readline.`);

  // 4. Always close the interface when you are done, otherwise the
  //    program will keep waiting for input and never exit.
  rl.close();
});


 
// 02 - Question with validation
//
// Same idea as example 01, but we *do something* with the answer:
// we convert it to a number and validate it before continuing.

const readline = require('node:readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question('How old are you? ', (answer) => {
  // The answer is always a string. Convert it to a number.
  const age = Number(answer);

  if (Number.isNaN(age) || age < 0) {
    console.log(`"${answer}" is not a valid age.`);
  } else if (age < 18) {
    console.log(`You are ${age} — still a minor.`);
  } else {
    console.log(`You are ${age} — an adult.`);
  }

  rl.close();
});
 

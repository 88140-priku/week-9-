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
 

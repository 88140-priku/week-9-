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
 

// 03 - Multiple questions
//
// Ask a sequence of questions. Each question must wait for the previous
// one to finish, so we *nest* the callbacks (or use Promises -- see
// example 10 for that style).

const readline = require('node:readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question('What is your first name? ', (firstName) => {
  rl.question('What is your last name? ', (lastName) => {
    rl.question('What is your favorite programming language? ', (language) => {
      console.log('\n--- Profile ---');
      console.log(`Name    : ${firstName} ${lastName}`);
      console.log(`Favorite: ${language}`);
      console.log('----------------');

      rl.close();
    });
  });
});
 

// 04 - Read a file line by line
//
// `readline` is not just for keyboard input. It can read ANY stream one
// line at a time -- a file, the network, etc. This is the right way to
// process large text files because it does NOT load the whole file into
// memory.

const fs = require('node:fs');
const path = require('node:path');
const readline = require('node:readline');

// Resolve the file path relative to this script, not the current working
// directory, so it works no matter where you run `node` from.
const filePath = path.join(__dirname, 'sample.txt');

// Create a readable stream from the file.
const fileStream = fs.createReadStream(filePath, { encoding: 'utf8' });

const rl = readline.createInterface({
  input: fileStream,
  // `crlfDelay: Infinity` makes sure Windows-style "\r\n" line endings
  // are treated as a single newline.
  crlfDelay: Infinity,
});

let lineNumber = 1;

// The "line" event fires once for every line in the input stream.
rl.on('line', (line) => {
  console.log(`${lineNumber}: ${line}`);
  lineNumber += 1;
});

// The "close" event fires when the file has been fully read.
rl.on('close', () => {
  console.log(`\nDone. Read ${lineNumber - 1} lines.`);
});
 

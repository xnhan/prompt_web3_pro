### README
## ❯ Install

```
$ npm install --save prompt_web3_pro
```

> This package supports Node 14 and above

## ❯ Usage

```js
const prompt_web3_pro = require('prompt_web3_pro');

(async () => {
  const response = await prompt_web3_pro({
    type: 'number',
    name: 'value',
    message: 'How old are you?',
    validate: value => value < 18 ? `Nightclub is 18+ only` : true
  });

  console.log(response); // => { value: 24 }
})();
```

## ❯ Examples

### Single Prompt

Prompt with a single prompt object. Returns an object with the response.

```js
const prompt_web3_pro = require('prompt_web3_pro');

(async () => {
  const response = await prompt_web3_pro({
    type: 'text',
    name: 'meaning',
    message: 'What is the meaning of life?'
  });

  console.log(response.meaning);
})();
```

### Prompt Chain

Prompt with a list of prompt objects. Returns an object with the responses.
Make sure to give each prompt a unique `name` property to prevent overwriting values.

```js
const prompt_web3_pro = require('prompt_web3_pro');

const questions = [
  {
    type: 'text',
    name: 'username',
    message: 'What is your GitHub username?'
  },
  {
    type: 'number',
    name: 'age',
    message: 'How old are you?'
  },
  {
    type: 'text',
    name: 'about',
    message: 'Tell something about yourself',
    initial: 'Why should I?'
  }
];

(async () => {
  const response = await prompt_web3_pro(questions);

  // => response => { username, age, about }
})();
```

### Dynamic prompt_web3_pro

Prompt properties can be functions too.
Prompt Objects with `type` set to `falsy` values are skipped.

```js
const prompt_web3_pro = require('prompt_web3_pro');

const questions = [
  {
    type: 'text',
    name: 'dish',
    message: 'Do you like pizza?'
  },
  {
    type: prev => prev == 'pizza' ? 'text' : null,
    name: 'topping',
    message: 'Name a topping'
  }
];

(async () => {
  const response = await prompt_web3_pro(questions);
})();
```

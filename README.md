# Node.js (Cheat Sheet)

## REPL

> A read--eval--print loop (REPL) or language shell, is a simple interactive programming environment
> that takes single user inputs, executes them, and returns the result to the user; a program
> written in a REPL environment is executed piecewise.

Source:
[wikipedia > Read–eval–print loop](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)

Simply open your terminal and type `node` to start the REPL.

```sh
$ node

Welcome to Node.js v18.14.2.
Type ".help" for more information.
>
```

### Import modules

Source: ChatGPT

Node.js supports dynamic imports using the `import()` function, which returns a promise. This method
is suitable for the REPL as it can handle asynchronous module loading. You can use it like so:

```sh
> const { BigNumber } = await import('bignumber.js');
```

This line tells Node.js to asynchronously load `bignumber.js` and extract `BigNumber` from the
exported values. The `await` keyword is used because `import()` returns a promise, and we need to
wait for the promise to resolve before continuing.

You can alsop import specific functions from a module using dynamic imports. Here's how to import
`readFileSync`:

```sh
> const { readFileSync } = await import('fs');
```

This line of code uses the ES module dynamic import syntax to load the `fs` module and destructures
`readFileSync` from it. This approach is compatible with the Node.js REPL and provides an
asynchronous way to load modules.

For example:

```sh
$ node
Welcome to Node.js v18.14.2.
Type ".help" for more information.
> const transactions = [
...   {
...     contract: 'GoldToken',
...     function: 'transfer',
...     args: ['0xC870dc32e84531DA06C0156f0dfa73CfA091C4bd', '42'],
...     value: '0',
...   },
... ]
> const transactionsToBeSaved = JSON.stringify(transactions)
undefined
> fs.writeFileSync('transactions.json', transactionsToBeSaved, { flag: 'w' })
undefined
> const { readFileSync } = await import('fs');
undefined
> const jsonString = readFileSync('transactions.json').toString()
undefined
> jsonString
'[{"contract":"GoldToken","function":"transfer","args":["0xC870dc32e84531DA06C0156f0dfa73CfA091C4bd","42"],"value":"0"}]'
> const path = await import('path');
undefined
> const currentDir = process.cwd();
undefined
> const filePath = path.join(currentDir, 'transactions.json');
undefined
> filePath
'/Users/arthur/Documents/celo-org/developer-tooling/transactions.json'
```
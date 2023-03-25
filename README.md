# vue-zip-code-app

This template should help get you started developing with Vue 3 in Vite.

This Vue.js app allows users to search for a US ZIP code and displays its corresponding address.


See [Demo](https://gabrielmaksimovich.github.io/vue-zip-code-app/).

## Technologies Used

Vue.js - A progressive framework for building user interfaces.

Vite - A build tool that aims to provide a faster and leaner development experience.

Axios - A promise-based HTTP client for the browser and node.js.

## Project Setup

To set up this project on your local machine, run the following command:

```sh
npm install
```

### How to Use

0. Start proxy using 'node proxy.js' command.
1. Enter a valid US ZIP code into the input field.
2. Click the "Search" button.
3. If the ZIP code is valid, the corresponding address will be displayed below the input field.
4. If the ZIP code is invalid, an error message will be displayed below the input field.

```sh
npm run dev
```

### Demo

Check out the live demo on [GitHub Pages](https://gabrielmaksimovich.github.io/vue-zip-code-app/).

### Compiles and minifies for production

```sh
npm run build
```

This will compile and minify the app for production.
For more information about the configuration, see the [Vite Configuration Reference](https://vitejs.dev/config/)

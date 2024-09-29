# Simple-app

This project demonstrates a basic React setup without using `npx`. It focuses on the use of Webpack for bundling JavaScript modules, including React components, and serves the app locally on port 5000 using Webpack's development server.

## Features

- **Custom React Setup**: No reliance on `create-react-app`. Manual setup using Webpack and Babel.
- **Webpack Bundling**: Configured to handle React JSX, ES6, and CSS.
- **Development Server**: Uses Webpack Dev Server for hot-reloading, running on port 5000.
- **Custom Host Configuration**: Requires setting the `host` key in the `devServer` object in `webpack.config.js` to `yourhost.domain.com`.

## Project Setup Steps

### 1. Initialize Project:
Create the necessary directories and files for the project.

```bash
mkdir app
cd app
mkdir public src
```

### 2. Install Dependencies:
Use npm to install the required modules:

```bash
npm init -y
npm install --save-dev @babel/core babel-loader @babel/cli @babel/preset-env @babel/preset-react
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save-dev html-webpack-plugin
npm install react react-dom
```

### 3. Create the HTML File:
Inside the `public` directory, create `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
```

### 4. Configure Babel:
Create a `.babelrc` file in the root directory with the following content:

```json
{
  "presets": ["@babel/preset-env","@babel/preset-react"]
}
```

### 5. Webpack Configuration:
Create `webpack.config.js` in the root directory:

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
  entry: './index.js',
  mode: 'development',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'index_bundle.js',
  },
  target: 'web',
  devServer: {
    port: '5000',
    host: 'yourhost.domain.com',
    static: {
      directory: path.join(__dirname, 'public')
},
    open: true,
    hot: true,
    liveReload: true,
  },
  resolve: {
    extensions: ['.js', '.jsx', '.json'],
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/, 
        exclude: /node_modules/, 
        use: 'babel-loader', 
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'public', 'index.html')
    })
  ]
};
```

### 6. Create React Components:
In the `src` directory, create `App.js`:

```javascript
import React from "react";

const App = () =>{
    return (
        <h1>
            Hello world! I am using React
        </h1>
    )
}

export default App
```

And in the root directory create the entry point, `index.js`:

```javascript
import React from 'react'
import  { createRoot }  from 'react-dom/client';
import App from './src/App.js'

const container = document.getElementById('root');
const root = createRoot(container);
root.render(<App/>);
```

### 7. Use these Webpack Scripts Settings:
Ensure that `package.json` has:

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack-dev-server .",
    "build": "webpack ."
  }
```

### 8. Run the Development Server:
Run the application:

```bash
npm start
```

## Importance of Webpack

Webpack is a crucial tool in this project because it bundles your JavaScript files for browser compatibility and allows you to develop and test your React application with features like:

- **Module Bundling**: Bundles all the modules (React, CSS, etc.) into a single file for efficient browser loading.
- **Hot Reloading**: Automatically refreshes your app when code changes.
- **Dev Server**: Easily sets up a local development environment with Webpack Dev Server.

The use of Webpack's `devServer` allows for live reloading on port 5000, and the `host` key in the configuration ensures the server runs on your specified domain, enhancing flexibility in deployment scenarios.

## License

This project is licensed under the MIT License.

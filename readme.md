# Webpack Guide

I'm trying to make an easy guide to create a webpack application
because I know I am going to forget. So...

[webpack for wordpress][wordpress]

[wordpress]:#webpack-for-wordpress
[home]:#webpack-guide

### webpack for wordpress

<details>
<summary>
View Content
</summary>

```js 
var path = require('path');
const extractPlugin = require('extract-text-webpack-plugin');
const ex = new extractPlugin('../style.css');
const themePath = "wp-content/themes/test/js";
const autoPrefix = {
    loader: 'postcss-loader',
    options: {
        plugins: (loader) => [require('autoprefixer')()]
    }
};

/*   SASS*/
const config = {
    entry:{
        main: path.resolve(`${themePath}/scss.js`)
    } 
   ,
    output: {
        path: path.resolve(themePath),
        filename: 'bundle.js'
    },

   
    module: {
        rules: [
            {
                test: /\.scss$/i,
                use: ex.extract(['css-loader', autoPrefix, 'sass-loader'])

            }
        ]
    },

    watch: true,
    mode: "development",
    plugins: [
        ex
    ]
}


module.exports = config;

```
</details>

[go back :house:][home]

## SCSS

**references**

- [Webpack 4 compatibility](https://github.com/webpack-contrib/extract-text-webpack-plugin/issues/701)

- If you have not initialized npm then first do it

```
npm init
```

- after creating the package the json install these packages

```
npm i css-loader sass-loader node-sass postcss-loader autoprefixer extract-text-webpack-plugin@next --save-dev
```

- make sure you make webpack global, so that you can run the program by typing it

```
npm i webpack webpack-cli -D
```

- create webpack config file

```
touch webpack.config.js
```

- in the config file paste this information

```js

var path = require('path');
const extractPlugin = require('extract-text-webpack-plugin');
const ex = new extractPlugin('./style.css');
const autoPrefix = { loader:'postcss-loader',options:{plugins:(loader)=>[require('autoprefixer')()]}};

/*   SASS  */
const config = {
    entry:'./js/sass.js',
    output:{
        path: path.resolve('css'),
        filename:'bundle.js'
    },
    module:{
        rules:[
            {
                test:/\.scss$/i,
                use:ex.extract(['css-loader',autoPrefix,'sass-loader'])

            },
        ]
    },
    watch:true,
    plugins:[
        ex
    ]
}

module.exports = config;

```

**Just to recap**
1. The entry property is where the imported files will be bundled together
2. the watch property will continue to run and bundled the files when a file has been changed
3. the extract-text-webpack-plugin allows your css to ouput into a regular css file

- now create a js folder and a js file

```
mkdir js ; cd js; touch sass.js
```

- also create a sass folder to hold your sass files

```
cd ../; mkdir sass
```
- create a sass file and add some random sass code

```
touch style.scss
```

```
$r : red;

p{
    color:$r;
}

```

- once done with sass code import the location of the sass file into sass.js

```js
import "../sass/style.scss"
```

- finally, start webpack and your files should be bundled

```
webpack
```

[go back home][home]

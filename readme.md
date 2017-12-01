# Webpack Guide

I'm trying to make an easy guide to create a webpack application
because I know I am going to forget. So...

- [setup typescript][setup]
- [install jquery into typescript][jquery]

[jquery]:#install-jquery-into-typescript
[setup]:#typescript
[home]:#webpack-guide

## Typescript

- If you have not initialized npm then first do it

```
npm init
```

- after creating the package the json install these packages

```
npm i ts-loader typescript --save-dev
```

- make sure you make webpack global, so that you can run the program by typing it

```
npm i webpack -g
```

- create webpack config file

```
touch webpack.config.js
```

- in the config file paste this information

```js

var path = require('path');

/*   TYPESCRIPT  */
const config = {
    devtool: 'inline-source-map',
    entry:'./js/type.js',
    output:{
        path: path.resolve('js'),
        filename:'bundle.js'
    },
    resolve:{
        extensions:['.ts', '.tsx', '.js']
    },
    module:{
        rules:[
            {
                test:/\.tsx?$/,
                loader:'ts-loader'

            },
        ]
    },
    watch:true,

}

module.exports = config;
```
- create ts config file and add this

```
//create the json file

touch tsconfig.json
```

```
// add this in json file
{
  "compilerOptions": {
    "sourceMap": true
  }
}
```

- now create a js folder and a js file

```
mkdir js ; cd js; touch type.js
```

- create a typescript folder to hold your typescript files

```
cd ../; mkdir typescript
```
- create a typescript file and add some random sass code

```
// create typescript file

touch app.ts
```

```
// add typescript code

enum Talk {
    yes = 1,
    no = 0,
    maybe = 2,
}

function action( message:Talk):void{
    switch(message){
        case 0:
        console.log("you said no");
        break;
        case 1:
        console.log("you said yes");
        break;
        case 2:
        console.log("you said maybe");
        break;
    }
}

```

- once done with typescript code import the location of the typescript file into type.js

```js
import "../typescript/app.ts"
```

- finally, start webpack and your files should be bundled

```
webpack
```

[go back home][home]

## Install jquery into typescript

**reference**
- [How to use jQuery with TypeScript](https://stackoverflow.com/questions/32050645/how-to-use-jquery-with-typescript)

- install jquery

```
npm i --save-dev @types/jquery
```

- add this property into` tsconfig.json`

```
"allowSyntheticDefaultImports": true
```

- add some jquery code into your ts file and you should be all set. If not, then
add this package just in case

```
// 1. Install typings
npm install typings -g
// 2. Download jquery.d.ts (run this command in the root dir of your project)
typings install dt~jquery --global --save
```

[go back home][home]

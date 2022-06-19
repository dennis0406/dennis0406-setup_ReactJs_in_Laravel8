# Setup ReactJs in Laravel 8

   ## Create new react app in the ``` resources ``` directoty
   ``` 
   npx create-react-app react-app
   ```
   ![image](https://user-images.githubusercontent.com/107058157/174471088-8d49e273-2cd4-49f0-8107-529d7a65e5cf.png)
   
   > Remove the ``` node_modules ``` folder into react-app
   ## Config the package.json in laravel app
   - Copy the ``` dependencies ``` in packages.json file in the ``` react-app ``` directory 
   - Then paste it into the ``` package.json ``` in the ``` laravel ``` directory (into ``` devDependencies ```
   - Run the following code in the ``` recources ``` directory 
     ```
     npm install
     ```
   ## Config webpack.mix.js
   - Paste the follwing code into webpack.mix.js
   ```javascript
   const mix = require('laravel-mix');
const { chunk } = require('lodash');

/*
 |--------------------------------------------------------------------------
 | Mix Asset Management
 |--------------------------------------------------------------------------
 |
 | Mix provides a clean, fluent API for defining some Webpack build steps
 | for your Laravel applications. By default, we are compiling the CSS
 | file for the application as well as bundling up all the JS files.
 |
 */

 mix.options({
    postCss:[
        require('autoprefixer'),
    ],
 })

mix.setPublicPath('public');
mix.webpackConfig({
    resolve:{
        extensions:['.js', '.vue'],
        alias:{
            '@' :__dirname + 'resources'
        }
    },
    output: {
        chunkFilename: 'js/chunks/[name].js',
    }
}).react();

//used to run app using reactjs
mix.js('resources/react-app/src/index.js', 'public/js/app.js').version();
mix.copy('resources/react-app/public', 'public');

```
- After copied, run:
```
npm run dev
```
## Change the welcome.blade.php
- Go to welcome.blade.php
- Remove and replace the codes into body tag with the ``` div ``` tag with id named ``` root ```
- Under the body tag write this javascript code
```javascript
<script type="text/javascript" src="{{ mix('js/app.js') }}"></script>
```
> Now you can run ``` php artisan serve ``` to start that app

### Note: 
> Each time you change any thing in App.js you need to run the ``` npm run dev ``` again
   

# Webpack Fundamentals Course

**This course is out of date.**

Webpack is now version 2, this course was built on version 1. Although most of the content of the course is still applicable, several small items have changed and will break through the course if you follow along. Notes to fix some of the issues follow here in this readme.

## Recent Updates

Babel has undergone a major revision since the course was recorded. Because of this, you'll have to make a couple simple changes for babel to work properly. This only matters if you are using the latest versions of babel, and not the ones shown in the course. If using the versions shown in the course, you can ignore this.

In the "Using Loaders" clip, Babel is introduced. You'll need to make the changes here:

1) when installing babel-core & babel-loader with npm, you will also need to install babel-preset-es2015. Either add it to your npm install command or the following command will do this:

`
npm install babel-preset-es2015 --save-dev
`

2) Create a .babelrc file and give it the following contents:

`
{
  "presets": ["es2015"]
}
`

You can download the .babelrc file from this repository to use if you want. Also, a fully working package.json file has been included in the repository if you want to download and use it.

Also, there are 2 differences in technical implementation in Webpack 2. 


1) webpack.config.js module "loaders" is now "rules" in Webpack 2 and "pre" and "post" loaders go in the "rules" section using "enforce" as "pre" or "post"



2) the v1 version of extract-text-webpack-plugin is not compatible with WebPack 2 and the syntax is different for using it. As of today, the v2 of the plugin is in beta but I successfully installed it and used it to process SASS/CSS in a separate bundle.

Finally, when adding jshint-loader in the Using Preloaders clip, you'll need to add an empty set of curly braces to .jshintrc:  
`
{}
`
  
This will prevent the jshint-loader module from erroring out.

### preLoader property no longer exists

The property preLoader no longer exists for the webpack configuration file. You will receive this error:
```
configuration.module has an unknown property 'preLoaders'.
```
A solution to this problem here:
http://stackoverflow.com/questions/39668579/webpack-2-1-0-beta-25-error-unknown-property-postloaders

So the code:
```javascript
module.exports = {
    entry: ["./utils", "./app.js"],
    output: {
        filename: "bundle.js"
    },
    watch: true,

    module: {
        preLoaders: [
            {
                test: /\.js$/, // include .js files
                exclude: /node_modules/, // exclude any and all files in the node_modules folder
                loader: "jshint-loader"
            }
        ],
        loaders: [
            {
                test: /\.es6$/,
                exclude: /node_modules/,
                loader: "babel-loader"
            }
        ]
    },
    resolve: {
        extensions: ['.js','.es6']
    }
}
```
Should now look like this:
```javascript
module.exports = {
    entry: ["./utils", "./app.js"],
    output: {
        filename: "bundle.js"
    },
    watch: true,

    module: {
        loaders: [
            {
                test: /\.es6$/,
                exclude: /node_modules/,
                loader: "babel-loader"
            },
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: "jshint-loader",
                enforce: 'pre'
            }
        ]
    },
    resolve: {
        extensions: ['.js','.es6']
    }
}
```
(thank you to James Daniel)




# Webpack Fundamentals Course
This course is out of date.

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
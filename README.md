# Boilerplate React Component
Project that's designed to be cloned when developing a new React component that can be used across projects.

This is currently designed for components that are built and transpiled as part of an applications webpack build.

## Demo
You can import your component into the storybook, a good place to showcase your component.

Run the storybook with `npm run storybook` and navigate to `http://localhost:6006` in your browser.

### Github Pages
Before commiting your changes to Github you can run `npm run build-storybook` to build the storybook so that it can be hosted on Github pages.

## Usage
Import the component/s into your project:

```javascript
import Button from 'MODULE_NAME';
```

Import the styles into your project also (in an existing SASS file):

```
@import "~MODULE_NAME/src/styles";
```

### Include JavaScript in Webpack build
Add the following code to `webpack.config.js` to resolve an absolute path to where your component is located:

```javascript
const componentModulePath = fs.realpathSync(
  path.resolve(__dirname, 'node_modules', 'MODULE_NAME', 'src')
);
```

Then in the rule that transpiles code, include the path to your component:

```javascript
{
  test: /\.jsx?$/,
  use: ['babel-loader'],
  include: [
    path.resolve(__dirname, 'src'),
    componentModulePath
  ]
}
```

### Include SASS in Webpack build
Add another path to include in the rule for SCSS files:

```javascript
{
  test: /\.scss$/,
  use: [{
    loader: 'style-loader'
  }, {
    loader: 'css-loader'
  }, {
    loader: 'sass-loader',
    options: {
      includePaths: [
        path.resolve(__dirname, 'src'),
        componentModulePath
      ]
    }
  }]
}
```


react-test-template
===================

This repository is an example of how to test React + Redux application.

## Tools used
- [Jest](http://facebook.github.io/jest) - Test runner
- [Enzyme](https://github.com/airbnb/enzyme) - JavaScript Testing utilities for React
- [Sinon](http://sinonjs.org/) - Standalone test spies, stubs and mocks for JavaScript.
- [Nock](https://github.com/node-nock/nock) - HTTP mocking and expectations library
- [redux-mock-store](https://github.com/arnaudbenard/redux-mock-store) - A mock store for testing your redux async action creators and middleware.
- [enzyme-to-json](https://github.com/adriantoine/enzyme-to-json) - Convert Enzyme wrappers to a format compatible with Jest snapshot testing.

## Note
- [Shallow rendering](https://facebook.github.io/react/docs/test-utils.html#shallow-rendering) is used achived testing component in isolation. It ensures that we do not assert child components behaviors. Enzyme providers [API](https://github.com/airbnb/enzyme/blob/master/docs/api/shallow.md) to make it easier to assert, manipulate, and traverse the output.


```javascript
// src/App.jsx
class App extends Component {
  render() {
    return (
      <div>
        <Foo />
        <YesNo />
      </div>
    )
  }
}

// Shallow rendering result
<div>
  <Foo />
  <YesNo />
</div>
```

- [Jest's Snapshot testing](http://facebook.github.io/jest/docs/snapshot-testing.html) is used to guarantee that the UI does not change unexpectedly. We config Jest to use `enzyme-to-json` as a serializer so we can run snapshot testing aginast shallow rendering results.
```json
// package.json
"jest": {
  "snapshotSerializers": {
    "enzyme-to-json/serializer"
  }
}
```

```javascript
// test/Foo.test.js
wrapper = shallow(<Foo />)
expect(wrapper).toMatchSnapshot();
```
- We use `react-redux`'s `connect()` to inject Redux state into a regular React component. Therefore, in order to test the component itself without Redux decoration, we need to export the undecorated component as well.

```javascript
// src/Foo.jsx

export class Foo extends Component {
...
}

export default connect(...)(Foo)
```


## Installation
```bash
git clone https://github.com/siwatpru/react-test-template.git && cd react-test-template
npm install

# Run test
npm test

# Run app
npm run build
cd build
python -m SimpleHTTPServer 8000
```

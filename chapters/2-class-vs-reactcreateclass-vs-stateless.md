## Class vs `React.createClass` vs stateless

  - Nếu bạn có state bên trong and/or refs, nên xài `class extends React.Component` over `React.createClass`. eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

    ```jsx
    // óc chó
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

    // người bình thường
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }
    ```

    And if you don't have state or refs, prefer normal functions (not arrow functions) over classes:

    ```jsx
    // óc chó
    class Listing extends React.Component {
      render() {
        return <div>{this.props.hello}</div>;
      }
    }

    // óc chó (dựa vào tên function để suy luận thì rất đau đầu)
    const Listing = ({ hello }) => (
      <div>{hello}</div>
    );

    // người bình thường
    function Listing({ hello }) {
      return <div>{hello}</div>;
    }
    ```

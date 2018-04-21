## So sánh class, `React.createClass`, stateless

  - Nếu Component có state hoặc refs, nên sử dụng `class extends React.Component` thay vì `React.createClass`. eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

    ```jsx
    // tệ
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

    // tốt
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }
    ```

    Và nếu trong Component không có state hoặc refs, nên sử dụng khai báo hàm (không phải arrow function) thay vì class:

    ```jsx
    // tệ
    class Listing extends React.Component {
      render() {
        return <div>{this.props.hello}</div>;
      }
    }

    // tệ (dựa vào tên hàm để suy luận thì rất đau đầu)
    const Listing = ({ hello }) => (
      <div>{hello}</div>
    );

    // tốt
    function Listing({ hello }) {
      return <div>{hello}</div>;
    }
    ```

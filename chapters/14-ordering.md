## Thứ tự

  - Các hàm trong `class extends React.Component` nên được viết theo thứ tự sau:

  1.  Các phương thức tĩnh `static` (không bắt buộc)
  1. `constructor`
  1. `getChildContext`
  1. `componentWillMount`
  1. `componentDidMount`
  1. `shouldComponentUpdate`
  1. `componentWillUpdate`
  1. `componentDidUpdate`
  1. `componentWillUnmount`
  1. *Hàm xử lí sự kiện như click hoặc submit* `onClickSubmit()` & `onChangeDescription()`
  1. *Các hàm lấy dữ liệu cho hàm `render`* chẳng hạn như `getSelectReason()` hay `getFooterContent()`
  1. *Các hàm render khác* như  `renderNavigation()` hay `renderProfilePicture()`
  1. `render`

  - Cách định nghĩa `propTypes`, `defaultProps`, `contextTypes`, ...

    ```jsx
    import React from 'react';
    import PropTypes from 'prop-types';

    const propTypes = {
      id: PropTypes.number.isRequired, // Nếu id không đúng kiểu number, màn hình console sẽ hiện ra cảnh báo
      url: PropTypes.string.isRequired, // Nếu url không đúng kiểu string, màn hình console sẽ hiện ra cảnh báo
      text: PropTypes.string, // Nếu text không đúng kiểu string, màn hình console sẽ hiện ra cảnh báo
    };

    const defaultProps = {
      text: 'Hello World',  // Gán giá trị mặc định cho text
    };

    class Link extends React.Component {
      static methodsAreOk() {
        return true;
      }

      render() {
        return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>;
      }
    }

    Link.propTypes = propTypes;
    Link.defaultProps = defaultProps;

    export default Link;
    ```

  - Các hàm trong `React.createClass` nên được viết theo thứ tự sau: ` eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

  1. `displayName`
  1. `propTypes`
  1. `contextTypes`
  1. `childContextTypes`
  1. `mixins`
  1. `statics`
  1. `defaultProps`
  1. `getDefaultProps`
  1. `getInitialState`
  1. `getChildContext`
  1. `componentWillMount`
  1. `componentDidMount`
  1. `componentWillReceiveProps`
  1. `shouldComponentUpdate`
  1. `componentWillUpdate`
  1. `componentDidUpdate`
  1. `componentWillUnmount`
  1. *Hàm xử lí sự kiện* như `onClickSubmit()` hay `onChangeDescription()`
  1. *Các hàm lấy dữ liệu cho phương thức `render`* như`getSelectReason()` hay `getFooterContent()`
  1. Các hàm render khác như `renderNavigation()` hay `renderProfilePicture()`
  1. `render`

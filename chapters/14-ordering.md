## Thứ tự

  - Thứ tự trong các hàm trong `class extends React.Component`:

  1.  Một vài phương thức tĩnh`static` (tùy chon)
  1. `constructor` (Hàm khởi tạo)
  1. `getChildContext`
  1. `componentWillMount`
  1. `componentDidMount`
  1. `componentWillReceiveProps`
  1. `shouldComponentUpdate`
  1. `componentWillUpdate`
  1. `componentDidUpdate`
  1. `componentWillUnmount`
  1. *Hàm xử lí sự kiện Click hay các sự kiện khác* như  `onClickSubmit()` hay `onChangeDescription()`
  1. *Các phương thức lấy dữ liệu cho phương thức `render`* chẳng hạn như `getSelectReason()` hay `getFooterContent()`
  1. Các phương thức render khác ( tùy chọn)  ví dụ như  `renderNavigation()` hay `renderProfilePicture()`
  1. `render`

  - Cách định nghĩa `propTypes`, `defaultProps`, `contextTypes`, etc...

    ```jsx
    import React from 'react';
    import PropTypes from 'prop-types';

    const propTypes = {
      id: PropTypes.number.isRequired,
      url: PropTypes.string.isRequired,
      text: PropTypes.string,
    };

    const defaultProps = {
      text: 'Hello World',
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

  - Thứ tự trong hàm `React.createClass`: eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

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
  1. *Hàm xử lí sự kiện Click hay các sự kiện khác* ví dụ như   `onClickSubmit()` hay `onChangeDescription()`
  1. *Các phương thức lấy dữ liệu cho phương thức `render`* như`getSelectReason()` hay `getFooterContent()`
  1. Các phương thức render khác ( tùy chọn)  chẳng hạn như `renderNavigation()` hay `renderProfilePicture()`
  1. `render`

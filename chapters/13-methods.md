
## Phương thức

  - Sử dụng arrow function để đóng gói các biến cục bộ.

    ```jsx
    function ItemList(props) {
      return (
        <ul>
          {props.items.map((item, index) => (
            <Item
              key={item.key}
              onClick={() => doSomethingWith(item.name, index)}
            />
          ))}
        </ul>
      );
    }
	```

  -  Nên trói (Bind) event handler cho phương thức render ở trong constuctor. eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

    > Tại sao? Lời gọi hàm bind trong render tạo ra một hàm mới toanh mỗi khi render.

    ```jsx
    // Tệ
    class extends React.Component {
      onClickDiv() {
        // Làm cái gì đó
      }

      render() {
        return <div onClick={this.onClickDiv.bind(this)} />;
      }
    }

    // Tốt
    class extends React.Component {
      constructor(props) {
        super(props);

        this.onClickDiv = this.onClickDiv.bind(this);
      }

      onClickDiv() {
        // Làm gì đó vui vẻ
      }

      render() {
        return <div onClick={this.onClickDiv} />;
      }
    }
    ```

  - Không dùng dấu _ đặt trước tên hàm cho các hàm nội tại của một React Component/
    > Lí do? Dấu gạch dước thi thoảng được dùng trong một số ngôn ngữ để biểu thị tính "riêng tư". Tuy nhiên, không giống các ngôn ngữ khác, trong JavaScript, mọi thứ đều là “public”. Cho dù bạn có cho dấu gạch dưới vào hay không nó vẫn là public, bất kể ý định của bạn. Hãy xem vấn đề  [#1024](https://github.com/airbnb/javascript/issues/1024), và [#490](https://github.com/airbnb/javascript/issues/490) để hiểu sâu hơn.

    ```jsx
    // Tệ
    React.createClass({
      _onClickSubmit() {
        // Quét nhà
      },

      // Nấu cơm
    });

    // Tốt
    class extends React.Component {
      onClickSubmit() {
        // Quét nhà
      }

      // Nấu cơm
    }
    ```

  - Hãy chắc là bạn đã trả về một giá trị trong phương thức `render`. eslint: [`react/require-render-return`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-render-return.md)

    ```jsx
    // Tệ
    render() {
      (<div />);
    }

    // Tốt
    render() {
      return (<div />);
    }
    ```


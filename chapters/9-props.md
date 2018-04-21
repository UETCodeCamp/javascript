## Props
 - Luôn luôn sử dụng camelCase khi đặt tên prop (camelCase : viết hoa chữa cái đầu của các từ , từ đầu tiên của cụm thì viết thường)
 
    ```jsx
    // tệ
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // tốt
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```
    
 - Bỏ giá trị của prop khi nó thực sự rõ ràng là `true`. eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

    ```jsx
    // tệ
    <Foo
      hidden={true}
    />

    // tốt
    <Foo
      hidden
    />

    // tốt
    <Foo hidden />
    ```
    
 - Luôn luôn sử dụng prop `alt` trong thẻ `<img>`. Nếu giá trị của thẻ là NULL , `alt` có thể là một chuỗi rỗng hoặc `<img>` phải có thuộc tính `role="presentation"`. eslint: [`jsx-a11y/alt-text`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/alt-text.md)

    ```jsx
    // tệ
    <img src="hello.jpg" />

    // tốt
    <img src="hello.jpg" alt="Me waving hello" />

    // tốt
    <img src="hello.jpg" alt="" />

    // tốt
    <img src="hello.jpg" role="presentation" />
    ```
    
 - Không dùng các từ  "image", "photo", hoặc "picture" trong `<img>` `alt` props. eslint: [`jsx-a11y/img-redundant-alt`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-redundant-alt.md)

    > Tại sao? Screenreaders đã tự hiểu `img` elements là image(ảnh), vì vậy không cần khai báo thông tin này trong alt

    ```jsx
    // tệ
    <img src="hello.jpg" alt="Picture of me waving hello" />

    // tốt
    <img src="hello.jpg" alt="Me waving hello" />
    ```
    
 - Chỉ sử dụng [ARIA roles](https://www.w3.org/TR/wai-aria/roles#role_definitions). eslint: [`jsx-a11y/aria-role`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/aria-role.md) hợp lệ, và không trừu tượng. [jsx-a11y/aria-role](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/aria-role.md)

    ```jsx
    // tệ - không phải ARIA roles
    <div role="datepicker" />

    //tệ- ARIA roles trừu tượng
    <div role="range" />

    // tốt
    <div role="button" />
    ```
      
 - Không dùng `accessKey` trong các elements. eslint: [`jsx-a11y/no-access-key`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/no-access-key.md)

  > Tại sao ? Sự mâu thuẫn giữa phím tắt và các lệnh bàn phím được những người dùng screenreaders sử dụng làm phức tạp hóa khả năng tiếp cận.

  ```jsx
  // tệ
  <div accessKey="h" />

  // tốt
  <div />
  ```
  
  - Tránh dùng chỉ số của mảng(index) cho thuộc tính `key`, nên sử dụng một unique ID(định danh duy nhất). ([why?](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318))

  ```jsx
  // tệ
  {todos.map((todo, index) =>
    <Todo
      {...todo}
      key={index}
    />
  )}

  // tốt
  {todos.map(todo => (
    <Todo
      {...todo}
      key={todo.id}
    />
  ))}
  ```
    
 - Luôn xác định rõ ràng các defaultProp(thuộc tính mặc định) cho tất cả non-required props(thuộc tính không bắt buộc).

  > Tại sao? propTypes được coi như tài liệu, và cung cấp defaultProps , nghĩa là người đọc mã nguồn của bạn không cần phải đoán quá nhiều. Ngoài ra, nó có thể bỏ qua một số kiểm tra kiểu(type checking).
  
  ```jsx
  // tệ
  function SFC({ foo, bar, children }) {
    return <div>{foo}{bar}{children}</div>;
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node,
  };

  // tốt
  function SFC({ foo, bar, children }) {
    return <div>{foo}{bar}{children}</div>;
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node,
  };
  SFC.defaultProps = {
    bar: '',
    children: null,
  };
  ```
  
  - Hạn chế lạm dụng toán tử spread cho việc truyền props
  >Tại sao? Vì bạn có khả năng truyền props không cần thiết xuống Components . Và với React v15.6.1 trờ lên, bạn cần [chuyển các thuộc tính hông hợp lệ của HTML sang DOM](https://reactjs.org/blog/2017/09/08/dom-attributes-in-react-16.html).

  Ngoại lệ:

  - HOCs có thể truyền thẳng props xuống và khai báo propTypes

  ```jsx
  function HOC(WrappedComponent) {
    return class Proxy extends React.Component {
      Proxy.propTypes = {
        text: PropTypes.string,
        isLoading: PropTypes.bool
      };

      render() {
        return <WrappedComponent {...this.props} />
      }
    }
  }
  ```

 - Sử dụng toán tử spread đối với prop được khai báo rõ ràng. Điều này có thể đặc biệt hữu ích khi test các React component với cấu trúc beforeEach của Mocha.

  ```jsx
  export default function Foo {
    const props = {
      text: '',
      isPublished: false
    }

    return (<div {...props} />);
  }
  ```

  Ghi chú:
  Lọc các prop không cần thiết khi có thể. Ngoài ra, sử dụng [prop-types-exact](https://www.npmjs.com/package/prop-types-exact) để giúp ngăn ngừa lỗi.

  ```jsx
  // tốt
  render() {
    const { irrelevantProp, ...relevantProps  } = this.props;
    return <WrappedComponent {...relevantProps} />
  }

  // tệ
  render() {
    const { irrelevantProp, ...relevantProps  } = this.props;
    return <WrappedComponent {...this.props} />
  }
  ```

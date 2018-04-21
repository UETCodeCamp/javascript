# Hướng dẫn mẫu Airbnb React/JSX

Bản hướng dẫn này dựa trên những chuẩn phổ biến của Javascript. Được dịch từ bản gốc [tại đây](https://github.com/airbnb/javascript/tree/master/react)

Những từ mang nặng tính kĩ thuật sẽ được giữ nguyên để tránh sự nhầm lẫn. Tuy nhiên có thể bạn sẽ thích một phiên bản thuần Việt hơn, cứ thoải mái đóng góp nhé ;) 

## Mục lục

  1. [Những luật cơ bản](#những-luật-cơ-bản)
  1. [So sánh Class vs `React.createClass` vs stateless](#so-sánh-class-vs-`React.createClass`-vs-stateless)
  1. [Mixins](#mixins)
  1. [Đặt tên](#đặt-tên)
  1. [Khai báo](#khai-báo)
  1. [Căn chỉnh mã nguồn](#căn-chỉnh-mã-nguồn)
  1. [Dấu nháy đơn và nháy kép](#dấu-nháy-đơn-và-nháy-kép)
  1. [Khoảng trắng](#khoảng-trắng)
  1. [Props](#props)
  1. [Refs](#refs)
  1. [Dấu ngoặc đơn](#dấu-ngoặc-đơn)
  1. [Thẻ](#thẻ)
  1. [Phương thức](#phương-thức)
  1. [Cách sắp xếp hàm](#cách-sắp-xếp-hàm)
  1. [Thuộc tính `isMounted`](#thuộc-tính-`isMounted`)

## Những luật cơ bản

  - Chỉ chứa một React Component trong 1 file.
  - Tuy nhiên, những component có khả năng sử dụng lại([Stateless Component, hoặc Pure Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions)) có thể viết chung một file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
  - Luôn luôn sử dụng cú pháp JSX.
  - Không sử dụng `React.createElement` chung với cú pháp JSX.

## So sánh class vs `React.createClass` vs stateless

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

## Mixins

  - [Chi tiết vì sao không nên sử dụng mixins](https://facebook.github.io/react/blog/2016/07/13/mixins-considered-harmful.html).

  > Mixins tạo ra các implicit dependencies(phụ thuộc ngầm), gây ra xung đột tên và tăng độ phức tạp. Có thể thay thế mixins bằng components, higher-order components, hoặc các utility modules(gói tiện ích).

## Đặt tên

  - **Phần mở rộng(extensions)**: Sử dụng phần mở rộng `.jsx` cho React Components.
  - **Tên file**: Sử dụng chuẩn PascalCase cho tên file. Ví dụ:  `ReservationCard.jsx`.
  - **Tên tham chiếu(Reference Naming)**: Sử dụng PascalCase cho React components và dùng camelCase cho các đối tượng(instances) của chúng. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

    ```jsx
    // tệ
    import reservationCard from './ReservationCard';

    // tốt
    import ReservationCard from './ReservationCard';

    // tệ
    const ReservationItem = <ReservationCard />;

    // tốt
    const reservationItem = <ReservationCard />;
    ```

  - **Đặt tên Component**: Sử dụng tên file trùng với tên component. Ví dụ: `ReservationCard.jsx` nên có tên tham chiếu là `ReservationCard`. Tuy nhiên, đối với các component gốc của một thư mục, hãy sử dụng `index.jsx` làm tên file và sử dụng tên thư mục làm tên component:

    ```jsx
    // tệ
    import Footer from './Footer/Footer';

    // tệ
    import Footer from './Footer/index';

    // tốt
    import Footer from './Footer';
    ```
  - **Đặt tên Higher-order Component**: Sử dụng sự kết hợp của Higher-order component và tên của component đuợc truyền như `displayName`(tên hiển thị) trên component đuợc tạo ra. Ví dụ component bậc cao `withFoo()`, khi truyền một component `Bar` sẽ tạo ra một component với `displayName` của `withFoo(Bar)`.

    > Tại sao? Vì `displayName` của component có thể đuợc sử dụng bởi những công cụ phát triển hoặc trong các thông báo lỗi, và có một giá trị mà thể hiện rõ mối quan hệ này sẽ giúp chúng hiểu rõ chuyện gì đang xảy ra.

    ```jsx
    // tệ
    export default function withFoo(WrappedComponent) {
      return function WithFoo(props) {
        return <WrappedComponent {...props} foo />;
      }
    }
    
    // tốt
    export default function withFoo(WrappedComponent) {
      function WithFoo(props) {
        return <WrappedComponent {...props} foo />;
      }
    
      const wrappedComponentName = WrappedComponent.displayName
        || WrappedComponent.name
        || 'Component';
    
      WithFoo.displayName = `withFoo(${wrappedComponentName})`;
      return WithFoo;
    }
    ```

  - **Đặt tên Props**: Tránh sử dụng tên props của DOM Component cho mục đích khác.

    > Tại sao? Mọi nguời mong đợi props như `style` và `className` có ý nghĩa riêng. Việc thay đổi mục đích sử dụng của API gốc làm cho mã khó đọc và khó bảo trì hơn, thậm chí có thể gây ra lỗi.

    ```jsx
    // tệ
    <MyComponent style="fancy" />

    // tệ
    <MyComponent className="fancy" />

    // tốt
    <MyComponent variant="fancy" />
    ```

## Khai báo

  - Không nên sử dụng `displayName` để đặt tên cho các Components. Thay vào đó, đặt tên cho các Components bằng references(tham chiếu).

    ```jsx
    // tệ
    export default React.createClass({
      displayName: 'ReservationCard',
      // một số thứ khác
    });

    // tốt
    export default class ReservationCard extends React.Component {
    }
    ```
    
## Căn chỉnh mã nguồn
  - Căn chỉnh cho cú pháp JSX. eslint: [react/jsx-closing-bracket-location](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [react/jsx-closing-tag-location](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)

    ```jsx
    // tệ
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // tốt
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // Nếu props phù hợp trong một dòng thì giữ nó trên cùng một dòng
    <Foo bar="bar" />

    // Component con được thụt lề bình thường
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>
    ```

## Dấu nháy đơn và nháy kép
  - Luôn luôn sử dụng dấu ngoặc kép (`"`) cho các thuộc tính JSX, nhưng dấu nháy đơn (`'`) cho tất cả các JS khác. Eslint: [jsx-quotes](https://eslint.org/docs/rules/jsx-quotes)

    > Tại sao? Vì các thuộc tính HTML thông thường thường sử dụng dấu ngoặc kép thay vì đơn, vì vậy thuộc tính JSX cũng như thế.

    ```jsx
    // tệ
    <Foo bar='bar' />
    
    // tốt
    <Foo bar="bar" />
    
    // tệ
    <Foo style={{ left: "20px" }} />
    
    // tốt
    <Foo style={{ left: '20px' }} />
    ```

## Khoảng trắng
  - Luôn luôn có duy nhất một kí tự space(khoảng trắng) trong thẻ tự đóng. eslint: [`no-multi-spaces`](https://eslint.org/docs/rules/no-multi-spaces), [`react/jsx-tag-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)

    ```jsx
    // tệ
    <Foo/>
    
    // rất tệ
    <Foo                 />
    
    // tệ
    <Foo
    />
    
    // tốt
    <Foo />
    ```
    
 - Không dùng khoảng trắng giữa giá trị bên trong ngoặc nhọn. eslint: [`react/jsx-curly-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)

    ```jsx
    // tệ
    <Foo bar={ baz } />

    // tốt 
    <Foo bar={baz} />
    ```

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
  >Tại sao? Vì bạn có khả năng truyền props không cần thiết xuống Components. Và với React v15.6.1 trờ lên, bạn cần [chuyển các thuộc tính không hợp lệ của HTML sang DOM](https://reactjs.org/blog/2017/09/08/dom-attributes-in-react-16.html).

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
  Nên lọc các props không cần thiết khi có thể. Ngoài ra, sử dụng [prop-types-exact](https://www.npmjs.com/package/prop-types-exact) để giúp ngăn ngừa lỗi.

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

## Refs

  - Luôn sử dụng hàm gọi lại(callback) cho khai báo ref. eslint: [`react/no-string-refs`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

    ```jsx
    // tệ
    <Foo
      ref="myRef"
    />

    // tốt
    <Foo
      ref={(ref) => { this.myRef = ref; }}
    />
    ```

## Dấu ngoặc đơn

  - Đóng gói các thẻ JSX trong ngoặc đơn khi chúng kéo dài nhiều dòng. 
  eslint: [`react/jsx-wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-wrap-multilines.md)

    ```jsx
    // tệ
    render() {
      return <MyComponent variant="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // Tốt
    render() {
      return (
        <MyComponent variant="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // Tốt, Khi chỉ có 1 dòng
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

## Thẻ

  - Luôn luôn tự đóng các thẻ(tags) không có con. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

    ```jsx
    // tệ
    <Foo variant="stuff"></Foo>

    // tốt
    <Foo variant="stuff" />
    ```

  - Nếu Component của bạn có thuộc tính nhiều dòng, hãy đóng thẻ đó trên 1 dòng mới. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

    ```jsx
    // tệ
    <Foo
      bar="bar"
      baz="baz" />

    // tốt
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

## Phương thức

  - Sử dụng arrow function để bao đóng các biến cục bộ.

    ```jsx
    function ItemList(props) {
      return (
        <ul>
          {props.items.map((item, index) => (
            <Item
              key={item.key}
              onClick={() => làmGìĐó(item.name, index)}
            />
          ))}
        </ul>
      );
    }
    ```

  - Các hàm binding được gọi trong lúc render nên đặt ở trong hàm khởi tạo(constructor). eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

    > Tại sao? Vì nếu bind trong hàm render thì mỗi khi render, hàm đó lại được tạo mới một lần khiến cho hiệu suất xử lí giảm.

    ```jsx
    // tệ
    class MyComponent extends React.Component {
      onClickDiv() {
        // làm việc gì đó
      }

      render() {
        return <div onClick={this.onClickDiv.bind(this)} />;
      }
    }

    // tốt
    class MyComponent extends React.Component {
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

  - Không nên dùng dấu "_" đặt trước tên các hàm của Component
    > Lí do? Vì dấu gạch dước thi thoảng được dùng trong một số ngôn ngữ để biểu thị tính "private". Tuy nhiên, không giống các ngôn ngữ khác, trong JavaScript, mọi thứ đều là “public”. Cho dù bạn có cho dấu gạch dưới vào hay không nó vẫn là public, bất kể ý định của bạn. Hãy xem vấn đề  [#1024](https://github.com/airbnb/javascript/issues/1024), và [#490](https://github.com/airbnb/javascript/issues/490) để hiểu sâu hơn.

    ```jsx
    // tệ
    React.createClass({
      _onClickSubmit() {
        // làm việc gì đó
      },

      // làm việc gì đó
    });

    // tốt
    class extends React.Component {
      onClickSubmit() {
        // làm việc gì đó
      }

      // làm việc gì đó
    }
    ```

  - Phải trả về một giá trị trong hàm `render`. eslint: [`react/require-render-return`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-render-return.md)

    ```jsx
    // tệ
    render() {
      (<div />);
    }

    // tốt
    render() {
      return (<div />);
    }
    ```

## Cách sắp xếp hàm

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

## `isMounted`

  - Không nên sử dụng `isMounted`. eslint: [`react/no-is-mounted`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-is-mounted.md)

  > Tại sao? Vì [`isMounted` là một anti-pattern(mẫu nên tránh)](https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html), không có sẵn khi dùng ES6 classes, và đang bị phản đối từ cộng đồng.


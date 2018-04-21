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


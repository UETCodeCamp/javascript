## Refs

  - Luôn sử dụng ref callback-truyền hàm A vào hàm B và một thời điểm nào đó hàm A sẽ được hàm B gọi lại. eslint: [`react/no-string-refs`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

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



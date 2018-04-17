## Tags

  - Luôn luôn tự đóng các thẻ không có con. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

    ```jsx
    // tệ
    <Foo variant="stuff"></Foo>

    // tốt
    <Foo variant="stuff" />
    ```

  - Nếu component của bạn có thuộc tính nhiều dòng, hãy đóng các thẻ đó trên 1 dòng mới. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

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

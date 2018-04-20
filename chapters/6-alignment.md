## Alignment
- Thực hiện theo các kiểu sắp xếp này cho cú pháp JSX. eslint: [react/jsx-closing-bracket-location](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [react/jsx-closing-tag-location](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)

 ```jsx
    // tệ
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // tốt
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // nếu props phù hợp trong một dòng thì giữ nó trên cùng một dòng
    <Foo bar="bar" />

    // phần tử con được thụt lề bình thường
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>
    ```

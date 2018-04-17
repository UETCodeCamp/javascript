## Basic Rules

  - Chỉ include một React component trong 1 file.
    - Tuy nhiên, [Stateless, or Pure, Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) có thể chung một file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
  - Luôn luôn sử dụng cú pháp JSX.
  - Không được sử dụng `React.createElement` nếu bạn không khởi tạo app từ một file nó không phải JSX.

## Basic Rules

  - Chỉ chứa một React Component trong 1 file.
  - Tuy nhiên, những component có khả năng sử dụng lại([Stateless Component, hoặc Pure Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions)) có thể chung một file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
  - Luôn luôn sử dụng cú pháp JSX.
  - Không sử dụng `React.createElement` chung với cú pháp JSX.

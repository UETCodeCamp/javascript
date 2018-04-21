## `isMounted`

  - Không nên sử dụng `isMounted`. eslint: [`react/no-is-mounted`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-is-mounted.md)

  > Tại sao? Vì [`isMounted` là một anti-pattern(mẫu nên tránh)](https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html), không có sẵn khi dùng ES6 classes, và đang bị phản đối từ cộng đồng.

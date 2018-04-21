## Naming

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

    > Tại sao? `displayName` của component có thể đuợc sử dụng bởi những công cụ phát triển hoặc trong các thông báo lỗi, và có một giá trị mà thể hiện rõ mối quan hệ này sẽ giúp chúng hiểu rõ chuyện gì đang xảy ra.

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



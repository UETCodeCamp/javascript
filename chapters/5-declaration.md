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

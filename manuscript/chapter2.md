# Cơ bản trong React

Chương này sẽ hướng dẫn các bạn về những điều cơ bản của React. Nó sẽ bao gồm trạng thái và các tương tác của thành phần khi chúng ta đi qua những thành phần tĩnh. Chúng ta cũng sẽ tìm hiểu qua những cách khác nhau để khai báo một thành phần, và cách thức để giữ thành phân luôn có thể kết hợp và tái sử dụng.

## Trạng thái cục bộ thành phần

Trạng thái cục bộ thành phần, thường được biết đến như một trạng thái bên trong của thành phần, cho phép bạn lưu, chỉnh sửa, và xóa những thuộc tính được lưu trữ trong thành phần của bạn. Thành phần lớp ES6 sau đó sử dụng một hàm khởi tạo để khởi tạo những biến thành phần cục bộ. Hàm khởi tạo được gọi một lần duy nhất, khi mà thành phần được khởi tạo:

Hãy cùng đến với hàm khởi tạo của lớp.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

# leanpub-start-insert
  constructor(props) {
    super(props);
  }
# leanpub-end-insert

  ...

}
~~~~~~~~

Thành phần App là một thành phần phụ của `Component`, bởi vì `extends Component` được khai báo trong thành phần App.

Việc gọi `super(props);` là cần thiết. nó sẽ thiết lập `this.props` trong hàm khởi tạo của bạn trong trường hợp bạn muốn truy cập vào chúng. Nếu không chúng sẽ là `undefined` khi truy cập `this.props` ở trong hàm khởi tạo của bạn. Trong trường hợp này, trạng thái ban đầu của thành phần nên là danh sách mẫu các phần tử:


{title="src/App.js",lang="javascript"}
~~~~~~~~
const list = [
  {
    title: 'React',
    url: 'https://reactjs.org/',
    author: 'Jordan Walke',
    num_comments: 3,
    points: 4,
    objectID: 0,
  },
  ...
];

class App extends Component {

  constructor(props) {
    super(props);

# leanpub-start-insert
    this.state = {
      list: list,
    };
# leanpub-end-insert
  }

  ...

}
~~~~~~~~

Trạng thái được gắn với lớp sử dụng đối tượng `this`, nhờ đó bạn có thể truy cập trạng thái cục bộ của toàn bộ thành phần. Ví dụ, nó có thể được dùng trong phương thức `render()`. Trước đó bạn đã ánh xạ một danh sách tĩnh các phần tử trong phương thức `render()` mà được định nghĩa bên ngoài thành phần của bạn. Bây giờ bạn sẽ sử dụng danh sách từ trạng thái cục bộ trong thành phần của bạn.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
# leanpub-start-insert
        {this.state.list.map(item =>
# leanpub-end-insert
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Danh sách hiện tại là một phần của thành phần, Ở trong trạng thái cục bộ của thành phần. Bạn có thể thêm, sửa, hoặc xóa những phần tử khỏi danh sách của bạn. Mỗi lần bạn thành đổi trạng thái của đối tượng, phương thức `render()` của thành phần của bạn sẽ chạy lại lần nữa. Đó là cách để bạn có thể thay đổi trạng thái cục bộ của thành phần và thấy việc trả về lại của dữ liệu mới từ trạng thái cục bộ.

Hãy cẩn thận đừng thay đổi trạng thái một cách trực tiếp. Thay vào đó, bạn nên sử dụng phương thức tên là `setState()` để chỉnh sửa trạng thái của bạn. Chúng ta sẽ được tìm hiểu về những khái niệm này một cách kỹ càng hơn trong chương tiếp theo.

### Luyện tập:

* Trải nghiệm với trạng thái cục bộ
  * Định nghĩa nhiều trạng thái ban đầu hơn trong hàm khởi tạo
  * Sử dụng và truy cập phương thức `render()`
* Đọc thêm [the ES6 class constructor](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor)

## Khởi tạo đối tượng ES6 

Trong JavaScript ES6, bạn có thể sử dụng một cú pháp ngắn gọn để khởi tạo đối tượng của bạn một cách nhanh chóng hơn, như cách khởi tạo đối tượng dưới đây:

{title="Code Playground",lang="javascript"}
~~~~~~~~
const name = 'Robin';

const user = {
  name: name,
};
~~~~~~~~

Khi thuộc tính name trong đối tượng của bạn trùng với biến name, bạn có thể làm như sau:

{title="Code Playground",lang="javascript"}
~~~~~~~~
const name = 'Robin';

const user = {
  name,
};
~~~~~~~~

Trong ứng dụng của bạn, bạn có thể làm tương tự. Tên biến danh sách và tên thuộc tính trạng thái là giống nhau.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// ES5
this.state = {
  list: list,
};

// ES6
this.state = {
  list,
};
~~~~~~~~

Tên phương thức ngắn gọn cũng vô cùng hữu dụng. Trong JavaScript ES6, bạn có thể khởi tạo phương thức trong một đối tượng một cách nhanh gọn hơn:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// ES5
var userService = {
  getUserName: function (user) {
    return user.firstname + ' ' + user.lastname;
  },
};

// ES6
const userService = {
  getUserName(user) {
    return user.firstname + ' ' + user.lastname;
  },
};
~~~~~~~~

Cuối cùng, bạn được phép sử dụng những tên thuộc tính đã được tính toán trong JavaScript ES6:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// ES5
var user = {
  name: 'Robin',
};

// ES6
const key = 'name';
const user = {
  [key]: 'Robin',
};
~~~~~~~~

Lát nữa, bạn sẽ có thể sử dụng tên thuộc tính được tính toán để lưu trữ giá trị bởi khóa trong đối tượng động, một cách dễ dàng để tạo ra bảng tra cứu trong JavaScript.

### Luyện tập:

* Trải nghiệm với khởi tạo đối tượng ES6
* Đọc thêm [ES6 object initializer](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Object_initializer)

## Dòng chảy dữ liệu vô hướng

Giờ thì bạn đã có trạng thái cục bộ trong thành phần App của bạn, nhưng chưa hề sử dụng trạng thái này. Trạng thái cục bộ là tĩnh, bởi vì thành phần của nó cũng là tĩnh. Một cách tốt để trải nghiệm việc thao túng trạng thái là bắt đầu làm việc với tương tác thành phần.

Chúng ta sẽ luyện tập khái niệm này bằng cách thêm một cái nút cho mỗi sản phẩm trong danh sách đã được hiển thị. Nút sẽ đọc "Dismiss", mục đích của nó là xóa sản phẩn khỏi danh sách. Trong một email của khách hàng, ví dụ, nó sẽ là một cách hiệu quả để đánh dấu một số sản phẩm của danh sách là 'đọc' trong khi đó giữ những sản phẩm chưa đọc tách biệt.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        {this.state.list.map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
# leanpub-start-insert
            <span>
              <button
                onClick={() => this.onDismiss(item.objectID)}
                type="button"
              >
                Dismiss
              </button>
            </span>
# leanpub-end-insert
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Phương thức lớp `onDismiss()` chưa được định nghĩa. Chúng ta sẽ định nghĩa nó ngay thôi, nhưng hiện tại, hãy cùng tập trung vào hàm xử lý `onClick` của phần tử button. Như bạn có thể thấy, phương thức `onDismiss()` trong hàm xử lý `onClick` được đóng gói bởi hàm mũi tên. Bạn có thể sử dụng nó với thuộc tính `objectID` của đối tượng `item` và xác định sản phẩm nào cần được loại bỏ. Một cách khác là định nghĩa một hàm bên ngoài hàm xử lý `onClick` và chỉ truyền vào hàm được định nghĩa cho nó. Chúng ta sẽ tìm hiểu những hàm xử lý này kỹ hơn trong quá trình học.

Chú ý việc sử dụng nhiều dòng cho phần tử element, và những phần tử với nhiều thuộc tính có thể bị lộn xộn dễ dàng như thế nào. Phần tử button được sử dụng với nhiều dòng và lùi đầu dòng để giúp nó dễ đọc . trong khi việc luyện tập này là không rõ ràng trong phát triển React, nó là phong cách lập trình mà tôi đề xuất để đạt được sự trong sạch và tâm trí yên bình.

Giờ thì chúng ta sẽ triển khai chức năng của `onDismiss()`. Nó nhận vào id để xác định sản phẩm cần xóa bỏ. Hàm được gắn vào lớp và trở thành phương thức lớp. Đó là lý do tại sao bạn truy cập nó với `this.onDismiss()` chứ không phải `onDismiss()`. đối tượng `this` là thực thể lớp. Để định nghĩa `onDismiss()` như phương thức lớp, bạn cần gắn nó với hàm khởi tạo:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
    };

# leanpub-start-insert
    this.onDismiss = this.onDismiss.bind(this);
# leanpub-end-insert
  }

  render() {
    ...
  }
}
~~~~~~~~

Tiếp theo, chúng ta định nghĩa chức năng của nó, logic kinh doanh, trong lớp:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
    };

    this.onDismiss = this.onDismiss.bind(this);
  }

# leanpub-start-insert
  onDismiss(id) {
    ...
  }
# leanpub-end-insert

  render() {
    ...
  }
}
~~~~~~~~

Giờ thì chúng ta có thể định nghĩa thứ gì xảy ra trong phương thức lớp. Hãy nhớ rằng, mục đích là để xóa bỏ sản phẩm được xác định bởi id khỏi danh sách và lưu trữ danh sách mới vào trạng thái cục bộ. Danh sách mới sẽ được sử dụng trong phương thức `render()` chạy lại để hiển thị nó, nơi mà những sản phẩm bị loại bỏ sẽ không còn xuất hiện nữa.

Bạn có thể loại bỏ sản phẩm trong danh sách sử dụng chức năng [JavaScript's built-in filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), nó nhận vào một hàm . Hàm có thể truy cập đến từng giá trị của danh sách bởi vì nó sẽ duyệt lần lượt qua mỗi sản phẩm, vì vậy bạn có thể tính toán chúng dựa trên những điều kiện cụ thể.

{title="Code Playground",lang="javascript"}
~~~~~~~~
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const filteredWords = words.filter(function (word) { return word.length > 6; });

console.log(filteredWords);
// expected output: Array ["exuberant", "destruction", "present"]
~~~~~~~~

Hàm sẽ trả về một danh sách mới thay vì thay đổi cái cũ, và nó hỗ trợ cú pháp React sử dụng một cấu trúc dữ liệu bất biến.

{title="src/App.js",lang="javascript"}
~~~~~~~~
onDismiss(id) {
# leanpub-start-insert
  const updatedList = this.state.list.filter(function isNotId(item) {
    return item.objectID !== id;
  });
# leanpub-end-insert
}
~~~~~~~~

Tiếp theo, chúng ta sẽ phân tách hàm và truyền nó vào hàm filter:

{title="src/App.js",lang="javascript"}
~~~~~~~~
onDismiss(id) {
# leanpub-start-insert
  function isNotId(item) {
    return item.objectID !== id;
  }

  const updatedList = this.state.list.filter(isNotId);
# leanpub-end-insert
}
~~~~~~~~

**Ghi nhớ**: Bạn có thể dọc một cách hiệu quả hơn sử dụng hàm mũi tênJavaScript ES6.

{title="src/App.js",lang="javascript"}
~~~~~~~~
onDismiss(id) {
# leanpub-start-insert
  const isNotId = item => item.objectID !== id;
  const updatedList = this.state.list.filter(isNotId);
# leanpub-end-insert
}
~~~~~~~~

Bạn thậm chí có thể viết nó một dòng như bạn đã làm với hàm xử lý `onClick` của nút, mặc dù nó có thể ít dễ đọc hơn:

{title="src/App.js",lang="javascript"}
~~~~~~~~
onDismiss(id) {
# leanpub-start-insert
  const updatedList = this.state.list.filter(item => item.objectID !== id);
# leanpub-end-insert
}
~~~~~~~~

Danh sách loại bỏ những sản phẩm được click, nhưng trạng thái chưa hề thay đổi. Sử dụng phương thức lớp `setState()` để thay đổi danh sách trong trạng thái cục bộ của thành phần:

{title="src/App.js",lang="javascript"}
~~~~~~~~
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedList = this.state.list.filter(isNotId);
# leanpub-start-insert
  this.setState({ list: updatedList });
# leanpub-end-insert
}
~~~~~~~~

Chạy ứng dụng lại lần nữa và thử nút "Dismiss". Những gì bạn trải nghiểm chính là **dòng chảy dữ liệu vô hướng** của React. Một hành động được kích hoạt trong lớp hiển thị với `onClick()`, một hàm hoặc phương thức lớp thay đổi trạng thái cục bộ, và rồi phương thức `render()` của thành phần chạy lại lần nữa để thay đổi giao diện.

### Luyện tập:

* Đọc thêm [the state and lifecycle in React](https://reactjs.org/docs/state-and-lifecycle.html)

## Gắn

Học về gắn trong JavaScript là quan trọng khi sử dụng lớp thành phần React ES6. Trong những chương trước, bạn đã gắn phương thức lớp `onDismiss()` trong hàm sinh.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      list,
    };

    this.onDismiss = this.onDismiss.bind(this);
  }

  ...
}
~~~~~~~~

Bước gắn là cần thiết bởi phương thức lớp không tự động gắn `this` với khởi tạo lớp. Hãy cùng trình diễn nó với sự trợ giúp của lớp thành phần ES6 dưới đây:

{title="Code Playground",lang="javascript"}
~~~~~~~~
class ExplainBindingsComponent extends Component {
  onClickMe() {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClickMe}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
~~~~~~~~

Thành phần trả về hoàn toàn ổn, nhưng bạn click vào nút, bạn thấy `undefined` console log nhà phát triển của bạn. Đây là một trong những nguồn chính của lỗi mà các nhà phát triển gặp phải trong React. Nếu bạn muốn truy cập `this.state` trong phương thức lớp, Nó không thể nhận được bởi `this` là `undefined`. để làm cho `this` có thể truy cập được trong phương thức lớp của bạn, bạn phải gắn phương thức lớp vào `this`.

Trong phương thức lớp của thành phần lớp dưới đây được gắn chính xác trong hàm sinh của lớp:

{title="Code Playground",lang="javascript"}
~~~~~~~~
class ExplainBindingsComponent extends Component {
# leanpub-start-insert
  constructor() {
    super();

    this.onClickMe = this.onClickMe.bind(this);
  }
# leanpub-end-insert

  onClickMe() {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClickMe}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
~~~~~~~~

Việc gắn phương thức lớp có thể xảy ra đâu đó nữa. Ví dụ, nó có thể xảy ra trong phương thức lớp `render()`:

{title="Code Playground",lang="javascript"}
~~~~~~~~
class ExplainBindingsComponent extends Component {
  onClickMe() {
    console.log(this);
  }

  render() {
    return (
      <button
# leanpub-start-insert
        onClick={this.onClickMe.bind(this)}
# leanpub-end-insert
        type="button"
      >
        Click Me
      </button>
    );
  }
}
~~~~~~~~

Để tránh thói quen này, tuy nhiên, bởi vì nó được gắn với phương thức lớp mỗi lần phương thức `render()` chạy, nghĩa là mỗi lần chạy thành phần sẽ cập nhật, thứ mà cuối cùng sẽ làm giảm hiệu suất của ứng dụng của bạn. Gắn phương thức lớp trong hàm khởi tạo cần được làm duy nhất một lần, khi thành phần được khởi tạo.

Một số nhà phát triển sẽ định nghĩa logic kinh doanh của những phương thức lớp trong hàm khởi tạo:

{title="Code Playground",lang="javascript"}
~~~~~~~~
class ExplainBindingsComponent extends Component {
  constructor() {
    super();

# leanpub-start-insert
    this.onClickMe = () => {
      console.log(this);
    }
# leanpub-end-insert
  }

  render() {
    return (
      <button
        onClick={this.onClickMe}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
~~~~~~~~

Tránh cách tiếp cận này, bởi lẽ nó sẽ làm hàm khởi tạo của bạn lộn xộn dần lên. Hàm khởi tạo chỉ ở đó để khởi tạo lớp của bạn với những thuộc tính của nó, vậy nên logic kinh doanh của phương thức lớp nên được định nghĩa bên ngoài hàm khởi tạo.

{title="Code Playground",lang="javascript"}
~~~~~~~~
class ExplainBindingsComponent extends Component {
  constructor() {
    super();

    this.doSomething = this.doSomething.bind(this);
    this.doSomethingElse = this.doSomethingElse.bind(this);
  }

  doSomething() {
    // do something
  }

  doSomethingElse() {
    // do something else
  }

  ...
}
~~~~~~~~

Phương thức lớp có thể được gắn tự động sử dụng hàm mũi tên JavaScript:

{title="Code Playground",lang="javascript"}
~~~~~~~~
class ExplainBindingsComponent extends Component {
  onClickMe = () => {
    console.log(this);
  }

  render() {
    return (
      <button
        onClick={this.onClickMe}
        type="button"
      >
        Click Me
      </button>
    );
  }
}
~~~~~~~~

Sử dụng phương pháp này nếu lặp lại việc gắn trong hàm khởi tạo làm phiền bạn. Tài liệu chính thức của React đi liền với phương pháp gắn phương thức lớp trong hàm khởi tạo, vậy nên cuốn sách này sẽ gắn liền với phương pháp này.

### Luyện tập:

* Thử cách tiếp cận khác của việc gắn và console log đối tượng `this`
* Tìm hiểu thêm về [an alternative React component syntax](https://github.com/the-road-to-learn-react/react-alternative-class-component-syntax)

## Xử lý sự kiện

Bây giờ chúng ta sẽ nói về xử lý sự kiện trong phần tử. Trong ứng dụng của bạn, bạn đang sử dụng những phần tử nút dưới đây để xóa sản phẩm trong danh sách.

{title="src/App.js",lang="javascript"}
~~~~~~~~
...

<button
  onClick={() => this.onDismiss(item.objectID)}
  type="button"
>
  Dismiss
</button>

...
~~~~~~~~

Hàm này đã phức tạp rồi, bởi vì nó truyền giá trị vào phương thức lớp và cần bọc nó trong một hàm mũi tên. Cần thiết, nó phải là hàm mà được truyền vào xử lý sự kiện. Mã lệnh dưới đây sẽ không hoạt động, bởi vì phương thức lớp sẽ thực hiện ngay lập tức khi bạn mở ứng dụng trong trình duyệt:

{title="src/App.js",lang="javascript"}
~~~~~~~~
...

<button
  onClick={this.onDismiss(item.objectID)}
  type="button"
>
  Dismiss
</button>

...
~~~~~~~~

Khi sử dụng `onClick={doSomething()}`, hàm `doSomething()` thực hiện ngay lập tức khi ứng dụng được mở trong trình duyệt. Biểu thức trong hàm xử lý được thực hiện. Bởi vì giá trị trả về của hàm không còn là một hàm nữa, nên sẽ không có gì xảy ra khi bạn click nút. Nhưng sử dụng `onClick={doSomething}` nơi mà `doSomething` là một hàm, nó sẽ chỉ được thực hiện nếu nút được click. Quy luật tương đương được áp dụng cho phương thức `onDismiss()`.

Tuy nhiên, sử dụng `onClick={this.onDismiss}` là không đủ, bởi vì thuộc tính `item.objectID` cần phải được truyền vào phương thức lớp để xác định sản phẩm sẽ được sẽ. chúng ta bọc nó vào một hàm khác để giấu thuộc tính. Khái niệm này được gọi là higher-order functions trong JavaScript, thứ mà chúng ta sẽ giới thiệu ngắn gọn lát nữa.


{title="src/App.js",lang="javascript"}
~~~~~~~~
...

<button
  onClick={() => this.onDismiss(item.objectID)}
  type="button"
>
  Dismiss
</button>

...
~~~~~~~~

Chúng ta cũng có thể định nghĩa hàm bọc lấy bên ngoài phương thức, để truyền duy nhất hàm được định nghĩa vào hàm xử lý. Bởi vì nó cần truy cập vào từng sản phẩm cụ thể, nó cần phải tồn taiji bên trong hàm map.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        {this.state.list.map(item => {
# leanpub-start-insert
          const onHandleDismiss = () =>
            this.onDismiss(item.objectID);
# leanpub-end-insert

          return (
            <div key={item.objectID}>
              <span>
                <a href={item.url}>{item.title}</a>
              </span>
              <span>{item.author}</span>
              <span>{item.num_comments}</span>
              <span>{item.points}</span>
              <span>
                <button
# leanpub-start-insert
                  onClick={onHandleDismiss}
# leanpub-end-insert
                  type="button"
                >
                  Dismiss
                </button>
              </span>
            </div>
          );
        }
        )}
      </div>
    );
  }
}
~~~~~~~~

Một hàm cần được truyền vào xử lý của phần tử. như ví dụ, thử mã lệnh sau thay thế:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        {this.state.list.map(item =>
            ...
            <span>
              <button
# leanpub-start-insert
                onClick={console.log(item.objectID)}
# leanpub-end-insert
                type="button"
              >
                Dismiss
              </button>
            </span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Phương thức này sẽ chạy mỗi khi bạn mở ứng dụng trong trình duyệt, nhưng sẽ không khi bạn click nút. Mã lệnh dưới đây sẽ chỉ chạy khi bạn click nút, một hàm mà nó được thực thi khi bạn kích hoạt hàm xử lý:

{title="src/App.js",lang="javascript"}
~~~~~~~~
...

<button
# leanpub-start-insert
  onClick={function () {
    console.log(item.objectID)
  }}
# leanpub-end-insert
  type="button"
>
  Dismiss
</button>

...
~~~~~~~~

**Ghi nhớ:** Bạn có thể chuyển hàm thành hàm mũi tên JavaScript ES6, chỉ khi chúng ta thực hiện với phương thức lớp `onDismiss()`:

{title="src/App.js",lang="javascript"}
~~~~~~~~
...

<button
# leanpub-start-insert
  onClick={() => console.log(item.objectID)}
# leanpub-end-insert
  type="button"
>
  Dismiss
</button>

...
~~~~~~~~

Những người mới tiếp cận React thường có khó khăn trong việc sử dụng hàm trong hàm xử lý sự kiện, vậy nên đường lùi bước nếu bạn gặp khó khăn lần đầu. Bạn nên quen với việc sử dụng hàm mũi tên 1 dòng JavaScript với truy cập vào thuộc tính `objectID` của đối tượng `item`:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {
  ...

  render() {
    return (
      <div className="App">
        {this.state.list.map(item =>
          <div key={item.objectID}>
            ...
            <span>
# leanpub-start-insert
              <button
                onClick={() => this.onDismiss(item.objectID)}
                type="button"
              >
                Dismiss
              </button>
# leanpub-end-insert
            </span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Sử dụng hàm mũi tên trong hàm xử lý sự kiện trực tiếp ảnh hưởng đến hiệu suất ứng dụng của bạn. Ví dụ, hàm xử lý  `onClick` cho phương thức `onDismiss()` bọc phương thức trong một hàm mũi tên khác để truyền id sản phẩm. Mỗi khi phương thức `render()` chạy, hàm xử lý khởi tạo hàm mũi tên bậc cao. Nó có thể gây ảnh hưởng đến hiệu suất ứng dụng của bạn, nhưng trong hầu hết mọi trường hợp bạ sẽ không nhận ra. Nếu bạn có một cái bảng dữ liệu lớn với  1000 sản phẩm và mỗi dòng hoặc cột có một hàm mũi tên trong hàm xử lý sự kiện, Hãy suy nghĩ về hiệu suất của ứng dụng, vậy nên bạn có thể triển khai một thành phần Button ứng cử viên để gắn phương thức trong hàm khởi tạo. Trước đó, mặc dù, nó là một tối ưu hóa sớm, và khôn ngoan hơn khi học cơ bản của React trước khi quan tâm về tối ưu hóa.

### Luyện tập:

* Thử những cách tiếp cận khác sử dụng hàm trong hàm xử lý `onClick` của nút của bạn

## Tương tác với Forms và Events

Chúng ta sẽ thêm một tương tác khác để tìm hiểu về forms và events trong React, một chức năng tìm kiếm nơi mà nhập vào vùng tìm kiếm sẽ tạm thời lọc danh sách dựa trên thuộc tính title của sản phẩm.

Đầu tiên, chúng ta định nghĩa form với một trường nhập trong JSX:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
# leanpub-start-insert
        <form>
          <input type="text" />
        </form>
# leanpub-end-insert
        {this.state.list.map(item =>
          ...
        )}
      </div>
    );
  }
}
~~~~~~~~

Trong trường hợp dưỡi đây bạn sẽ gõ vào trường nhập và lọc danh sách tạm thời bằng khái niệm tìm kiếm được sử dụng trong trường nhập. Để lọc danh sách dựa trên giá trị của trường nhập, chúng ta lưu giá trị của trường nhập trong tráng thái cục bộ. Chúng ta sử dụng **synthetic events** trong React để truy cập giá trị trong event payload.

Hãy cùng định nghĩa hàm xử lý `onChange` cho trường nhập:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
# leanpub-start-insert
          <input
            type="text"
            onChange={this.onSearchChange}
          />
# leanpub-end-insert
        </form>
        ...
      </div>
    );
  }
}
~~~~~~~~

Hàm này được gắn với thành phần, nên một lần nữa nó chính là phương thức. Bạn chỉ cần gắn và định nghĩa phương thức

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
    };

# leanpub-start-insert
    this.onSearchChange = this.onSearchChange.bind(this);
# leanpub-end-insert
    this.onDismiss = this.onDismiss.bind(this);
  }

# leanpub-start-insert
  onSearchChange() {
    ...
  }
# leanpub-end-insert

  ...
}
~~~~~~~~

Khi sử dụng một hàm xử lý trong thành phần, bạn truy cập vào synthetic React event trong giá trị hàm callback.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

# leanpub-start-insert
  onSearchChange(event) {
# leanpub-end-insert
    ...
  }

  ...
}
~~~~~~~~

Event có giá trị của trường nhập trong đối tượng target của nó, từ đó bạn có thể cập nhật trạng thái cục bộ với khái niệm search sử dụng `this.setState()`.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  onSearchChange(event) {
# leanpub-start-insert
    this.setState({ searchTerm: event.target.value });
# leanpub-end-insert
  }

  ...
}
~~~~~~~~

Đừng quên việc định nghĩa trạng thái khởi tạo cho thuộc tính `searchTerm` trong hàm sinh. Trường nhập nên được bỏ trống lúc đầu, vậy cho giá trị của nó là một chuỗi rỗng.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
# leanpub-start-insert
      searchTerm: '',
# leanpub-end-insert
    };

    this.onSearchChange = this.onSearchChange.bind(this);
    this.onDismiss = this.onDismiss.bind(this);
  }

  ...
}
~~~~~~~~

Chúng ta lưu giá trị nhập vào trạng thái cục bộ mỗi lần giá trị của trường nhập thay đổi.

Chúng ta có thể giá sử rằng khi ta cập nhật `searchTerm` với `this.setState()`, danh sách cũng cần được truyền để bảo toàn nó. `this.setState()` của React là một shallow merge, tuy nhiên, nó sẽ bảo toàn thuộc tính kề trong đối tượng trạng thái khi nó cập nhật thuộc tính. Trạng thái danh sánh, mặc dù bạn đã xóa phần tử khỏi nó, nó vẫn giữ nguyên khi cập nhật thuộc tính `searchTerm`.

Quay trở lại ứng dụng, để kiểm tra xem danh sách đã được lọc hay chưa, dựa trên giá trị được lưu trữ của trường nhập trong trang thái cục bộ. Chúng ta cần lọc danh sách tạm thời dựa trên `searchTerm`, và chúng ta có tất cả mọi thứ chúng ta cần để thực hiện thao tác này. Trong phương thức `render()`, trước khi biến đổi qua danh sách, chúng ta áp dụng lọc cho nó. Hàm lọc sẽ chỉ xác định nếu `searchTerm` trùng với thuộc tính title của sản phẩm. Chúng ta đã sử dụng hàm filter có sẵn trong JavaScript, nào hãy cùng sử dụng nó một lần nữa để lọc danh sách trước khi biến đổi nó. Hàm lọc sẽ trả về một mảng mới, để cho hàm biến đổi có thể sử dụng nó.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
          <input
            type="text"
            onChange={this.onSearchChange}
          />
        </form>
# leanpub-start-insert
        {this.state.list.filter(...).map(item =>
# leanpub-end-insert
          ...
        )}
      </div>
    );
  }
}
~~~~~~~~

Hãy cùng tiếp cận hàm lọc theo một cách khác lần này. Chúng ta muốn định nghĩa tham số lọc, thứ mà là hàm truyền cho hàm lọc bên ngoài thành phần lớp ES6. Chúng ta không thể truy cập vào trạng thái của thành phần, nên chúng ta không thể truy cập vào thuộc tính `searchTerm` để xác định điều kiện lọc. Điều này có nghĩa là chúng ta sẽ cần truyền `searchTerm` vào hàm lọc, trả về hàm mới để xác định điều kiện. Đây được gọi là hàm bậc cao.

Bạn nên biết về hàm bậc cao, bởi lẽ React làm việc với khái niệm gọi là thành phần bậc cao. Bạn sẽ bắt đầu tìm hiểu khái niệm này lát nữa trong quyển sách này. Bây giờ thì, hãy tập trung vào chức năng của hàm lọc.

Trước tiên, bạn phải định nghĩa hàm bậc cao bên ngoài thành phần App của bạn.

{title="src/App.js",lang="javascript"}
~~~~~~~~
# leanpub-start-insert
function isSearched(searchTerm) {
  return function (item) {
    // some condition which returns true or false
  }
}
# leanpub-end-insert

class App extends Component {

  ...

}
~~~~~~~~

Hàm này nhận vào `searchTerm` và trả về một hàm khác, bởi vì hàm lọc chỉ nhận kiểu đó cho đầu vào của nó. Hàm trả về truy cập vào đối tượng sản phẩm, bởi vì nó là thứ được truyền vào hàm lọc.

Nó cũng được sử dụng để lọc danh sách dựa trên điều kiện được định nghĩa trong hàm, hãy cùng nhau định nghĩa điều kiện:

{title="src/App.js",lang="javascript"}
~~~~~~~~
function isSearched(searchTerm) {
  return function (item) {
# leanpub-start-insert
    return item.title.toLowerCase().includes(searchTerm.toLowerCase());
# leanpub-end-insert
  }
}

class App extends Component {

  ...

}
~~~~~~~~

Điều kiện trùng với kiểu của `searchTerm` đến với thuộc tính title của sản phẩm từ danh sách của bạn. Bạn có thể thực hiện nó với hàm `includes` có sẵn của JavaScript. Khi kiểu phù hợp, nó trả về true và những sản phẩm giữ nguyên trong danh sách; khi kiểu không khớp, sản phẩm sẽ bị xóa khỏi danh sách. Đừng quên để việc khớp viết hoa trong cả hai chuỗi của chữ, bởi sẽ có sự không khớp giữa 'redux' và title sản phẩm 'Redux'. Bởi vì chúng ta đang làm việc với danh sách bất biến và trả về danh sách mới bằng cách sử dụng hàm lọc, danh sách ban đầu trong biến cục bộ sẽ không thay đổi.

Chúng ta đã sử dụng tính năng JavaScript ES7, nhưng chưa hề có trong ES5. Dành cho ES5, sử dụng hàm `indexOf()` để lấy được index của sản phẩm trong danh sách. Khi một sản phẩm trong sách dánh, `indexOf()` sẽ trả về index của nó trong mảng.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// ES5
string.indexOf(pattern) !== -1

// ES6
string.includes(pattern)
~~~~~~~~

Một cách tối giản hóa có thể đạt được với hàm mũi tên ES6 lần nữa. Nó giúp cho hàm được ngắn gọn hơn:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// ES5
function isSearched(searchTerm) {
  return function (item) {
    return item.title.toLowerCase().indexOf(searchTerm.toLowerCase()) !== -1;
  }
}

// ES6
const isSearched = searchTerm => item =>
  item.title.toLowerCase().includes(searchTerm.toLowerCase());
~~~~~~~~

Hệ sinh thái React sử dụng rất nhiều khái niệm của lập trình hàm, thường sử dụng một hàm mà trả lại hàm (khái niệm này là hàm bậc cao) để truyền thông tin. JavaScript ES6 giúp chúng ta biểu diễn những thứ này thậm chí ngắn gọn hơn với hàm mũi tên.

Cuối cùng, sử dụng hàm được định nghĩa `isSearched()` để lọc danh sách. Chúng ta truyền cho nó thuộc tính `searchTerm` từ biến cục bộ, vì vậy nó sẽ trả về hàm lọc của hàm và lọc danh sách của bạn dựa trên điều kiện lọc. Sau đó nó sẽ biến đổi danh sách đã được lọc để hiện thị từng phần tử cho mỗi sản phẩm của danh sách.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
          <input
            type="text"
            onChange={this.onSearchChange}
          />
        </form>
# leanpub-start-insert
        {this.state.list.filter(isSearched(this.state.searchTerm)).map(item =>
# leanpub-end-insert
          ...
        )}
      </div>
    );
  }
}
~~~~~~~~

Chúc năng tìm kiếm giờ sẽ hoạt động. Hãy tự kiểm tra nó trên trình duyệt.

### Luyện tập:

* Đọc thêm [React events](https://reactjs.org/docs/handling-events.html)
* Đọc thêm [higher-order functions](https://en.wikipedia.org/wiki/Higher-order_function)

## ES6 Destructuring

Destructuring trong JavaScript ES6 cung cấp một cách truy cập dễ dàng hơn vào thuộc tính trong đối tượng và mảng. So sánh đoạn dưới đây trong JavaScript ES5 và ES6:

{title="Code Playground",lang="javascript"}
~~~~~~~~
const user = {
  firstname: 'Robin',
  lastname: 'Wieruch',
};

// ES5
var firstname = user.firstname;
var lastname = user.lastname;

console.log(firstname + ' ' + lastname);
// output: Robin Wieruch

// ES6
const { firstname, lastname } = user;

console.log(firstname + ' ' + lastname);
// output: Robin Wieruch
~~~~~~~~

Trong khi chúng ta thêm vào 1 dòng mỗi lần chúng ta truy cập thuộc tính của đối tượng trong in JavaScript ES5, Nó chỉ mất một dòng trong JavaScript ES6. Để dễ đọc, sử dụng nhiều dòng khi bạn destructure một đối tượng thành nhiều thuộc tính.

{title="Code Playground",lang="javascript"}
~~~~~~~~
const {
  firstname,
  lastname
} = user;
~~~~~~~~

Cùng một khái niệm được áp dụng cho mảng. Bạn có thể destructure chúng, một lần nữa sử dụng nhiều dòng để giúp mã lệnh của bạn dễ đọc hơn.

{title="Code Playground",lang="javascript"}
~~~~~~~~
const users = ['Robin', 'Andrew', 'Dan'];
const [
  userOne,
  userTwo,
  userThree
] = users;

console.log(userOne, userTwo, userThree);
// output: Robin Andrew Dan
~~~~~~~~

Chú ý rằng đối tượng trạng thái cục bộ trong thành phần App có thể được destructure như trên. Bạn có thể ngắn gọn hàm lọc và hàm biến đổi.

{title="src/App.js",lang="javascript"}
~~~~~~~~
  render() {
# leanpub-start-insert
    const { searchTerm, list } = this.state;
# leanpub-end-insert
    return (
      <div className="App">
        ...
# leanpub-start-insert
        {list.filter(isSearched(searchTerm)).map(item =>
# leanpub-end-insert
          ...
        )}
      </div>
    );
~~~~~~~~

Bạn có thể thực hiện với ES5 hoặc ES6:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// ES5
var searchTerm = this.state.searchTerm;
var list = this.state.list;

// ES6
const { searchTerm, list } = this.state;
~~~~~~~~

Nhưng bởi vì quyển sách này hầu như sử dụng JavaScript ES6, bạn nên quen với nó.

### Luyện tập:

* Đọc thêm [ES6 destructuring](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

## Controlled Components

Chúng ta đã tìm hiểu về dòng dữ liệu vô hướng trước đây, cùng một quy tắc áp dụng cho trường nhập, thứ mà cập nhật trạng thái cục bộ với `searchTerm` để lọc danh sách. Khi trạng thái thay đổi, phương thức `render()` chạy lại và sử dụng `searchTerm` gần nhất từ trạng thái cục bộ để áp dụng điều kiện lọc.

Nhưng liệu chúng ta có quên gì đó trong thành phần nhập? Một thẻ nhập HTML đi cùng với thuộc tính `value`. Thuộc tính value thường chứa giá trị được hiển thị trong trường nhập. Trong trường hợp này, đó là thuộc tính `searchTerm`. Thành phần form như `<input>`, `<textarea>`, và `<select>` giữ trạng thái của chúng trong HTML thuần. chúng chỉnh sửa giá trị bên trong mỗi khi có ai thay đổi nó từ bên ngoài. Trong React, đó được gọi là 1 **uncontrolled component**, bởi vì nó xử lý trạng thái của riêng nó. Chúng ta muốn chắc chắn thay thế bằng những phần tử này là **controlled components**.

Để làm vậy, chúng ta thiết lập thuộc tính giá trị của trường nhập, thứ mà đã được lưu trong thuộc tính trạng thái `searchTerm` , vậy nên chúng ta có thể truy cập nó từ đó:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
        <form>
          <input
            type="text"
# leanpub-start-insert
            value={searchTerm}
# leanpub-end-insert
            onChange={this.onSearchChange}
          />
        </form>
        ...
      </div>
    );
  }
}
~~~~~~~~

Dòng chảy dữ liệu vô hướng lặp lại cho trường nhập được tự chứa chính nó, và trạng thái thành phần cục bộ là nguồn duy nhất cho trường nhập.

Quản lý trạng thái cục bộ và dòng chảy dữ liệu vô hướng có thể mới với bạn, nhưng một khi bạn điều chỉnh để phù hợp với nó, nó sẽ trở thành dòng chảy tự nhiên nhất của việc triển khai React. React mang khuôn mẫu tiểu thuyết với dòng chảy dữ liệu vô hướng, thứ mà đã được một vài frameworks và thư viện dùng để tạo ra ứng dụng trang đơn.

### Luyện tập:

* Đọc thêm [React forms](https://reactjs.org/docs/forms.html)
* Tìm hiểu về [different controlled components](https://github.com/the-road-to-learn-react/react-controlled-components-examples)

## Chia nhỏ thành phần

Bây giờ chúng ta đã có một ứng dụng App component lớn và tiếp tục phát triển và có thể cuối cùng trở nên quá phức tạp để quản lý hiệu quả. Chúng ta cần chia nó ra nhỏ hơn, nhiều phần dễ quản lý hơn bằng cách tạo ra những thành phần tách biệt cho phần nhập tìm kiếm và danh sách sản phẩm.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
# leanpub-start-insert
        <Search />
        <Table />
# leanpub-end-insert
      </div>
    );
  }
}
~~~~~~~~

Chúng ta truyền thuộc tính của thành phần mà chúng có thể sử dụng chính chúng. Thành phần App cần truyền những thuộc tính đã được quản lý trong trạng thái cục bộ và phương thức lớp của nó.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
# leanpub-start-insert
        <Search
          value={searchTerm}
          onChange={this.onSearchChange}
        />
        <Table
          list={list}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
# leanpub-end-insert
      </div>
    );
  }
}
~~~~~~~~

Giờ thì chúng ta định nghĩa thành phần bên cạnh thành phần App, thứ mà sẽ được thực hiện với JavaScript ES6 sử dụng lớp. Chúng ta trả về những phần tử tương tự như trước.

Đầu tiên là thành phần Search:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {
  ...
}

# leanpub-start-insert
class Search extends Component {
  render() {
    const { value, onChange } = this.props;
    return (
      <form>
        <input
          type="text"
          value={value}
          onChange={onChange}
        />
      </form>
    );
  }
}
# leanpub-end-insert
~~~~~~~~

Tiếp theo là thành phần Table.

{title="src/App.js",lang="javascript"}
~~~~~~~~
...

# leanpub-start-insert
class Table extends Component {
  render() {
    const { list, pattern, onDismiss } = this.props;
    return (
      <div>
        {list.filter(isSearched(pattern)).map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
            <span>
              <button
                onClick={() => onDismiss(item.objectID)}
                type="button"
              >
                Dismiss
              </button>
            </span>
          </div>
        )}
      </div>
    );
  }
}
# leanpub-end-insert
~~~~~~~~

Và giờ bạn có 3 thành phần lớp ES6. Chú ý rằng đối tượng `props` có thể truy cập được qua khởi tạo của lớp sử dụng `this`. Props, viết tắt cho thuộc tính (properties), có đầy đủ những giá trị được truyền vào thành phần khi chúng ta sử dụng thành phần App. Bằng cách đó, thành phần có thể truyền những thuộc tính xuống cây thành phần.

Bằng cách tách những thành phần này ra khỏi thành phần App, chúng trở nên dễ dàng tái sử dụng. Bởi vì những thành phần nhận giá trị của chúng sử dụng đối tượng `props`, bạn có thể truyền vào những props khác nhau vào thành phần của bạn mỗi lần bạn sử dụng ở đâu đó khác.

### Luyện tập:

* Tìm hiểu thêm về thành phần mà có thể chia nhỏ được như Search và Table, nhưng đợi đến khi chúng ta sẽ tìm hiểu nhiều hơn về khái niệm của nó trước khi bạn triển khai bất kì thứ gì.

## Thành phần có thể kết hợp được

Thuộc tính `children` được dùng để truyền những phần tử vào thành phần từ phía trên, những thứ mà không rõ với bản thân thành phần nhưng có thể làm nó có thể kết hợp những thành phần cùng nhau. Chúng ta sẽ xem nó trông như thế nào khi bạn truyền một chuỗi văn bản như một đứa con vào thành phần Search.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
# leanpub-start-insert
        <Search
          value={searchTerm}
          onChange={this.onSearchChange}
        >
          Search
        </Search>
# leanpub-end-insert
        <Table
          list={list}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
      </div>
    );
  }
}
~~~~~~~~

Giờ thì thành phần Search component có thể destructure thuộc tính `children` từ đối tượng `props`, và xác định nơi mà nó nên được hiển thị.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class Search extends Component {
  render() {
# leanpub-start-insert
    const { value, onChange, children } = this.props;
# leanpub-end-insert
    return (
      <form>
# leanpub-start-insert
        {children} <input
# leanpub-end-insert
          type="text"
          value={value}
          onChange={onChange}
        />
      </form>
    );
  }
}
~~~~~~~~

Văn bản "Search" nên được hiển thị cạnh trường nhập của bạn. Khi bạn sử dụng thành phần Search component ở nơi khác, bạn có thể sử dụng những thực thế khác nhau, bởi vì nó không chỉ là văn bản có thể truyền như con. Bạn có thể truyền một phần tử, hoặc một cây phần tử có thể được đóng gói bởi thành phần, như những đứa con. Thuộc tính children giúp cho nó có thể kết nối các thành lại với nhau.

### Luyện tập:

* Đọc thêm [the composition model of React](https://reactjs.org/docs/composition-vs-inheritance.html)

## Thành phần tái sử dụng

Tái sử dụng và kết hợp thành phần tăng sức mạnh cho bạn với khả năng của cây thành phần, nền tảng của lớp hiển thị của React. Phần cuối cùng đề cập đến tính tái sử dụng, và giờ thì chúng ta sẽ xem làm thế nào để việc tái sử dụng thành phần Table và Search hoạt động trong trường hợp của ta. Ngay cả thành phần App cũng có thể tái sử dụng được, khi nó có thể được khởi tạo ở nơi nào đó khác nữa.

Hãy cùng định nghĩa một thành phần tái sử dụng nữa, một thành phần Button mà chúng ta sẽ cùng tái sử dụng thường xuyên:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class Button extends Component {
  render() {
    const {
      onClick,
      className,
      children,
    } = this.props;

    return (
      <button
        onClick={onClick}
        className={className}
        type="button"
      >
        {children}
      </button>
    );
  }
}
~~~~~~~~

Khai báo thành phần như này có vẻ thừa thãi, nhưng thực ra không hề. Chúng ta sử dụng thành phần `Button` thay vì một phần tử `button`, thứ mà chỉ bổ sung thêm `type="button"`. Có vẻ như đây không phải một bước tiến lớn, nhưng những việc này dành cho quá trình lâu dài, tuy nhiên. Tưởng tượng bạn có vài nút trong ứng dụng của bạn, và bạn muốn thay đổi thuộc tính, style, hay hành vi cho chỉ một nút. Nếu không dùng thành phần, bạn sẽ phải thay đổi (sửa lại) từng cái một. Thành phần Button đảm bảo rằng quá trình này chỉ là duy nhất, hoặc một nút để chỉnh sửa tất cả cùng lúc.

Bởi vì bạn đã có phần tử nút, bạn có thể sử dụng thành phần Button thay thế. Nó sẽ bỏ đi kiểu thuộc tính, bởi vì thành phần Button component xác định nó.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class Table extends Component {
  render() {
    const { list, pattern, onDismiss } = this.props;
    return (
      <div>
        {list.filter(isSearched(pattern)).map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
            <span>
# leanpub-start-insert
              <Button onClick={() => onDismiss(item.objectID)}>
                Dismiss
              </Button>
# leanpub-end-insert
            </span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Thành phần Button nhận vào thuộc tính `className` trong `props`. Thuộc tính `className` là một React khác có nguồn gốc từ thuộc tính class HTML. Chúng ta không truyền bất cứ `className` khi Button được sử dụng, mặc dù vậy. Một cách rõ ràng hơn trong thành phần Button `className` là không bắt buộc, bởi vì chúng ta sẽ gán một giá trị mặc định trong đối tượng destructuring.

{title="src/App.js",lang="javascript"}
~~~~~~~~
class Button extends Component {
  render() {
    const {
      onClick,
# leanpub-start-insert
      className = '',
# leanpub-end-insert
      children,
    } = this.props;

    ...
  }
}
~~~~~~~~

Giờ thì, mỗi khi thuộc tính `className` không được xác định rõ trong thành phần Button, giá trị sẽ là một chuối rỗng thay vì `undefined`.

### Luyện tập:

* Đọc thêm [how to pass props in React](https://www.robinwieruch.de/react-pass-props-to-component/)

## Khai báo thành phần

Hiện giờ chúng ta đã có 4 thành phần lớp ES6, nhưng ứng dụng vẫn có thể được cải thiện thêm bằng những thành phần hàm khuyết trạng thái như là một thay thế cho thành phần lớp ES6. Trước khi bạn chau chuốt lại những thành phần của bạn, hãy cùng giới thiệu những kiểu khác.

* **Thành phần hàm vô trạng thái** là những hàm mà nhận dữ liệu vào và trả dữ liệu ra. Dữ liệu vào là props, và dữ liệu ra là một khởi tạo thành phần trong JSX thuần. Đến đây, nó khá giống với thành phần lớp ES6. Tuy nhiên, thành phần hàm vô trạng thái là những hàm (mang tính chất hàm) và chúng không có trạng thái cục bộ (vô trạng thái). Bạn không thể truy cập hay cập nhật trạng thái với `this.state` hay `this.setState()` bởi không hề có đối tượng `this` nào. Thêm nữa, chúng không hề có phương thức vòng đời ngoại trừ cho phương thức `render()` mà sẽ được áp dụng ngầm vào thành phần hàm vô trạng thái. Bạn chưa hề học về những phương thức vòng đời, nhưng bạn đã sử dụng hai thứ là: `constructor()` và `render()`. Hàm sinh chạy duy nhất một lần trong vòng đời của thành phần, nơi mà phương thức lớp `render()` chạy một lần lúc đầu và mỗi khi thành phần thay đổi. Hãy ghi nhớ rằng thành phần hàm vô trạng thái không về có phương thức vòng đời, khi mà chúng ta đến với chương về phương thức vòng đời.

* **Thành phần lớp ES6** kế thừa từ thành phần React. Từ khóa `extend` kết nối các phương thức vòng đời, có sẵn trong API của thành phần React, với thành phần. Đây là lý do vì sao chúng ta có thể sử dụng phương thức lớp `render()`. Bạn cũng có thể lưu trữ và thao tùng trạng thái trong lớp ES6 sử dụng `this.state` và `this.setState()`.

* **React.createClass** được sử dụng trong phiên bản cũ hơn của React, và vẫn được sử dụng trong ứng dụng  JavaScript ES5 React. Nhưng [Facebook chỉ ra nó đã lỗi thời](https://reactjs.org/blog/2015/03/10/react-v0.13.html) với hương vị JavaScript ES6. Họ thậm chí thêm vào [cảnh báo lỗi thời tại phiên bản 15.5](https://reactjs.org/blog/2017/04/07/react-v15.5.0.html), vậy nên ta sẽ không sử dụng nó trong quyển sách này.

Khi quyết định khi nào sử dụng thành phần hàm vô trạng thái thay vì thành phần lớp ES6, một quy tắc tốt là sử dụng thành phần hàm vô trạng thái khi bạn không cần trạng thái cục bộ hoặc phương thức vòng đời của thành phần. Thường thì, chúng ta triển khai thành phần dưới dạng thành phần hàm vô trạng thái, nhưng một khi truy cập vào trạng thái hoặc phương thức vòng đời cần thiết, chúng ta phải sửa lại nó trở thành thành phần lớp ES6. Chúng ta bắt đầu cách khác xung quanh ứng dụng của ta cho quá trình học.

Quay trở lại với úng dụng, chúng ta sẽ thấy thành phần App component sử dụng trạng thái cục bộ, bởi vì nó cần phải giữ nguyên như một thành phần lớp ES6. Bà thành phần lớp ES6 khác là vô trạng thái, vậy chúng không cần truy cập vào `this.state` và `this.setState()`, và chúng không có phương thức vòng đời. Chúng ta sẽ sửa lại thành phần Search để trở thành thành phần hàm vô trạng thái. Thành phần Table và Button cần phải được sửa lại chính là bài luyện tập dành cho bạn.

{title="src/App.js",lang="javascript"}
~~~~~~~~
# leanpub-start-insert
function Search(props) {
  const { value, onChange, children } = props;
  return (
    <form>
      {children} <input
        type="text"
        value={value}
        onChange={onChange}
      />
    </form>
  );
}
# leanpub-end-insert
~~~~~~~~

`props` được truy cập trong hàm, và giá trị trả về là JSX; nhưng chúng ta có thể làm nhiều hơn với mã lệnh trên trong thành phần hàm vô trạng thái sử dụng ES6 destructuring. Luyện tập tốt là sử dụng nó trong hàm để  destructure `props`:

{title="src/App.js",lang="javascript"}
~~~~~~~~
# leanpub-start-insert
function Search({ value, onChange, children }) {
# leanpub-end-insert
  return (
    <form>
      {children} <input
        type="text"
        value={value}
        onChange={onChange}
      />
    </form>
  );
}
~~~~~~~~

Hãy nhớ rằng hàm mũi tên ES6 cho phép bạn giữ cho hàm của bạn ngắn gọn và để bạn loại bỏ đi thân khối của hàm. Trong một thân ngắn gọn, một trả về ngầm được gắn vào, giúp chúng ta loại bỏ từ khóa `return`. Bởi vì thành phần hàm vô trạng thái là hàm, nó có thể trở nên ngắn gọn hơn nữa như sau:

{title="src/App.js",lang="javascript"}
~~~~~~~~
# leanpub-start-insert
const Search = ({ value, onChange, children }) =>
  <form>
    {children} <input
      type="text"
      value={value}
      onChange={onChange}
    />
  </form>
# leanpub-end-insert
~~~~~~~~

Một bước cuối cùng là đặc biệt hữu dụng để bắt buộc props như là giá trị nhập vào và JSX như giá trị trả về. Vẫn vậy, bạn có thể  *làm gì đó* ở giữa bằng cách sử dụng thân khối trong hàm mũi tên ES6 của bạn:

{title="Code Playground",lang="javascript"}
~~~~~~~~
const Search = ({ value, onChange, children }) => {

  // do something

  return (
    <form>
      {children} <input
        type="text"
        value={value}
        onChange={onChange}
      />
    </form>
  );
}
~~~~~~~~

Hiện giờ bạn có thể có một thành phần hàm vô trạng thái nhẹ. khi bạn cần truy cập vào trạng thái cục bộ hoặc phương thức vòng đời, chúng ta có thể thay đổi nó thành thành phần lớp ES6. Khi sử dụng những thân khối, lập trình viện có ý định làm hàm của họ trở nên phức tạp hơn, nhưng việc bỏ đi thân khối giúp bạn tập trung vào đầu vào và đầu ra. JavaScript ES6 trong thành phần React làm cho thành phần dễ đọc và sạch đẹp hơn .

### Luyện tập:

* Sửa lại thành phần Table và Button trở thành thành phần hàm vô trạng thái
* Đọc thêm [ES6 class components and functional stateless components](https://reactjs.org/docs/components-and-props.html)

## Thành phần Style

Tại mục này, chúng ta sẽ thêm một chút giao diện cơ bản cho ứng dụng của chúng ta và thành phần sử dụng tệp *src/App.css* và *src/index.css*. Những tệp này nên có sẵn trong dự án của bạn, bởi lẽ bạn đã đẩy nhanh nó với *create-react-app*. Chúng nên được thêm vào tệp *src/App.js* và *src/index.js*  nữa. Những thứ dưới đây là CSS mà có thể sao chép và dán vào những tệp này, nhưng hãy tự do sử dụng của riêng bạn nếu bạn cảm thấy mình ổn với CSS.

Đầu tiên, style cho toàn bộ ứng dụng:

{title="src/index.css",lang="css"}
~~~~~~~~
body {
  color: #222;
  background: #f4f4f4;
  font: 400 14px CoreSans, Arial, sans-serif;
}

a {
  color: #222;
}

a:hover {
  text-decoration: underline;
}

ul, li {
  list-style: none;
  padding: 0;
  margin: 0;
}

input {
  padding: 10px;
  border-radius: 5px;
  outline: none;
  margin-right: 10px;
  border: 1px solid #dddddd;
}

button {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #dddddd;
  background: transparent;
  color: #808080;
  cursor: pointer;
}

button:hover {
  color: #222;
}

*:focus {
  outline: none;
}
~~~~~~~~

Tiếp theo, style cho thành phần của bạn trong tệp App:

{title="src/App.css",lang="css"}
~~~~~~~~
.page {
  margin: 20px;
}

.interactions {
  text-align: center;
}

.table {
  margin: 20px 0;
}

.table-header {
  display: flex;
  line-height: 24px;
  font-size: 16px;
  padding: 0 10px;
  justify-content: space-between;
}

.table-empty {
  margin: 200px;
  text-align: center;
  font-size: 16px;
}

.table-row {
  display: flex;
  line-height: 24px;
  white-space: nowrap;
  margin: 10px 0;
  padding: 10px;
  background: #ffffff;
  border: 1px solid #e3e3e3;
}

.table-header > span {
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 5px;
}

.table-row > span {
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 5px;
}

.button-inline {
  border-width: 0;
  background: transparent;
  color: inherit;
  text-align: inherit;
  -webkit-font-smoothing: inherit;
  padding: 0;
  font-size: inherit;
  cursor: pointer;
}

.button-active {
  border-radius: 0;
  border-bottom: 1px solid #38BB6C;
}
~~~~~~~~

Giờ thì chúng ta có thể sử dụng style này với một phần của những thành phần của chúng ta. Hãy nhớ sử dụng `className` thay vì `class` như là một thuộc tính HTML.

Đầu tiên, áp dụng nó vào thành phần lớp ES6 App:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
# leanpub-start-insert
      <div className="page">
        <div className="interactions">
# leanpub-end-insert
          <Search
            value={searchTerm}
            onChange={this.onSearchChange}
          >
            Search
          </Search>
# leanpub-start-insert
        </div>
# leanpub-end-insert
        <Table
          list={list}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
# leanpub-start-insert
      </div>
# leanpub-end-insert
    );
  }
}
~~~~~~~~

Tiếp theo, áp dụng nó trong thành phần hàm vô trạng thái Table:

{title="src/App.js",lang="javascript"}
~~~~~~~~
const Table = ({ list, pattern, onDismiss }) =>
# leanpub-start-insert
  <div className="table">
# leanpub-end-insert
    {list.filter(isSearched(pattern)).map(item =>
# leanpub-start-insert
      <div key={item.objectID} className="table-row">
# leanpub-end-insert
        <span>
          <a href={item.url}>{item.title}</a>
        </span>
        <span>{item.author}</span>
        <span>{item.num_comments}</span>
        <span>{item.points}</span>
        <span>
          <Button
            onClick={() => onDismiss(item.objectID)}
# leanpub-start-insert
            className="button-inline"
# leanpub-end-insert
          >
            Dismiss
          </Button>
        </span>
# leanpub-start-insert
      </div>
# leanpub-end-insert
    )}
# leanpub-start-insert
  </div>
# leanpub-end-insert
~~~~~~~~

Giờ thì ứng dụng và thành phần đã được style cơ bản với CSS. Ngoài ra, chúng ta biết JSX trộn với HTML và JavaScript, và chúng ta có thể sử dụng và giờ chúng ta có thể thêm CSS vào thứ trộn đó. Đó gọi là style một dòng, nơi bạn có thể định nghĩa đối tượng JavaScript và truyền chúng vào thuộc tính style của một phần tử.

Hãy giữ độ rộng cột của Table linh hoạt sử style một dòng.

{title="src/App.js",lang="javascript"}
~~~~~~~~
const Table = ({ list, pattern, onDismiss }) =>
  <div className="table">
    {list.filter(isSearched(pattern)).map(item =>
      <div key={item.objectID} className="table-row">
# leanpub-start-insert
        <span style={{ width: '40%' }}>
          <a href={item.url}>{item.title}</a>
        </span>
        <span style={{ width: '30%' }}>
          {item.author}
        </span>
        <span style={{ width: '10%' }}>
          {item.num_comments}
        </span>
        <span style={{ width: '10%' }}>
          {item.points}
        </span>
        <span style={{ width: '10%' }}>
          <Button
            onClick={() => onDismiss(item.objectID)}
            className="button-inline"
          >
            Dismiss
          </Button>
        </span>
# leanpub-end-insert
      </div>
    )}
  </div>
~~~~~~~~

Style giờ đã thành một dòng. Định nghĩa đối tượng style bên ngoài phần tử của bạn giúp nó sạch sẽ hơn.

{title="Code Playground",lang="javascript"}
~~~~~~~~
const largeColumn = {
  width: '40%',
};

const midColumn = {
  width: '30%',
};

const smallColumn = {
  width: '10%',
};
~~~~~~~~

Sau những thứ trên, chúng ta sử dụng chúng trong  cột: `<span style={smallColumn}>`. Có những lựa chon khác nhau và giải pháp về style trong React, nhưng CSS một dòng sạch sẽ chúng ta sử dụng để cung cấp cho hướng dẫn này. Tôi không muốn nêu ý kiến chủ quan tại đây, nhưng tôi muốn để cho bạn nhiều lựa chọn hơn. Bạn có thể đọc về chúng và tự sử dụng chúng:

* [styled-components](https://github.com/styled-components/styled-components)
* [CSS Modules](https://github.com/css-modules/css-modules) (read my short article on [how to use CSS modules in create-react-app](https://www.robinwieruch.de/create-react-app-css-modules/))
* [Sass](https://sass-lang.com/) (read my short article on [how to use Sass in create-react-app](https://www.robinwieruch.de/create-react-app-with-sass-support/))

Nhưng nếu bạn mới với React, tôi sẽ khuyên bạn sử dụng CSS thuần và style một dòng cho hiện tại.

{pagebreak}

Bạn đã học được những điều cơ bản về cách để viết ứng dụng riêng của bạn với React! Hãy cùng tóm tắt chương vừa rồi:

* **React**
  * Sử dụng `this.state` và `setState()` để quản lý trạng thái cục bộ của thành phần
  * Truyền hàm hoặc phương thức lớp vào phần tử xử lý của bạn
  * Sử dụng forms và events trong React để thêm tương tác
  * Dòng chảy dữ liệu vô hướng là một khái niệm quan trọng trong React
  * Vây quanh thành phần được kiểm soát
  * Kết hợp thành phần với con và tái sử dụng thành phần
  * Cú pháp và triển khai của thành phần lớp ES6 và thành phần hàm vô trạng thái
  * Bước đầu style thành phần của bạn
* **ES6**
  * Hàm mà gắn liền với lớp được gọi là phương thức lớp
  * Destructuring của đối tượng và mảng
  * Tham số mặc định
* **Tổng quan**
  * Hàm bậc cao

Một lần nữa, thật có lý khi nghỉ một chút, ghi nhớ bài học, và tự mình áp dụng chúng. Trải nghiệm với mã nguồn bạn đã viết ra cho đến nay. Mã nguồn của dự án này được tìm thấy tại [kho chính thức](https://github.com/the-road-to-learn-react/hackernews-client/tree/5.2).

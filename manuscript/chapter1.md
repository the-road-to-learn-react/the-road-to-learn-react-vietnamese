# Nhập môn React

Chương này chúng ta sẽ giới thiệu về React, một thư viện JavaScript cho việc trả về giao diện ở trang đơn và các ứng dụng di động, nơi mà tôi sẽ giải thích tại sao các nhà phát triển nên cân nhắc thêm thư viện React vào các công cụ của họ. Chúng ta sẽ đi sâu vào hệ sinh thái React, hãy cùng tạo ứng dụng React đầu tiên của bạn từ đầu mà không cần cấu hình bất cứ thứ gì. Cùng nhau, chúng ta sẽ giới thiệu về **JSX**, cú pháp cho React, và **ReactDOM**, từ đó bạn có thể hiểu về sức mạnh thực tế của React trong các ứng dụng web hiện đại.

## Xin chào, tên mình là React.

Các ứng dụng trang đơn (Single page applications) ([SPA](https://en.wikipedia.org/wiki/Single-page_application)) đã trở nên nổi tiếng nhanh chóng trong những năm gần đây, một frameworks như Angular, Ember, và Backbone cho phép các nhà phát triển JavaScript xây dựng ứng dụng web sử dụng những kỹ thuật vượt qua JavaScript thuần và JQuery. Những framework trên là một trong những SPAs đầu tiên, chúng tự xuất hiện vào giữ những năm 2010 và 2011, những có nhiều lựa chọn hơn cho phát triển trang đơn. Thế hệ đầu tiên của SPA frameworks ra đời ở mức độ cao cấp hơn, vì vậy những frameworks này cứng cáp hơn. React, ngược lại, giữ vững là một thư viện đầy sáng tạo được sử dụng bởi nhiều tập đoàn công nghệ lớn như [Airbnb, Netflix, and Facebook](https://github.com/facebook/react/wiki/Sites-Using-React).

React được ra đời bởi đội ngũ phát triển web của Facebook vào năm 2013 như một thư viện hiển thị (view library), điều làm nên chữ 'V' trong [MVC](https://en.wikipedia.org/wiki/Model–view–controller) (model view controller). Với một lớp hiển thị, nó cho phép bạn trả về các thành phần như là các phần tử có thể hiện thị trong trình duyệt, khi mà hệ sinh thái của nó giúp chúng ta xây dựng ứng dụng trang đơn. Trong khi thế hệ đầu tiên của frameworks cố gắng để giải quyết nhiều vấn đề một lúc, React chỉ xử dụng để xây dụng lớp hiển thị của bạn; đặc biệt, nó là một thư viện mà ở đó hiển thị là hệ thống phân cấp của các thành phần có thể kết hợp. Nếu bạn chưa từng nghe về mô hình MVC, đừng quá bận tâm về nó ,bởi vì nó chỉ ở đó để dấu mốc lịch sử của React vào bối cảnh cho những người đến từ những ngôn ngữ lập trình khác .

Với React, sự tập trung duy trì ở lớp hiển thị cho đến khi nhiều diện mạo đến với ứng dụng. Có những khối xây dựng dành cho SPA, thứ mà là cần thiệt để xây dựng một ứng dụng hoàn chỉnh. Chúng đi kèm với hai lợi ích:

* Bạn có thể học các khối xây dựng cùng lúc mà không cần phải hiểu tất cả cùng nhau. Ngược lại, một SPA framework cho bạn mọi khối xây dựng từ đầu. Quyển sách này tập trung vào React như là một khối xây dựng đầu tiên. Nhiều khối xây dựng cuối cùng sẽ đi theo.

* Tất cả các khối xây dựng đều có thể thay đổi được, điều này làm cho hệ sinh thái xung quanh React mang tính sáng tạo cao. Những giải pháp có thể cạnh tranh với nhau, và bạn có thể chọn giải pháp hợp lý nhất cho thử thách được đề ra.

React là một trong những sự lựa chọn tuyệt vời nhất để xây dựng những ứng dụng web hiện đại. Một lần nữa, nó chỉ cung cấp lớp hiển thị, những xung quanh hệ sinh thái tạo nên một framework hoàn toàn linh hoạt và dễ dàng thay đổi. React có một đơn giản API, một hệ sinh thái mạnh mẽ và tiến hóa, và một cộng đồng tuyệt vời.

### Luyện tập

Nếu bạn muốn tìm hiểu thêm về tại sao tôi chọn React, hoặc là muốn tìm hiểu sâu hơn về những chủ đề được nhắc đến ở trên, những bài viết sau mang đến cho bạn một cái nhìn sâu hơn:

* [Why I moved from Angular to React](https://www.robinwieruch.de/reasons-why-i-moved-from-angular-to-react/)
* [React's flexible ecosystem](https://www.robinwieruch.de/essential-react-libraries-framework/)
* [How to learn a framework](https://www.robinwieruch.de/how-to-learn-framework/)

## Yêu cầu

Tiếp túc với quyển sách này, bạn nên làm quen với những thứ cơ bản của phát triển web, ví dụ làm thế nào để sử dụng HTML, CSS, và JavaScript. Điều đó rất dễ hiểu làm thế nào [APIs](https://www.robinwieruch.de/what-is-an-api-javascript/) hoạt động, chúng sẽ được đề cập kỹ càng. Ngoài ra, Ngoài ra tôi khuyến khích các bạn tham gia vào nhóm chính thức [Slack Group](https://slack-the-road-to-learn-react.wieruch.com/) để trở thành một phần của sự phát triển cộng đồng React nơi bạn có thể học từ việc giúp đỡ những người khác.

### Editor and Terminal

Dành cho bài học này, bạn sẽ cần một trình soạn thảo văn bản hoặc một IDE và terminal (command line tool). Tôi đã cung cấp [một hướng dẫn cài đặt](https://www.robinwieruch.de/developer-setup/) Nếu bạn cần thêm sự giúp đỡ. Tùy chọn, chúng ta khuyên bạn giữ những dự án của bạn ở GitHub trong lúc thực hành các bài tập trong quyển sách này. Đây là một [hướng dẫn ngắn gọn](https://www.robinwieruch.de/git-essential-commands/) về làm thế nào sử dụng những công cụ này. Github có một khả năng quản lý phiên bản tuyệt vời, vì vậy bạn có thể theo dõi những thay đổi được tạo ra nếu bạn mắc lỗi hay bạn chỉ muốn có một cách trực tiếp để làm theo.

### Node and NPM

Cuối cùng, bạn sẽ cần một bản cài đặt của [node và npm](https://nodejs.org/en/). Cả hai được sử dụng để quản lý những thư viện bạn sẽ cần trong quá trình học. Trong cuốn sách này, bạn sẽ cài đặt những gói node bên ngoài qua npm (node package manager). Những gói node này có thể là thư viện hoặc cả một framework.

Bạn có thể kiểm tra phiên bản của node và npm trên giao diện dòng lệnh. Nếu bạn không nhận được bất cứ kết quả nào ở terminal, bạn cần phải cài đặt node và npm trước. Đây là những phiên bản của tôi vào thời điểm viết quyển sách này:

{title="Command Line",lang="text"}
~~~~~~~~
node --version
*v10.11.0
npm --version
*v6.4.1
~~~~~~~~

Nội dung bổ sung của phần này là một khóa học đầy đủ về node và npm. Nó không toàn diện, nhưng nó sẽ mang đến tất cả cả công cụ cần thiết. Nếu bạn đã quen thuộc với chúng, bạn có thể bỏ qua phần này.

The **node package manager** (npm) cài đặt những gói node bên ngoài từ giao diện dòng lệnh. Những gói này có thể là tập hợp của những hàm tiện ích, những thư viện, hay cả một framework, và chúng là những phụ thuộc cho ứng dụng của bạn. Bạn có thể hoặc là cài đặt những gói này vào thư mục gói node toàn cục của bạn, hoặc là vào thư mục dự án cục bộ của bạn.

Những gói node toàn cục có thể được truy cập từ bất cứ đâu trong terminal, và chỉ cần được cài đặt vào thư mục toàn cục một lần duy nhất. Cài đặt một gói toàn cục bằng cách nhập dòng lệnh sau vào terminal:

{title="Command Line",lang="text"}
~~~~~~~~
npm install -g <package>
~~~~~~~~

Cờ `-g` nói với npm cài đặt gói một cách toàn cục. Những gói cục bộ được sử dụng trong ứng dụng của bạn một cách mặc định. Dành cho mục đích của chúng ta, ta sẽ cài đặt React vào thư mục cục bộ qua terminal bằng cách nhập lệnh:

{title="Command Line",lang="text"}
~~~~~~~~
npm install react
~~~~~~~~

Gói được cài đặt sẽ tự động xuất hiện ở trong một thư mục có tên là *node_modules/* và sẽ được thêm vào tệp *package.json* cạnh bên những phụ thuộc khác.

Để khởi tạo thư mục *node_modules/*  và tệp *package.json* cho dự án của bạn, sử dụng dòng lệnh npm sau. Sau đó, bạn có thể cài đặt những gói cục bộ mới qua npm:

{title="Command Line",lang="text"}
~~~~~~~~
npm init -y
~~~~~~~~

Cờ `-y` khởi tạo tất cả những thiết lập mặc định trong tệp *package.json* của bạn. Sau khi khởi tạo dự án npm, bạn đã sẵn sàng để cài đặt những gói mới thông qua`npm install <package>`.

Tệp *package.json* cho phép bạn chia sẻ dự án của bạn với những nhà phát triển khác mà không chia sẻ tất cả các gói node. Nó sẽ bao gồm những tham chiếu tới tất cả các gói node dùng trong dự án của bạn, được gọi là **dependencies**. Những người dùng khác có thể sao chép dự án mà không chứa các phụ thuộc sử dụng tham chiếu trong *package.json*, nơi mà những tham chiếu này giúp cho dễ dàng cài đặt tất cả các gói sử dụng lệnh`npm install`. Một dòng lệnh`npm install sẽ lo hết phần cài đặt trong *package.json* và cài đặt chúng vào thư mục *node_modules/*.

Cuối cùng, còn một vài lệnh nữa để hoàn thiện về npm:

{title="Command Line",lang="text"}
~~~~~~~~
npm install --save-dev <package>
~~~~~~~~

Cờ `--save-dev`chỉ ra rằng gói node chỉ được sử dụng trong môi trường phát triển, nghĩa là nó sẽ không được sử dụng khi ứng dụng được triển khai trên một máy chủ hay được sử dụng trong phiên bản sản phẩm. Nó vô cùng hữu dụng để kiểm tra một ứng dụng sử dụng gói node, nhưng muốn loại trừ nó khỏi môi trường sản phậm của bạn.

Các bạn có thể muốn sử dụng trình quản lý gói khác để làm việc với gói node trong ứng dụng của bạn. **Yarn** là một trình quản lý phụ thuộc mà làm việc tương tự như **npm**. Nó có danh sách dòng lệnh riêng của chính nó, nhưng bạn vẫn cần phải truy cập vào cùng npm registry. Yarn được tạo ra để giải quyết những vấn đề mà npm không thể, nhưng cả hai công cụ cùng phát triển để chỉ ra rằng thứ nào sẽ làm tốt hơn ngày nay.

### Luyện tập:

* Cài đặt một dự án npm bằng những dòng lệnh sử dụng terminal:
  * Tạo một thư mục với lệnh `mkdir <folder_name>`
  * Chuyển đến thư mục với `cd <folder_name>`
  * Thực hiện `npm init -y` or `npm init`
  * Cài một gói cục bộ như React với `npm install react`
  * Kiểm tra *package.json* và thư mục *node_modules/* 
  * Thử gỡ bỏ và cài đặt lại gói node *react* 
* Đọc thêm [npm](https://docs.npmjs.com/)
* Đọc thêm [yarn](https://yarnpkg.com/en/docs/) trình quản lý gói

## Cài đặt

Có rất nhiều cách tiếp cận để bắt đầu với ứng dụng React. Thứ đầu tiên chúng ta sẽ khám phá là một CDN, viết tắt cho [content delivery network](https://en.wikipedia.org/wiki/Content_delivery_network). Đừng quá lo lắng về CDNs bây giờ, bởi vì bạn sẽ không sử dụng chúng trong quyển sách này, nhưng rất có lý để giải thích chúng một cách ngắn gọn. Rất nhiều công ty sử dụng CDNs để  lưu trữ tệp công khai cho người dùng của họ. Một trong những tệp này như là React, bởi lẽ thư viện được nén lại của React chỉ là một tệp JavaScript *react.js* .

Để bắt đầu với React sử dụng một CDN, tìm thẻ `<script>` ở trong trang web HTML và trỏ tới đường dẫn CDN. Bạn sẽ cần hai thư viện: *react* và *react-dom*.

{title="Code Playground",lang="javascript"}
~~~~~~~~
<script
  crossorigin
  src="https://unpkg.com/react@16/umd/react.development.js"
></script>

<script
  crossorigin
  src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"
></script>
~~~~~~~~

Bạn có thể cũng sẽ nhận vào ứng dụng của bạn bằng cách khởi tạo một dự án node. Với một tệp *package.json* , bạn có thể cài đặt *react* và *react-dom* từ giao diện dòng lệnh. Tuy nhiên, thư mục cần phải được khởi tạo như là một dự án npm sử dụng lệnhnpm init -y` với một tệp *package.json* . Bạn có thể cài đặt những gói node với npm:

{title="Command Line",lang="text"}
~~~~~~~~
npm install react react-dom
~~~~~~~~

Phương pháp này thường được sử dụng để thêm React vào một ứng đã tồn tại được quản lý bởi npm.

Bạn có thể cũng phải làm việc với [Babel](http://babeljs.io/) để giúp cho ứng dụng của bạn nhận ra được JSX (the React syntax) và JavaScript ES6. Babel biên dịch mã của bạn, nó chuyển mã thành JavaScript thuần--thứ mà hầu hết trình duyệt có thể  thông dịch JavaScript ES6 và JSX. Bởi vì quá trình cài đặt phức tạp này, Facebook giới thiệu *create-react-app* như là một giải pháp React không cần cấu hình. Phần tiếp theo sẽ cho bạn thấy làm thế nào để cài đặt ứng dụng của bạn bằng công cụ cực nhanh này.

### Luyện tập:

* Đọc thêm [React installations](https://reactjs.org/docs/getting-started.html)

## Cài đặt không cần cấu hình

Ở Road to learn React, chúng ta sẽ sử dụng [create-react-app](https://github.com/facebookincubator/create-react-app) để đẩy nhanh ứng dụng của chúng ta. Đó là một ý tưởng gói mở đầu không cần cấu hình cho React được giới thiệu bởi Facebook vào 2016, [recommended for beginners by 96% of React users](https://twitter.com/dan_abramov/status/806985854099062785). Trong *create-react-app* công cụ và cấu hình thực hiện ngầm, trong khi chúng ta có thể tập trung triển khai ứng dụng.

Để bắt đầu, cài đặt gói này vào những gói node toàn cục của bạn, điều này sẽ giữ nó luôn có sẵn trong giao diện dòng lệnh để đẩy nhanh những dự án React mới:

{title="Command Line",lang="text"}
~~~~~~~~
npm install -g create-react-app
~~~~~~~~

Bạn có thể kiểm tra phiên bản của *create-react-app* để chắc chắn cài đặt đã thành công trong giao diện dòng lệnh:

{title="Command Line",lang="text"}
~~~~~~~~
create-react-app --version
*v2.0.2
~~~~~~~~

Ngay bây giờ bạn đã sẵn sàng để đẩy nhanh dự án React đầu tiên của bạn. Ví dụ sẽ liên quan đến *hackernews*, nhưng bạn có thể chọn bất kỳ tên nào bạn muốn. Trước tiên, chuyển tới thư mục:

{title="Command Line",lang="text"}
~~~~~~~~
create-react-app hackernews
cd hackernews
~~~~~~~~

Bây giờ bạn có thể mở ứng dụng trong trình soạn thảo. Đây là cấu trúc thư mục, hoặc một biến thể của nó phụ thuộc vào phiên bản *create-react-app* , nên xuất hiện:

{title="Folder Structure",lang="text"}
~~~~~~~~
hackernews/
  README.md
  node_modules/
  package.json
  .gitignore
  public/
    favicon.ico
    index.html
    manifest.json
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
    serviceWorker.js
~~~~~~~~

Đây là một phần chia nhỏ của thư mục và tệp:

* **README.md:** phần mở rộng .md chỉ ra tệp này là một tệp markdown. Markdown được sử dụng như là một ngôn ngữ đánh dấu siêu nhẹ với cú pháp định dạng văn bản giản dị. Rất nhiều dự án mã nguồn đi kèm với tệp *README.md* để đưa ra cho bản những chỉ dẫn cơ bản về dự án. Khi đưa dự án lên một nền tảng như GitHub, tệp *README.md* thường hiển thị thông tin về nội dung được bao gồm trong kho. Bởi lẽ bạn sử dụng *create-react-app*, tệp *README.md* của bạn sẽ giống hệt với bản chính thức [create-react-app GitHub repository](https://github.com/facebookincubator/create-react-app).

* **node_modules/:** Thư mục này chứa các gói node được cài đặt qua npm. Vì bạn sử dụng *create-react-app*, thư mục của bạn nên sẵn có một vài thứ của node modules cài đặt cho bạn. Bạn sẽ hiếm khi cần động đến thư mục này, bởi lẽ những gói node được cài đặt một cách chung và cài đặt với npm từ giao diện dòng lệnh.

* **package.json:** Tệp này cho bạn thấy danh sách của những gói node phụ thuộc và những cầu hình khác của dự án.

* **.gitignore:** Tệp này sẽ hiển thị tất cả những tệp và thư mục không nên thêm vào kho git của bạn khi sử dụng git; những tệp và thư mục chỉ nên xuất hiện trong dự án cục bộ của bạn. Ví dụ như thư mục *node_modules/* . Chia sẻ tệp *package.json*  đã là đủ với người khác, bởi vậy họ có thể tự cài đặt các phụ thuộc với lệnh`npm install` mà không cần đến những thư mục phụ thuộc của bạn.

* **public/:** Thư mục này chứa những tệp phát triển, như là *public/index.html*. Tệp index hiển thị ở localhost:3000 khi phát triển ứng dụng của bạn. Bản mãu chăm sóc những tệp index liên quan với tất cả các mã lệnh trong *src/*.

* **build/** Thư mục này được tạo ra khi bạn xây dựng dự án cho phiên bản sản phẩm, nó nắm giữ tất cả những tệp sản phẩm. khi xây dựng dự án của bạn cho phiên bản sản phẩm, tất cả mã nguồn của bạn ở trong  *src/* và *public/* được nén lại và đặt trong thư mục build.

* **manifest.json** và **serviceWorker.js:** Những tệp này không được sử dụng trong dự án này, nên bạn có thể  tạm thời bỏ qua chúng.

Ngay khi bắt đầu, tất cả những gì bạn cần tập trung ở thư mục *src/*. Những dòng chính tập trung ở trong tệp *src/App.js* thứ mà được sử dụng để triển khai những thành phần React. Nó sẽ được sử dụng để triển khai ứng dụng của bạn, nhưng sau này bạn có thể muốn chia nhỏ những thành phần của bạn ra nhiều tệp khác, nơi mà mỗi tệp duy trì một hoặc nhiều thành phần của riêng nó.

Thêm vào đó, bạn có thể tìm thấy tệp *src/App.test.js* cho quá trình kiểm thử của bạn, và một tệp*src/index.js* như là điểm vào của thế giới React. Bạn sẽ bắt đầu làm quen với cả hai tệp trong chương tiếp theo. Còn có tệp *src/index.css* và một tệp *src/App.css* để style cho ứng dụng và thành phần chung của bạn, thứ mà đi kèm với những style mặc định khi bạn mở chúng. Bạn sẽ thay đổi chúng ngay sau đây.

Ứng dụng *create-react-app* là một dự án npm bạn có thể sử dụng để cài đặt và gỡ bỏ những gói node. Nó đi kèm với những lệnh npm sau đây cho giao diện dòng lệnh của bạn:

{title="Command Line",lang="text"}
~~~~~~~~
# Runs the application in http://localhost:3000
npm start

# Runs the tests
npm test

# Builds the application for production
npm run build
~~~~~~~~

Những lệnh được định nghĩa trong tệp *package.json* của bạn, và dự án React cơ bản đã được xây dựng nhanh chóng. Những luyện tập dưới đây sẽ cho phép bạn cuối cùng chạy thử ứng dụng của bạn trên một trình duyệt.

### Luyện tập:

* `npm start` ứng dụng của bạn và ghé thăm ứng dụng trong trình duyệt (Thoát khỏi lệnh bằng cách nhấn Control + C)
* Chạy lệnh `npm test` 
* Chạy lệnh `npm run build` và kiểm tra lại xem thư mục *build/* đã được thêm vào dự án của bạn  (bạn có thể xóa nó đi sau). Chú ý rằng thư mục build có thể được sử dụng lát nữa tại [triển khai ứng dụng của bạn](https://www.robinwieruch.de/deploy-applications-digital-ocean/))
* Làm quen với cấu trúc thư mục
* Kiểm tra lại nội dung tệp
* Đọc thêm [npm scripts and create-react-app](https://github.com/facebookincubator/create-react-app)

## Giới thiệu về JSX

Giờ thì chúng ta sẽ chính thức làm quen với JSX, cú pháp trong React. Như đã được nhắc đến trước đó, *create-react-app* đã đẩy nhanh tốc độ phát triển ứng dụng của bạn, và tất cả các tệp đã đi kèm với phần triển khai mặc định của chúng. Hiện giờ, tệp duy nhất chúng ta sẽ thay đổi là *src/App.js* .

{title="src/App.js",lang="javascript"}
~~~~~~~~
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;
~~~~~~~~

Đừng lo lắng nếu bạn bối rối với the import/export dòng và khai báo lớp. Đây là những tính năng mới của ES6 chúng ta sẽ ghé thăm chúng ngay trong chương tiếp theo.

Trong tệp này bạn nên thấy một **React ES6 class component** với tên App. Đây là thành phần khai báo thành phần. Sau khi bạn khai báo một thành phần, bạn có thể sử dụng nó như là một như một phần tử ở bất cứ đầu trong ứng dụng của bạn. Nó sẽ tạo ra một **instance** của **component** hay, nói cách khác, thành phần đã được khởi tạo.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// component declaration
class App extends Component {
  ...
}

// component usage (also called instantiation for a class)
// creates an instance of the component
<App />
~~~~~~~~

**Phần tử** trả về được định ra trong phương thức`render(). Những thành phần bạn khởi tạo trước đó được tạo nên bởi các phần tử, vậy nên nó rất quan trọng để hiểu sự khác biệt giữa một thành phần, một khởi tạo của thành phần, và một phần tử.

Bạn nên thấy nơi mà thành phần App được khởi tạo, hoặc là bạn không thể thấy kết của được trả về ở trình duyệt. Thành phần App chỉ được khai báo, chứ không được sử dụng. Bạn có thể khởi tạo thành phần ở bất cứ đầu trong JSX của bạn với`<App />`. Lát nữa bạn sẽ thấy nơi điều kỳ diệu xảy ra trong ứng dụng này.

Nội dung của khối được trả về có thể trông khá giống như HTML, nhưng thực ra nó lại là JSX. JSX cho phép bạn trộn HTML và JavaScript. Nó rất mạnh mẽ, nhưng nó dễ  gây hiểu lầm khi bạn dừng để tách biệt hai ngôn ngữ. Nó là một ý tưởng hay để bắt đầu sử dụng HTML cơ bản trong JSX của bạn. Mở tệp `App.js` và xóa bỏ những mã HTML không cần thiết như sau:

{title="src/App.js",lang="javascript"}
~~~~~~~~
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <h2>Welcome to the Road to learn React</h2>
      </div>
    );
  }
}

export default App;
~~~~~~~~

Bây giờ, bạn chỉ cần trả về  HTML trong phương thức`render()`mà không cần một chút JavaScript nào. Hãy cùng nhau định nghĩa "Welcome to the Road to learn React" như một biến. Một biến được thiết lập trong  by cặp ngoặc nhọn.

{title="src/App.js",lang="javascript"}
~~~~~~~~
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
# leanpub-start-insert
    var helloWorld = 'Welcome to the Road to learn React';
# leanpub-end-insert
    return (
      <div className="App">
# leanpub-start-insert
        <h2>{helloWorld}</h2>
# leanpub-end-insert
      </div>
    );
  }
}

export default App;
~~~~~~~~

Khởi chạy ứng dụng của bạn từ giao diện dòng lệnh với lệnh npm start` để kiểm tra lại nhưng thay đổi bạn vừa thực hiện.

Có lẽ bạn đã nhận ra thuộc tính`className. Nó tương tự như thuộc tính`class` chuẩn trong HTML. JSX đã thay đổi một số thuộc tính bên trong của HTML, nhưng bạn có thể tìm thấy tất cả chúng tại đây [supported HTML attributes in React's documentation](https://reactjs.org/docs/dom-elements.html#all-supported-html-attributes), tất cả chúng tuân theo quy tắc camelCase. Trên con đường học React, hay mong đợi để sử dụng nhiều hơn nhưng thuộc tính cụ thể của JSX.

### Luyện tập:

* Định nghĩa nhiều biến hơn và trả về chúng trong JSX
  * Sử dụng một đối tượng phúc tạp để đại diện cho người dùng với họ và tên
  * Render the user properties in JSX
* Đọc thêm [JSX](https://reactjs.org/docs/introducing-jsx.html)
* Đọc thêm [React components, elements and instances](https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html)

## ES6 const và let

Chú ý rằng chúng ta đã khai báo biến`helloWorld`với`var`. JavaScript ES6 đi kèm với hai cách khai báo biến khác: `const` và `let`. Với JavaScript ES6, bạn sẽ hiếm khi thấy`var` nữa. Một biến được khai báo với`const`không thể bị gán lại hay khai báo lại nữa, và không thể bị thay đổi hay sửa đổi. Một khi nó đã được gán giá trị, bạn không thể thay đổi nó:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// not allowed
const helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
~~~~~~~~

Conversely, a variable declared with `let` can be modified:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// allowed
let helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
~~~~~~~~

**MẸO:** Khai báo biến với`let` nếu bạn nghĩ bạn sẽ muốn gán lại giá trị cuả nó sau.

Chú ý rằng một biến được khai báo trực tiếp với `const` không thể bị chỉnh sửa. Tuy nhiên, khi biến này là một mảng hoặc một đối tượng, giá trị của nó nắm giữ sẽ vẫn được cập nhật một cách gián tiếp qua:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// allowed
const helloWorld = {
  text: 'Welcome to the Road to learn React'
};
helloWorld.text = 'Bye Bye React';
~~~~~~~~

Có khá nhiều ý kiến khác nhau về việc khi nào thì nên sử dụng *const* và khi nào thì nên sử dụng *let*. Tôi sẽ khuyên các bạn nên sử dụng`const` bất cứ khi nào có thể để thể hiện ý định giữ cấu trúc dữ liệu của bạn bất biến, vậy nên bạn chỉ cần lo lắng về giá trị được chứa trong mảng và đối tượng. Tính bất biến được vây quanh trong hệ sinh thái của React, vậy nên `const` nên trở thành lựa chọn mặc định để định nghĩa một biến, mặc dù nó không hoàn toàn là bất biến, nhưng nó chỉ gán giá trị duy nhất một lần. Nó cho bạn thấy ý định không thay đổi (gán lại giá trị) của biến ngay cả khi nội dung của nó có thể bị thay đổi.

{title="src/App.js",lang="javascript"}
~~~~~~~~
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
# leanpub-start-insert
    const helloWorld = 'Welcome to the Road to learn React';
# leanpub-end-insert
    return (
      <div className="App">
        <h2>{helloWorld}</h2>
      </div>
    );
  }
}

export default App;
~~~~~~~~

Trong ứng dụng của bạn, chúng ta sẽ sử dụng `const` và `let` thay vì `var` cho phần còn lại của cuốn sách.

### Luyện tập:

* Đọc thêm [ES6 const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
* Đọc thêm [ES6 let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
* Hiểu thêm về tính bất biến của cấu trúc dữ liệu:
  * Tại sao chúng quan trọng trong lập trình?
  * Tại sao chúng được vây quanh trong React và hệ sinh thái của nó?

## ReactDOM

Thành phần App được xác định trong điểm đầu vào thế giới React : tệp *src/index.js* .

{title="src/index.js",lang="javascript"}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
~~~~~~~~

`ReactDOM.render()` sử dụng một nốt trong HTML của bạn để thay thế nó với JSX. Đó là một cách để tích hợp React với bất kỳ ứng dụng bên ngoài nào một cách dễ dàng, và bạn có thể sử dụng`ReactDOM.render()` nhiều lần trong ứng dụng của bạn. Bạn có thể sử dụng nó để đẩy nhanh cú pháp JSX đơn giản, một thành phần React, nhiều thành phần React, hay thậm chí toàn bộ ứng dụng. Ở trong một ứng dụng thuần React, bạn chỉ nên sử dụng nó một lần để tạo ra cây thành phần nhanh chóng.

`ReactDOM.render()` nhận vào hai tham số. Tham số thứ nhất để trả về  JSX. Tham số thứ hai xác định nơi mà ứng dụng kết nối với HTML của bạn. Nó nhận vào một phần tử với`id='root'`, được tìm thấy trong tệp *public/index.html* .

{title="Code Playground",lang="javascript"}
~~~~~~~~
ReactDOM.render(
  <h1>Hello React World</h1>,
  document.getElementById('root')
);
~~~~~~~~

Trong quá trình triển khai, `ReactDOM.render()` nhận vào thành phần App, mặc dù nó có thể truyền qua  JSX đơn giản. Nó không nên yêu cầu một khởi tạo của thành phần.

### Luyện tập:

* Mở *public/index.html* để xem nơi mà ứng dụng React kết nối với HTML của bạn
* Đọc thêm [rendering elements in React](https://reactjs.org/docs/rendering-elements.html)

## Hot Module Replacement

Hot Module Replacement có thể được sử dụng trong *src/index.js* để cải thiện trải nghiệm của nhà phát triển. Mặc định, *create-react-app* sẽ khiến cho trình duyệt làm mới lại trang ngay khi mã nguồn của nó được sửa đổi. Thử sử dụng nó bằng cách thay đổi biến `helloWorld` trong tệp *src/App.js* , nó sẽ khiến trình duyệt làm mới lại trang. Có một cách tốt hơn để làm việc với sự thay đổi mã nguồn trong quá trình phát triển, tuy nhiên.

Hot Module Replacement (HMR) là một công cụ để tải lại ứng dụng của bạn ở trình duyệt mà không cần làm mới lại trang. Bạn có thể kích hoạt nó trong *create-react-app* bằng cách theo cấu hình sau vào tệp *src/index.js* :

{title="src/index.js",lang="javascript"}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);

# leanpub-start-insert
if (module.hot) {
  module.hot.accept();
}
# leanpub-end-insert
~~~~~~~~

Một lần nữa, hãy thử thay đổi biến helloWorld trong tệp *src/App.js*. Trình duyệt sẽ không làm mới, nhưng ứng dụng sẽ tải lại và hiện thị kết quả chính xác. HMR đi kèm với những lợi ích sau:

Tưởng tượng bạn đang gỡ lỗi trong mã của bạn với`console.log()`. Những dòng này sẽ nằm trong console nhà phát triển của bạn, mặc dù bạn thay đổi mã của bạn, bởi vì trình duyệt không làm mới trang nữa. Trong một ứng dụng lớn, làm mới lại trang sẽ làm giảm tính sản phẩm; HMR loại của bỏ trở ngại này bằng cách loại bỏ thời gian tăng bị mất để trình duyệt tải lại.

Lợi ích tuyệt vời nhất của HMR đó là bạn có thể giữ trạng thái của ứng dụng ngay sau khi ứng dụng tải lại. Ví dụ, giả sử bạn có một cửa sổ hội thoại hoặc một hộp thoại với nhiều bước trong ứng dụng của bạn, và bạn đang ở bước thứ 3. nếu không có HMR, bạn thay đổi mã nguồn và trình duyệt làm mới lại trang. Bạn sẽ phải mở lại hộp thoại từ đầu và quay trở lại từ bước 1 đến bước 3 mỗi lần. với HMR hộp thoại của bạn giữ nguyên đang mở ở bước 3, giúp cho bạn có thể gỡ lỗi từ vị trí chính xác bạn đang làm việc. tiết kiệm được thời gian từ việc tải trang, điều này có thể giúp HMR trở thành công cụ vô giá cho các nhà phát triển React.

### Luyện tập:

* Thay đổi mã nguồn của bạn *src/App.js* một vài lần để thấy HMR hoạt động
* Xem 10 phút đầu với [Live React: Hot Reloading with Time Travel](https://www.youtube.com/watch?v=xsSnOQynTHs) bởi Dan Abramov

## JavaScript phức tạp trong JSX

Đến đây, bạn đã trả về được một vài biến cơ bản bản trong JSX của bạn. Giờ thì, chúng ta sẽ trả về một danh sách các vật phẩm. Danh sách sẽ chứa dữ liệu mẫu ngay từ đầu, nhưng sau này chúng ta sẽ học cách nhận dữ liệu từ một API bên ngoài.

Trước tiên bạn cần định nghĩa danh sách các vật phẩm:

{title="src/App.js",lang="javascript"}
~~~~~~~~
import React, { Component } from 'react';
import './App.css';

# leanpub-start-insert
const list = [
  {
    title: 'React',
    url: 'https://reactjs.org/',
    author: 'Jordan Walke',
    num_comments: 3,
    points: 4,
    objectID: 0,
  },
  {
    title: 'Redux',
    url: 'https://redux.js.org/',
    author: 'Dan Abramov, Andrew Clark',
    num_comments: 2,
    points: 5,
    objectID: 1,
  },
];
# leanpub-end-insert

class App extends Component {
  ...
}
~~~~~~~~

Dự liệu mẫu thể hiện những thông tin chúng ta sẽ nhận từ API sau này. Những vật phẩm trong danh sách đều có tiêu đề, một url, và một tác giả, cũng như một ID, điểm (thử chỉ ra bài báo này nổi tiếng như nào), và một số lượng bình luận.

Giờ thì bạn có thể sử dụng [built-in JavaScript map functionality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) trong JSX, thứ sẽ lặp qua danh sách của vật phẩm để hiển thị chúng dựa trên những thuộc tính cụ thể. Một lần nữa, chúng ta sử dụng ngoặc nhọn để đóng gói biểu thức JavaScript trong JSX:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {
  render() {
    return (
      <div className="App">
# leanpub-start-insert
        {list.map(function(item) {
          return <div>{item.title}</div>;
        })}
# leanpub-end-insert
      </div>
    );
  }
}

export default App;
~~~~~~~~

Sử dụng JavaScript cùng HTML trong JSX thật là vô cùng mạnh mẽ. Cho mỗi công việc khác nhau bạn có thể sử dụng map để chuyển đổi một danh sách các sản phẩm thành một thứ khác. Lần này, chúng ta sẽ sử dụng map để chuyển đổi thành những phần tử HTML.

{title="Code Playground",lang="javascript"}
~~~~~~~~
const array = [1, 4, 9, 16];

// pass a function to map
const newArray = array.map(function (x) { return x * 2; });

console.log(newArray);
// expected output: Array [2, 8, 18, 32]
~~~~~~~~

Đến đây, Tiêu đề là thứ duy nhất được hiển thị cho mỗi sản phậm. Hãy cùng thử nhiều hơn với các thuộc tính khác:

{title="src/App.js",lang="javascript"}
~~~~~~~~
class App extends Component {
  render() {
    return (
      <div className="App">
# leanpub-start-insert
        {list.map(function(item) {
          return (
            <div>
              <span>
                <a href={item.url}>{item.title}</a>
              </span>
              <span>{item.author}</span>
              <span>{item.num_comments}</span>
              <span>{item.points}</span>
            </div>
          );
        })}
# leanpub-end-insert
      </div>
    );
  }
}

export default App;
~~~~~~~~

Chú ý rằng hàm`map`cùng dòng với JSX của bạn. Mỗi thuộc tính của sản phẩm được hiển thị với một thẻ `<span>, và thuộc tính url của những sản phẩm được sử dụng trong thuộc tính `href` của thẻ anchor .

React sẽ hiển thị mỗi sản phẩm, nhưng bạn vẫn cần phải làm thêm môt việc nữa để giúp React thức tỉnh toàn bộ khả năng tiềm ẩn của nó . Bằng cách gán một thuộc tính khóa cho mỗi phần tử của danh sách, React có thể nhận diện và chỉnh sữa những sản phẩm khi danh sách thay đổi. Những sản phẩm danh sách mẫu này đi kèm với một ID:

{title="src/App.js",lang="javascript"}
~~~~~~~~
{list.map(function(item) {
  return (
# leanpub-start-insert
    <div key={item.objectID}>
# leanpub-end-insert
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
  );
})}
~~~~~~~~

Chắc chắn rằng thuộc tính khóa là một ID ổn định. Tránh sử dụng số đếm của phần tử trong mảng, bởi lẽ số đếm của mảng là không ổn định. Ví dụ nếu danh sách thay đổi trật tự của chính nó, React sẽ không sẽ xác định được thuộc tính của phần tử.

{title="src/App.js",lang="javascript"}
~~~~~~~~
// don't do this
{list.map(function(item, key) {
  return (
    <div key={key}>
      ...
    </div>
  );
})}
~~~~~~~~

Khởi động ứng dụng của bạn trên trình duyệt, và bạn nên thấy cả hai sản phẩm của danh sách được hiển thị.

### Luyện tập:

* Đọc thêm [React lists and keys](https://reactjs.org/docs/lists-and-keys.html)
* Tóm tắt [standard built-in array functionalities in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/)
* Dùng nhiều biểu thức JavaScript expressions trong cú pháp JSX của chính bạn

## ES6 Hàm mũi tên

JavaScript ES6 mang đến những biểu thức hàm mũi tên, cú pháp ngắn gọn hơn biểu thức hàm bình thường.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// function declaration
function () { ... }

// arrow function declaration
() => { ... }
~~~~~~~~

Bạn có thể xóa bỏ dấu ngoặc ở trong hàm mũi tên nếu nó chỉ có một tham số, nhưng bạn cần phải giữ lại dấu ngoặc nếu nó nhận vào nhiều tham số:

{title="Code Playground",lang="javascript"}
~~~~~~~~
// allowed
item => { ... }

// allowed
(item) => { ... }

// not allowed
item, key => { ... }

// allowed
(item, key) => { ... }
~~~~~~~~

Bạn có thể viết hàm `map` một cách ngắn gọn hơn với hàm mũi tên ES6:

{title="src/App.js",lang="javascript"}
~~~~~~~~
# leanpub-start-insert
{list.map(item => {
# leanpub-end-insert
  return (
    <div key={item.objectID}>
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
  );
})}
~~~~~~~~

Bạn có thể bỏ đi phần *thân khối*, dấu ngoặc nhọn, với hàm mũi tên ES6. Ở trong một *thân ngắn gọn*, một trả về ngầm đã được gắn vào; vì vậy, bạn có thể xóa bỏ `return`. Điều này sẽ được dùng khá thường xuyên trong cuốn sách này, hãy chắc chắn hiểu rõ sự khác biệt giữ thân khối và thân ngắn gọn khi sử dụng hàm mũi tên.

{title="src/App.js",lang="javascript"}
~~~~~~~~
# leanpub-start-insert
{list.map(item =>
# leanpub-end-insert
  <div key={item.objectID}>
    <span>
      <a href={item.url}>{item.title}</a>
    </span>
    <span>{item.author}</span>
    <span>{item.num_comments}</span>
    <span>{item.points}</span>
  </div>
# leanpub-start-insert
)}
# leanpub-end-insert
~~~~~~~~

JSX của bạn nên trông ngắn gọn và dễ đọc hơn bây giờ, vì nó lược bỏ `function`, dấu ngoặc nhọn, và return.

### Luyện tập:

* Đọc thêm [ES6 arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## ES6 Lớp

JavaScript ES6 mang đến cho chúng ta lớp, thứ mà thường được sử dụng trong lập trình hướng đối tượng. JavaScript, luôn luôn linh hoạt trong khuynh hướng lập trình của nó, nó cho phép lập trình hàm và lập trình hướng đối tượng làm việc cùng nhau.

Trong khi React vây quanh lập trình hàm, ví dụ. cấu trúc dữ liệu bất biến và hàm hợp, lớp được dùng để khai báo thành phần lớp ES6. React kết hợp các điểm mạnh của cả hai khuynh hướng lập trình.

Xem qua lớp Developer dưới đây để kiểm tra lớp JavaScript ES6 không có thành phần.

{title="Code Playground",lang="javascript"}
~~~~~~~~
class Developer {
  constructor(firstname, lastname) {
    this.firstname = firstname;
    this.lastname = lastname;
  }

  getName() {
    return this.firstname + ' ' + this.lastname;
  }
}
~~~~~~~~

Một lớp có hàm khởi tạo để làm cho nó mang tính khởi tạo hơn. Hàm khởi tạo nhận vào các tham số và gán chúng vào lớp khởi tạo. Một lớp có thể định nghĩa nhiều hàm. Bởi những hàm này được gắn với lớp, chúng được gọi là phương thức, hoặc phương thức lớp.

Lớp Developer chỉ khai báo bằng class chúng ta sử dụng ở đây, bạn có thể tạo ra nhiều khởi tạo của lớp bằng cách gọi nó. Nó tương tự như lớp thành phần ES6, thứ có một khai báo, nhưng bạn phải sử dụng nó một chỗ nào đó để khởi tạo nó:

{title="Code Playground",lang="javascript"}
~~~~~~~~
const robin = new Developer('Robin', 'Wieruch');
console.log(robin.getName());
// output: Robin Wieruch
~~~~~~~~

React sử dụng những lớp JavaScript ES6 cho lớp thành phần ES6, thứ mà bạn đã từng sử dụng ít nhất một lần:

{title="src/App.js",lang="javascript"}
~~~~~~~~
import React, { Component } from 'react';

...

class App extends Component {
  render() {
    ...
  }
}
~~~~~~~~

Khi bạn khai báo thành phần component nó mở rộng từ một thành phần khác. Trong lập trình hướng đối tượng, khái niệm "extends" liên quan đến nguyên lý kế thừa, có nghĩa là chức năng có thể được truyền từ một lớp đến lớp khác. Lớp App mở rộng từ lớp thành phần, nghĩa là nó kể thừa chức năng từ lớp thành phần. Lớp thành phần được sử dụng để mở rộng lớp ES6 cơ bản tới lớp thành phần ES6. Nó có đầy đủ các chức năng một thành phần React cần. Phương thức trả về là một hàm bạn đã sử dụng. Bạn sẽ tìm hiểu về những phương thức lớp thành phần khác khi chúng ta tiếp tục.

Lớp thành phần `Component` đóng gói tất cả những triển khai chi tiết của thành phần React, nó cho phép nhà phát triển sử dụng lớp như là một thành phần trong React.

Những phương thức xuất ra ngoài bởi React `Component` là những giao diện công khai của nó. Một trong những phương thức này cần phải được ghi đè, trong khi những phương thức khác không cần ghi đè. Bạn sẽ tìm hiểu về những phương thức này khi chúng ta thảo luận về các phương thức vòng đời lát nữa. Phương thức `render()` cần phải được ghi đè, bởi vì nó định nghĩa kết quả của React `Component`, vậy nên nó phải được định nghĩa. Những điều này là cơ bản của lớp JavaScript ES6, và cách chúng được sử dụng trong React để mở rộng chúng tới thành phần.

### Luyện tập:

* Đọc thêm [JavaScript fundamentals before learning React](https://www.robinwieruch.de/javascript-fundamentals-react-requirements/)
* Đọc thêm [ES6 classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)

{pagebreak}

Chúc mừng, bạn đã tìm hiểu về cách khởi tạo nhanh chóng ứng dụng React đầu tiên của bạn! Hãy cùng tóm tắt nào:

* **React**
  * Create-react-app đẩy nhanh phát triển ứng dụng React
  * JSX kết hợp HTML và JavaScript  để định nghĩa đầu ra của thành phần React trong phương thức trả về của nó
  * Các thành phần, khởi tạo, và phần tử là những phần khác nhau trong React
  * `ReactDOM.render()` là điểm đầu vào cho ứng dụng React để kết nối với DOM
  * Những hàm được xây dựng sẵn trong JavaScript có thể được sử dụng trong JSX
  * Map có thể được dùng để trả về một danh sách các sản phẩm như là phần tử HTML
* **ES6**
  * Khai báo biến với `const` và `let` có thể được sử dụng trong những trường hợp cụ thể
  * Ưu tiên sử dụng const hơn let trong ứng dụng React
  * Hàm mũi tên có thể được dùng để giữ hàm của bạn ngắn gọn
  * Lớp được sử dụng để định nghĩa thành phần trong React bằng cách mở rộng chúng

Giờ thì bạn đã hoàn thành chương đầu tiên, Bạn nên trải nghiệm với những mã nguồn bạn đã viết đến giờ và xem lại những thay đổi bạn đã tự thực hiện. Bạn có thể tìm thấy mã nguồn tại [kho chính thức](https://github.com/the-road-to-learn-react/hackernews-client/tree/5.1).

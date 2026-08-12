# 📖 Xem giải thích chi tiết từng dòng code 
---
# 1. index.html — Bộ khung của trang
```html
<!DOCTYPE html>
```
- Dòng đầu tiên bắt buộc phải có, báo cho trình duyệt biết "đây là tài liệu HTML5" để nó hiển thị đúng chuẩn

```html
<html>
    <head>
        <title>Quiz Game</title>
        <link rel="stylesheet" href="style.css">
    </head>
```
- `<html>`: thẻ bao trọn toàn bộ trang web.
- `<head>`: phần "hậu trường" — chứa thông tin không hiển thị trực tiếp lên trang (tiêu đề tab, liên kết CSS...).
- `<title>`Quiz Game</title>: chữ hiện trên tab trình duyệt
- `<link rel="stylesheet" href="style.css">`: nối file CSS vào trang. Nếu thiếu dòng này, trang sẽ không có màu sắc/style gì cả — chỉ chữ đen trắng thô

```html
 <body>
     <div class="container">
```
- `<body>`: phần hiển thị được của trang — mọi thứ người dùng nhìn thấy nằm trong đây
- `<div class="container">`: Là "chiếc hộp lớn" bao bọc toàn bộ ứng dụng.Nó giúp gom tất cả nội dung lại một chỗ để dễ dàng căn giữa màn hình, giới hạn chiều rộng và tạo khung viền (bo góc, đổ bóng) cho Quiz.

### 1.1 MÀN HÌNH BẮT ĐẦU (START SCREEN)
```html
<div class="screen active" id="start-screen">
    <h1>Quiz Time!</h1>
    <p>Test your knowledge with these fun questions</p>
    <button id="start-btn">Start Quiz</button>
</div>
```
- `class="screen active"`: class screen dùng chung cho cả 3 màn hình (start/quiz/result). Class active nghĩa là "màn hình này đang được hiển thị" (CSS sẽ ẩn/hiện dựa vào class này — giải thích kỹ hơn ở phần CSS).
-`id="start-screen"`: giống như "tên riêng, chỉ một cái duy nhất" để JavaScript có thể tìm ra chính xác thẻ này (id phải là duy nhất trong cả trang, khác với class có thể dùng lại nhiều lần).
-`<h1>`: tiêu đề lớn nhất.
-`<p>`: đoạn văn bản mô tả.
- `<button id="start-btn">Start Quiz</button>`: nút bấm để bắt đầu. id="start-btn" để JS biết "đây là nút Start, khi ai bấm vào thì làm gì đó".

### 1.2 MÀN HÌNH QUIZ( QUIZ SCREEN)
```html
<div class="screen" id="quiz-screen">
    <div class="quiz-header">
        <h2 id="question-text">Question goes here</h2>
```
- `class="screen" (không có active)` → mặc định màn hình này bị ẩn lúc đầu, chỉ hiện khi bấm Start.
- ` <h2 id="question-text">`: chỗ hiển thị câu hỏi. Chữ "Question goes here" chỉ là placeholder, JS sẽ thay bằng câu hỏi thật.

```html
        <div class="quiz-info">
            <p>
                Question <span id="current-question">1</span> of <span id="total-questions">5</span>
            </p>
            <p>
                Score:<span id="score">0</span>
            </p>
        </div>
    </div>
```
- `<span id="current-question">`: ô nhỏ hiển thị số thứ tự câu hỏi hiện tại (VD: câu số 2).
- `<span id="total-questions">`: hiển thị tổng số câu hỏi.
- `<span id="score">`: hiển thị điểm số hiện tại.
- `Dùng <span> (không phải <div>)` vì đây là chữ nhỏ nằm chung một dòng với chữ khác — span không tự xuống dòng


```html
<div class="progress-bar">
        <div id="progress" class="progress"></div>
    </div>
</div>
```
- 'progress-bar': cái "đường ray" nền (thanh xám dài).
- 'progress': cái "thanh màu" chạy bên trong, độ dài của nó sẽ tăng dần theo % số câu đã làm — JS sẽ chỉnh width (chiều rộng) của nó bằng code.

### 1.3 MÀN HÌNH KẾT QUẢ(RESULT SCREEN)
```html
<div id="result-screen" class="screen">
    <h1>Quiz Results</h1>
    <div class="result-info">
        <p>You Score <span id="final-score">0</span> out of <span id="max-score">5</span></p>
        <div id="result-message">Good Job!</div>
    </div>
    <button id="restart-btn">Restart Quiz</button>
</div>
```
- final-score: điểm số cuối cùng bạn đạt được.
- max-score: tổng điểm tối đa có thể đạt (bằng số câu hỏi).
- result-message: câu nhận xét (VD: "Perfect!", "Good effort!"...) — JS sẽ đổi chữ tùy theo điểm.
- restart-btn: nút để chơi lại từ đầu.

```html
</div>
        <script src="script.js"></script>
    </body>
</html>
```
- `<script src="script.js">`: nối file JavaScript vào trang. Đặt ở cuối <body> để trình duyệt load xong hết HTML rồi mới chạy JS (tránh lỗi "tìm không thấy thẻ" vì thẻ chưa kịp tạo ra).

---
## 2. Style.css-Trang Trí giao diện
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```
- `*` nghĩa là "chọn TẤT CẢ thẻ".
- `margin`: 0; padding: 0;: xóa khoảng cách mặc định mà trình duyệt tự thêm vào (mỗi trình duyệt có mặc định hơi khác nhau, xóa hết để mình tự kiểm soát).
- `box-sizing`: border-box;: khi tính chiều rộng/cao của 1 thẻ, sẽ tính luôn cả viền (border) và khoảng đệm (padding) vào bên trong — giúp tính toán kích thước dễ đoán hơn, không bị "phình" ra ngoài ý muốn.

```css
body {
    background-color: #f5efe6;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 1rem;
    font-family: sans-serif;
}
```

- `background-color`: #f5efe6;: màu nền be nhạt cho cả trang.
- `display: flex;`: biến body thành "hộp linh hoạt" (flexbox) để dễ canh giữa nội dung bên trong.
- `justify-content: center;`: canh giữa theo chiều ngang.
- ` align-items: center;`: canh giữa theo chiều dọc.
- ` min-height: 100vh;`: chiều cao tối thiểu = 100% chiều cao màn hình (vh = viewport height), để nội dung luôn nằm giữa màn hình dù ít hay nhiều.
- `padding: 1rem;`: đệm một khoảng cách nhỏ với mép màn hình, tránh dính sát.
- `font-family: sans-serif;`: dùng font chữ không chân (kiểu chữ hiện đại, dễ đọc).

```css
.container {
    background-color: white;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 600px;
    overflow: hidden;
    position: relative;
```
- `.container` = chọn thẻ có class="container" (chính là cái <div> bao ngoài trong HTML).
- `background-color`: white;: nền trắng cho khối quiz.
- `border-radius`: 1rem;: bo tròn 4 góc.
- `box-shadow: ...`: tạo bóng đổ nhẹ phía dưới, giúp khối quiz trông "nổi" lên khỏi nền — rgba(0,0,0,0.1) là màu đen với độ mờ (alpha) 10%, tức bóng rất nhạt.
- `width: 100%; max-width: 600px;`: chiều rộng co giãn theo màn hình, nhưng không bao giờ vượt quá 600px (để trên màn hình to nó không bị kéo dài quá mức).
- `overflow: hidden;`: cắt bỏ phần nào tràn ra ngoài khung bo tròn (tránh góc vuông "ló" ra khỏi góc tròn).
- `position: relative;`: thiết lập "mốc tọa độ" cho khối này, phòng khi cần định vị thẻ con bên trong theo absolute (dù ở đây chưa dùng tới nhưng là thói quen tốt)

```css
.screen {
    display: none;
    padding: 2rem;
    text-align: center;
}

.screen.active {
    display: block;
}
```
Đây là phần quan trọng nhất để hiểu cơ chế chuyển màn hình.
-` .screen { display: none; }`: mặc định, MỌI thẻ có class screen đều bị ẩn (không hiển thị, không chiếm chỗ).
- `.screen.active { display: block; }`: NHƯNG nếu thẻ đó có thêm class active (viết liền .screen.active nghĩa là "vừa có class screen VỪA có class active"), thì nó sẽ được hiện ra.
→ Đây chính là "phép thuật" đằng sau việc chuyển từ màn Start → Quiz → Result: JavaScript chỉ cần thêm/xóa class active vào đúng thẻ, CSS sẽ tự ẩn/hiện.
padding: 2rem;: đệm khoảng cách với viền trong.
text-align: center;: canh chữ vào giữa.

```css
#start-screen h1 {
    color: #e86a33;
    margin-bottom: 20px;
    font-size: 2.5rem;
}
```
- ` #start-screen h1`: chọn thẻ` <h1>` nhưng chỉ khi nó nằm bên trong thẻ có id="start-screen".
- `color`: #e86a33;: màu chữ cam.
- `margin-bottom: 20px;`: khoảng cách phía dưới với phần tử kế tiếp.
- `font-size: 2.5rem;`: cỡ chữ lớn (2.5 lần cỡ chữ gốc).

```css
#start-screen p {
    color: #666;
    margin-bottom: 30px;
    font-size: 1.1rem;
}
```
- Tương tự, style riêng cho đoạn `<p>` trong màn Start: màu xám #666, cỡ chữ hơi lớn hơn bình thường

```css
.quiz-header {
    margin-bottom: 2rem;
}

#question-text {
    color: #333;
    font-size: 1.5rem;
    margin-bottom: 1rem;
    line-height: 1.4;
}
```
- `.quiz-header`: chừa khoảng cách bên dưới phần header của câu hỏi.
- `#question-text`: style cho dòng câu hỏi — line-height: 1.4 là khoảng cách giữa các dòng chữ (nếu câu hỏi dài, xuống 2 dòng thì các dòng không bị dính sát nhau)

```css
.quiz-info {
    display: flex;
    justify-content: space-between;
    color: #666;
    font-size: 1rem;
    margin-bottom: 10px;
}
```
- `display: flex; + justify-content: space-between;`: đặt 2 dòng "Question x of y" và "Score: z" nằm 2 đầu, cách xa nhau tối đa (một bên trái, một bên phải) thay vì xếp chồng lên nhau.

```css
.answers-container {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 25px;
}
```
- `display: flex; flex-direction: column;`: xếp các nút trả lời theo cột dọc (nút này nằm dưới nút kia).
gap: 10px;: khoảng cách đều 10px giữa các nút, không cần margin thủ công cho từng nút.

```css
.answer-btn {
    background-color: white;
    color: #333;
    border: 2px solid #eadbc8;
    border-radius: 10px;
    padding: 1rem;
    cursor: pointer;
    text-align: left;
    transition: all 0.3s ease;
}
```
- Style mặc định cho mỗi nút trả lời (những nút này do JS tạo ra bằng code, không có sẵn trong HTML).
- `border: 2px solid #eadbc8;`: viền be nhạt dày 2px.
- `cursor: pointer;`: khi rê chuột vào, con trỏ đổi thành hình bàn tay — báo hiệu "cái này bấm được".
-` text-align: left;`: chữ căn trái (khác với các phần khác căn giữa).
- `transition: all 0.3s ease;`: khi có gì thay đổi (màu nền, viền...), nó chuyển đổi mượt trong 0.3 giây thay vì đổi màu "giật cục" ngay lập tức.

```css
.answer-btn:hover {
    background-color: #eadbc8;
    border-color: #dac0ae;
}

```
- `:hover là giả-class (pseudo-class)`: style này chỉ áp dụng khi con chuột đang rê lên trên nút đó.

```css
.answer-btn.correct {
    background-color: #e6fff0;
    border-color: #a3f0c4;
    color: #28a745;
}

.answer-btn.incorrect {
    background-color: #fff0f0;
    border-color: #ffbdbd;
    color: #dc3545;
}
```
- `.answer-btn.correct`: khi nút trả lời vừa có class answer-btn vừa có class correct → tô xanh lá (đáp án đúng).
- `.answer-btn.incorrect`: tương tự nhưng tô đỏ (đáp án bạn chọn sai).
Hai class correct/incorrect này không có sẵn trong HTML — JavaScript sẽ tự thêm vào bằng code khi bạn bấm chọn một đáp án (xem phần JS bên dưới).

```css
.progress-bar {
    height: 10px;
    background-color: #f8f0e5;
    border-radius: 5px;
    overflow: hidden;
    margin-top: 20px;
}

.progress {
    height: 100%;
    background-color: #e86a33;
    width: 0%;
    transition: width 0.3s ease;
}
```

- `.progress-bar`: thanh nền xám nhạt, cao 10px, bo tròn.
- `.progress`: thanh màu cam nằm bên trong, ban đầu rộng 0% (chưa làm câu nào thì thanh trống trơn).
JavaScript sẽ tăng dần width (chiều rộng, tính theo %) của thanh này mỗi khi qua câu mới, tạo cảm giác "thanh tiến trình" chạy dần.

```css
#result-screen h1 { color: #e86a33; margin-bottom: 30px; }

.result-info {
    background-color: #f8f0e5;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 30px;
}

.result-info p {
    font-size: 1.2rem;
    color: #333;
    margin-bottom: 1rem;
}
```
- Style cho màn hình kết quả: tiêu đề cam, khối thông tin có nền be nhạt bo góc, chữ điểm số cỡ vừa.

```css
button {
    background-color: #e86a33;
    color: white;
    border: none;
    padding: 15px 30px;
    border-radius: 10px;
    font-size: 1.1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #d45b28;
}
```
- Style mặc định cho mọi thẻ `<button>` trong trang (nút Start và nút Restart) — nền cam, chữ trắng, không viền, bo góc.
- `padding: 15px 30px;`: đệm 15px trên/dưới, 30px trái/phải.
Khi hover thì đổi sang màu cam đậm hơn 

```css
@media (max-width: 500px) {
    .screen { padding: 1rem; }
    #start-screen h1 { font-size: 2rem; }
    #question-text { font-size: 1.3rem; }
    .answer-btn { padding: 12px; }
    button { padding: 12px 25px; font-size: 1rem; }
}
```
- @media (max-width: 500px): đây là "responsive design" — bộ quy tắc này chỉ áp dụng khi màn hình rộng ≤ 500px (ví dụ điện thoại).
- Trên màn hình nhỏ: giảm padding, giảm cỡ chữ tiêu đề, để giao diện không bị vỡ/tràn.
---
## 3. script.js- BỘ NÃO xử lý logic
### PHẦN 1:Lấy các thể HTML ra để điều khiển
```javascript
const startScreen = document.getElementById("start-screen");
const quizScreen = document.getElementById("quiz-screen");
const resultScreen = document.getElementById("result-screen");
const startButton = document.getElementById("start-btn");
const questionText = document.getElementById("question-text");
const answerContainer = document.getElementById("answer-container");
const currentQuestionSpan = document.getElementById("current-question");
const totalQuestionSpan = document.getElementById("total-questions");
const scoreSpan = document.getElementById("score");
const finalScoreSpan = document.getElementById("final-score");
const maxScoreSpan = document.getElementById("max-score");
const resultMessage = document.getElementById("result-message");
const restartButton = document.getElementById("restart-btn");
const progressBar = document.getElementById("progress");
```
- `document` là "cả trang web" nhìn từ góc độ JavaScript.
- `document.getElementById("xxx")`: tìm thẻ HTML có id="xxx" và trả về nó, để JS có thể đọc/sửa nó.
- `const`: khai báo biến (variable) — một cái "hộp" đặt tên để lưu giá trị. const nghĩa là hộp này không được gán lại giá trị khác sau khi tạo (khác với let, có thể đổi giá trị).
- Mỗi dòng ở đây tương ứng đúng 1-1 với một id trong file HTML — đây là bước "kết nối" HTML với JS, để sau này JS có thể thay đổi nội dung/chuyển màn hình.

### PHẦN 2: Dữ liệu câu hỏi
```javascript
const quizQuestions = [
    {
        question: "What is the Capital of France?",
        answers: [
            { text: "London", correct: false },
            { text: "Berlin", correct: false },
            { text: "Paris", correct: true },
            { text: "Madrid", correct: false },
        ],
    },
    // ... còn 4 câu hỏi khác cùng cấu trúc
];
```
- quizQuestions là một mảng (array) — danh sách các câu hỏi, đặt trong dấu [ ].
- Mỗi câu hỏi là một object (đối tượng), đặt trong dấu { }, gồm 2 phần:
question: chuỗi chữ (string) — nội dung câu hỏi.
  - answers: một mảng con chứa 4 đáp án.
Mỗi đáp án cũng là 1 object nhỏ gồm:
  - text: chữ hiển thị trên nút.
  - correct: true hoặc false — đánh dấu đây có phải đáp án đúng hay không.
- Đây chính là "database" của cả quiz. Muốn thêm/sửa câu hỏi, bạn chỉ cần sửa ở đây, không cần đụng vào HTML/CSS.

### PHẦN 3: Biến trạng thái( ghi nhớ "quiz" đang ở đâu)
```javascript
let currentQuestionIndex = 0;
let score = 0;
let answerDisabled = false;
```
- let (khác const): khai báo biến có thể thay đổi giá trị về sau — hợp lý vì các giá trị này sẽ đổi liên tục khi chơi.
- currentQuestionIndex = 0: chỉ số (index) của câu hỏi đang hiển thị. Trong lập trình, mảng luôn đếm từ 0, nên câu hỏi đầu tiên có index = 0, câu thứ 2 = index 1, v.v.
- score = 0: điểm số, bắt đầu bằng 0.
- answerDisabled = false: cờ (flag) đúng/sai để kiểm tra "người chơi đã chọn đáp án cho câu này chưa". Dùng để chặn bấm nhiều lần liên tục vào các nút trả lời (giải thích kỹ hơn bên dưới).


```javascript
totalQuestionSpan.textContent = quizQuestions.length;
maxScoreSpan.textContent = quizQuestions.length;
```
- `.textContent`: thuộc tính để đọc hoặc gán chữ hiển thị bên trong 1 thẻ HTML.
- `quizQuestions.length`: số lượng phần tử trong mảng quizQuestions (ở đây = 5 câu hỏi).
- Hai dòng này chạy ngay khi trang vừa load xong, để tự động điền số "5" vào ô "of 5" và "out of 5" — không cần gõ tay số 5 trong HTML, nên nếu sau này bạn thêm/bớt câu hỏi, số này tự cập nhật theo.

### PHẦN 4: Gắn sự kiện(event listener) cho các nút
```javascript
startButton.addEventListener("click", startQuiz);
restartButton.addEventListener("click", restartQuiz);
```
- `.addEventListener("click", tênHàm)`: nghĩa là "lắng nghe" xem thẻ này có bị click hay không, nếu có thì chạy hàm được chỉ định.
- Dòng 1: khi bấm nút Start → chạy hàm startQuiz().
- Dòng 2: khi bấm nút Restart → chạy hàm restartQuiz().
- Lưu ý: chỉ ghi tên hàm startQuiz, không có dấu ngoặc () — vì ta đang "giao" hàm đó cho trình duyệt để nó tự gọi khi cần, chứ không phải gọi hàm ngay bây giờ.

### PHẦN 5:Hàm bắt đầu quiz
```javascript
function startQuiz() {
    currentQuestionIndex = 0;
    score = 0;
    scoreSpan.textContent = 0;

    startScreen.classList.remove("active");
    quizScreen.classList.add("active");

    showQuestion();
}
```
- `function startQuiz() { ... }`: định nghĩa một hàm (function) — một khối lệnh được đặt tên, có thể gọi lại nhiều lần.
- Reset lại `currentQuestionIndex` và `score` về 0 — để nếu chơi lại từ đầu, điểm cũ không bị giữ lại.
- `scoreSpan.textContent = 0;`: cập nhật chữ hiển thị điểm trên màn hình về "0".
- `startScreen.classList.remove("active")`: xóa class active khỏi màn Start → theo CSS đã học ở trên, .screen không có active sẽ bị display: none → màn Start biến mất.
- `quizScreen.classList.add("active")`: thêm class active vào màn Quiz → nó chuyển sang display: block → màn Quiz hiện ra.
- `.classList` là công cụ để thêm (add)/xóa (remove)/kiểm tra class của 1 thẻ HTML bằng JS.
- `showQuestion();`: gọi hàm hiển thị câu hỏi (định nghĩa bên dưới) để hiển thị câu hỏi đầu tiên ngay lập tức.

### PHẦN 6: Hàm hiển thị câu hỏi
```javascript
function showQuestion() {
    answerDisabled = false;
    const currentQuestion = quizQuestions[currentQuestionIndex];
    currentQuestionSpan.textContent = currentQuestionIndex + 1;
```
- `answerDisabled = false;`: mở khóa cho phép người chơi được bấm chọn đáp án (đầu mỗi câu mới phải mở khóa lại).
- `quizQuestions[currentQuestionIndex]`: lấy ra câu hỏi tại vị trí đó trong mảng. Ví dụ nếu `currentQuestionIndex = 0` → lấy câu hỏi đầu tiên (về Pháp).
- `currentQuestionSpan.textContent = currentQuestionIndex + 1;`: hiển thị số thứ tự câu hỏi cộng thêm 1 — vì máy tính đếm từ 0 (0,1,2,3,4) nhưng người chơi muốn thấy số dễ hiểu (1,2,3,4,5).

```javascript
 const progressPercent = (currentQuestionIndex / quizQuestions.length) * 100;
    progressBar.style.width = progressPercent + "%";
```
- Tính % tiến trình = (số câu đã qua ÷ tổng số câu) × 100.
- Ví dụ đang ở câu 3 (index = 2): (2 ÷ 5) × 100 = 40%.
- `progressBar.style.width = ...:` gán trực tiếp CSS width cho thanh tiến trình bằng JS — đây là cách JS "chỉnh CSS" ngay trong code thay vì phải sửa file CSS.
- `+ "%"`: nối chuỗi ký tự "%" vào sau con số, vì CSS cần dạng chữ như "40%", không nhận số thuần 40.

```javascript
questionText.textContent = currentQuestion.question;
    answerContainer.innerHTML = "";
```
- `questionText.textContent = currentQuestion.question;`: đổi chữ trong thẻ <h2> thành nội dung câu hỏi hiện tại.
- `answerContainer.innerHTML = "";`: xóa sạch nội dung bên trong hộp chứa đáp án (dọn dẹp đáp án của câu trước, chuẩn bị chỗ trống cho đáp án câu mới). innerHTML là toàn bộ mã HTML bên trong 1 thẻ; gán chuỗi rỗng "" = xóa hết.

```javascript
currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.textContent = answer.text;
        button.classList.add("answer-btn");
        button.dataset.correct = answer.correct;

        button.addEventListener("click", selectAnswer);
        answerContainer.appendChild(button);
    });
}
```
- `currentQuestion.answers.forEach(answer => { ... })`: lặp qua từng đáp án trong mảng answers (4 lần, vì có 4 đáp án). answer là tên biến đại diện cho từng đáp án trong mỗi lượt lặp.
- `document.createElement("button")`: tạo mới một thẻ `<button>` (chưa gắn vào trang, mới chỉ tồn tại "trong bộ nhớ").
- `button.textContent = answer.text;`: gán chữ hiển thị trên nút (VD: "Paris").
- `button.classList.add("answer-btn");`: gắn class answer-btn để nút này được CSS tô style giống các nút khác.
- `button.dataset.correct = answer.correct;`: gắn một thuộc tính dữ liệu tùy chỉnh (data-correct) vào nút, lưu giá trị true/false — để lát nữa khi bấm vào, JS biết được "nút này đúng hay sai" mà không cần tra lại mảng gốc.
- `button.addEventListener("click", selectAnswer);`: gắn sự kiện — khi bấm nút này, chạy hàm selectAnswer.
- `answerContainer.appendChild(button);`: gắn nút vừa tạo vào trang thật (bỏ nó vào bên trong answerContainer) — chỉ tới bước này, nút mới thực sự hiện lên màn hình.
Lặp lại 4 lần → tạo ra đủ 4 nút trả lời.

### PHẦN 7: hàm xử lý khi người chơi chọn đáp án
```javascript
function selectAnswer(event) {
    if (answerDisabled) return;

    answerDisabled = true;
```
- `function selectAnswer(event)`: hàm này tự động nhận được một tham số tên `event` — chứa thông tin về sự kiện vừa xảy ra (ví dụ: người dùng đã click vào đâu).
- `if (answerDisabled) return;`: nếu đã có người bấm chọn rồi `(answerDisabled = true)` thì dừng hàm ngay lập tức `(return)`, không làm gì thêm — đây là cách chặn người chơi bấm thêm lần 2, 3 vào các nút khác trong lúc đang chờ chuyển câu.
- `answerDisabled = true;`: khóa lại ngay khi có 1 lựa chọn được thực hiện.

```javascript
const selectButton = event.target;
    const isCorrect = selectButton.dataset.correct === "true";
```
- `event.target:` chính là cái nút mà người dùng vừa bấm vào.
- `selectButton.dataset.correct`: lấy giá trị data-correct đã gắn lúc tạo nút (nhớ lại phần 6). Giá trị này luôn là chuỗi chữ "true"/"false", không phải boolean thật, nên phải so sánh === "true" để ra kết quả đúng/sai (kiểu boolean).

```javascript
Array.from(answerContainer.children).forEach(button => {
        if (button.dataset.correct === "true") {
            button.classList.add("correct");
        } else if (button === selectButton) {
            button.classList.add("incorrect");
        }
    });
```
- `answerContainer.children`: danh sách tất cả các nút con bên trong hộp đáp án.
- `Array.from(...)`: chuyển nó thành mảng thật sự để dùng được .forEach (danh sách children gốc không phải mảng chuẩn, phải chuyển đổi trước).
- Duyệt qua cả 4 nút:
           - Nếu nút đó là đáp án đúng (dataset.correct === "true") → luôn tô xanh (class correct), dù người chơi có chọn nó hay không — để họ luôn thấy đáp án đúng nằm đâu.
           - Ngược lại, nếu nút đó chính là nút người chơi vừa bấm (button === selectButton) mà lại không đúng → tô đỏ (class incorrect) — báo đây là lựa chọn sai của họ.

```javascript
    if (isCorrect) {
        score++;
        scoreSpan.textContent = score;
    }
```
- Nếu `isCorrect` là true: score++ nghĩa là tăng biến score lên 1 (giống như score = score + 1).
Cập nhật lại chữ hiển thị điểm trên màn hình ngay lập tức

```javascript
setTimeout(() => {
        currentQuestionIndex++;

        if (currentQuestionIndex < quizQuestions.length) {
            showQuestion();
        } else {
            showResult();
        }
    }, 1000);
}
```
- `setTimeout(hàm, 1000)`: chờ 1000 mili-giây (= 1 giây) rồi mới chạy đoạn code bên trong — mục đích là để người chơi kịp nhìn thấy màu xanh/đỏ trước khi màn hình đổi qua câu tiếp theo (nếu không có dòng này, màn hình sẽ nhảy câu ngay tức thì, không kịp nhìn đáp án đúng/sai).
- `() => { ... }`: đây là arrow function — một cách viết hàm ngắn gọn, không cần từ khóa function. Hàm này không có tên, chỉ dùng 1 lần ngay tại chỗ (gọi là "hàm ẩn danh").
- `currentQuestionIndex++;`: tăng chỉ số câu hỏi lên 1, chuẩn bị sang câu kế.
- `if (currentQuestionIndex < quizQuestions.length)`: nếu vẫn còn câu hỏi tiếp theo (chưa hết 5 câu) → gọi lại `showQuestion()` để hiện câu mới.
- `else { showResult(); }`: nếu đã hết câu hỏi (đã làm xong hết 5/5) → gọi hàm `showResult()` để chuyển sang màn hình kết quả.

### PHẦN 8: Hàm hiển thị kết quả
```javascript
function showResult() {
    quizScreen.classList.remove("active");
    resultScreen.classList.add("active");

    finalScoreSpan.textContent = score;

    const percentage = (score / quizQuestions.length) * 100;
```
- Ẩn màn Quiz, hiện màn Result — dùng lại đúng kỹ thuật `classList.remove/add("active") `như hàm `startQuiz`.
- `finalScoreSpan.textContent = score;`: hiển thị điểm số cuối cùng lên màn Result.
- Tính phần trăm điểm đạt được = `(điểm số ÷ tổng số câu) × 100. Ví dụ đúng 4/5 câu → (4÷5)×100 = 80%`.

```javascript
if (percentage === 100) {
        resultMessage.textContent = "Perfect!";
    } else if (percentage >= 80) {
        resultMessage.textContent = "Great Job! You know your stuff";
    } else if (percentage >= 60) {
        resultMessage.textContent = "Good effort! Keep learning";
    } else if (percentage >= 40) {
        resultMessage.textContent = "Not bad! Try again to improve";
    } else {
        resultMessage.textContent = "Keep studying! You'll get better";
    }
}
```
- Đây là chuỗi lệnh if / else if / else — kiểm tra lần lượt từ trên xuống, gặp điều kiện nào đúng đầu tiên thì chạy dòng đó rồi bỏ qua các điều kiện còn lại:
- Đúng 100% → "Perfect!"
- Từ 80% đến dưới 100% → "Great Job!..."
- Từ 60% đến dưới 80% → "Good effort!..."
- Từ 40% đến dưới 60% → "Not bad!..."
- Dưới 40% (else, không cần điều kiện, là trường hợp còn lại) → "Keep studying!..."
- Kết quả được gán vào resultMessage.textContent để hiển thị câu nhận xét phù hợp với điểm số.

### PHẦN 9: Hàm chơi lại
```javascript
function restartQuiz() {
    resultScreen.classList.remove("active");
    startQuiz();
}
```

- Ẩn màn Result đi.
- Gọi lại startQuiz() — hàm này (đã học ở Phần 5) sẽ tự reset điểm, chỉ số câu hỏi, ẩn màn Start / hiện màn Quiz, và hiển thị lại câu hỏi đầu tiên. Vậy là quay vòng lại từ đầu, y hệt lúc mới bấm "Start Quiz".

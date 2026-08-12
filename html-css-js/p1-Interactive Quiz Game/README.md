# 🎯 Quiz Game - Giải Thích Code Từng Dòng 
### - Đây là project game trắc nghiệm(quiz) nhỏ gồm 3 file:  index.html/style.css/script.js
### - README.md này giải thích từng dòng code theo kiểu dễ hiểu nhất
#### 💡 Mẹo đọc: đừng cố nhớ hết một lúc. Đọc từng phần, tự gõ lại code, chạy thử, rồi mới qua phần tiếp theo. Não cần thời gian để "ngấm" — chậm mà chắc là bình thường, không phải bạn kém.
---
## 📁 Cấu trúc project
```markdown
├── index.html   -> Khung sườn (bộ xương) của trang web
├── style.css    -> Trang trí, làm đẹp giao diện
└── script.js    -> "Bộ não" xử lý logic, làm mọi thứ hoạt động
```
#### Cách hoạt động chung: HTML dựng ra các thẻ (button, div, h1...) → CSS tô màu, canh chỉnh → JavaScript "bắt sự kiện" (ví dụ: bấm nút) rồi thay đổi nội dung/HTML để tạo cảm giác "sống động".

## 📖 Xem giải thích chi tiết từng dòng code tại [EXPLAINED.md]
---
## 🧠 Tóm tắt luồng chạy toàn bộ chương trình (Big Picture)
### 1. Trang load xong → chỉ màn Start hiện ra (do class active chỉ có ở start-screen trong HTML gốc).
### 2. Bấm Start Quiz → startQuiz() chạy → reset điểm, chuyển sang màn Quiz, gọi showQuestion().
### 3. showQuestion() → lấy câu hỏi hiện tại, cập nhật thanh tiến trình, tạo 4 nút đáp án bằng code và gắn sự kiện click cho từng nút.
### 4. Người chơi bấm 1 đáp án → selectAnswer() chạy → khóa không cho bấm thêm → tô xanh đáp án đúng, tô đỏ đáp án sai (nếu chọn sai) → cộng điểm nếu đúng → chờ 1 giây → qua câu tiếp theo hoặc hiện kết quả.
### 5. Hết 5 câu → showResult() → hiện điểm số cuối, hiện câu nhận xét theo %.
### 6. Bấm Restart Quiz → quay lại y hệt bước 2.
---
## 📌 Vài khái niệm lập trình xuất hiện trong bài (tra cứu nhanh)
| Khái Niệm| Giải thích ngắn gon|
|---|---|
|const / let	|Khai báo biến. const = không đổi giá trị được, let = đổi được.|
|Mảng ([])	|Danh sách nhiều giá trị, đánh số thứ tự từ 0.|
|Object ({})	|Nhóm nhiều dữ liệu có tên (key: value) lại với nhau|.
|Hàm (function)	|Khối lệnh có tên, gọi lại được nhiều lần.|
|Arrow function () => {}	|Cách viết hàm ngắn gọn, thường dùng cho hàm dùng 1 lần.|
|document.getElementById	|Tìm 1 thẻ HTML theo id.|
|.textContent	|Đọc/ghi chữ hiển thị bên trong 1 thẻ.|
|.classList.add/remove	|Thêm/xóa 1 class CSS khỏi thẻ bằng JS.|
|addEventListener("click", fn)	|Chạy hàm fn khi thẻ đó được bấm.|
|.forEach	|Lặp qua từng phần tử trong mảng.|
|.dataset	|Đọc/ghi thuộc tính data-* tùy chỉnh trên thẻ HTML.|
|setTimeout(fn, ms)	|Chờ ms mili-giây rồi mới chạy hàm fn.|
|if / else if / else	|Rẽ nhánh, kiểm tra điều kiện theo thứ tự từ trên xuống.|
# Shoe Sort Puzzle

## Video Gameplay
[Watch Gameplay](https://youtube.com/shorts/KJ3jWdtoe6w?si=3nkqK__1wwZ6hFjB)

## APK
[Download APK](https://github.com/Tang979/GDD_APK_Shoe_Sort_Puzzle/releases)

## Source Code
[View Source Code](https://github.com/nguyenkhacnhat203-dev/Shoe_Sort_Puzzle)

---

## 1. Tổng quan
- **Tên game:** Shoe Sort Puzzle  
- **Thể loại:** Puzzle  
- **Nền tảng:** Mobile (Android / iOS)  
- **Chế độ chơi:** Single-player  
- **Đối tượng người chơi:** Mọi lứa tuổi  

### Giới thiệu
Shoe Sort Puzzle là game giải đố sắp xếp, trong đó người chơi cần di chuyển các chiếc giày để đưa 3 chiếc giày giống nhau vào cùng một box nhằm tạo match và loại bỏ chúng khỏi màn chơi cho đến khi hết toàn bộ giày.

### Mục tiêu thiết kế
- Lối chơi đơn giản, tập trung vào khả năng quan sát và sắp xếp của người chơi  
- Mỗi màn chơi có giới hạn thời gian tùy theo độ khó  
- Dễ tiếp cận với mọi đối tượng người chơi  

---

## 2. Cấu trúc Scene
Game sử dụng duy nhất **1 Gameplay Scene**.

### UI Menu
- Background game  
- Nút bắt đầu trò chơi  
- Hiển thị level hiện tại  

### UI Gameplay
- Hệ thống box và shelf chứa giày theo độ khó màn chơi  
- Các booster hỗ trợ người chơi  
- Thanh thời gian đếm ngược  
- Hiển thị level hiện tại  

UI được điều khiển bằng code thông qua việc bật/tắt các nhóm giao diện.

---

## 3. Core Gameplay Loop
1. Khởi tạo số lượng box và số lượng giày dựa trên dữ liệu level  
2. Sắp xếp ngẫu nhiên giày vào box và shelf chờ  
3. Mỗi box và shelf chứa tối đa 3 giày  
4. Luôn đảm bảo có ít nhất 1 ô trống khi khởi tạo màn chơi  
5. Người chơi di chuyển giày vào các ô trống để gom 3 giày giống nhau vào cùng box  
6. Khi 3 giày giống nhau cùng nằm trong 1 box, chúng sẽ được match và biến mất  
7. Nếu box trống hoặc vừa match xong, giày từ shelf sẽ được đẩy lên box  
8. Tiếp tục cho đến khi hết toàn bộ giày hoặc hết thời gian  

---

## 4. Luật chơi
- Người chơi có thể di chuyển giày bằng:
  - Kéo thả (drag & drop)  
  - Chọn giày và nhấn vào vị trí muốn di chuyển  

- Khi 1 box chứa đủ 3 giày giống nhau:
  - 3 giày sẽ biến mất  
  - Giày từ shelf được đẩy lên box nếu có  

---

## 5. Điều kiện thắng
Người chơi chiến thắng khi match hết toàn bộ giày trước khi thời gian kết thúc.

---

## 6. Điều kiện thua
Game Over khi thời gian đếm ngược kết thúc nhưng vẫn còn giày chưa được match hết.

---

## 7. Tính năng chính
- Random shoe generation  
- Match-3 mechanic  
- Drag & Drop + Tap input  
- Countdown timer  
- Hint system  
- Booster system  

### Booster
**Magnet**
- Tìm 3 giày giống nhau trên box và shelf rồi loại bỏ trực tiếp  

**Shuffle**
- Xáo trộn ngẫu nhiên vị trí giày giữa các box và shelf  

**Add Box**
- Spawn thêm 1 box trống giúp người chơi có thêm không gian xử lý  

---

## 8. Công việc tôi thực hiện
- Xây dựng toàn bộ gameplay chính
- Đọc dữ liệu level từ JSON để khởi tạo màn chơi
- Khởi tạo box, shoe và random phân phối vào box/shelf
- Thiết kế ràng buộc random để tránh trạng thái khởi tạo không hợp lệ
- Xây dựng hệ thống drag & drop và tap-to-move
- Kiểm tra điều kiện match và xử lý loại bỏ giày
- Xây dựng hệ thống booster (Magnet, Shuffle, Add Box)
- Xây dựng hệ thống hint tự động sau mỗi khoảng thời gian
- Xây dựng Game State Manager để quản lý trạng thái gameplay và kiểm soát Timescale theo từng state
- Giới hạn input chỉ hoạt động khi game ở trạng thái OnGame
- Xây dựng Resource Manager quản lý Heart, Gold, Booster và thời gian hồi Heart
- Xây dựng logic energy system: trừ Heart khi thua, replay, thoát giữa màn chơi và chặn tiếp tục chơi khi hết Heart
- Xây dựng flow mua Heart và Booster thông qua popup xác nhận
- Lưu tiến trình người chơi bằng PlayerPrefs
- Reset level và chuyển level mới
- Quản lý timer và logic bắt đầu đếm thời gian sau tương tác đầu tiên

---

## 9. Technical Challenges
### 1. Xử lý random khởi tạo hợp lệ
- Thiết kế logic random giày vào box và shelf nhưng vẫn đảm bảo:
  - Không spawn sẵn 3 giày giống nhau trong cùng 1 box  
  - Luôn tồn tại ít nhất 1 ô trống để người chơi bắt đầu  

### 2. Xử lý xung đột input
- Đồng thời hỗ trợ:
  - Drag & Drop  
  - Click/Tap to Move  

- Giải quyết xung đột giữa 2 phương thức input để tránh lỗi thao tác và sai trạng thái object.

### 3. Đồng bộ animation với gameplay logic
- Sử dụng DOTween cho:
  - Di chuyển giày  
  - Match animation  
  - Push shoe từ shelf lên box  

- Đảm bảo gameplay state chỉ cập nhật sau khi animation hoàn tất.

### 4. Quản lý luồng dữ liệu giữa Box và Shelf
- Sau mỗi lần match hoặc box trống:
  - Đẩy giày từ shelf lên box  
  - Dịch chuyển hàng chờ mới  
  - Ẩn shelf khi không còn dữ liệu  

### 5. Thiết kế logic booster an toàn
- Booster có thể thay đổi trực tiếp game state:
  - Xóa object  
  - Shuffle dữ liệu  
  - Spawn thêm box  

- Đảm bảo sau khi booster hoạt động vẫn giữ gameplay state hợp lệ.

### 6. Quản lý trạng thái game và gameplay flow
- Xây dựng Game State để quản lý các trạng thái:
  - Menu
  - OnGame
  - Pause
  - Win
  - Lose
  - Popup

- Đồng bộ:
  - Time.timeScale
  - Input handling
  - Popup flow

- Đảm bảo gameplay chỉ hoạt động khi game ở trạng thái hợp lệ.

### 7. Quản lý tài nguyên và energy system
- Xây dựng hệ thống tài nguyên bao gồm:
  - Heart
  - Gold
  - Booster inventory

- Quản lý logic:
  - Trừ Heart theo hành động gameplay
  - Heart recovery theo thời gian
  - Popup mua thêm tài nguyên khi không đủ điều kiện tiếp tục chơi

---

## 10. Tech Stack
- Unity  
- C#  
- JSON  
- DOTween  
- PlayerPrefs  

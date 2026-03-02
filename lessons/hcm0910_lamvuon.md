## 🌳 Bài: Làm Vườn (Giao 3 Hình Chữ Nhật) 
<br>
<div class="step-card border-blue">
<div class="step-badge bg-blue">Phân tích đề bài</div>

Xác định diện tích vùng đất mà cả 3 người cùng chăm sóc. Đây là bài toán tìm **diện tích phần giao của 3 hình chữ nhật** trên mặt phẳng tọa độ $Oxy$.

Vùng giao nhau của nhiều hình chữ nhật (nếu tồn tại) luôn là một hình chữ nhật mới. Một ô đất $(x, y)$ chỉ được tính nếu nó đồng thời thuộc về cả 3 hình chữ nhật.

<div class="important-note">

**📌 Dạng bài:** Duyệt ma trận (vét cạn) - Hình học
</div>
</div>

<div class="step-card border-orange">
<div class="step-badge bg-orange">Cách 1: Thuật toán Vét cạn (Subtask 1: Tọa độ nhỏ)</div>

### 💡 Ý tưởng Ma trận đánh dấu
Sử dụng một mảng 2 chiều đại diện cho tọa độ khu vườn. Với mỗi hình chữ nhật, ta duyệt qua mọi tọa độ đơn vị bên trong và tăng giá trị đánh dấu. Kết quả là số ô có giá trị đúng bằng **3**

**Mã giả thuật toán:**
<pre class="pseudocode">
<span class="kw">Khởi tạo</span> <span class="var">mtx</span>[<span class="val">max_y</span>][<span class="val">max_x</span>] = <span class="val">0</span>;
<span class="kw">Duyệt</span> qua 3 hình chữ nhật:
    <span class="kw">Lặp</span> <span class="var">i</span> từ <span class="var">y1</span> đến <span class="var">y2</span> - <span class="val">1</span>:
        <span class="kw">Lặp</span> <span class="var">j</span> từ <span class="var">x1</span> đến <span class="var">x2</span> - <span class="val">1</span>:
            <span class="var">mtx</span>[<span class="var">i</span>][<span class="var">j</span>]++;

<span class="var">kết_quả</span> = <span class="val">0</span>;
<span class="kw">Duyệt</span> toàn bộ ma trận:
    <span class="kw">Nếu</span> (<span class="var">mtx</span>[<span class="var">i</span>][<span class="var">j</span>] == <span class="val">3</span>) <span class="kw">THÌ</span> <span class="var">kết_quả</span>++;
</pre>
</div>

<div class="step-card border-green">
<div class="step-badge bg-green">Cách 2: Thuật toán Hình học (Subtask 2: Tọa độ lớn)</div>

### 💡 Tư duy tìm miền giao nhau
Ta tìm các biên **Trái, Phải, Trên, Dưới** của vùng giao bằng cách so sánh các biên của 3 hình chữ nhật:
* **Biên trái ($X_{L}$):** Lấy **Max** của các $x_1$ (Biên trái phải nằm bên phải nhất).
* **Biên dưới ($Y_{B}$):** Lấy **Max** của các $y_1$ (Biên dưới phải nằm bên trên nhất).
* **Biên phải ($X_{R}$):** Lấy **Min** của các $x_2$ (Biên phải phải nằm bên trái nhất).
* **Biên trên ($Y_{T}$):** Lấy **Min** của các $y_2$ (Biên trên phải nằm bên dưới nhất).

**Mã giả thuật toán:**
<pre class="pseudocode">
<span class="var">xL</span> = <span class="fn">max</span>(<span class="var">h1.x1</span>, <span class="var">h2.x1</span>, <span class="var">h3.x1</span>);
<span class="var">yB</span> = <span class="fn">max</span>(<span class="var">h1.y1</span>, <span class="var">h2.y1</span>, <span class="var">h3.y1</span>);
<span class="var">xR</span> = <span class="fn">min</span>(<span class="var">h1.x2</span>, <span class="var">h2.x2</span>, <span class="var">h3.x2</span>);
<span class="var">yT</span> = <span class="fn">min</span>(<span class="var">h1.y2</span>, <span class="var">h2.y2</span>, <span class="var">h3.y2</span>);

<span class="var">chiều_rộng</span> = <span class="var">xR</span> - <span class="var">xL</span>;
<span class="var">chiều_cao</span> = <span class="var">yT</span> - <span class="var">yB</span>;

<span class="kw">Nếu</span> (<span class="var">chiều_rộng</span> > <span class="val">0</span> VÀ <span class="var">chiều_cao</span> > <span class="val">0</span>) <span class="kw">THÌ</span>:
    <span class="kw">Xuất</span> <span class="var">chiều_rộng</span> * <span class="var">chiều_cao</span>;
<span class="kw">Ngược lại</span> <span class="kw">Xuất</span> <span class="val">0</span>;
</pre>
</div>
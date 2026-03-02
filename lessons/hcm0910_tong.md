## ➕ Bài: Tổng (Phân tích số thành các số hạng khác nhau) 
<br>
<div class="step-card border-blue">
<div class="step-badge bg-blue">Phân tích đề bài</div>

Tính số cách phân tích một số nguyên dương $N$ thành tổng của một hoặc nhiều số nguyên dương sao cho các số hạng đó phải **đôi một khác nhau**.

**Ví dụ:** Với $N = 6$:
- Cách 1: $6$
- Cách 2: $5 + 1$
- Cách 3: $4 + 2$
- Cách 4: $3 + 2 + 1$
Tổng cộng có **4** cách. (Kết quả cần chia lấy dư cho $10^9 + 7$).

<div class="important-note">

**📌 Dạng bài:** Quy hoạch động trên ma trận dạng bài toán đếm
</div>
</div>

<div class="step-card border-orange">
<div class="step-badge bg-orange">Subtask 1: Vét cạn (N < 100)</div>

### 💡 Ý tưởng Đệ quy (DFS)
Sử dụng phương pháp thử và sai. Với mỗi số nguyên dương $X$ tăng dần, ta có hai lựa chọn: cộng $X$ vào tổng hoặc bỏ qua để xét số tiếp theo.

**Mã giả thuật toán:**
<pre class="pseudocode">
<span class="kw">Hàm</span> <span class="fn">DFS</span>(<span class="var">x</span>, <span class="var">tổng_tạm</span>):
    <span class="kw">Nếu</span> (<span class="var">tổng_tạm</span> == <span class="var">N</span>) <span class="kw">THÌ</span> <span class="var">biến_đếm</span>++; <span class="kw">Quay_lại</span>;
    <span class="kw">Nếu</span> (<span class="var">tổng_tạm</span> > <span class="var">N</span> hoặc <span class="var">x</span> > <span class="var">N</span>) <span class="kw">THÌ</span> <span class="kw">Quay_lại</span>;
    <span class="com">// Lựa chọn 1: Chọn x vào tổng</span>
    <span class="fn">DFS</span>(<span class="var">x</span> + <span class="val">1</span>, <span class="var">tổng_tạm</span> + <span class="var">x</span>);
    <span class="com">// Lựa chọn 2: Không chọn x</span>
    <span class="fn">DFS</span>(<span class="var">x</span> + <span class="val">1</span>, <span class="var">tổng_tạm</span>);
</pre>
</div>

<div class="step-card border-green">
<div class="step-badge bg-green">Subtask 2: Quy hoạch động (N ≤ 10000)</div>

### 💡 Ý tưởng DP trên ma trận
**Bước 1: Ý nghĩa ma trận DP và bài toán cơ sở**
- Gọi `DP[i][j]` là số cách tạo ra tổng bằng `i` bằng cách chỉ sử dụng các số hạng từ tập  `{1, 2, ..., j}` và các số phải khác nhau.
- Trường hợp cơ sở: `DP[0][j] = 1` với mọi `j >= 0` (có $1$ cách tạo ra tổng $0$ là không chọn số nào)

**Bước 2: Công thức truy hồi:**
Để tính `DP[i][j]` ta xét 2 trường hợp:
- Nếu **không chọn** số `j`: số cách là `DP[i][j-1]`.
- Nếu **có chọn** số `j` (khi `i >= j`): thì số cách là `DP[i-j][j-1]`.

<div class="math-formula">
                $DP[i][j] = (DP[i][j-1] + DP[i-j][j-1]) \pmod{10^9+7}$
</div>

**Mã giả thuật toán:**
<pre class="pseudocode">
<span class="kw">Cho</span> <span class="var">j</span> từ <span class="val">0</span> tới <span class="var">N</span>: <span class="var">dp</span>[<span class="val">0</span>][<span class="var">j</span>] = <span class="val">1</span>;

<span class="kw">Duyệt</span> <span class="var">i</span> từ <span class="val">1</span> tới <span class="var">N</span>:
    <span class="kw">Duyệt</span> <span class="var">j</span> từ <span class="val">1</span> tới <span class="var">N</span>:
        <span class="var">dp</span>[<span class="var">i</span>][<span class="var">j</span>] = <span class="var">dp</span>[<span class="var">i</span>][<span class="var">j-1</span>];
        <span class="kw">Nếu</span> (<span class="var">i</span> >= <span class="var">j</span>) <span class="kw">THÌ</span>:
            <span class="var">dp</span>[<span class="var">i</span>][<span class="var">j</span>] = (<span class="var">dp</span>[<span class="var">i</span>][<span class="var">j</span>] + <span class="var">dp</span>[<span class="var">i-j</span>][<span class="var">j-1</span>]) % <span class="val">1000000007</span>;
</pre>
</div>
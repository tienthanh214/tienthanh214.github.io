---
title: "Sweep Line Technique"
excerpt: "Kỹ thuật sweepline và ứng dụng trong các bài toán về hình học"

show_date: true
tags:
  - algorithm
categories:
  - Competitive Programming
toc: true
  
---
Đang hoàn thiện ....

# Sweepline là gì?

# Ứng dụng

## Độ dài đoạn phủ
### Bài toán:
Cho *N* đoạn thẳng trên trục Ox, mỗi đoạn được biểu diễn bởi hai điểm đầu và cuối $$[a_i, b_i]$$  $$(a_i \le b_i) $$. Yêu cầu cho biết điểm có nhiều đoạn phủ lên nhất.

### Lời giải
Đây là một trong những bài kinh điển và cơ bản nhất có thể sử dụng kỹ thuật Sweepline để giải một cách gọn gàng.

Nhận thấy, điểm được phủ nhiều nhất có thể nằm ở các đầu mút.
### Cài đặt
```c++
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
  vector<pair<int, bool>> points;
  int n; cin >> n;
  for (int i = 0; i < n; ++i) {
      int l, r;
      cin >> l >> r;
      points.push_back({l, false}); // điểm bắt đầu
      points.push_back({r, true});  // điểm kết thúc
  }
  // sort các điểm tăng dần để sweep từ trái -> phải
  sort(points.begin(), points.end()); 
  // Thực hiện sweepline, xét các điểm tăng dần theo hoành độ
  int cnt = 0; // số lượng đoạn phủ lên tọa độ hiện tại
  long long total = 0;
  for (size_t i = 0; i < points.size(); ++i) {
      if (cnt > 0) { 
          // nếu có ít nhất 1 đoạn phủ lên
          // -> độ dài đoạn được phủ tăng thêm
          total += points[i].first - points[i - 1].first;
      }
      // nếu gặp điểm bắt đầu 1 đoạn thì cnt + 1
      // ngược lại nếu gặp điểm kết thúc thì cnt - 1
      cnt += points[i].second ? -1 : 1;
  }
  return 0;
}
```
## Diện tích các hình chữ nhật

### Bài toán
Cho N hình chữ nhật song song với hai trục tọa độ, hãy tính tổng diện tích mà những hình chữ nhật này phủ lên mặt phẳng

### Lời giải 
Về bản chất thì bài toán này giống với bài toán độ dài đoạn phủ được nêu ở trên, điểm khác biệt là độ dài đoạn phủ chỉ tính trên trục Ox (tức tại tung độ bằng 0), còn với hình chữ nhật thì đó chính là một đoạn phủ liên tục. Các hình chữ nhật khi chiếu lên Oy sẽ tạo thành các đoạn phủ, và việc của ta là tính tổng độ dài đoạn phủ trên trục Oy nhân với chênh lệch giữa 2 khe kề nhau trên đường sweepline theo Ox, đó chính là diện tích.

### Cài đặt
Dưới đây là cài đặt đã AC bài [AREA - SPOJ](https://vn.spoj.com/problems/AREA/)

```c++
#include <bits/stdc++.h>

using namespace std;

const int N = 1E4 + 10;
const int X = 3E4 + 10;

struct Rect {
    int y, x1, x2;
    bool open;
    Rect(int _y = 0, int _x1 = 0, int _x2 = 0, bool _open = 0) {
        y = _y; x1 = _x1; x2 = _x2; open = _open;
    }
    bool operator < (const Rect &other) const {
        if (y != other.y) return y < other.y;
        return open < other.open;
    }
};

struct SegmentTree {
    int val[X * 5], cnt[X * 5];

    void Update(int id, int l, int r, int u, int v, int key) {
        if (r < u || v < l || l > r) return;
        if (u <= l && r <= v) {
            cnt[id] += key;
            if (cnt[id]) val[id] = r - l + 1;
                else val[id] = val[id << 1] + val[id << 1 | 1];
            return;
        }
        int mid = (l + r) >> 1;
        Update(id << 1, l, mid, u, v, key);
        Update(id << 1 | 1, mid + 1, r, u, v, key);
        if (!cnt[id]) val[id] = val[id << 1] + val[id << 1 | 1];
    }
    void Update(int u, int v, int key) {
        Update(1, 0, 3E4, u, v, key);
    }
} ST;

int n;
Rect a[N * 2];

void Read_Input() {
    scanf("%d", &n);
    for (int i = 1; i <= n; ++i) {
        int x, y, u, v;
        scanf("%d%d%d%d", &x, &y, &u, &v);
        a[i] = Rect(y, x, u, 1);
        a[i + n] = Rect(v, x, u, 0);
    }
    sort(a + 1, a + 1 + 2 * n);
}

void Solve() {
    int ans = 0;
    for (int i = 1; i < 2 * n; ++i) {
        if (a[i].open) ST.Update(a[i].x1, a[i].x2 - 1, 1);
            else ST.Update(a[i].x1, a[i].x2 - 1, -1);
        ans += ST.val[1] * (a[i + 1].y - a[i].y);
    }
    printf("%d", ans);
}

int main() {
    Read_Input();
    Solve();
    return 0;
}

```
# Nguồn tham khảo
1. [Line Sweep Technique - Hackerearth][hackerearth]
2. [How to sweep like a Sir - Codeforces][codeforces]
3. [Line Sweep Algorithms - Topcoder][topcoder]

[codeforces]: https://codeforces.com/blog/entry/20377
[topcoder]: https://www.topcoder.com/thrive/articles/Line%20Sweep%20Algorithms
[hackerearth]: https://www.hackerearth.com/practice/math/geometry/line-sweep-technique/tutorial/




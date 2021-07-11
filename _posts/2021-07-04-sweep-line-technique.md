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
Cho *N* đoạn thẳng trên trục Ox, mỗi đoạn được biểu diễn bởi hai điểm đầu và cuối $$[a_i, b_i]$$ 


$$ equation $$

### Lời giải
Đây là một trong những bài kinh điển và cơ bản nhất có thể sử dụng kỹ thuật Sweepline để giải một cách gọn gàng.
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
Về bản chất thì bài toán này giống với bài toán độ dài đoạn phủ được nêu ở trên, điểm khác biệt là độ dài đoạn phủ chỉ tính trên trục Ox (tức tại tung độ bằng 0), còn với hình chữ nhật thì đó chính là một đoạn phủ liên tục. 
### Cài đặt

# Luyện tập

# Nguồn tham khảo
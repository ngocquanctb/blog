---
layout: post
title: "Vietnamese Spoofing Aware Speaker Verification (Vietnamese Post, English version below)"
author: "Ngoc Quan"
categories: facts
tags: [sample]
image: cuba-2.jpg
katex: True
---
## Giới thiệu bài toán
Bài toán chúng tôi giải quyết thuộc cuộc thi VLSP 2023 năm nay, là kết hợp của hai bài toán Speaker Verification và Audio Anti-spoofing dành riêng cho ngôn ngữ tiếng Việt. Yêu cầu chung của bài toán đó là input bao gồm 2 file audio, với tên gọi là target file và second file. Trong đó target file là file ghi âm giọng nói thật của một người(bonafide), và second file là một giọng nói có thể là thật(bonafide) hoặc giả(spoof). Model cần dự đoán và gán nhãn positive label cho cặp file thỏa mãn các điều kiện sau: Second file phải là giọng nói thật(bonafide), ngoài ra phải là của cùng người nói với target file.

## A little bit about mathematics
### Ý tưởng: Sử dụng embedding của ECAPA và AASIST sau đó cross attention vì nghĩ rằng chúng nó chứa trùng thông tin của nhau.

### Ý tưởng: DNN quá overfit, suy nghĩ đến việc dùng Machine Learning để học từ embedding thay vì DL

Note: Khi thực hiện catboost có một số ý sau:
+ Tìm được một repo implement bài tương tự nhưng là bằng tensorflow, dự định sẽ chuyển sang pytorch để dùng, nhưng... (implement rồi mới thấy mọi chuyện khó khăn hơn tưởng tượng nhiều)

+ Lúc đầu định nối 2 model LCNN và catboost trực tiếp vào nhau để train end-to-end => Rõ ràng là không khả thi
+ Cần học thêm kĩ năng fix bug model, mặc dù chỉ là code lại LCNN mà cũng khá nhiều bug
+ Chú ý rằng kích thước tensor của mọi input phải giống nhau (đến từ việc tính stft) => colate function
+ Không được thực hiện những gì quá phức tạp trong dataloader(ví dụ như VAD, tính stft...) vì quá lâu => Thay vào đó hãy tính sẵn embedding, lưu file pickle, khi cần dùng gọi trực tiếp ra ở trong dataloader
+ Lo lắng về thời gian chạy của stft(Hiện tại có khoảng có 300k file wav, mỗi file tính stft mất ít nhất 1 giây, dùng vòng for nên khả năng dùng GPU cũng ko thể tính toán song song)
+ Lo lắng tiếp :))) Tính thử với 1000 file thì embedding của 1000 files này vào khoảng 300MB, mà tập training của mình có 300k files =>>> Bao nhiêu bộ nhớ để lưu đây, trong khi kaggle output tối đa 20GB




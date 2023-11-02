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




---
layout: post
title: 遅延伝播SegmentTree
date: 2018-05-01
category: データ構造
tags: データ構造
---

## 説明
2つ配列を持つことで、セグメント木を区間に対する操作に対応させたもの。<br>
区間に操作をする際には、普通のセグメント木と同様に区間を下ろしていって、区間全体を覆うならそこにとどめておく。クエリのときに必要に応じて分割する。すると、更新と取得が$O(\log N)$回の演算で可能になる。<br>
実装では、モノイド構造体を渡すようにしている。構造体には、次のようなものを定義する。
- 要素の型 $T$
- $T$の単位元$e$
- 作用素の型 $L$
- $L$の単位元$l$
- $f(T, T) \rightarrow T$ 要素同士のマージ
- $g(T, L) \rightarrow T$ 要素と作用素のマージ
- $h(L, L) \rightarrow L$ 作用素同士のマージ

以下にモノイドの例をあげておく。
#### 区間加算-区間min
- $e = \infty$
- $l = 0$
- $f(x, y) = min(x, y), g(x, y) = x + y, h(x, y) = x + y$
#### 区間更新-区間max
- $e = 0$
- $l = 0$
- $f(x, y) = max(x, y)$
- $g(x, y) = h(x, y) = \left\{ \begin{array}{||} a & (b = e) \\ b & (b \neq e) \end{array} \right$

{% include a.html code="lazysegtree.cpp" %}
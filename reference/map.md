#map
`map` はユニークな要素を格納する連想コンテナの一種であり、キーとそれに対応する値を格納する。 
連想コンテナは特にそれらキーによる要素アクセスが効率的になるようよう設計されたコンテナである（要素への相対位置または絶対位置によるアクセスが効率的であるシーケンシャルコンテナとは異なる）。 
内部的には、`map` 内の要素は、コンテナの構築時に設定された狭義の弱順序基準に従って小さいものから大きいものへとソートされる。 

`map` は一般的に、二分木として実装される。従って、連想コンテナである `map` の主な特性は以下の通りである。

- ユニークな要素のキー：互いに等しい二つのキーを持つ要素が `map` に格納されることは無い。複数の等しいキーを許す同様の連想コンテナは `multimap` を参照のこと。
- 要素の値はキーと値のpair型である。
- 要素は常に厳密で弱い順序付けに従う。
- insertとemplaceはイテレータや要素の参照に影響を与えない。

このコンテナクラスは、双方向イテレータをサポートする。

　C++ 標準テンプレートライブラリの実装において、map コンテナは 4 つのテンプレートパラメータを取る。

```cpp
namespace std {
  template <class Key, class T, class Compare = less<Key>, class Allocator = allocator<pair<const Key, T> > >
  class map;
}
```

* [less](./functional/comparisons.md)
* [allocator](./memory/allocator.md)


各テンプレートパラメータは以下のような意味である。

- `Key`: キーの型。キーの値の大小に従って自動的に並び替えられる。
- `T`: 値の型。
- `pair<const Key,T>`: 要素の型。
- `Compare`: 比較クラス。このクラスは 2 つの引数（同じ型）をとり `bool` 値を返す。狭義の弱順序において `a` が `b` よりも前の場所に位置づけられる場合に `true` である。これはクラスが関数呼び出しオブジェクトを実装したクラスであっても良いし関数ポインタであっても良い（例は コンストラクタ を参照）。これは、`operator<()` を適用( `a < b` )したときと同じ値を返す `less<Key>` がデフォルトである。
- `Allocator`: ストレージアロケーションモデルを決定づける、アロケータオブジェクトの型である。デフォルトでは、`Key` への `allocator` クラステンプレート（これは値に依存しないシンプルなメモリ確保モデルを定義する）が使われる。


##メンバ関数

| | |
|------------------------------------------------------------------------------------------------|--------------------------------------------------|
| [`(constructor)`](./map/map.md) | コンストラクタ |
| [`(destructor)`](./map/-map.md) | デストラクタ |
| [`operator=`](./map/op_assign.md) | 代入演算子 |
| [`get_allocator`](./map/get_allocator.md) | アロケータオブジェクトを取得する |

##イテレータ

| | |
|-------------------------------------------------------------------------------------------|--------------------------------------------------|
| [`begin, cbegin`](./map/begin.md) | 先頭を指すイテレータを取得する |
| [`end, cend`](./map/end.md) | 末尾を指すイテレータを取得する |
| [`rbegin, crbegin`](./map/rbegin.md) | 末尾を指す逆イテレータを取得する |
| [`rend, crend`](./map/rend.md) | 先頭を指す逆イテレータを取得する |

##領域

| | |
|--------------------------------------------------------------------------------------|-----------------------------------------------------|
| [`empty`](./map/empty.md) | コンテナが空であるかどうかを調べる |
| [`size`](./map/size.md) | 要素数を取得する |
| [`max_size`](./map/max_size.md) | 格納可能な最大の要素数を取得する |

##コンテナの変更

| | |
|----------------------------------------------------------------------------------------------|----------------------------------------------|
| [`clear`](./map/clear.md) | 全ての要素を削除する |
| [`insert`](./map/insert.md) | 要素を挿入する |
| [`emplace`](./map/emplace.md) | 要素を直接構築する(C++11) |
| [`emplace_hint`](./map/emplace_hint.md) | ヒントを使って要素を直接構築する(C++11) |
| [`erase`](./map/erase.md) | 要素を削除する |
| [`swap`](./map/swap.md) | コンテンツを交換する |

##要素アクセス

| | |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| [`operator[]`](./map/op_at.md) | 指定したキーを持つ要素を返す |
| [`count`](./map/count.md) | 指定したキーにマッチする要素の数を返す |
| [`find`](./map/find.md) | 指定したキーで要素を探す |
| [`equal_range`](./map/equal_range.md) | 指定したキーにマッチする要素範囲を返す |
| [`lower_bound`](./map/lower_bound.md) | 与えられた値より小さくない最初の要素へのイテレータを返す |
| [`upper_bound`](./map/upper_bound.md) | 特定の値よりも大きい最初の要素へのイテレータを返す |

##オブザーバー

| | |
|------------------------------------------------------------------------------------------|--------------------------------------|
| [`key_comp`](./map/key_comp.md) | キーを比較した結果を返す |
| [`value_comp`](./map/value_comp.md) | 値を比較した結果を返す |


##非メンバ関数

| | |
|------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| [`operator==`](./map/op_equal.md) | 左辺と右辺が等しいかの判定を行う |
| [`operator!=`](./map/op_not_equal.md) | 左辺と右辺が等しくないかの判定を行う |
| [`operator<`](./map/op_less_than.md) | 左辺が右辺より小さいかの判定を行う |
| [`operator<=`](./map/op_greater_equal.md) | 左辺が右辺より小さいか等しいかの判定を行う |
| [`operator>`](./map/op_greater_than.md) | 左辺が右辺より大きいかの判定を行う |
| [`operator>=`](./map/op_greater_equal.md) | 左辺が右辺より大きいか等しいかの判定を行う |
| [`swap`](./map/swap.md) | 2つの`map`オブジェクトを入れ替える |



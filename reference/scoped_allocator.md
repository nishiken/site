#scoped_allocator
`<scoped_allocator>`ヘッダでは、`vector<string>`のような、要素とコンテナで両方にメモリ確保が必要になった場合、コンテナと要素で同じアロケータからメモリ確保する戦略をとるためのアロケータアダプタを提供する。

| | |
|------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| [`scoped_allocator_adaptor`](./scoped_allocator/scoped_allocator_adaptor.md) | 入れ子になったオブジェクトに同じアロケータを使用するためのアダプタ(class template) |


##バージョン
###言語
- C++11


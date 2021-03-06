---
title: '* 演算子 - C# リファレンス'
ms.custom: seodec18
ms.date: 04/04/2018
f1_keywords:
- '*_CSharpKeyword'
helpviewer_keywords:
- multiplication operator (*) [C#]
- '* operator [C#]'
ms.assetid: abd9a5f0-9b24-431e-971a-09ee1c45c50e
ms.openlocfilehash: f4490c4632d9344eb879ea55c20787b838781d91
ms.sourcegitcommit: 5c36aaa8299a2437c155700c810585aff19edbec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54333734"
---
# <a name="-operator-c-reference"></a>* 演算子 (C# リファレンス)

乗算演算子 (`*`) は、そのオペランドの積を計算します。 すべての数値型には定義済みの乗算演算子があります。

また、`*` はポインターへの読み書きを可能にする逆参照演算子としても機能します。

## <a name="remarks"></a>コメント

`*` 演算子は、ポインターの種類の宣言、およびポインターの逆参照にも使用されます。 この演算子は、[unsafe](../keywords/unsafe.md) キーワードの使用によって示され、[/unsafe](../compiler-options/unsafe-compiler-option.md) コンパイラ オプションを必要とする、unsafe コンテキストでのみ使用できます。  逆参照演算子は、間接演算子とも呼ばれます。

ユーザー定義型は二項 `*` 演算子をオーバーロードできます (「[演算子](../keywords/operator.md)」を参照)。 二項演算子をオーバーロードすると、対応する代入演算子がある場合、これも暗黙的にオーバーロードされます。

## <a name="example"></a>例

[!code-csharp-interactive[csRefOperators#50](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefOperators/CS/csrefOperators.cs#50)]

## <a name="example"></a>例

[!code-csharp[csRefOperators#51](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefOperators/CS/csrefOperators.cs#51)]

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [アンセーフ コードとポインター](../../programming-guide/unsafe-code-pointers/index.md)
- [C# 演算子](index.md)
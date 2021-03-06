---
title: IsFalse 演算子 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.isfalse
helpviewer_keywords:
- AndAlso operator [Visual Basic]
- IsFalse operator [Visual Basic]
ms.assetid: 37fc9dbf-e5cc-4570-b93f-7213447974df
ms.openlocfilehash: ec8d7bcd2f4ca3fb1c74f4edcf6ec8af78fd144d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54740423"
---
# <a name="isfalse-operator-visual-basic"></a>IsFalse 演算子 (Visual Basic)
式は、かどうかを判断します`False`します。  
  
 呼び出すことはできません`IsFalse`明示的に、コードが、Visual Basic のコンパイラが使用できることからコードを生成する`AndAlso`句。 クラスまたは構造体を定義しでその型の変数を使用している場合、`AndAlso`句が定義する必要があります`IsFalse`でそのクラスまたは構造体。  
  
 コンパイラは、`IsFalse`と`IsTrue`演算子として、*ペア*します。 つまり、それらのいずれかを定義する場合をする必要がありますも定義、もう 1 つ。  
  
> [!NOTE]
>  `IsFalse`演算子は、*オーバー ロードされた*、いるクラスまたは構造体を再定義できますの動作のオペランドがそのクラスまたは構造体の型を持つときにすることを意味します。 コードは、このようなクラスまたは構造体に、この演算子を使用する場合は、再定義された動作を確認ください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例の定義を含む構造体のアウトラインを定義する、`IsFalse`と`IsTrue`演算子。  
  
 [!code-vb[VbVbalrOperators#28](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/isfalse-operator_1.vb)]  
  
## <a name="see-also"></a>関連項目
- [IsTrue 演算子](../../../visual-basic/language-reference/operators/istrue-operator.md)
- [方法: 演算子を定義します。](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [AndAlso 演算子](../../../visual-basic/language-reference/operators/andalso-operator.md)

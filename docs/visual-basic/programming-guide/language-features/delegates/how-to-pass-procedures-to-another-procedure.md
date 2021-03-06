---
title: '方法: Visual Basic での別のプロシージャに渡す'
ms.date: 07/20/2015
helpviewer_keywords:
- AddressOf operator [Visual Basic]
- delegates [Visual Basic], passing procedures
ms.assetid: 5adbba15-5a1d-413f-ab3e-3ff6cc0a4669
ms.openlocfilehash: cf5a8447cbedcd8071da98ac6763ff06eb608199
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54506759"
---
# <a name="how-to-pass-procedures-to-another-procedure-in-visual-basic"></a>方法: Visual Basic での別のプロシージャに渡す
この例では、プロシージャを別のプロシージャに渡すデリゲートを使用する方法を示します。  
  
 デリゲートは、Visual Basic での他の種類のように使用できる型です。 `AddressOf`演算子プロシージャ名に適用する場合は、デリゲート オブジェクトを返します。  
  
 この例では、プロシージャを別のプロシージャを使用して取得への参照を受け取ることができます delegate パラメーターを持つ、`AddressOf`演算子。  
  
### <a name="create-the-delegate-and-matching-procedures"></a>デリゲートと一致するプロシージャを作成します。  
  
1.  という名前のデリゲートを作成する`MathOperator`します。  
  
     [!code-vb[VbVbalrDelegates#1](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_1.vb)]  
  
2.  という名前のプロシージャを作成する`AddNumbers`パラメーターと戻り値のものと一致する`MathOperator`署名が一致するようにします。  
  
     [!code-vb[VbVbalrDelegates#2](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_2.vb)]  
  
3.  という名前のプロシージャを作成する`SubtractNumbers`と一致するシグネチャを持つ`MathOperator`します。  
  
     [!code-vb[VbVbalrDelegates#3](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_3.vb)]  
  
4.  という名前のプロシージャを作成`DelegateTest`をパラメーターとしてデリゲートを取得します。  
  
     この手順への参照を受け入れることができる`AddNumbers`または`SubtractNumbers`、署名が一致しているため、`MathOperator`署名します。  
  
     [!code-vb[VbVbalrDelegates#4](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_4.vb)]  
  
5.  という名前のプロシージャを作成する`Test`を呼び出す`DelegateTest`のデリゲートが 1 回`AddNumbers`をパラメーターとして、もう一度のデリゲートと`SubtractNumbers`をパラメーターとして。  
  
     [!code-vb[VbVbalrDelegates#5](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_5.vb)]  
  
     ときに`Test`が呼び出されると、その最初の結果を表示`AddNumbers`に機能している`5`と`3`8 であります。 結果、`SubtractNumbers`に作用する`9`と`3`が表示されたら、6 であります。  
  
## <a name="see-also"></a>関連項目
- [デリゲート](../../../../visual-basic/programming-guide/language-features/delegates/index.md)
- [AddressOf 演算子](../../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Delegate ステートメント](../../../../visual-basic/language-reference/statements/delegate-statement.md)
- [方法: デリゲート メソッドを呼び出す](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)

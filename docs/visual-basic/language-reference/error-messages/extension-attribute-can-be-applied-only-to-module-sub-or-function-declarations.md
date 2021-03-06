---
title: "'Extension' 属性は 'Module'、'Sub'、または 'Function' の各宣言にのみ適用できます"
ms.date: 07/20/2015
f1_keywords:
- bc36550
- vbc36550
helpviewer_keywords:
- BC36550
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
ms.openlocfilehash: e2e2c41d713b0b04b8bc7208a83d059f0d16bf06
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55278721"
---
# <a name="extension-attribute-can-be-applied-only-to-module-sub-or-function-declarations"></a>'Extension' 属性は 'Module'、'Sub'、または 'Function' の各宣言にのみ適用できます
Visual Basic でのデータ型を拡張する唯一の方法では、標準のモジュール内で拡張メソッドを定義します。 拡張メソッドになる、`Sub`プロシージャまたは`Function`プロシージャ。 すべての拡張メソッドは、拡張機能の属性でマークする必要があります`<Extension()>`から、<xref:System.Runtime.CompilerServices?displayProperty=nameWithType>名前空間。 必要に応じて、拡張メソッドを含むモジュールの場合は、同じ方法でマークされている可能性があります。 拡張属性の他の使用が有効ではありません。  
  
 **エラー ID:** BC36550  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
-   拡張属性を削除します。  
  
-   外側のモジュールで定義されている、方法として、拡張機能を再設計します。  
  
## <a name="example"></a>例  
 次の例では、定義、`Print`のメソッド、`String`データ型。  
  
```  
Imports StringUtility  
Imports System.Runtime.CompilerServices  
Namespace StringUtility  
    <Extension()>   
    Module StringExtensions  
        <Extension()>   
        Public Sub Print (ByVal str As String)  
            Console.WriteLine(str)  
        End Sub  
    End Module  
End Namespace  
```  
  
## <a name="see-also"></a>関連項目
- [属性の概要](../../../visual-basic/programming-guide/concepts/attributes/index.md)
- [拡張メソッド](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
- [Module ステートメント](../../../visual-basic/language-reference/statements/module-statement.md)

---
title: '方法: クリッピング領域を使用します。'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regions [Windows Forms], clipping
- regions [Windows Forms], restricting drawing surface
ms.assetid: 43d121b4-e14c-4901-b25c-2d6c25ba4e29
ms.openlocfilehash: 5482218a8d6310ce49a1f9f5f02b3b8e36c1fd90
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54590657"
---
# <a name="how-to-use-clipping-with-a-region"></a>方法: クリッピング領域を使用します。
プロパティの 1 つ、<xref:System.Drawing.Graphics>クラスは、クリップ領域。 によって実行するすべての描画を指定した<xref:System.Drawing.Graphics>オブジェクトは、そのクリップ領域に制限<xref:System.Drawing.Graphics>オブジェクト。 クリップ領域を設定するには、呼び出すことによって、<xref:System.Drawing.Graphics.SetClip%2A>メソッド。  
  
## <a name="example"></a>例  
 次の例では、1 つの多角形で構成されるパスを作成します。 コードは、そのパスに基づいて、領域を構築します。 渡されるが、地域、<xref:System.Drawing.Graphics.SetClip%2A>のメソッドを<xref:System.Drawing.Graphics>オブジェクト、および、2 つの文字列を描画します。  
  
 次の図は、クリップされた文字列を示します。  
  
 ![クリップ](../../../../docs/framework/winforms/advanced/media/clip1.png "clip1")  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.MiscLegacyTopics#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 前の例は、Windows フォームで使用するために設計されていて、<xref:System.Windows.Forms.PaintEventHandler> のパラメーターである <xref:System.Windows.Forms.PaintEventArgs> `e` を必要とします。  
  
## <a name="see-also"></a>関連項目
- [GDI+ での領域](../../../../docs/framework/winforms/advanced/regions-in-gdi.md)
- [領域の使用](../../../../docs/framework/winforms/advanced/using-regions.md)

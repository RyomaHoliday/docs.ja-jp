---
title: '方法: ScrollViewer を持つエキスパンダーを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Expander
- ScrollViewer control [WPF], with Expander control
- Expander control [WPF], creating
- controls [WPF], ScrollViewer
ms.assetid: 2ad124d2-2406-4157-aaf2-64e067298f01
ms.openlocfilehash: 8d21c7ec0172dca23f218a0d710c3976872f162c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54681964"
---
# <a name="how-to-create-an-expander-with-a-scrollviewer"></a>方法: ScrollViewer を持つエキスパンダーを作成する
この例は、作成する方法を示します、<xref:System.Windows.Controls.Expander>イメージやテキストなどの複雑なコンテンツを格納しているコントロール。 例では、コンテンツを囲むことも、<xref:System.Windows.Controls.Expander>で、<xref:System.Windows.Controls.ScrollViewer>コントロール。  
  
## <a name="example"></a>例  
 次の例を作成する方法を示しています、<xref:System.Windows.Controls.Expander>します。 この例では、 <xref:System.Windows.Controls.Primitives.BulletDecorator> 、コントロールを定義するには、画像とテキストを含む、<xref:System.Windows.Controls.HeaderedContentControl.Header%2A>します。 A<xref:System.Windows.Controls.ScrollViewer>コントロールが展開されたコンテンツ スクロール メソッドを提供します。  
  
 例では、設定に注意してください、<xref:System.Windows.FrameworkElement.Height%2A>プロパティを<xref:System.Windows.Controls.ScrollViewer>の代わりに、コンテンツにします。 場合、 <xref:System.Windows.FrameworkElement.Height%2A> 、コンテンツが設定されて、<xref:System.Windows.Controls.ScrollViewer>ユーザー コンテンツをスクロールすることはできません。 <xref:System.Windows.FrameworkElement.Width%2A>プロパティが設定されて、<xref:System.Windows.Controls.Expander>に制御し、この設定が適用されます、<xref:System.Windows.Controls.HeaderedContentControl.Header%2A>と展開されたコンテンツ。  
  
 [!code-xaml[ExpanderRichContent#CreateExpander](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#createexpander)]  
  
 [!code-csharp[ExpanderRichContent#CreateExpanderCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#createexpandercode)]  
  
## <a name="see-also"></a>関連項目
- <xref:System.Windows.Controls.Expander>
- [エキスパンダーの概要](../../../../docs/framework/wpf/controls/expander-overview.md)
- [方法トピック](../../../../docs/framework/wpf/controls/expander-how-to-topics.md)

---
title: '方法: ストーリーボード アニメーション間で HandoffBehavior を指定する'
ms.date: 03/30/2017
helpviewer_keywords:
- Storyboards [WPF], handoff behavior between animations
- animation [WPF], handoff behavior between
ms.assetid: 97bd6842-929b-49d9-813e-46553ae46472
ms.openlocfilehash: 9a27c377e2993c1e67ada508071698a541cec660
ms.sourcegitcommit: bef803e2025642df39f2f1e046767d89031e0304
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56305442"
---
# <a name="how-to-specify-handoffbehavior-between-storyboard-animations"></a>方法: ストーリーボード アニメーション間で HandoffBehavior を指定する
この例では、ストーリー ボード アニメーション間のハンドオフ動作を指定する方法を示します。 <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>プロパティの<xref:System.Windows.Media.Animation.BeginStoryboard>新しいアニメーションを指定します。 プロパティに既に適用されている既存の対話します。  
  
## <a name="example"></a>例  
 次の例では、2 つのボタン上にマウス カーソルを移動すると拡大、カーソルがすぐに移動すると、縮小を作成します。 ボタンの上にマウス カーソルをすばやく削除して場合、は、1 つ目が終了する前に、2 番目のアニメーションが適用されます。 間の差が表示されるこのような 2 つのアニメーションが重なっている場合は、<xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>値<xref:System.Windows.Media.Animation.HandoffBehavior.Compose>と<xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace>します。 値<xref:System.Windows.Media.Animation.HandoffBehavior.Compose>の値の中にアニメーション間で遷移をスムーズに重なり合うアニメーションを組み合わせて<xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace>新しいアニメーションをすぐに重複する前のアニメーションを置き換えます。  
  
 [!code-xaml[timingbehaviors_snip#HandoffBehaviorWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/HandoffBehaviorExample.xaml#handoffbehaviorwholepage)]  
  
## <a name="see-also"></a>関連項目
- <xref:System.Windows.Media.Animation.BeginStoryboard>
- <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>
- [アニメーションの概要](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)
- [アニメーションとタイミング](https://msdn.microsoft.com/library/7d83765b-d5ae-41b1-b423-80206e1124aa)
- [アニメーションとタイミングに関するトピック](animation-and-timing-how-to-topics.md)

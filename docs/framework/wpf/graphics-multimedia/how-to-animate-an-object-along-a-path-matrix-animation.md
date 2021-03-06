---
title: '方法: パスに沿ってオブジェクトをアニメーション化する (行列アニメーション)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], objects along paths (matrix animation)
- matrix animation [WPF]
ms.assetid: 7000e697-1414-468c-b915-cf66062fc49e
ms.openlocfilehash: 836f61e062b921c7e51166a35d8169f903fcbab9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54738301"
---
# <a name="how-to-animate-an-object-along-a-path-matrix-animation"></a>方法: パスに沿ってオブジェクトをアニメーション化する (行列アニメーション)
この例は、使用する方法を示します、<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>で定義されているパスに沿ってオブジェクトをアニメーション化するクラス、<xref:System.Windows.Media.PathGeometry>します。  
  
## <a name="example"></a>例  
 次の例では、以下の処理を実行し、パスに沿ってオブジェクトをアニメーション化します。  
  
-   適用対象を<xref:System.Windows.Media.MatrixTransform>移動するには、オブジェクトにします。  
  
-   使用してパスを定義、<xref:System.Windows.Media.PathGeometry>します。  
  
-   作成、<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>をアニメーション化するために使用して、<xref:System.Windows.Media.Matrix>のプロパティ、<xref:System.Windows.Media.MatrixTransform>します。 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>は、<xref:System.Windows.Media.PathGeometry>しを使用して生成<xref:System.Windows.Media.Matrix>値。  
  
 [!code-xaml[PathAnimationGallery_snippet#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexample.xaml#matrixanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExample.cs#matrixanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExample.vb#matrixanimationusingpathwholepage)]  
  
 サンプル全体については、次を参照してください。[パス アニメーションのサンプル](https://go.microsoft.com/fwlink/?LinkID=160028)します。 ジオメトリック パスの詳細については、次を参照してください。、[ジオメトリの概要](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)します。  
  
## <a name="see-also"></a>関連項目
- [アニメーションの概要](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)
- [パス アニメーションのサンプル](https://go.microsoft.com/fwlink/?LinkID=160028)
- [パス アニメーションに関する「方法」トピック](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)

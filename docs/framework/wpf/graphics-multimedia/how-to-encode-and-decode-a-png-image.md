---
title: '方法: PNG イメージのエンコードおよびデコード'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- PNG encoding [WPF]
- decoding PNG images [WPF]
- PNG decoding [WPF]
- encoding image formats [WPF]
- decoding image formats [WPF]
- encoding PNG images [WPF]
ms.assetid: 3d31d186-af73-47f0-b5a7-c26ae46409a6
ms.openlocfilehash: 3e3f4d498b18901538b1d6df0ade3b8017407346
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54740126"
---
# <a name="how-to-encode-and-decode-a-png-image"></a>方法: PNG イメージのエンコードおよびデコード
次の例では、デコードおよびエンコードする方法、[!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)]特定を使用するイメージ<xref:System.Windows.Media.Imaging.PngBitmapDecoder>と<xref:System.Windows.Media.Imaging.PngBitmapEncoder>オブジェクト。  
  
## <a name="example"></a>例  
 デコードする方法を示します、[!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)]イメージを使用して、<xref:System.Windows.Media.Imaging.PngBitmapDecoder>から、<xref:System.IO.FileStream>します。  
  
 [!code-cpp[PngBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#1)]
 [!code-csharp[PngBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#1)]
 [!code-vb[PngBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#1)]  
  
## <a name="example"></a>例  
 エンコードする方法を示します、<xref:System.Windows.Media.Imaging.BitmapSource>に、[!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)]イメージを使用して、<xref:System.Windows.Media.Imaging.PngBitmapEncoder>します。  
  
 [!code-cpp[PngBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#4)]
 [!code-csharp[PngBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#4)]
 [!code-vb[PngBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#4)]  
  
## <a name="see-also"></a>関連項目
- [イメージングの概要](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)

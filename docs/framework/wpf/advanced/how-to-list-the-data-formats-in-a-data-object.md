---
title: '方法: データ オブジェクト内のデータ形式の一覧を表示する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drag-and-drop [WPF], listing data formats
- DataFormats class [WPF]
- data formats [WPF], listing
ms.assetid: 18e7ba4b-ccef-4815-ae2d-3a32891010c0
ms.openlocfilehash: 7d96cc7f7327ff7d33cf1147dbae75bc7620e310
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54595891"
---
# <a name="how-to-list-the-data-formats-in-a-data-object"></a>方法: データ オブジェクト内のデータ形式の一覧を表示する
次の例を使用する方法を示して、<xref:System.Windows.DataObject.GetFormats%2A>メソッドのオーバー ロードは、各データ オブジェクトで使用できるデータ形式を示す文字列の配列を取得します。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例を使用して、 <xref:System.Windows.DataObject.GetFormats%2A> (ネイティブおよび自動変換可能) は、データ オブジェクトで使用可能なすべてのデータ形式を示す文字列の配列を取得するオーバー ロードします。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例を使用して、<xref:System.Windows.DataObject.GetFormats%2A>データ オブジェクト (自動変換できるデータの形式はフィルター処理) で使用可能なデータ形式だけを示す文字列の配列を取得するオーバー ロードします。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats_nativeonly)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats_nativeonly)]  
  
## <a name="see-also"></a>関連項目
- <xref:System.Windows.IDataObject>
- [ドラッグ アンド ドロップの概要](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)

---
title: '方法: .NET Framework ストリームと Windows ランタイム ストリームの間で変換を行う (Windows のみ)'
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 23a763ea-8348-4244-9f8c-a4280b870b47
author: mairaw
ms.author: mairaw
ms.openlocfilehash: dc38e69a79af7c7220b8e3b55d4cb1f4ca3695f6
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55255199"
---
# <a name="how-to-convert-between-net-framework-and-windows-runtime-streams-windows-only"></a>方法: .NET Framework ストリームと Windows ランタイム ストリームの間で変換を行う (Windows のみ)

UWP アプリ用 .NET Framework は、完全な .NET Framework のサブセットです。 UWP アプリのセキュリティおよびその他の要件のために、ファイルを開いたり読み取ったりするために使用する .NET Framework API の完全なセットを使用できません。 詳細については、「[.NET for UWP apps overview](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))」(UWP アプリ用 .NET の概要) を参照してください。 ただし、他のストリームの処理操作のために .NET Framework API を使用することもできます。 これらのストリームを操作するには、<xref:System.IO.MemoryStream> や <xref:System.IO.FileStream> などの .NET Framework ストリーム型と、<xref:Windows.Storage.Streams.IInputStream>、<xref:Windows.Storage.Streams.IOutputStream>、<xref:Windows.Storage.Streams.IRandomAccessStream> などの Windows ランタイム ストリームの間で変換できます。

[System.IO.WindowsRuntimeStreamExtensions](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.aspx) クラスには、これらの変換を簡単にできるようにするメソッドが含まれています。 ただし、次のセクションで説明するように、.NET Framework と Windows ランタイムのストリームの間にある根本的な違いにより、これらのメソッドの使用結果に影響があります。

## <a name="convert-from-a-windows-runtime-to-a-net-framework-stream"></a>Windows ランタイムから .NET Framework ストリームに変換する
Windows ランタイム ストリームから .NET Framework ストリームに変換するには、次の [System.IO.WindowsRuntimeStreamExtensions](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.aspx) メソッドのうちの 1 つを使用します。

- [System.IO.WindowsRuntimeStreamExtensions.AsStream](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asstream.aspx) では、Windows ランタイムのランダム アクセス ストリームが、UWP アプリ用 .NET のマネージド ストリームに変換されます。
  
- [System.IO.WindowsRuntimeStreamExtensions.AsStreamForWrite](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asstreamforwrite.aspx) では、Windows ランタイムの出力ストリームが、UWP アプリ用 .NET のマネージド ストリームに変換されます。
  
- [System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asstreamforread.aspx) では、Windows ランタイムの入力ストリームが、UWP アプリ用 .NET のマネージド ストリームに変換されます。

Windows ランタイムでは、読み取り専用、書き込み専用、または読み取りと書き込みをサポートするストリームの種類が提供されています。 Windows ランタイム ストリームを .NET Framework ストリームに変換するとき、これらの機能は維持されます。 さらに、Windows ランタイム ストリームを .NET Framework ストリームに変換してから元に戻すと、元の Windows ランタイム インスタンスに戻ります。 

変換する Windows ランタイム ストリームの機能と一致する変換メソッドを使用することをお勧めします。 ただし、<xref:Windows.Storage.Streams.IRandomAccessStream> は読み取りも書き込みも可能なので (<xref:Windows.Storage.Streams.IOutputStream> と <xref:Windows.Storage.Streams.IInputStream> の両方を実装しているので)、変換メソッドでは元のストリームの機能が維持されます。 たとえば、[System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asstreamforread.aspx) を使用して <xref:Windows.Storage.Streams.IRandomAccessStream> を変換すると、変換された .NET Framework ストリームは読み取り可能だけに制限されません。 書き込みも可能です。

## <a name="example-convert-windows-runtime-random-access-to-net-framework-stream"></a>例:Windows ランタイム ランダム アクセスを、.NET Framework ストリームに変換する
Windows ランタイム ランダム アクセス ストリームを .NET Framework ストリームに変換するには、[System.IO.WindowsRuntimeStreamExtensions.AsStream](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asstream.aspx) メソッドを使用します。

次のコード例では、ファイルを選択するように求められ、そのファイルが Windows ランタイム API で開かれた後、.NET Framework ストリームに変換されます。 ストリームを読み取って、テキスト ブロックに出力します。 通常、結果を出力する前に .NET Framework API でストリームを処理します。

この例を実行するには、`TextBlock1` という名前のテキスト ブロックと `Button1` という名前のボタンを含む UWP XAML アプリを作成します。 ボタン クリック イベントを、例で示されている `button1_Click` メソッドに関連付けます。

  [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage1.xaml.cs)]
  [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage1.xaml.vb)]

## <a name="convert-from-a-net-framework-to-a-windows-runtime-stream"></a>.NET Framework から Windows ランタイム ストリームに変換する
.NET Framework ストリームから Windows ランタイム ストリームに変換するには、次のいずれかの [System.IO.WindowsRuntimeStreamExtensions](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.aspx) メソッドを使用します。

- [System.IO.WindowsRuntimeStreamExtensions.AsInputStream](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asinputstream.aspx) では、UWP アプリ用 .NET のマネージド ストリームが、Windows ランタイムの入力ストリームに変換されます。
  
- [System.IO.WindowsRuntimeStreamExtensions.AsOutputStream](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asoutputstream.aspx) では、UWP アプリ用 .NET のマネージド ストリームが、Windows ランタイムの出力ストリームに変換されます。
  
- [AsRandomAccessStream](../../../docs/standard/cross-platform/windowsruntimestreamextensions-asrandomaccessstream-method.md) では、UWP アプリ用 .NET のマネージド ストリームが、Windows ランタイムで読み取りまたは書き込みに使用できるランダム アクセス ストリームに変換されます。

.NET Framework ストリームを Windows ランタイム ストリームに変換する場合、変換されたストリームの機能は元のストリームによって異なります。 たとえば、元のストリームで読み取りと書き込みの両方がサポートされている場合、[System.IO.WindowsRuntimeStreamExtensions.AsInputStream](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.asinputstream.aspx) を呼び出してストリームを変換すると、返される型は `IRandomAccessStream` になります。 `IRandomAccessStream` では `IInputStream` と `IOutputStream` が実装されており、読み取りと書き込みがサポートされます。

.NET Framework ストリームでは、変換後も複製はサポートされません。 .NET Framework ストリームを Windows ランタイム ストリームに変換し、<xref:Windows.Storage.Streams.RandomAccessStreamOverStream.CloneStream%2A> を呼び出す <xref:Windows.Storage.Streams.InMemoryRandomAccessStream.GetInputStreamAt%2A> または <xref:Windows.Storage.Streams.IRandomAccessStream.GetOutputStreamAt%2A> を呼び出した場合、または <xref:Windows.Storage.Streams.RandomAccessStreamOverStream.CloneStream%2A> を直接呼び出した場合は、例外が発生します。

## <a name="example-convert-net-framework-to-windows-runtime-random-access-stream"></a>例:.NET Framework を Windows ランタイム ランダム アクセス ストリームに変換する

次の例で示すように、.NET Framework ストリームから Windows ランタイム ランダム アクセス ストリームに変換するには、[AsRandomAccessStream](../../../docs/standard/cross-platform/windowsruntimestreamextensions-asrandomaccessstream-method.md) メソッドを使用します。

> [!IMPORTANT]
> 使用している .NET Framework ストリームがシークをサポートすること、またはそれを実行するストリームにコピーすることを確認します。 この確認には、 <xref:System.IO.Stream.CanSeek%2A?displayProperty=nameWithType> プロパティを使用できます。

この例を実行するには、.NET Framework 4.5.1 を対象とし、`TextBlock2` という名前のテキスト ブロックと `Button2` という名前のボタンを含む、UWP XAML アプリを作成します。 ボタン クリック イベントを、例で示されている `button2_Click` メソッドに関連付けます。

  [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage2.xaml.cs)]
  [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](~/samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage2.xaml.vb)]

## <a name="see-also"></a>関連項目

- [クイック スタート:ファイルの読み取りと書き込みを行う (Windows)](https://msdn.microsoft.com/library/windows/apps/hh464978.aspx)  
- [Windows ストア アプリ用 .NET の概要](https://msdn.microsoft.com/library/windows/apps/br230302.aspx)  
- [Windows ストア アプリのための .NET:サポートされる API](https://msdn.microsoft.com/library/windows/apps/br230232.aspx)  

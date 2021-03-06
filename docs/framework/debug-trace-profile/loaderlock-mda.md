---
title: loaderLock MDA
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- LoaderLock MDA
- MDAs (managed debugging assistants), loader locks
- managed debugging assistants (MDAs), loader locks
- operating system loader locks
- loader locks
- locks, threads
ms.assetid: 8c10fa02-1b9c-4be5-ab03-451d943ac1ee
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1001777f00524f3a183e1641718b9d3121c94e66
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637938"
---
# <a name="loaderlock-mda"></a>loaderLock MDA
`loaderLock` マネージド デバッグ アシスタント (MDA) は、Microsoft Windows オペレーティング システムのローダー ロックを保持しているスレッド上でマネージド コードを実行する試行を検出します。  このような実行は、デッドロックの原因になる可能性があり、オペレーティング システムのローダーが初期化する前に DLL が使用される可能性があるため、不適切です。  
  
## <a name="symptoms"></a>現象  
 オペレーティング システムのローダー ロック内でコードを実行する場合に発生する最も一般的なエラーは、ローダー ロックを必要とする他の Win32 関数を呼び出そうとしたときにスレッドがデッドロックする問題です。  このような関数の例として、`LoadLibrary`、`GetProcAddress`、`FreeLibrary`、`GetModuleHandle` があります。  アプリケーションはこれらの関数を直接呼び出さない可能性があります。<xref:System.Reflection.Assembly.Load%2A> など高位の呼び出しや、プラットフォーム呼び出しメソッドの最初の呼び出しの結果として共通言語ランタイム (CLR) からこれらの関数が呼び出される可能性があります。  
  
 スレッドが別スレッドの開始または完了を待機している場合にもデッドロックが発生する可能性があります。  スレッドが実行を開始または完了した場合、影響を受ける DLL にイベントを配信するためにオペレーティング システムのローダー ロックを獲得する必要があります。  
  
 最後に、オペレーティング システムのローダーが DLL を適切に初期化する前に、それらの DLL の呼び出しが発生する場合があります。  デッドロック エラーの場合、デッドロックに関係する全スレッドのスタックを調べることで診断できますが、この MDA を使用せずに初期化されていない DLL の使用を診断することは非常に困難です。  
  
## <a name="cause"></a>原因  
 .NET Framework バージョン 1.0 または 1.1 用に構築されたマネージド/アンマネージド混在 C++ アセンブリの場合、特別な措置 (**/NOENTRY** とリンクするなど) を取っていなければ、一般的にローダー ロック内でマネージド コードを実行しようとします。
  
 .NET Framework バージョン 2.0 用に構築されたマネージ/アンマネージ混在 C++ アセンブリの場合、このような問題の影響をあまり受けません。オペレーティング システムのルールに違反するアンマネージ DLL を使用するアプリケーションと同程度に少ないリスクです。  たとえば、アンマネージド DLL の `DllMain` エントリ ポイントが `CoCreateInstance` を呼び出して、COM に公開されているマネージド オブジェクトを取得する場合、結果として、ローダー ロック内のマネージド コードを実行することになります。 .NET Framework バージョン 2.0 以降のローダー ロックの問題については、「[混在アセンブリの初期化](/cpp/dotnet/initialization-of-mixed-assemblies)」を参照してください。  
  
## <a name="resolution"></a>解像度  
 Visual C++ .NET 2002 および Visual C++ .NET 2003 では、`/clr` コンパイラ オプションを指定してコンパイルされた DLL は、読み込み時に非確定的にデッドロックを生じる可能性があります。この問題は、混在モード DLL 読み込み時の問題 (またはローダー ロックの問題) と呼ばれていました。 Visual C++ 2005 以降の場合、混在モード DLL の読み込みプロセスで、このような確定的でない場合の問題はほとんどなくなりました。 ただし、ローダー ロックが (確定的に) 発生する可能性のあるシナリオはいくつか残っています。 その他のローダー ロック問題の原因と解決策の詳細については、「[混在アセンブリの初期化](/cpp/dotnet/initialization-of-mixed-assemblies)」を参照してください。 このトピックでローダー ロックの問題が特定できない場合は、スレッドのスタックを調べて、ローダー ロックが発生している理由と問題の解決方法を判断する必要があります。 この MDA をアクティブにしたスレッドのスタック トレースを確認してください。  オペレーティング システムのローダー ロックを保持しているときに、スレッドが不正にマネージド コードを呼び出そうとしています。  スタックに DLL の `DllMain` または同等のエントリ ポイントが存在するはずです。  このようなエントリ ポイント内から実行が許可されることについて、オペレーティング システムのルールは非常に制限されています。  オペレーティング システムのルールでは、あらゆるマネージド実行が除外されています。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 通常、プロセス内の複数のスレッドでデッドロックが発生します。  多くの場合、このようなスレッドの 1 つはガベージ コレクションの実行を担当しているため、このデッドロックによってプロセス全体に重大な影響が及ぶ可能性があります。  さらに、オペレーティング システムのローダー ロックが必要な追加の操作も実行できなくなります。たとえば、アセンブリの読み込みまたはアンロード、スレッドの開始や終了などの操作です。  
  
 まれではありますが、初期化される前に呼び出された DLL で、アクセス違反などの問題が発生する可能性もあります。  
  
## <a name="output"></a>出力  
 この MDA は、不正なマネージド実行が試行されていることを報告しています。  スレッドのスタックを調べて、ローダー ロックが発生している理由と問題の解決方法を判断する必要があります。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <loaderLock/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目
- [マネージド デバッグ アシスタントによるエラーの診断](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)

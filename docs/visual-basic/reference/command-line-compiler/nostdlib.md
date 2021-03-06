---
title: -nostdlib (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- nostdlib compiler option [Visual Basic]
- -nostdlib compiler option [Visual Basic]
- /nostdlib compiler option [Visual Basic]
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
ms.openlocfilehash: 32a5b0531851e9f8b4280e8d2908bfe2d011bf90
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54547724"
---
# <a name="-nostdlib-visual-basic"></a>-nostdlib (Visual Basic)
コンパイラが自動的に標準のライブラリを参照します。  
  
## <a name="syntax"></a>構文  
  
```  
-nostdlib  
```  
  
## <a name="remarks"></a>Remarks  
 `-nostdlib`オプションは、System.dll アセンブリへの自動参照を削除し、コンパイラが Vbc.rsp ファイルを読み取ることを防ぎます。 Vbc.exe のファイルと同じディレクトリにある、Vbc.rsp ファイルを一般的に使用される参照[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]アセンブリとインポート、`System`と`Microsoft.VisualBasic`名前空間。  
  
> [!NOTE]
>  Mscorlib.dll および Microsoft.VisualBasic.dll のアセンブリは、常に参照されます。  
  
> [!NOTE]
>  `-nostdlib`オプションは、Visual Studio 開発環境内からは使用できません。 コマンドラインからコンパイルする場合にのみ使用可能なです。  
  
## <a name="example"></a>例  
 次のコードのコンパイル`T2.vb`標準ライブラリを参照することがなく。 設定する必要があります、`_MYTYPE`条件付きコンパイル定数文字列を削除するには、「空」に、`My`オブジェクト。  
  
```console
vbc -nostdlib -define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## <a name="see-also"></a>関連項目
- [-noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)
- [Visual Basic のコマンド ライン コンパイラ](../../../visual-basic/reference/command-line-compiler/index.md)
- [コンパイル コマンド ラインのサンプル](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [My で利用可能なオブジェクトのカスタマイズ](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)

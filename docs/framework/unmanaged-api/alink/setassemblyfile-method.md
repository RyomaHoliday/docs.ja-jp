---
title: SetAssemblyFile メソッド
ms.date: 03/30/2017
api_name:
- IALink.SetAssemblyFile
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetAssemblyFile
helpviewer_keywords:
- SetAssemblyFile method
ms.assetid: 3a912787-f139-43ca-a841-8bbda3107ecf
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 006360203518f74adb964634af52505a71d51473
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54587100"
---
# <a name="setassemblyfile-method"></a>SetAssemblyFile メソッド
ビルドするアセンブリの名前を割り当てます。 非バインド モジュールを生成するときに使用しないでください。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT SetAssemblyFile(  
    LPCWSTR pszFilename,  
    IMetaDataEmit* pEmitter,  
    AssemblyFlags afFlags,  
    mdAssembly* pAssemblyID  
) PURE;  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszFilename`  
 マニフェスト ファイルの完全修飾名。  
  
 `pEmitter`  
 ポインター [IMetaDataEmit インターフェイス](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)インターフェイス。  
  
 `afFlags`  
 定義されているフラグ[AssemblyFlags 列挙体](../../../../docs/framework/unmanaged-api/metadata/assemblyflags-enumeration.md)します。  
  
 `pAssemblyID`  
 結果として得られるアセンブリの ID へのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は、S_OK を返します。  
  
## <a name="requirements"></a>必要条件  
 Alink.h が必要です。  
  
## <a name="see-also"></a>関連項目
- [IALink インターフェイス](../../../../docs/framework/unmanaged-api/alink/ialink-interface.md)
- [IALink2 インターフェイス](../../../../docs/framework/unmanaged-api/alink/ialink2-interface.md)
- [ALink API](../../../../docs/framework/unmanaged-api/alink/index.md)

---
title: ICorDebugAssembly3::EnumerateContainedAssemblies メソッド
ms.date: 03/30/2017
ms.assetid: 98f15b05-afad-4616-9e2a-1a9af31948b6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: aa99e7289e0e86032f7bb85bbe209932f5c50d16
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54627578"
---
# <a name="icordebugassembly3enumeratecontainedassemblies-method"></a>ICorDebugAssembly3::EnumerateContainedAssemblies メソッド
このアセンブリに含まれているアセンブリの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT EnumerateContainedAssemblies(  
    ICorDebugAssemblyEnum **ppAssemblies  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppAssemblies`  
 [out]列挙子である ICorDebugAssemblyEnum インターフェイス オブジェクトのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 この `S_OK` オブジェクトがコンテナーの場合は、`ICorDebugAssembly3`。それ以外の場合は、`S_FALSE` で、列挙子は空です。  
  
## <a name="remarks"></a>Remarks  
 含まれているアセンブリを列挙するためにシンボルが必要です。 シンボルがない場合、メソッドは `S_FALSE` を返し、有効な列挙子は提供されません。  
  
> [!NOTE]
>  このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**[システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目
- [ICorDebugAssembly3 インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebugassembly3-interface.md)
- [デバッグ インターフェイス](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)

---
title: CorDebugThreadState 列挙型
ms.date: 03/30/2017
api_name:
- CorDebugThreadState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugThreadState
helpviewer_keywords:
- CorDebugThreadState enumeration [.NET Framework debugging]
ms.assetid: a3ccdf18-4ec6-494d-9024-48e5c8c724f5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2296f6e386f35aed91a8aea4392a9cd00ec27ccb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54724361"
---
# <a name="cordebugthreadstate-enumeration"></a>CorDebugThreadState 列挙型
デバッグのスレッドの状態を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
typedef enum CorDebugThreadState {  
    THREAD_RUN,  
    THREAD_SUSPEND  
} CorDebugThreadState;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`THREAD_RUN`|デバッグ イベントが発生しない限り、スレッドは、自由に実行されます。|  
|`THREAD_SUSPEND`|スレッドは実行できません。|  
  
## <a name="remarks"></a>Remarks  
 デバッガーを使用して、`CorDebugThreadState`スレッドの実行を制御する列挙。 使用してスレッドの状態を設定することができます、 [icordebugthread::setdebugstate](../../../../docs/framework/unmanaged-api/debugging/icordebugthread-setdebugstate-method.md)または[icordebugcontroller::setallthreadsdebugstate](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-setallthreadsdebugstate-method.md)メソッド。  
  
 提供されるコールバック、 [API をホストしている](../../../../docs/framework/unmanaged-api/hosting/index.md)メッセージ ポンプを使用するため、中断状態は必要ありません。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**[システム要件](../../../../docs/framework/get-started/system-requirements.md)に関するページを参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDegug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
- [列挙型のデバッグ](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)

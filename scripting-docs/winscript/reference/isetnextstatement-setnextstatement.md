---
title: ISetNextStatement::SetNextStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISetNextStatement.SetNextStatement
apilocation:
- scrobj.dll
ms.assetid: c5534f3b-39a5-4466-b8fc-69b717c6eee9
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d21dafcd8cdb762e39f0cfcbde1162dd66c275ec
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733876"
---
# <a name="isetnextstatementsetnextstatement"></a>ISetNextStatement::SetNextStatement
Este método atualizará o contexto do código próximo que pode executar o interpretador de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetNextStatement(  
   IDebugStackFrame*  pStackFrame,  
   IDebugCodeContext*  pCodeContext  
)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pStackFrame`  
 [in] Ponteiro para um objeto de quadro de pilha.  
  
 `pCodeContext`  
 [in] Ponteiro para um objeto de contexto de código.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Interface ISetNextStatement](../../winscript/reference/isetnextstatement-interface.md)
---
title: Pontos de interrupção (Visual Studio SDK) | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 194551141ed6d56344a4ed49962df41fd3b8d2ae
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "47460980"
---
# <a name="breakpoints-visual-studio-sdk"></a>Pontos de interrupção (SDK do Visual Studio)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A versão mais recente deste tópico pode ser encontrada em [pontos de interrupção (SDK do Visual Studio)](https://docs.microsoft.com/visualstudio/extensibility/debugger/breakpoints-visual-studio-sdk).  
  
Há três tipos de pontos de interrupção: pendente, associação e o erro.  
  
 **Um ponto de interrupção:**  
  
-   É uma abstração que contém todas as informações necessárias para associar um ponto de interrupção para um ou mais contextos de código em um ou mais programas. Cada vez que um programa que está sendo depurado causa o código para carregar, o mecanismo de depuração verifica todos os pontos de interrupção pendentes para ver se elas podem ser associadas.  
  
     Um ponto de interrupção pendente em si nunca se associa ao código, mas em vez disso, coleta e deve conter todos os acoplado pontos de interrupção que ele gera.  
  
-   É representado por um [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) interface.  
  
 **Um ponto de interrupção associado:**  
  
-   É uma abstração para um ponto de interrupção associada com ou associada a um contexto de código único. Cada ponto de interrupção associado é gerado em resposta a um ponto de interrupção pendente. Um ponto de interrupção pendente pode, no entanto, gerar mais de um ponto de interrupção associado.  
  
     Quando o código é descarregado, um ponto de interrupção associado pode ser desacoplado e descartado.  
  
-   É representado por um [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) interface.  
  
 **Um ponto de interrupção de erro:**  
  
-   É uma abstração para descrever um erro ao tentar associar um ponto de interrupção pendente para um contexto de código. Um ponto de interrupção de erro descreve um erro no local ou na expressão de ponto de interrupção em si. Para obter mais informações, consulte [associação de pontos de interrupção](../../extensibility/debugger/binding-breakpoints.md).  
  
     O erro de ponto de interrupção pode ser um erro ou um aviso.  
  
-   É representado por um [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [Programas](../../extensibility/debugger/programs.md)   
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)   
 [Contexto de código](../../extensibility/debugger/code-context.md)   
 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)   
 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)

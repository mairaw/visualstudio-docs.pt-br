---
title: 'CA1823: evitar campos privados não usados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedPrivateFields
- CA1823
helpviewer_keywords:
- AvoidUnusedPrivateFields
- CA1823
ms.assetid: 614f94f6-0dc7-430f-8124-cb889a4a720f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3a9ef0e63e13ab6e05025ef1a24c4032feb5eacd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49923700"
---
# <a name="ca1823-avoid-unused-private-fields"></a>CA1823: evitar campos privados não usados

|||
|-|-|
|NomeDoTipo|AvoidUnusedPrivateFields|
|CheckId|CA1823|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Essa regra é relatada quando um campo particular em seu código existe, mas não é usado por qualquer caminho de código.

## <a name="rule-description"></a>Descrição da regra
 Foram detectados campos particulares que aparentemente não são acessados no assembly.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, remova o campo ou adicionar código que o usa.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1812: evitar classes internas sem instâncias](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801: examinar parâmetros não usados](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804: remover locais não usados](../code-quality/ca1804-remove-unused-locals.md)

 [CA1811: evitar código privado não chamado](../code-quality/ca1811-avoid-uncalled-private-code.md)
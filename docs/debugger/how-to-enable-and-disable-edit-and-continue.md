---
title: 'Como: habilitar e desabilitar editar e continuar (C#, VB, C++) | Microsoft Docs'
ms.custom: ''
ms.date: 10/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- /INCREMENTAL linker option
- Apply Code Changes command
- Edit and Continue, disabling
- code changes, applying in break mode
- INCREMENTAL linker option
- Edit and Continue, enabling
- break mode, applying code changes
- Edit and Continue, applying code changes
- Step command
- Go command
ms.assetid: fd961a1c-76fa-420d-ad8f-c1a6c003b0db
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: f0bf354f64be9c03a64beadcffdd7ff1138218df
ms.sourcegitcommit: c5e72875206b8c5737c29d5b1ec7b86eec747303
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49382734"
---
# <a name="how-to-enable-and-disable-edit-and-continue-c-vb-c"></a>Como: habilitar e desabilitar editar e continuar (C#, VB, C++)

Você pode desabilitar ou habilitar **editar e continuar** no Visual Studio **opções** caixa de diálogo em tempo de design. **Editar e continuar** compilações funciona apenas na depuração. Para obter mais informações, consulte [editar e continuar](../debugger/edit-and-continue.md). 
  
Para o C++ nativo, **editar e continuar** requer o uso de `/INCREMENTAL` opção. Para obter mais informações sobre os requisitos de recurso no C++, consulte este [postagem de blog](https://blogs.msdn.microsoft.com/vcblog/2016/07/01/c-edit-and-continue-in-visual-studio-2015-update-3/) e [editar e continuar (Visual C++)](../debugger/edit-and-continue-visual-cpp.md).
  
**Para habilitar ou desabilitar editar e continuar:**  
  
1.  Se você estiver em uma sessão de depuração, pare a depuração (**Debug** > **parar depuração** ou **Shift**+**F5**) .

1.  Na **ferramentas** > **opções** > (ou **depurar** > **opções**) > **dedepuração**  >  **Gerais**, selecione **editar e continuar** no painel direito.  
  
    > [!NOTE]
    >  Se IntelliTrace estiver habilitado e você coletar eventos de IntelliTrace e informações de chamada, Editar e Continuar estará desabilitado. Para obter mais informações, consulte [IntelliTrace](../debugger/intellitrace.md).
    
1.  Para código C++, certifique-se **habilitar nativo editar e continuar** está selecionado e definir as opções adicionais:
    - **Aplicar alterações ao continuar (somente nativo)**  
      
      Se selecionado, o Visual Studio compila automaticamente e aplica as alterações de código quando você continuar a depuração a partir de um estado de interrupção. Caso contrário, você pode optar por aplicar as alterações usando **Debug** > **aplicar alterações de código**.  
      
    - **Avisar sobre código obsoleto (somente nativo)**  
      
      Se selecionado, dá avisos sobre código obsoleto. 
  
1.  Clique em **OK**.    

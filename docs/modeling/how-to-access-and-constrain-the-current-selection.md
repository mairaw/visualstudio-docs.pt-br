---
title: "Como: acessar e restringir a seleção atual | Documentos do Microsoft"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, accessing the current selection
ms.assetid: 2990981e-dfae-416f-b0d0-7197f1242dfa
caps.latest.revision: 14
author: alancameronwills
ms.author: awills
manager: douge
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: 43c66804a42e6af9ba8ee5c9ced5aea6194a9a39
ms.lasthandoff: 02/22/2017

---
# <a name="how-to-access-and-constrain-the-current-selection"></a>Como acessar e restringir a seleção atual
Quando você escreve um manipulador de comando ou gesto para sua linguagem específica do domínio, você pode determinar qual elemento o usuário pequeno. Você também pode impedir alguns campos ou formas seja selecionada. Por exemplo, você pode organizar que quando o usuário clica em um decorador de ícone, de forma que o contém for selecionada. Restringir a seleção dessa maneira reduz o número de manipuladores que você precisa escrever. Ele também torna mais fácil para o usuário, que pode clicar em qualquer lugar na forma sem a necessidade de evitar o decorador.  
  
## <a name="accessing-the-current-selection-from-a-command-handler"></a>Acessando a seleção atual de um manipulador de comando  
 A classe do conjunto de comandos para uma linguagem específica do domínio contém os manipuladores de comando para os comandos personalizados. O <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>classe, da qual deriva a classe do conjunto de comandos para uma linguagem específica do domínio, fornece alguns membros para acessar a seleção atual.</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>  
  
 Dependendo do comando, o manipulador de comandos talvez precise a seleção no designer de modelo, o Gerenciador de modelos ou a janela ativa.  
  
#### <a name="to-access-selection-information"></a>Para acessar informações sobre a seleção  
  
1.  O <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>classe define os seguintes membros que podem ser usados para acessar a seleção atual.</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>  
  
    |Membro|Descrição|  
    |------------|-----------------|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A>método</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A>|Retorna `true` se qualquer um dos elementos selecionados no designer de modelo é uma forma de compartimento; caso contrário, `false`.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A>método</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A>|Retorna `true` se o diagrama for selecionado no designer de modelo; caso contrário, `false`.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A>método</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A>|Retorna `true` se exatamente um elemento é selecionado no designer de modelo; caso contrário, `false`.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A>método</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A>|Retorna `true` se exatamente um elemento é selecionado na janela ativa; caso contrário, `false`.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A>propriedade</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A>|Obtém uma coleção somente leitura dos elementos selecionados no designer de modelo.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A>propriedade</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A>|Obtém uma coleção somente leitura dos elementos selecionados na janela ativa.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A>propriedade</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A>|Obtém o elemento principal da seleção no designer de modelo.|  
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A>propriedade</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A>|Obtém o elemento principal da seleção da janela ativa.|  
  
2.  O <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A>propriedade o <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>classe fornece acesso ao <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>objeto que representa a janela do designer de modelo e fornece acesso adicional elementos selecionados no designer de modelo.</xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView> </xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> </xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A>  
  
3.  Além disso, o código gerado define uma propriedade de janela de ferramenta do explorer e uma propriedade de seleção do explorer no comando definir a classe para a linguagem específica do domínio.  
  
    -   A propriedade de janela de ferramenta explorer retorna uma instância da classe de janela de ferramenta explorer para a linguagem específica do domínio. A classe de janela de ferramenta explorer deriva de <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>classe e representa o Gerenciador de modelos para a linguagem específica do domínio.</xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>  
  
    -   O `ExplorerSelection` propriedade retorna o elemento selecionado na janela do Gerenciador de modelo para a linguagem específica do domínio.  
  
## <a name="determining-which-window-is-active"></a>Determinando qual janela está ativa  
 O <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>contém interface define os membros que fornecem acesso ao estado atual de seleção no shell.</xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> Você pode obter um <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>a classe do pacote ou a classe do conjunto de comandos para a linguagem específica do domínio por meio do objeto de `MonitorSelection` propriedade definida na classe base de cada um.</xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> A classe de pacote deriva de <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>classe e a classe do conjunto de comandos deriva de <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>classe.</xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> </xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>  
  
#### <a name="to-determine-from-a-command-handler-what-type-of-window-is-active"></a>Para determinar de um manipulador de comandos que tipo de janela está ativo  
  
1.  O <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A>propriedade o <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>classe retorna um <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>objeto que fornece acesso para o estado da seleção atual no shell.</xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> </xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> </xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A>  
  
2.  O <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A>propriedade o <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>interface obtém o contêiner de seleção ativa, que pode ser diferente da janela ativa.</xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> </xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A>  
  
3.  Adicione que as seguintes propriedades para o comando definido classe para você linguagem específica do domínio para determinar que tipo de janela está ativo.  
  
    ```c#  
    // using Microsoft.VisualStudio.Modeling.Shell;  
  
    // Returns true if the model designer is the active selection container;  
    // otherwise, false.  
    protected bool IsDesignerActive  
    {  
        get  
        {  
            return (this.MonitorSelection.CurrentSelectionContainer  
                is DiagramDocView);  
        }  
    }  
  
    // Returns true if the model explorer is the active selection container;  
    // otherwise, false.  
    protected bool IsExplorerActive  
    {  
        get  
        {  
            return (this.MonitorSelection.CurrentSelectionContainer  
                is ModelExplorerToolWindow);  
        }  
    }  
    ```  
  
## <a name="constraining-the-selection"></a>Restringir a seleção  
 Adicionando regras de seleção, você pode controlar quais elementos são selecionados quando o usuário seleciona um elemento no modelo. Por exemplo, para permitir que o usuário tratar um número de elementos como uma única unidade, você pode usar uma regra de seleção.  
  
#### <a name="to-create-a-selection-rule"></a>Para criar uma regra de seleção  
  
1.  Crie um arquivo de código personalizado no projeto DSL  
  
2.  Defina uma classe de regra de seleção que deriva de <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>classe.</xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>  
  
3.  Substituir o <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A>método da classe de regra de seleção para aplicar os critérios de seleção.</xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A>  
  
4.  Adicione uma definição de classe parcial para a classe ClassDiagram ao seu arquivo de código personalizado.  
  
     O `ClassDiagram` classe deriva de <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>classe e é definido no arquivo de código gerado, a Diagram.cs, no projeto DSL.</xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>  
  
5.  Substituir o <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A>propriedade o `ClassDiagram` classe para retornar a regra de seleção personalizada.</xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A>  
  
     A implementação padrão de <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A>propriedade obtém um objeto de regra de seleção que não modifica a seleção.</xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A>  
  
### <a name="example"></a>Exemplo  
 O arquivo de código a seguir cria uma regra de seleção que expande a seleção para incluir todas as instâncias de cada uma das formas de domínio que foi inicialmente selecionado.  
  
```c#  
using System;  
using System.Collections.Generic;  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
  
namespace CompanyName.ProductName.GroupingDsl  
{  
    public class CustomSelectionRules : DiagramSelectionRules  
    {  
        protected Diagram diagram;  
        protected IElementDirectory elementDirectory;  
  
        public CustomSelectionRules(Diagram diagram)  
        {  
            if (diagram == null) throw new ArgumentNullException();  
  
            this.diagram = diagram;  
            this.elementDirectory = diagram.Store.ElementDirectory;  
        }  
  
        /// <summary>Called by the design surface to allow selection filtering.  
        /// </summary>  
        /// <param name="currentSelection">[in] The current selection before any  
        /// ShapeElements are added or removed.</param>  
        /// <param name="proposedItemsToAdd">[in/out] The proposed DiagramItems to  
        /// be added to the selection.</param>  
        /// <param name="proposedItemsToRemove">[in/out] The proposed DiagramItems  
        /// to be removed from the selection.</param>  
        /// <param name="primaryItem">[in/out] The proposed DiagramItem to become  
        /// the primary DiagramItem of the selection. A null value signifies that  
        /// the last DiagramItem in the resultant selection should be assumed as  
        /// the primary DiagramItem.</param>  
        /// <returns>true if some or all of the selection was accepted; false if  
        /// the entire selection proposal was rejected. If false, appropriate  
        /// feedback will be given to the user to indicate that the selection was  
        /// rejected.</returns>  
        public override bool GetCompliantSelection(  
            SelectedShapesCollection currentSelection,  
            DiagramItemCollection proposedItemsToAdd,  
            DiagramItemCollection proposedItemsToRemove,  
            DiagramItem primaryItem)  
        {  
            if (currentSelection.Count == 0 && proposedItemsToAdd.Count == 0) return true;  
  
            HashSet<DomainClassInfo> itemsToAdd = new HashSet<DomainClassInfo>();  
  
            foreach (DiagramItem item in proposedItemsToAdd)  
            {  
                if (item.Shape != null)  
                    itemsToAdd.Add(item.Shape.GetDomainClass());  
            }  
            proposedItemsToAdd.Clear();  
            foreach (DomainClassInfo classInfo in itemsToAdd)  
            {  
                foreach (ModelElement element  
                    in this.elementDirectory.FindElements(classInfo, false))  
                {  
                    if (element is ShapeElement)  
                    {  
                        proposedItemsToAdd.Add(  
                            new DiagramItem((ShapeElement)element));  
                    }  
                }  
            }  
  
            return true;  
        }  
    }  
  
    public partial class ClassDiagram  
    {  
        protected CustomSelectionRules customSelectionRules = null;  
  
        protected bool multipleSelectionMode = true;  
  
        public override DiagramSelectionRules SelectionRules  
        {  
            get  
            {  
                if (multipleSelectionMode)  
                {  
                    if (customSelectionRules == null)  
                    {  
                        customSelectionRules = new CustomSelectionRules(this);  
                    }  
                    return customSelectionRules;  
                }  
                else  
                {  
                    return base.SelectionRules;  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet></xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>   
 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage></xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>   
 <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView></xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>   
 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow></xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>   
 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService></xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>   
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules></xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>   
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram></xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>
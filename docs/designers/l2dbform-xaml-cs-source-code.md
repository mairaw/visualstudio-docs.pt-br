---
title: "Código-fonte de L2DBForm.xaml.cs | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5a40dad3-6763-4576-b3ad-874df3f2c8d9
caps.latest.revision: 2
author: kempb
ms.author: kempb
manager: ghogen
translation.priority.ht:
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
translationtype: Human Translation
ms.sourcegitcommit: 5db97d19b1b823388a465bba15d057b30ff0b3ce
ms.openlocfilehash: 753635060d71edf9d71e5919d00c9b566e16320d
ms.lasthandoff: 02/22/2017

---
# <a name="l2dbformxamlcs-source-code"></a>Código de L2DBForm.xaml.cs
Este tópico contém o conteúdo e a descrição do código-fonte C# no arquivo L2DBForm.xaml.cs. A classe parcial de L2XDBForm contida neste arquivo pode ser dividida em três seções lógicas: membros de dados e o botão de `OnRemove` e de `OnAddBook` clique manipuladores de eventos.  
  
## <a name="data-members"></a>Membros de Dados  
 Dois membros de dados confidenciais são usados para associar essa classe para recursos da janela usados em L2DBForm.xaml.  
  
-   O namespace `myBooks` variável é inicializada a `"http://www.mybooks.com"`.  
  
-   O membro `bookList` é inicializado no construtor para a cadeia de caracteres CDATA em L2DBForm.xaml com a seguinte linha:  
  
    ```  
    bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;  
    ```  
  
## <a name="onaddbook-event-handler"></a>Manipulador de eventos OnAddBook  
 Este método contém as três declarações:  
  
-   A primeira declaração condicional é usada para validação de entrada.  
  
-   A segunda instrução cria um novo <xref:System.Xml.Linq.XElement> de valores de cadeia de caracteres que o usuário inseriu na seção **Adicionar Novo Livro** da IU (interface do usuário).  
  
-   A última instrução adicionar esse novo elemento de livro para o provedor de dados em L2DBForm.xaml. Portanto, a associação de dados dinâmicos atualizará automaticamente interface do usuário com esse novo item; nenhum código de acrescentar fornecido é necessário.  
  
## <a name="onremove-event-handler"></a>Manipulador de eventos OnRemove  
 O manipulador de `OnRemove` é mais complicado que o manipulador de `OnAddBook` por dois motivos. Primeiro, como o XML brutos contém o espaço em branco preservada, as novas linhas correspondentes também devem ser removidos com a entrada de livro. Segundo, como uma conveniência, a seleção, que estava no item excluído, é reiniciada a anterior na lista.  
  
 No entanto trabalho principal de remover o item selecionado de livro é feito por apenas duas instruções:  
  
-   Primeiro, o elemento de livro associado com o item atualmente selecionado na caixa de listagem é recuperado:  
  
    ```  
    XElement selBook = (XElement)lbBooks.SelectedItem;   
    ```  
  
-   Em seguida, esse elemento é excluído do provedor de dados:  
  
    ```  
    selBook.Remove();  
    ```  
  
 Além disso, a associação de dados dinâmicos garante que interface do usuário do programa é atualizado automaticamente.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
  
### <a name="code"></a>Código  
  
```c#  
using System;  
using System.Linq;  
using System.Collections;  
using System.Collections.Generic;  
using System.Diagnostics;  
using System.Text;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Input;  
using System.Xml;  
using System.Xml.Linq;  
  
namespace LinqToXmlDataBinding {  
    /// <summary>  
    /// Interaction logic for L2XDBForm.xaml  
    /// </summary>  
  
    public partial class L2XDBForm : System.Windows.Window   
    {  
        XNamespace mybooks = "http://www.mybooks.com";  
        XElement bookList;  
  
        public L2XDBForm()   
        {  
            InitializeComponent();  
            bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;  
        }  
  
        void OnRemoveBook(object sender, EventArgs e)   
        {  
            int index = lbBooks.SelectedIndex;  
            if (index < 0) return;  
  
            XElement selBook = (XElement)lbBooks.SelectedItem;  
            //Get next node before removing element.  
            XNode nextNode = selBook.NextNode;  
            selBook.Remove();  
  
            //Remove any matching newline node.  
            if (nextNode != null && nextNode.ToString().Trim().Equals(""))  
            { nextNode.Remove(); }  
  
            //Set selected item.   
            if (lbBooks.Items.Count > 0)  
            {  lbBooks.SelectedItem = lbBooks.Items[index > 0 ? index - 1 : 0]; }  
        }  
  
        void OnAddBook(object sender, EventArgs e)   
        {  
            if (String.IsNullOrEmpty(tbAddID.Text) ||  
                String.IsNullOrEmpty(tbAddValue.Text))  
            {  
                MessageBox.Show("Please supply both a Book ID and a Value!", "Entry Error!");  
                return;   
            }  
            XElement newBook = new XElement(  
                                mybooks + "book",  
                                new XAttribute("id", tbAddID.Text),  
                                tbAddValue.Text);  
            bookList.Add("  ", newBook, "\r\n");  
        }  
    }  
}  
  
```  
  
### <a name="comments"></a>Comentários  
 Para o código-fonte XAML associado desses manipuladores, consulte [Código-fonte de L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: exemplo de LinqToXmlDataBinding](../designers/walkthrough-linqtoxmldatabinding-example.md)   
 [Código-fonte de L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md)
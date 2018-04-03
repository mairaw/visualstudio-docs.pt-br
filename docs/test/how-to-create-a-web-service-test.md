---
title: Criar um teste de serviço Web no Visual Studio | Microsoft Docs
ms.date: 10/19/2016
ms.topic: article
helpviewer_keywords:
- Web performance tests, creating Web service tests
- Web services [Visual Studio ALM], creating
- service tests, Web
ms.assetid: fbcd57ee-06ad-4260-8694-09f8e0f93e39
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-ide-test
ms.openlocfilehash: b7d7a864b7fc62527bdd2593523ccdc91bf913aa
ms.sourcegitcommit: 900ed1e299cd5bba56249cef8f5cf3981b10cb1c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="how-to-create-a-web-service-test"></a>Como criar um teste de serviço Web

Você pode usar um teste de desempenho na Web para testar serviços Web. Usando as opções **Inserir solicitação** e **Inserir solicitação de serviço Web**, você pode personalizar as solicitações individuais no **Editor de Testes de Desempenho Web** para localizar páginas de serviço Web. Normalmente, você não exibe essas páginas no aplicativo Web. Portanto, você deve personalizar a solicitação para acessar essas páginas.

Os procedimentos a seguir usam um serviço Web contido no Commerce Starter Kit. Você pode baixá-lo do [ASP.NET Commerce Starter Kit](http://go.microsoft.com/fwlink/?LinkId=181469).

 **Requisitos**

-   Visual Studio Enterprise

## <a name="to-test-a-web-service"></a>Para testar um serviço Web

1.  Crie um novo teste de desempenho na Web. Assim que o navegador abrir, escolha **Parar**.

2.  No **Editor de Testes de Desempenho Web**, clique com o botão direito do mouse no teste de desempenho Web e selecione **Adicionar solicitação de serviço Web**.

3.  Na propriedade **URL** da nova solicitação, digite o nome do serviço Web, como **http://localhost/storecsvs/InstantOrder.asmx**.

4.  Abra uma sessão separada do navegador e digite a URL da página .asmx na barra de ferramentas **Endereço**. Selecione o método que você deseja testar e examine a mensagem SOAP. Contém `SOAPAction`.

5.  No **Editor de Testes de Desempenho Web**, clique com o botão direito do mouse na solicitação e selecione **Adicionar Cabeçalho** para adicionar um novo cabeçalho. Na propriedade **Nome**, digite `SOAPAction`. Na propriedade **Valor**, digite o valor que você vê em `SOAPAction`, como `"http://tempuri.org/CheckStatus"`.

6.  Expanda o nó da URL no editor, selecione o nó **Corpo da String** e na propriedade **Tipo de Conteúdo** insira um valor de `text/xml`.

7.  Retorne ao navegador na etapa 4, selecione a parte XML da solicitação SOAP da página de descrição do serviço Web e copie-a para a área de transferência.

8.  O conteúdo XML é semelhante ao seguinte exemplo:

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
     <soap:Body>
       <CheckStatus xmlns="http://tempuri.org/">
         <userName>string</userName>
         <password>string</password>
         <orderID>int</orderID>
       </CheckStatus>
     </soap:Body>
     </soap:Envelope>
     ```

9. Retorne ao **Editor de Testes de Desempenho Web** e escolha as reticências (…) na propriedade de **Corpo da string**. Cole o conteúdo da área de transferência na propriedade.

10. Você deve substituir todos os valores de espaço reservado do XML com os valores válidos para que o teste seja aprovado. No exemplo anterior, substitua as duas instâncias de `string` e uma de `int`. Essa operação de serviço Web somente será concluída se houver um usuário registrado que tenha feito um pedido.

11. Clique com o botão direito do mouse na solicitação de serviço Web e selecione **Adicionar URL do parâmetro QueryString**.

12. Atribua um nome e um valor ao parâmetro de cadeia de caracteres de consulta. No exemplo anterior, o nome é `op` e o valor é `CheckStatus`. Isso identifica a operação de serviço Web a ser executada.

    > [!NOTE]
    > Você pode usar a vinculação de dados no corpo SOAP para substituir o valor de qualquer espaço reservado por valores associados a dados usando a sintaxe `{{DataSourceName.TableName.ColumnName}}`.

13. Execute o teste. No painel superior do Visualizador de Resultados de Teste de Desempenho na Web, selecione a solicitação de serviço Web. No painel inferior, selecione a guia Navegador da Web. O XML retornado pelo serviço Web e os resultados de todas as operações serão exibidos.

## <a name="see-also"></a>Consulte também

- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
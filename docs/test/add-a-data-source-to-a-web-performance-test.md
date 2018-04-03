---
title: Adicionar uma fonte de dados a um teste de desempenho Web no Visual Studio | Microsoft Docs
ms.date: 10/03/2016
ms.topic: article
helpviewer_keywords:
- Web performance tests, walkthroughs
- Web performance tests, data binding (database)
ms.assetid: 2ada376d-f168-455d-9643-6acb535360c1
author: gewarren
ms.author: gewarren
manager: ghogen
ms.technology: vs-ide-test
ms.openlocfilehash: 2880f5d0abef181e5d30d9c36f897dc9057ea54d
ms.sourcegitcommit: 900ed1e299cd5bba56249cef8f5cf3981b10cb1c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="add-a-data-source-to-a-web-performance-test"></a>Adicionar uma fonte de dados a um teste de desempenho Web

Associe dados para fornecer valores diferentes para o mesmo teste, por exemplo, para fornecer valores diferentes para seus parâmetros de postagem de formulário.

 ![Associando dados a um teste de desempenho Web](../test/media/web_test_databinding_conceptual.png)

 Usaremos um aplicativo de exemplo do ASP.NET. Ele tem três páginas .aspx – a página padrão, uma página Vermelha e uma página Azul. A página padrão tem um controle de rádio para escolher vermelho ou azul e um botão enviar. As outras duas páginas .aspx são muito simples. Uma tem um rótulo chamado Vermelho e a outra, Azul. Quando você opta por enviar a página padrão, exibimos uma das outras páginas. É possível baixar a amostra [ColorWebApp](http://code.msdn.microsoft.com/Sample-ColorWebApp-76ff7506) ou simplesmente prosseguir usando seu próprio aplicativo Web.

 ![Executando o aplicativo Web a ser testado](../test/media/web_test_databinding_runwebapp.png)

 Sua solução também deve incluir um teste de desempenho Web que navegará pelas páginas do aplicativo Web.

 ![Solução com o teste de desempenho Web](../test/media/web_test_databinding_solution.png)

## <a name="create-a-sql-database"></a>Criar um banco de dados SQL

1. Se não tiver o Visual Studio Enterprise, você poderá baixá-lo na página de [Downloads do Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).

2. Crie um banco de dados SQL.

     ![Adicione um novo banco de dados SQL](../test/media/web_test_databinding_sql_addnewdb.png)

3. Crie um projeto de banco de dados.

     ![Crie um novo projeto do banco de dados](../test/media/web_test_databinding_sql_addnewdbproject.png)

4. Adicione uma tabela ao projeto de banco de dados.

     ![Adicione uma nova tabela ao projeto de banco de dados](../test/media/web_test_databinding_sql_addnewdbtablename.png)

5. Adicione campos à tabela.

     ![Adicione campos à tabela](../test/media/web_test_databinding_sql_addnewdbaddfields.png)

6. Publique o projeto de banco de dados.

     ![Publique o projeto de banco de dados do Gerenciador de Soluções](../test/media/web_test_databinding_sql_addnewdbpublish.png)

7. Adicione dados aos campos.

     ![Adicione dados aos campos](../test/media/web_test_databinding_sql_addnewfieldsadddata.png)

## <a name="add-the-data-source"></a>Adicionar a fonte de dados

1. Adicione uma fonte de dados.

     ![Adicione uma fonte de dados ao teste de desempenho Web](../test/media/web_test_databinding_sql_adddatasource.png)

2. Escolha o tipo de fonte de dados e nomeie-o.

     ![Nomeie a origem do banco de dados](../test/media/web_test_databinding_sql_adddatasourcedialog.png)

3. Crie uma conexão.

     ![Escolha a nova conexão](../test/media/web_test_databinding_sql_adddatasourcedialogconnectionnew.png)

     Insira os detalhes da conexão.

     ![Insira as propriedades de conexão de banco de dados SQL](../test/media/web_test_databinding_sql_adddatasourcedialogconnection.png)

4. Selecione a tabela que você deseja usar no seu teste.

     ![Adicione a tabela de cores como a fonte de dados](../test/media/web_test_databinding_sql_adddatasourcedialogaddtable.png)

     A tabela é associada ao teste.

     ![Adicione o nó Fontes de dados ao teste de desempenho Web](../test/media/web_test_databinding_requestnodeadded_mdb.png)

5. Salve o teste.

## <a name="bind-the-data"></a>Associar os dados

1. Associe o campo ColorName.

     ![Associe o campo ColorName ao valor RadioButtonList1](../test/media/web_test_databinding_sql_binddatasource.png)

2. Abra o arquivo Local.testsettings no Gerenciador de Soluções e selecione aquele executado pela opção de linha da fonte de dados.

     ![Editar o arquivo de configurações de teste](../test/media/web_test_databinding_sql_testsettings.png)

3. Salve o teste de desempenho na Web.

## <a name="run-the-test-with-the-data"></a>Executar o teste com os dados

1. Execute o teste.

     ![Execute o teste de desempenho Web para confirmar a associação](../test/media/web_test_databinding_sql_runtest.png)

     As duas execuções são exibidas para cada linha de dados. A Execução 1 envia uma solicitação para a página Red.aspx e a Execução 2 envia uma solicitação para a página Blue.aspx.

     ![Resultados da execução de teste](../test/media/web_test_databinding_sql_runresults.png)

     Ao associar a uma fonte de dados, você pode violar a regra da URL de resposta padrão. Nesse caso, o erro na Execução 2 é causado pela regra que espera a página Red.aspx da gravação original de teste, mas a associação de dados agora a direciona para a página Blue.aspx.

2. Corrija o erro de validação excluindo a regra de validação da URL de resposta e executando o teste novamente.

     ![Excluir a regra de validação da URL de resposta](../test/media/web_test_databinding_sql_deleteresponseurl.png)

     O teste de desempenho na Web agora passa usando-se a associação de dados.

     ![Teste é aprovado usando associação de dados](../test/media/web_test_databinding_sql_deleteresponseurlrunresults.png)

## <a name="q--a"></a>Perguntas e respostas

### <a name="q-what-databases-can-i-use-as-a-data-source"></a>P: Quais bancos de dados posso usar como uma fonte de dados?

**R:** Você pode usar os seguintes:

- Microsoft SQL Azure.

- Qualquer versão do Microsoft SQL Server 2005 ou posterior.

- Arquivo de banco de dados do Microsoft SQL Server (incluindo o SQL Express).

- Microsoft ODBC.

- Arquivo do Microsoft Access usando o provedor do .NET Framework para OLE DB.

- Oracle 7.3, 8i, 9i ou 10g.

### <a name="q-how-do-i-use-a-comma-separated-value-csv-text-file-as-a-data-source"></a>P: Como uso um arquivo de valores separados por vírgula (CSV) de texto como uma fonte de dados?

**R:** Veja como:

1. Crie uma pasta para organizar seus artefatos de banco de dados de projetos e adicione um item.

     ![Adicionar novo item à pasta de Dados](../test/media/web_test_databinding_foldernewitem.png "Web_Test_DataBinding_FolderNewItem")

2. Crie um arquivo de texto.

     ![Dar ao novo arquivo de texto o nome ColorData.csv](../test/media/web_test_databinding_foldernewitemtextfile.png "Web_Test_DataBinding_FolderNewItemTextFile")

3. Edite o arquivo de texto e adicione o seguinte:

    ```
    ColorId, ColorName
    0,Red
    1,Blue
    ```

4. Use as etapas em [Associando os dados SQL](#AddingDataBindingWebTest_BindSQLData), mas escolha o arquivo CSV como a fonte de dados.

     ![Inserir um nome e escolher o arquivo CSV](../test/media/web_test_databinding_adddatasourcedialog.png "Web_Test_DataBinding_AddDataSourceDialog")

### <a name="q-what-if-my-existing-csv-file-does-not-contain-column-headers"></a>P: E se meu arquivo CSV existente não contiver cabeçalhos de coluna?

**R:** Se não conseguir adicionar cabeçalhos de coluna, você poderá usar um arquivo de descrição do esquema para manipular o arquivo CSV como um banco de dados.

1. Adicione um novo arquivo de texto chamado schema.ini.

     ![Adicionar um arquivo schema.ini](../test/media/web_test_databinding_schemafile.png "Web_Test_DataBinding_SchemaFile")

2. Edite o arquivo schema.ini para adicionar informações que descrevam a estrutura dos seus dados. Por exemplo, um arquivo de esquema descrevendo o arquivo CSV pode ser parecido com este:

    ```
    [testdata.csv]
    ColNameHeader=False
    ```

3. Adicione uma fonte de dados ao teste.

     ![Adicionar fonte de dados a um teste de desempenho Web](../test/media/web_test_databinding_sql_adddatasource.png "Web_Test_DataBinding_SQL_AddDataSource")

4. Se você estiver usando um arquivo schema.ini, escolha Banco de Dados (e não o arquivo CSV) como a fonte de dados e nomeie-o.

     ![Adicionar fonte de dados do banco de dados](../test/media/web_test_databinding_adddatasourcecolortext.png "Web_Test_DataBinding_AddDataSourceColorText")

5. Crie uma nova conexão.

     ![Escolher nova conexão](../test/media/web_test_databinding_sql_adddatasourcedialogconnectionnew.png "Web_Test_DataBinding_SQL_AddDataSourceDialogConnectionNew")

6. Selecione o Provedor de Dados do .NET Framework para OLE DB.

     ![Selecionar provedor de dados do OLE DB do .NET framework](../test/media/web_test_databinding_adddatasourcecolortext2.png "Web_Test_DataBinding_AddDataSourceColorText2")

7. Escolha Avançado.

     ![Escolher Avançado](../test/media/web_test_databinding_advanced.png "Web_Test_DataBinding_Advanced")

8. Para a propriedade Provedor, selecione Microsoft.Jet.OLEDB.4.0 e defina Propriedades Estendidas como Text;HDR=NO.

     ![Aplicar propriedades avançadas](../test/media/web_test_databinding_advancedproperties.png "Web_Test_DataBinding_AdvancedProperties")

9. Digite o nome da pasta que contém o arquivo de esquema e teste sua conexão.

     ![Digitar o caminho para a pasta de dados](../test/media/web_test_databinding_adddatasourcecolortext5.png "Web_Test_DataBinding_AddDataSourceColorText5")

10. Selecione o arquivo CSV que você deseja usar.

     ![Selecionar o arquivo de texto](../test/media/web_test_databinding_adddatasourcecolortext6.png "Web_Test_DataBinding_AddDataSourceColorText6")

     Depois de terminar, o arquivo CSV aparecerá como uma tabela.

     ![Fonte de dados adicionada ao teste](../test/media/web_test_databinding_adddatasourcecolortext7.png "Web_Test_DataBinding_AddDataSourceColorText7")

### <a name="q-how-do-i-use-an-xml-file-as-a-data-source"></a>P: Como uso um arquivo XML como uma fonte de dados?

**R:** Sim.

1. Crie uma pasta para organizar seus artefatos de banco de dados de projetos e adicione um item.

     ![Adicionar novo item à pasta de Dados](../test/media/web_test_databinding_foldernewitem.png "Web_Test_DataBinding_FolderNewItem")

2. Crie um arquivo XML.

     ![Adicionar arquivo ColorData.xml](../test/media/web_test_databinding_additemxmlfile.png "Web_Test_DataBinding_AddItemXMLFile")

3. Edite o arquivo XML e adicione seus dados:

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <ColorData>
        <Color>
            <ColorId>0</ColorId>
            <ColorName>Red</ColorName>
        </Color>
        <Color>
            <ColorId>1</ColorId>
            <ColorName>Blue</ColorName>
        </Color>
    </ColorData>
    ```

4. Use as etapas em [Associando os dados SQL](#AddingDataBindingWebTest_BindSQLData), mas escolha o arquivo XML como a fonte de dados.

     ![Inserir um nome e escolher o arquivo XML](../test/media/web_test_databinding_adddatasourcedialogxml.png "Web_Test_DataBinding_AddDataSourceDialogXML")

### <a name="q-can-i-add-data-binding-to-a-web-service-request-that-uses-soap"></a>P: Posso adicionar associação de dados a uma solicitação de serviço Web que usa SOAP?

**R:** Sim, você deve alterar o XML SOAP manualmente.

1. Escolha a solicitação de serviço da Web na árvore de solicitação e, na janela Propriedades, clique nas reticências (…) na propriedade Corpo da Cadeia de Caracteres.

     ![Editar o corpo da cadeia de caracteres do serviço Web](../test/media/web_test_databinding_webservicerequest.png "Web_Test_DataBinding_WebServiceRequest")

2. Substitua valores no corpo SOAP pelos valores associados de dados usando a seguinte sintaxe:

    ```
    {{DataSourceName.TableName.ColumnName}}
    ```

    Por exemplo, se você tiver o seguinte código:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <CheckStatus xmlns="http://tempuri.org/">
                <userName>string</userName> <password>string</password> <orderID>int</orderID>
            </CheckStatus>
        </soap:Body>
    </soap:Envelope>
    ```

    Você poderá alterar para:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <CheckStatus xmlns="http://tempuri.org/">
                <userName>{{DataSourceName.Users.Name}}</userName> <password>{{DataSourceName.Users.Password}}</password> <orderID>{{DataSourceName.Orders.OrderID}}</orderID>
            </CheckStatus>
        </soap:Body>
    </soap:Envelope>
    ```

3. Salve o teste.
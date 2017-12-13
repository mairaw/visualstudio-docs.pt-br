---
title: Propriedades do vinculador Clang (Android C++) | Microsoft Docs
ms.custom: 
ms.date: 10/23/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 66e88848-116c-4eb0-bc57-183394d35b57
author: corob
ms.author: mblome
manager: ghogen
f1_keywords:
- VC.Project.VCLinkerTool.OutputFile
- VC.Project.VCLinkerTool.ShowProgress
- VC.Project.VCLinkerTool.Version
- VC.Project.VCLinkerTool.VerboseOutput
- VC.Project.VCLinkerTool.IncrementalLink
- VC.Project.VCLinkerTool.SharedLibrarySearchPath
- VC.Project.VCLinkerTool.AdditionalLibraryDirectories
- VC.Project.VCLinkerTool.UnresolvedReferences
- VC.Project.VCLinkerTool.OptimizeForMemory
- VC.Project.VCLinkerTool.IgnoreDefaultLibraryNames
- VC.Project.VCLinkerTool.ForceSymbolReferences
- VC.Project.VCLinkerTool.ForceFileOutput
- VC.Project.VCLinkerTool.OmitDebuggerSymbolInformation
- VC.Project.VCLinkerTool.GenerateMapFile
- VC.Project.VCLinkerTool.Relocation
- VC.Project.VCLinkerTool.FunctionBinding
- VC.Project.VCLinkerTool.NoExecStackRequired
- VC.Project.WholeArchive
- VC.Project.AdditionalOptionsPage
- VC.Project.VCLinkerTool.AdditionalDependencies
- VC.Project.VCLinkerTool.LibraryDependencies
ms.openlocfilehash: 0e7b1d5b417250282092a780afc30aee965e4dfa
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2017
---
# <a name="clang-linker-properties-android-c"></a>Propriedades do vinculador Clang (Android C++)

Propriedade | Descrição | Opções
--- | ---| ---
Arquivo de saída | A opção substitui o nome e o local padrão do programa que o vinculador cria. (-o)
Mostrar progresso | Imprime mensagens de progresso do vinculador.
Versão | A opção -version instrui o vinculador a colocar um número de versão no cabeçalho do executável.
Habilitar saída detalhada | A opção -verbose instrui o vinculador a produzir mensagens detalhadas para depuração.
Habilitar vinculação incremental | A opção instrui o vinculador a habilitar a vinculação incremental.
Caminho de pesquisa de biblioteca de compartilhada | Permite que o usuário popule o caminho de pesquisa de biblioteca compartilhada.
Diretórios de Biblioteca Adicionais | Permite que o usuário substitua o caminho da biblioteca ambiental. (-L folder).
Relatar referências de símbolo não resolvidas | Quando habilitada, esta opção relatará referências de símbolo não resolvidas.
Otimizar uso de memória | Otimizar o uso de memória relendo as tabelas de símbolos, conforme o necessário.
Ignorar bibliotecas padrão específicas | Especifica um ou mais nomes de bibliotecas padrão a serem ignoradas.
Forçar referências de símbolo | Forçar o símbolo a ser inserido no arquivo de saída como um símbolo indefinido.
Informações de símbolo do depurador | Informações de símbolo do depurador do arquivo de saída. | **Incluir tudo**<br>**Omitir símbolos desnecessários para o processamento de realocação**<br>**Omitir somente informações de símbolo do depurador**<br>**Omitir todas as informações de símbolo**<br>
Informações de símbolo do depurador de pacotes | Remover as informações de símbolos do depurador antes do empacotamento.  Uma cópia do binário original será usada para depuração.
Nome do arquivo de mapa | A opção Map instrui o vinculador a criar um arquivo de mapa com o nome especificado pelo usuário.
Marcar variáveis como ReadOnly após a realocação | Essa opção marca as variáveis como somente leitura após a realocação.
Habilitar associação de função imediata | Essa opção marca o objeto para associação de função imediata.
Exigir pilha executável | Essa opção marca a saída para não exigir uma pilha executável.
Arquivo morto inteiro | O arquivo morto inteiro usa todo o código das fontes e das dependências adicionais.
Opções Adicionais | Opções adicionais.
Dependências adicionais | Especifica itens adicionais a serem adicionados à linha de comando do link.
Dependências de biblioteca | Essa opção permite especificar as bibliotecas adicionais a serem adicionadas à linha de comando do vinculador. As bibliotecas adicionais serão adicionadas ao final da linha de comando do vinculador, começando com 'lib' e terminando com extensão '.a' ou '.so'.  (-lFILE)
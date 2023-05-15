# recoll_pt-br
Tradução do Recoll, aplicativo desktop para pesquisa (indexador) de textos (.txt, .pdf, .odt, .ods, .csv, .xlsm, .doc, .docx...)

O Recoll (www.recoll.org) é baseado no Xapian (www.xapian.org), para a qual fornece uma poderosa camada de extração de texto e uma interface gráfica Qt completa, mas fácil de usar.

A tradução do Recoll começou sem pretensão de torná-la pública, até mesmo porque não sou programador nem fluente em inglês. No entanto, não foi um trabalho rápido e precisei fazer algumas descobertas, logo, acredito outras pessoas possam se interessar e, também, melhorar a tradução, principalmente em relação aos termos técnicos. 

# Para traduzir

1. O aplicativo usado para traduzir é o Qt Linguist, que é muito intuitivo. No Arch Linux esse aplicativo é instalado junto com o pacote qt5-tools, veja em qual pacote ele faz parte na distribuição Linux que usa.

2. Para traduzir basta abrir o "arquivo de tradução" (extensão QM) e começar a traduzir ou corrigir. 

3. No caso do Recoll, as traduções originais ficam em /usr/share/recoll/translations/.

4. Os arquivos possuem o nome recoll_XX.qm, onde XX é o idioma do arquivo e, no caso para o idioma português, o nome precisa ser recoll_pt.qm.

5. Quando um aquivo qm é aberto e depois salvo no Qt Linguist, um arquivo XML com extensão TS é criado, para salvar novamente no formato QM é preciso no menu clicar em “file” e depois “release” ou “release as”. O Qt Linguist, ao menos no Arch, não está em português.

6. Para a tradução funcionar é preciso colocar o arquivo traduzido, no caso recoll_pt.qm, dentro do diretório /usr/share/recoll/translations/.

7. Sugestão, deixe o arquivo recoll_pt.qm dentro da pasta de configuração do recoll em sua home, no caso ~/.recoll e crie um link simbólico (sudo ln -s ~/.recoll/recoll_pt.qm /usr/share/recoll/translations/recoll_pt.qm) dentro do diretório /usr/share/recoll/translations/ para ele.

# Dicas

## Melhorando a resolução do Recoll

Se Recoll ficar com botões feios na resolução que usa é possível resolver escolhendo uma resolução apenas para ele. Se você utiliza o KDE Plamas use execute o Recoll da seguinte forma:

env QT_SCALE_FACTOR=0.8 recoll

Onde tem 0.8 é a resolução que estou usando para o Recoll, você pode escolher outra, 0.9, 1.0, 1.25..

Se estiver usando o Gnome ou alguma outra DE ou WM que usa GTK3, você deve utilizar (não testei):

env GDK_DPI_SCALE=1.25

## Resolvendo o problema "aspell dictionary creation command failed"

Caso esteja recebendo a mensagem abaixo:

Non-fatal indexing message: 
aspell : aspell dictionary creation command failed: /usr/bin/aspell --lang=pt --encoding=utf-8 create master /home/usuario/.recoll/aspdict.pt.rws One possible reason might be missing language data files for lang = pt. Maybe try to execute the command by hand for a better diag.

Faça o seguinte:

1. No menu, clique "preferências" e "configuração do índice";

2. Na primeira aba, em "parâmetros globais", em "linguagem derivada" clique no + e escolha "portuguese".

3. Logo abaixo, no campo "linguagem Aspell" coloque pt_BR, clique no botão "OK" e saia do Recoll.

4. Abra o arquivo recoll.conf que fica na pasta .recoll em sua home (~/.recoll).

5. Acrescente no arquivo: aspellLanguage = pt_BR

6. Caso não tenha instalado, instale o aspell e o aspell-pt.

7. Atualize seus índices, "aquivo" e "atualizar indice". Veja se o problema foi resolvido.

8. Um arquivo de nome aspdict.pt_BR.rws será criado na pasta de configurações do recoll (~/.recoll).

## Melhorando a aprência dos resultados





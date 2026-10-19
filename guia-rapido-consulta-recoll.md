# Guia rápido da linguagem de consulta do Recoll

Ficou em dúvida sobre o que uma busca faz? No Recoll, clique em **Mostrar detalhes da consulta** para ver como o programa entendeu o que você digitou. Para conhecer todos os recursos, consulte o manual (**F1**).

> **Sobre os exemplos:** os nomes de campos e operadores (`author:`, `dir:`, `date:`, `OR`, `AND` etc.) são a sintaxe real da busca e ficam sempre em inglês. As palavras buscadas (`relatório`, `contrato`…) são só exemplos: troque pelas suas.

---

## 1. Palavras e operadores

**Todas as palavras (E)**: o espaço já significa E.

- `relatório vendas`
- `relatório AND vendas`
- `relatório && vendas`

**Qualquer uma das palavras (OU)**: escreva `OR` em maiúsculas.

- `gato OR cachorro`
- `gato || cachorro`

**Excluir uma palavra (NÃO)**: sinal de menos colado na palavra.

- `orçamento -rascunho`

**Combinações complexas**: o `OR` tem prioridade sobre o `AND`. Use parênteses quando precisar. Sem parênteses, `a b OR c` vale como `a AND (b OR c)`.

- `(contrato AND 2023) OR proposta`

## 2. Frases e proximidade

**Frase exata**: palavras juntas e nessa ordem.

- `"orgulho e preconceito"`

**Proximidade em ordem (slack=1)**: as palavras nessa ordem, com até 1 palavra no meio.

- `"orgulho preconceito"o1` (acha "orgulho **e** preconceito")

**Proximidade em qualquer ordem (slack=1)**: com até 1 palavra no meio.

- `"preconceito orgulho"po1`

**Proximidade em qualquer ordem (slack padrão=10)**: com até 10 palavras no meio.

- `"preconceito orgulho"p`

**Sem expansão de radicais**: comece a palavra com letra maiúscula. Sem isso, "casa" também acharia "casas".

- `Casa`

> **O que é *slack*?** É a tolerância: quantas palavras a mais podem aparecer entre as palavras da sua frase. `slack=0` seria a frase exata, `slack=1` aceita uma palavra no meio, e assim por diante. Uma letra `o` depois das aspas exige a ordem, `p` (de *proximidade*) aceita qualquer ordem, e o número é o slack.

## 3. Buscar em um campo específico

Use `campo:palavra`, sem espaço depois dos dois pontos.

**Buscar em um campo**

- `author:assis title:casmurro`

**Várias palavras no mesmo campo**: todas, em qualquer ordem. Separe com vírgula.

- `author:machado,assis`

**Uma ou outra palavra no mesmo campo**: separe com barra.

- `author:assis/alencar`

### Nomes de campos disponíveis

Nomes separados por `/` são sinônimos: pode usar qualquer um deles.

| Campo | Significado |
|---|---|
| `title` / `subject` / `caption` | título |
| `author` / `from` | autor |
| `recipient` / `to` | destinatário |
| `filename` | nome do arquivo |
| `ext` | extensão do arquivo |

## 4. Filtros

**Somente arquivos de uma pasta**: caminho completo ou só um trecho dele.

- `dir:/home/maria`
- `dir:contratos`

**Somente um tipo de arquivo**: por tipo MIME ou por extensão. O `*` vale para qualquer subtipo.

- `mime:application/pdf`
- `mime:image/*`
- `ext:pdf`

**Datas**: use o formato **ANO-MÊS-DIA**.

- `date:2018-01-01/2018-12-31` (de uma data até outra)
- `date:2018` (o ano inteiro)
- `date:2018-01-01/P12M` (12 meses a partir da data)

**Tamanho**: `k`, `m` e `g` valem KB, MB e GB.

- `size>100k size<1M` (maior que 100 KB e menor que 1 MB)

---

## Exemplos combinados

Pode misturar tudo: as condições se somam (E) e cada uma restringe mais o resultado.

| Você quer achar… | Digite |
|---|---|
| PDFs sobre vendas | `vendas ext:pdf` |
| Contratos de 2023, sem os rascunhos | `contrato -rascunho date:2023-01-01/2023-12-31` |
| Arquivos grandes na pasta de documentos | `dir:/home/maria/documentos size>10M` |
| Livros de Machado de Assis ou de José de Alencar | `author:assis/alencar` |
| Documentos que falam de "orgulho" perto de "preconceito" | `"orgulho preconceito"po3` |
| Planilhas ou apresentações sobre orçamento | `orçamento (ext:xlsx OR ext:pptx)` |
| Relatório de 2024 em PDF ou Word | `relatório date:2024 (ext:pdf OR ext:docx)` |

## Dicas

- **`OR` e `AND` sempre em maiúsculas.** Em minúsculas eles viram palavras comuns da busca: `gato or cachorro` procura documentos que tenham a palavra "or".
- **Acentos e maiúsculas:** por padrão o Recoll ignora acentos e maiúsculas, então `orçamento` também acha `orcamento` e `ORÇAMENTO`. Se as opções automáticas estiverem ativadas nas configurações do índice, digitar acentos ou uma letra maiúscula fora da primeira posição faz a busca diferenciá-los.
- **Não achou o que esperava?** Abra **Mostrar detalhes da consulta** e veja como o Recoll interpretou a sua busca.
- **Radicais:** por padrão o Recoll também acha variações da palavra ("casa" acha "casas"). Para buscar só a forma exata, comece com maiúscula: `Casa`.

# Afya Admin — Dashboard com Blazor WebAssembly e MudBlazor

## Identificação

| | |
|---|---|
| **Aluno(a)** | Pedro Henrique Teixeira Souza de Sá |
| **Matrícula** | 000000 |
| **Faculdade** | São Lucas |
| **Curso** | Ciências da Computação |
| **Disciplina** | Desenvolvimento de sistemas web |
| **Professor(a)** | Nome do professor(a) Liluyoud Cury de Lacerda |
| **Semestre** | 2026.2 |

## Objetivo do projeto

Explique com suas palavras o objetivo do projeto e o que a página faz (2 a 4 parágrafos).

## Tecnologias utilizadas

- .NET 10 / Blazor WebAssembly
- MudBlazor 9

## Como executar

Passo a passo para outra pessoa clonar e rodar o projeto:

```bash
git clone https://github.com/pedro-tsa/afya-admin.git
cd afya-admin
dotnet watch
```

Informe também a versão do .NET SDK necessária.

## Telas

### Tema claro
![Dashboard — tema claro](docs/prints/tema-claro.png)
<img width="1867" height="942" alt="image" src="https://github.com/user-attachments/assets/8c302518-accc-478e-a048-ea8e26ada6bf" />


### Tema escuro
![Dashboard — tema escuro](docs/prints/tema-escuro.png)
<img width="1868" height="947" alt="dAk7cmee9u" src="https://github.com/user-attachments/assets/c3d6cb06-0e14-4785-928d-fcc787dcb523" />


### Versão mobile
![Dashboard — celular](docs/prints/mobile.png)
<img width="413" height="791" alt="firefox_0N864cQz47" src="https://github.com/user-attachments/assets/229b3a2d-adc9-4106-8d5a-df657d382a8a" />


### HTML gerado (DevTools)
![Inspeção do HTML no DevTools](docs/prints/devtools.png)
<img width="1871" height="661" alt="image" src="https://github.com/user-attachments/assets/c99d768a-f987-497e-9fb9-9e1485f24dde" />


Explique em poucas linhas o que o print do DevTools mostra: qual componente você inspecionou, qual HTML ele gerou e quais classes apareceram.
O Primeiro chart, com diversos Mud Papers e Mud Grid Item.

## Estrutura do projeto

Mostre a árvore de pastas e arquivos e explique em uma linha o papel de cada pasta (`Components`, `Data`, `Layout`, `Pages`, `wwwroot`).
<img width="425" height="559" alt="image" src="https://github.com/user-attachments/assets/8c19b6af-622c-476e-bdfd-e082d9689596" />
Components: componentes reutilizáveis por toda a página
Data: modelos e dados (acesso ao banco de dados por ex)
Layout: esqueleto visual comum nas páginas
Pages: componente com rotas (telas acessadas pela url)
wwwroot: arquivos servidos direto do navegador.


## Componentes criados

| Componente | Responsabilidade | Parâmetros que recebe |
|---|---|---|
| `App` | Roteamento das páginas com layout padrão | — |
| `MainLayout` | Barra superior, tema Afya e modo escuro | `Body` |
| `Dashboard` | KPIs, gráficos, performance, atividades e projetos recentes | — |
| `NotFound` | Página de rota não encontrada | — |

## O que aprendi

Responda **com suas próprias palavras** (um parágrafo curto por pergunta):

Como uma aplicação Blazor WebAssembly inicia no navegador? Qual é o papel do index.html, da <div id="app"> e do Program.cs?
R: O navegador carrega o index.html, que baixa o runtime do .NET e as DLLs do projeto. Enquanto isso, a <div id="app"> mostra o carregamento. Depois o Program.cs registra os serviços e coloca o componente App dentro dessa div.

Qual é a diferença entre um Layout, uma Page e um Component neste projeto? Dê um exemplo de cada.
R: O layout é a estrutura que se repete em todas as telas, como o MainLayout. A page tem rota com @page, como o Dashboard. O component é uma peça reutilizável sem rota, como o DashboardCard.

O que é um RenderFragment e como o DashboardCard usa esse recurso para ser reutilizado por vários cards?
R: É um pedaço de interface passado como parâmetro. O DashboardCard recebe o conteúdo pelo ChildContent e só cuida da parte visual, então serve para qualquer card.

Como funciona o @bind-Valor no SeletorPeriodo? Qual é o papel do ValorChanged?
R: O @bind-Valor liga a variável da página ao componente nos dois sentidos. O ValorChanged é o evento que avisa a página quando o usuário escolhe outro valor.

Por que os dados ficam na pasta Data, separados dos componentes? Que vantagem isso traz se, no futuro, os dados vierem de uma API?
R: Assim os componentes só exibem os dados, sem saber de onde eles vêm. Se os dados passarem a vir de uma API, basta mudar a pasta Data.

Como o MudGrid com xs, sm e lg faz os cards de KPI se reorganizarem em telas de tamanhos diferentes?
R: O grid tem 12 colunas, e cada valor diz quantas o card ocupa em cada tamanho de tela. Fica um card por linha no celular, dois em telas médias e quatro em telas grandes.

Como foi possível estilizar a página inteira sem escrever CSS? Explique o papel do tema (MudTheme) e das classes utilitárias.
R: O MudTheme define as cores de toda a aplicação, e os componentes do MudBlazor já vêm estilizados. Os ajustes foram feitos com classes utilitárias, como pa-4, mb-4 e d-flex.

Por que o namespace do projeto é afya_admin e não afya-admin?
R: O C# não aceita hífen em namespace, porque entende o hífen como sinal de menos. Por isso o .NET trocou o hífen por underline.

## Dificuldades e soluções

Descreva pelo menos **dois problemas** que você enfrentou durante o desenvolvimento e como resolveu cada um.

Dificuldades e soluções

1. Gráficos não compilavam depois de atualizar o MudBlazor
Problema: a versão 9 mudou a API dos gráficos e o build falhava.
Solução: troquei ChartSeries por ChartSeries<double>, adicionei T="double" no MudChart e usei ChartLabels no lugar de XAxisLabels.

2. Menu lateral aparecendo vazio
Problema: o layout usava um <NavMenu /> que não existia, e a barra lateral ficava em branco.
Solução: removi o MudDrawer e o botão de menu, deixando o conteúdo ocupar a tela toda.

## Melhorias futuras (opcional)

O que você implementaria a seguir? Se fez algum dos desafios da seção 20 do tutorial, descreva aqui.

Buscar os dados de uma API em vez de deixá-los fixos no código.
Separar o Dashboard em componentes reutilizáveis, como KpiCard e DashboardCard.
Adicionar um filtro de período (mês, trimestre, ano) para atualizar os gráficos.

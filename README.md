# 🎮 Dashboard de Vendas – Xbox Game Pass

Dashboard em Excel que transforma a base bruta de assinaturas do Xbox Game Pass em indicadores visuais para apoiar decisões de negócio.

[Prévia do dashboard]<img width="1095" height="515" alt="dashboard" src="https://github.com/user-attachments/assets/8993ad07-ef7e-4750-9757-b7e418532763" />


## 🎯 Objetivo

Organizar e visualizar os dados de vendas de assinaturas, respondendo a quatro perguntas de negócio:

| # | Pergunta | Resultado |
|---|----------|-----------|
| 1 | Qual o faturamento total dos planos **anuais** (todas as assinaturas agregadas)? | R$ 1.754,00 |
| 2 | Qual o faturamento dos planos anuais, separado por **auto renovação** (sim/não)? | Com: R$ 1.537,00 · Sem: R$ 217,00 |
| 3 | Qual o total de vendas do **EA Play Season Pass** (por plano)? | R$ 2.940,00 (somente plano Ultimate) |
| 4 | Qual o total de vendas do **Minecraft Season Pass** (por plano)? | R$ 3.880,00 (Standard R$ 1.920 + Ultimate R$ 1.960) |

> Os resultados de 3 e 4 mudam conforme o filtro de tipo de assinatura (valores acima com o filtro em **Todos**).

## 📂 Estrutura do repositório

```
xbox-dashboard/
├── dashboard_xbox.xlsx   # Arquivo Excel com o dashboard concluído
├── docs/
│   └── dashboard.png     # Prévia do dashboard
└── README.md
```

## 🗂️ Abas do arquivo Excel

| Aba | Conteúdo |
|-----|----------|
| **Assets** | Paleta de cores e logos usados no visual |
| **Bases** | Dados brutos (tabela `Tabela1`): 295 assinaturas, de jan a dez/2024 |
| **Cálculos** | Uma seção por pergunta de negócio, com fórmulas `SUMIFS` ligadas à base |
| **Dashboard** | Painel final: cartões de KPI, gráficos e filtro |

## 📊 Dados utilizados

Colunas da aba **Bases**:

- `Subscriber ID`, `Name` – identificação do assinante
- `Plan` – Core, Standard ou Ultimate
- `Start Date` – data de início
- `Auto Renewal` – Yes/No
- `Subscription Price`, `Subscription Type` – preço e periodicidade (Monthly, Quarterly, Annual)
- `EA Play Season Pass` e `Price` – contratou o EA Play? Valor (`-` quando não contratou)
- `Minecraft Season Pass` e `Price` – contratou o Minecraft? Valor
- `Coupon Value` – desconto aplicado
- `Total Value` – valor total da venda

## 🛠️ Como o dashboard foi construído

1. **Bases** – dados importados e formatados como Tabela do Excel.
2. **Cálculos** – cada pergunta de negócio responde com `SUMIFS`, por exemplo:
   ```excel
   =SUMIFS(Bases!M:M, Bases!G:G, "Annual")                                    // Pergunta 1
   =SUMIFS(Bases!M:M, Bases!G:G, "Annual", Bases!E:E, "Yes")                  // Pergunta 2
   =SUMIFS(Bases!I:I, Bases!C:C, "Ultimate", Bases!G:G, <filtro>)             // Pergunta 3
   ```
3. **Dashboard** – 3 cartões de KPI + 2 gráficos de barras, usando a paleta Xbox (`#22C55E`, `#9BC848`, fundo `#E8E6E9`).
4. **Filtro** – lista suspensa (validação de dados) na célula `H5` do Dashboard: *Todos, Annual, Quarterly, Monthly*. Atua nos cartões/gráfico de EA Play e Minecraft.

## ▶️ Como reproduzir

1. Baixe `dashboard_xbox.xlsx` e abra no **Excel** (2016 ou superior).
2. Vá à aba **Dashboard** e escolha o tipo de assinatura na lista suspensa.
3. Para ver como cada número é calculado, abra a aba **Cálculos**.
4. Para usar dados novos, substitua o conteúdo da aba **Bases** mantendo as mesmas colunas; tudo recalcula automaticamente (as fórmulas usam colunas inteiras).

Para recriar do zero: insira sua base, crie as fórmulas `SUMIFS` na aba Cálculos, monte os cartões (células mescladas com fundo branco e cabeçalho verde) e insira os gráficos de barras apontando para as tabelas de Cálculos.

## 📝 Observações

- A coluna `EA Play Season Pass Price` traz `-` (texto) para quem não contratou; o `SUMIFS` ignora textos, então a soma considera só os valores numéricos.
- Os valores estão em R$ conforme a base fornecida.

## 👤 Autor
Jonathan Moreira
Projeto desenvolvido como desafio de dashboard de vendas no Excel.

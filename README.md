# URBANFLOW — Smart Mobility Analytics

## 📌 Visão Geral do Projeto

URBANFLOW é um projeto de portfólio sênior focado em mobilidade urbana e eficiência de transporte, desenvolvido para demonstrar competências avançadas em análise de dados, modelagem dimensional, DAX, storytelling executivo e design analítico.

O projeto simula um cenário realista de grandes cidades que enfrentam congestionamento, altos custos operacionais e desafios de sustentabilidade, utilizando dados sintéticos não homogêneos e visualmente contrastantes.

---

## 🎯 Objetivos de Negócio

* Entender padrões de tráfego urbano
* Avaliar desempenho por região, corredor e modal
* Reduzir tempo médio de viagem
* Otimizar frota e rotas
* Avaliar custos operacionais e eficiência
* Analisar impacto ambiental (CO₂)
* Apoiar decisões estratégicas de gestores públicos

---

## 🧠 Abordagem Metodológica — DEASA

O projeto segue o método DEASA:

1. Definição do Problema
   Ineficiência do transporte urbano em grandes cidades.

2. Estruturação do Problema
   Segmentação por tempo, região, corredor, modal, veículo e clima.

3. Análise de Dados
   Base simulada realista, assimétrica e com horários de pico bem definidos.

4. Desenvolvimento de Soluções
   KPIs, métricas DAX e dashboards orientados à decisão.

5. Apresentação dos Resultados
   Storytelling executivo com visual Data Tech.

---

## 🗂️ Modelo de Dados — Estrela

### 🎯 Fato

Fato_Deslocamentos (250.000 registros)

Campos:

* ID_Deslocamento
* Date
* ID_Regiao
* ID_Corredor
* ID_Modal
* ID_Veiculo
* ID_Clima
* Distancia_km
* Tempo_Viagem_min
* Velocidade_Media_kmh
* Passageiros
* Custo_Operacional_R$
* Emissao_CO2

### 📐 Dimensões

* Dim_Tempo
* Dim_Regiao
* Dim_Corredor
* Dim_Modal
* Dim_Veiculo
* Dim_Clima

Granularidade: 1 linha = 1 deslocamento

---

## 📊 KPIs Principais

* Total de Deslocamentos
* Passageiros Transportados
* Tempo Médio de Viagem
* Velocidade Média
* Custo Total
* Custo por Passageiro
* Emissão Total de CO₂
* Eficiência do Transporte
* Variação YoY / MoM

---

## 🧮 Medidas DAX (Exemplos-Chave)

🔢 Métricas de Volume

Total de Deslocamentos
Total Deslocamentos =
COUNT ( Fato_Deslocamentos[ID_Deslocamento] )

Passageiros Totais
Passageiros Totais =
SUM ( Fato_Deslocamentos[Passageiros] )

⏱️ Tempo de Viagem

Tempo Médio de Viagem (min)
Tempo Médio de Viagem =
AVERAGE ( Fato_Deslocamentos[Tempo_Viagem_min] )

Tempo Médio de Viagem (Ponderado)
Tempo Médio de Viagem (Ponderado) =
DIVIDE (
    SUM ( Fato_Deslocamentos[Tempo_Viagem_min] ),
    [Total Deslocamentos],
    0
)

🚀 Velocidade

Velocidade Média (km/h)

Velocidade Média =
DIVIDE (
    SUM ( Fato_Deslocamentos[Distancia_km] ),
    SUM ( Fato_Deslocamentos[Tempo_Viagem_min] ) / 60,
    0
)

💰 Custos Operacionais

Custo Total
Custo Total =
SUM ( Fato_Deslocamentos[Custo_Operacional_R$] )

Custo Médio por Deslocamento
Custo Médio por Deslocamento =
AVERAGE ( Fato_Deslocamentos[Custo_Operacional_R$] )

Custo por Passageiro
Custo por Passageiro =
DIVIDE (
    [Custo Total],
    [Passageiros Totais],
    BLANK()
)

🌱 Sustentabilidade & Emissões

Emissão Total de CO₂
Emissão CO2 Total =
SUM ( Fato_Deslocamentos[Emissao_CO2] )

Emissão Média por Deslocamento
Emissão CO2 Média =
AVERAGE ( Fato_Deslocamentos[Emissao_CO2] )

Emissão de CO₂ por Passageiro
Emissão CO2 por Passageiro =
DIVIDE (
    [Emissão CO2 Total],
    [Passageiros Totais],
    BLANK()
)

⚙️ Eficiência do Transporte

Eficiência do Transporte
Eficiência do Transporte =
DIVIDE (
    [Passageiros Totais],
    [Custo Total],
    0
)


Interpretação: quanto maior o valor, maior a eficiência do sistema de transporte.

📅 Indicadores Temporais (YoY / MoM)

Passageiros YoY
Passageiros YoY =
CALCULATE (
    [Passageiros Totais],
    SAMEPERIODLASTYEAR ( Dim_Tempo[Date] )
)

Variação YoY (%)
Passageiros YoY % =
DIVIDE (
    [Passageiros Totais] - [Passageiros YoY],
    [Passageiros YoY],
    BLANK()
)

Passageiros MoM
Passageiros MoM =
CALCULATE (
    [Passageiros Totais],
    DATEADD ( Dim_Tempo[Date], -1, MONTH )
)

Variação MoM (%)
Passageiros MoM % =
DIVIDE (
    [Passageiros Totais] - [Passageiros MoM],
    [Passageiros MoM],
    BLANK()
)

📏 Métricas Complementares

Distância Total Percorrida (km)
Distância Total =
SUM ( Fato_Deslocamentos[Distancia_km] )

Distância Média por Deslocamento (km)
Distância Média =
AVERAGE ( Fato_Deslocamentos[Distancia_km] )
---

## 📈 Dashboard — Estrutura

### Página 1 — Resumo Executivo

<img width="874" height="800" alt="pag1" src="https://github.com/user-attachments/assets/3556bf10-9bcd-4f12-b80e-c04259c63d90" />

* KPIs principais
* Passageiros por Modal
* Tempo Médio por Região
* Mapa de fluxos

### Página 2 — Tráfego & Sazonalidade

<img width="978" height="802" alt="pag2" src="https://github.com/user-attachments/assets/05510ae9-b9f5-4e18-a37d-4fb445d7990c" />

* Tempo por Hora do Dia
* Heatmap Hora x Região
* Velocidade por Corredor

### Página 3 — Modais & Eficiência

<img width="989" height="802" alt="pag3" src="https://github.com/user-attachments/assets/95e627e0-e039-40c2-8073-bbe91d49ed44" />

* Passageiros por Modal
* Scatter Distância x Tempo
* Custo por Modal

### Página 4 — Custos & Sustentabilidade

<img width="991" height="801" alt="pag4" src="https://github.com/user-attachments/assets/ab2abaed-ed84-4059-a75f-bf302c679263" />

* Custo por Região
* Emissão CO₂ por Modal
* Emissão ao longo do tempo
* Ranking de corredores menos eficientes

---

## 🎨 Design & Layout

Tema visual: Data Tech / Smart Mobility Analytics

* Fundo escuro
* Alto contraste
* Paleta fria (azul, roxo, verde tech)
* Ênfase em leitura e comparação

Ferramentas:

* Power BI
* Figma (layout e identidade visual)

---

## 🧪 Validações Importantes

* Métricas não aditivas calculadas corretamente
* Relação física coerente entre distância, tempo e velocidade
* Distribuições assimétricas e não homogêneas
* Diferença visual clara entre regiões e modais

---

## 🧠 Principais Insights (Exemplos)

* Modais coletivos apresentam economia de escala significativa
* Regiões periféricas possuem maior tempo médio de viagem
* Horários de pico impactam fortemente corredores arteriais
* Eficiência varia mais por corredor do que por região

---


## 🚀 Objetivo do Projeto

Este projeto foi desenvolvido para:

* Portfólio profissional
* GitHub
* LinkedIn
* Entrevistas técnicas
* Demonstração de senioridade em Analytics

---

## 👤 Autor

Projeto desenvolvido por Guilherme Alencar
Área: Data Analytics / Business Intelligence 

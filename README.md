# SPN — Servidor Web

Trabalho 07: Modelagem e Avaliação de Desempenho com Redes de Petri Estocásticas (SPN).
Contexto escolhido: **Servidor Web** (fila de capacidade limitada com vários núcleos de processamento).

- Artigo (PDF, formato IEEE, 6 páginas): *a adicionar*
- Vídeo de apresentação (5 min): *a adicionar*

## Conteúdo

| Caminho | Descrição |
|---|---|
| `spn_servidor_web.ipynb` | Notebook com o simulador SPN, o modelo, a validação e os experimentos E1 a E4 |
| `results/` | CSVs gerados: tabela consolidada, resultados por experimento, réplicas brutas e validação |
| `figures/` | Gráficos (PNG e PDF) e figura do modelo SPN usados no artigo |

## Como reproduzir

```bash
pip install -r requirements.txt
jupyter notebook spn_servidor_web.ipynb   # Run All (cerca de 30 s)
```

As sementes são fixas, então os resultados são idênticos a cada execução.

## Modelo

Lugares: `P_Chegada`, `P_Req`, `P_Vagas` (K_q), `P_Fila`, `P_Servidores` (c), `P_Proc`, `P_Concluidas`, `P_Descartadas`.
Transições: `T_Chegada` (temporizada, λ), `T_Admite`, `T_Descarta` (imediata com arco inibidor de `P_Vagas`), `T_Inicio` (imediatas) e `T_Servico` (temporizada, μ, servidor infinito).
O simulador de SPN é implementado no próprio notebook (sem bibliotecas de Petri nets) e é validado contra a solução analítica da fila M/M/c/K.

## Métricas

Throughput (TP), Mean Response Time (MRT), Mean Queue Time (MQT), Mean Processing Time (MPT), Utilização (U) e Drop Probability (DP).

## Experimentos

Referência: λ = 72 req/s, μ = 20 req/s por núcleo, c = 4, K_q = 20.

- **E1**: taxa de chegada (24, 48, 72, 96, 120 req/s)
- **E2**: núcleos (3, 4, 5)
- **E3**: capacidade da fila (5, 20, 80)
- **E4**: demanda e recursos combinados (S1, S2 e S3, todos com ρ = 0,8)

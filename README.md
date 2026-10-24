# Código-Fonte do Trabalho de Conclusão de Curso

SCA-Lab: simulador de análise de energia (power analysis) sobre um AES-128 simulado, com e sem mascaramento.

## Como executar

Abra [`simulador-analise-energia.html`](./simulador-analise-energia.html) no navegador. Não há dependências, etapa de build ou servidor: todos os cálculos ocorrem no próprio navegador.

## Estrutura

Todo o código da ferramenta está em um único arquivo HTML, dividido em três partes: o bloco de estilos (CSS), a marcação da página (HTML) e o bloco de script (JavaScript). O script segue a divisão em módulos da arquitetura, nesta ordem:

| Parte | Funções e constantes |
|---|---|
| Parâmetros do experimento | `KEY`, `SIGMA`, `BASE`, `WIN` |
| AES-128 de referência | `xtime`, `gmul`, `buildSBox`, `keyExpansion`, `shiftRows`, `mixColumns`, `aesRun`, `aesSelfTest` |
| Geração dos dados | `hw`, `randn`, `simulateTrace`, `acquire` |
| Análises | `makeCheckpoints`, `runAttack`, `tvla`, `spaAnalyze` |
| Desenho e apresentação | `drawTrace`, `drawCorr`, `attachTip`, `render` |
| Tratador do botão "Rodar simulação" | encadeia as etapas |

## Testes

A pasta [`testes`](./testes) contém os testes automatizados e os resultados registrados. Eles não fazem parte da ferramenta entregue.

| Arquivo | Conteúdo | Resultado registrado |
|---|---|---|
| `lib.js` | Carrega as funções direto do arquivo HTML e troca o `Math.random` por um gerador com semente | |
| `unit.js` | Testes unitários da cifra, das funções básicas e dos dados | `resultado_unit.json` |
| `experimentos.js` | Ataque, teste de vazamento e análise simples em muitas repetições | `resultado_experimentos.json` |
| `sensibilidade.js` | Taxa de acerto do ataque em função do número de execuções | `resultado_sensibilidade.json` |
| `interface.js` | Testes de interface com Playwright | `resultado_interface.json` |

Para executar, com Node.js instalado, a partir da pasta `testes`:

```
node unit.js
node experimentos.js
node sensibilidade.js
node interface.js
```

O `interface.js` exige o Playwright instalado globalmente (`npm install -g playwright`) e o navegador Chromium do Playwright. Cada script regrava o arquivo de resultado correspondente.

---
name: imersao-ceos-guardanapo-para-sistema
description: 'Imersão CEOs: This skill should be used when the user sends a photo, image, transcription, or description of the Guardanapo dynamics, says "Estou na dinâmica do Guardanapo e o meu poço é esse", uses an equivalent phrase such as "esse é o meu poço" or "transforma esse fluxo em sistema", or describes a sheet with Empresa, Área, Fluxo and steps marked H, HA or A. It reads the Onde and Como sides, asks only what is missing, obtains scope approval, and implements the first functional phase through the Skip MCP.'
version: 0.1.0
---

# Guardanapo → Sistema

Transformar a dinâmica do Guardanapo no menor sistema funcional capaz de resolver um caso real e gerar valor para o participante. Não construir uma maquete nem limitar artificialmente o sistema a uma coleção de dados. Derivar a estrutura necessária do fluxo: usuários, registros, itens relacionados, histórico, arquivos e outras entidades entram quando forem necessários para a execução real.

## Quando acionar

Acionar ao receber:

- foto ou imagem da frente e do verso do Guardanapo;
- transcrição ou descrição textual da dinâmica;
- a frase “Estou na dinâmica do Guardanapo e o meu poço é esse”;
- formulações equivalentes, como “esse é o meu poço”, “quero transformar esse fluxo em sistema” ou “crie um sistema para esse fluxo”.

Considerar frente e verso enviados juntos como a entrada esperada. A identificação do poço é conduzida pela pessoa facilitadora; não assumir essa responsabilidade nem refazer a dinâmica sem necessidade.

## Resultado esperado

Conduzir o participante do guardanapo até um sistema rodando com um caso
real, nesta ordem:

1. leitura confirmada do Onde e do Como;
2. perguntas mínimas apenas quando houver lacunas reais;
3. escopo de MVP para aprovação na conversa, com as fases definidas;
4. Fase 1 implementada pelo MCP do Skip, aplicada e verificada;
5. checklist de teste manual da Fase 1, cobrindo acesso, entrada,
   persistência e o que estiver na fase;
6. Fase 2 implementada, aplicada e verificada, com o checklist
   correspondente: botões, campos, status, apoio de IA e ações automáticas;
7. Fase 3: um caso verdadeiro do participante rodando do início ao fim,
   com a saída prometida existindo e podendo ser usada;
8. passagem de bastão entregue em bloco único.

Dois portões governam esse percurso. Não iniciar a construção antes de o
participante aprovar o escopo explicitamente. Não avançar para a fase
seguinte antes de o checklist da fase atual ser validado por ele — fase
aplicada sem teste confirmado esconde erro que só aparece no caso real,
quando corrigir custa muito mais.

Se o percurso for interrompido antes da Fase 3, entregar mesmo assim o
link, o escopo e o estado de cada fase, para que o trabalho continue
depois.

## Passo 1 — Ler e confirmar

Interpretar a frente como a cadeia Empresa → Área → Fluxo e o verso como o fluxo quebrado em etapas. Devolver uma leitura curta, sem inventar texto ilegível:

```text
Li isto no seu guardanapo:

POÇO (o fluxo): [fluxo]
RESULTADO DA ÁREA: [resultado]

ETAPAS:
1. [etapa] — [H/HA/A ou classificação pendente]
2. [etapa] — [H/HA/A ou classificação pendente]
...

Está certo? Corrija somente o que eu li errado antes de eu montar o sistema.
```

Sinalizar exatamente a linha ilegível ou ambígua. Não preencher buracos com etapas inventadas.

## Passo 2 — Perguntar somente o necessário

Perguntar apenas quando a informação for indispensável para desenhar um sistema funcional. Fazer uma única rodada curta, com no máximo quatro perguntas. Priorizar:

1. quem opera o fluxo no sistema;
2. o que dispara o fluxo e quais informações existem nesse momento;
3. o que precisa existir quando o fluxo termina bem;
4. quais campos, documentos ou dados são indispensáveis, somente se não for possível deduzi-los.

Propor uma interpretação para cada resposta em vez de abrir um questionário. Usar fallback quando o fluxo estiver mal definido, faltar informação essencial, houver trecho ilegível, a descrição tiver parado numa área em vez de chegar a um fluxo, ou não estiver claro o início, o fim, a entrada ou a saída.

Não usar a ausência de H, HA ou A como fallback principal. Resolver tecnicamente essa classificação conforme o Passo 3.

## Passo 3 — Traduzir as etapas para o sistema

Colocar toda etapa relevante no sistema. A letra indica o grau de execução, não se a etapa será descartada.

| Classificação | Tradução no sistema | Regra de decisão |
|---|---|---|
| H | Status ou etapa humana com campos de trabalho, instruções, responsável, data e saída registrada | Usar quando a pessoa executa, decide, negocia, interpreta ou produz algo que exige julgamento humano |
| HA | Status ou etapa humana com apoio de IA, incluindo botão para gerar rascunho, análise ou sugestão e revisão antes do avanço | Usar quando a pessoa permanece responsável, mas a IA consegue preparar ou analisar parte relevante |
| A | Ação executável pelo sistema, com resultado visível, verificável e registrado | Usar quando a ação é objetiva, determinística e pode ser executada sem decisão humana nova |

Se a classificação estiver ausente ou ambígua, decidir pela natureza da etapa. Não pedir ao participante que classifique novamente salvo se a ambiguidade mudar substancialmente o produto e não puder ser resolvida tecnicamente.

Nenhuma etapa H deve ser um checkbox vazio. Registrar os dados que a etapa produz: notas, decisões, valores, documentos, motivos, responsáveis ou evidências. Nenhuma etapa HA deve esconder a revisão humana. Toda etapa A deve mostrar a saída e registrar a execução.

Transformar o fluxo em status, ações ou painéis conforme necessário. Não forçar todas as etapas ao mesmo modelo se isso impedir a entrega de valor. Manter entre quatro e sete unidades operacionais quando possível; se o guardanapo tiver mais, agrupar apenas quando o agrupamento preservar a execução e explicar o agrupamento no escopo.

## Passo 4 — Escrever o escopo e aguardar aprovação

Gerar um escopo curto e concreto, usando este formato:

```markdown
# [Nome do sistema]

**Em uma frase:** Quando [entrada], o sistema [faz X] e devolve [saída], para [quem].
**Número que isso tem que mexer:** [resultado mensurável da Área]

## O que o sistema precisa guardar
[Entidades, registros e relações necessárias para executar o caso real. Não limitar previamente a uma coleção.]

## As etapas, virando sistema
| # | Status ou ação | Letra | O que acontece na tela |
|---|---|---|---|
| 1 | ... | H/HA/A | ... |

## Fora do MVP (v2)
- [pedido que não é necessário para resolver o caso real agora]

## As três fases da construção
Fase 1 — Fundação funcional: [login básico, segurança mínima, estrutura necessária, entrada e persistência]
Fase 2 — Execução do fluxo: [status, campos, ações, apoio de IA e automações cabíveis]
Fase 3 — Caso real: [rodar um caso verdadeiro e corrigir bloqueios]
```

Definir MVP pelo valor entregue, não por uma contagem fixa de telas, tabelas ou coleções. Incluir tudo que for necessário para o caso real funcionar de ponta a ponta e excluir funcionalidades que não contribuam para esse caso.

Perguntar exatamente: **“Aprovo assim?”**. Se houver mudança que aumente o escopo, indicar o que será retirado ou adiado. Corrigir e reapresentar o escopo antes de construir.

## Passo 5 — Construir com o MCP do Skip

Usar o MCP do Skip para implementar a fase aprovada. Consultar as instruções e capacidades disponíveis do Skip antes de escolher a forma de execução. Escrever os arquivos necessários, aplicar as mudanças e verificar o resultado real antes de reportar.

### Fase 1 — Fundação funcional

Implementar:

- login básico e segurança mínima;
- usuários e acesso necessários ao caso, sem deixar dados expostos indevidamente;
- estrutura de dados derivada do fluxo;
- entrada do caso;
- criação, edição e persistência dos registros necessários;
- primeira visualização funcional do processo.

Aplicar as mudanças ao fim da fase e entregar o link de preview, quando disponível, junto com o checklist de teste.

### Fase 2 — Execução do fluxo

Implementar:

- status, ações ou painéis que representem as etapas;
- campos e evidências produzidos por cada etapa H;
- apoio de IA nas etapas HA, sempre com revisão humana;
- ações automáticas nas etapas A, com saída visível e registrada;
- avanço do caso até a saída final.

Aplicar e verificar a fase antes de entregar o checklist correspondente.

### Fase 3 — Caso real

Rodar um caso verdadeiro do participante do início ao fim. Não ampliar o produto durante essa fase sem necessidade. Corrigir o que o caso real revelar e verificar se a saída prometida foi produzida.

## Regras técnicas do MVP

- Incluir login básico e segurança mínima desde a fundação; não remover autenticação para ganhar velocidade.
- Derivar a estrutura de dados do fluxo real; não impor uma única coleção nem qualquer outra restrição artificial.
- Priorizar o menor sistema funcional que resolva o caso real de ponta a ponta.
- Usar o MCP do Skip quando contribuírem para a solução.
- Evitar integrações, permissões avançadas ou automações externas que não sejam necessárias para o caso escolhido; colocar no v2 somente o que puder ser adiado sem quebrar o valor principal.
- Proteger dados de usuários e registros conforme as capacidades disponíveis no Skip.
- Não sinalizar tempo de construção ou prometer duração: o tempo com IA é variável e não é critério de qualidade.

## Passo 6 — Testes manuais

Entregar uma lista curta e ordenada ao fim de cada fase. Cada item deve ser verificável por alguém que não programa. Incluir, conforme a fase:

```text
FASE 1 — teste agora:
[ ] Abrir o link do sistema
[ ] Criar ou acessar uma conta autorizada
[ ] Confirmar que uma pessoa sem acesso não consegue entrar nos dados protegidos
[ ] Criar um caso real e preencher os campos de entrada
[ ] Salvar e encontrar o caso na tela do sistema
[ ] Recarregar a página e confirmar que os dados continuam lá

Avançar para a Fase 2 somente depois de validar cada linha. Se travar, informar o número da linha e o que apareceu na tela.
```

Na Fase 2, testar cada botão, campo, status, ferramenta de IA e ação automática. Na Fase 3, levar um caso verdadeiro do começo ao fim e confirmar que a saída prometida existe e pode ser usada.

Fechar com o teste de passagem de bastão: entregar o link a uma pessoa que não conhece o fluxo e pedir que execute um caso sem explicações adicionais. Registrar onde ela travar; esse ponto revela o que ainda depende da cabeça do operador.

## Passo 7 — Entregar a passagem de bastão

Depois de validar o caso real, entregar em bloco único:

- link do sistema;
- frase de escopo;
- etapas, classificações e ações correspondentes;
- etapa candidata a receber um agente ou automação posterior, com justificativa;
- itens fora do MVP;
- mensagem curta para a pessoa que operará o sistema.

## Situações de guardanapo fraco

- **Área sem fluxo:** pedir o pedaço específico que mais trava dentro da área e seguir com esse fluxo.
- **Fluxo com poucas etapas:** perguntar o que acontece imediatamente antes e depois apenas se isso for necessário para fechar a entrada e a saída.
- **Fluxo com muitas etapas:** agrupar etapas relacionadas sem apagar o trabalho necessário; registrar o agrupamento no escopo.
- **Lacuna de entrada, saída ou responsável:** perguntar somente a lacuna que impede o sistema funcional.
- **Letras ausentes:** classificar tecnicamente como H, HA ou A conforme a etapa; não transformar isso em questionário.
- **Todas as etapas classificadas A ou nenhuma classificada A:** construir conforme a natureza real das etapas e indicar, na passagem de bastão, a melhor candidata a agente ou automação posterior.

## Recursos adicionais

Consultar o MCP do Skip para instruções atuais de projeto, arquivos, aplicação, preview, autenticação e dados antes de executar a construção. Não inventar nomes de ferramentas, contratos ou capacidades do MCP.

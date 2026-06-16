# Estrutura de Dados — Central Operacional CFTA • Belli • Governor

## 1. Objetivo deste documento

Este documento define a estrutura de dados da Central Operacional CFTA • Belli • Governor.

A finalidade é padronizar os campos, categorias, status e relações entre os módulos do sistema, evitando cadastros soltos e preparando a plataforma para futuras melhorias com Codex, banco de dados, login, upload real e relatórios automáticos.

A versão atual da Central funciona em HTML/CSS/JavaScript com salvamento local no navegador. Mesmo assim, a estrutura abaixo já deve ser pensada como base para uma futura migração para banco de dados.

---

# 2. Módulos principais do sistema

A Central deve ser organizada nos seguintes módulos:

1. Dashboard;
2. Atividades / Kanban;
3. Projetos Legislativos CFTA;
4. Congresso / Comissões / Parlamentares;
5. Calendário;
6. Biblioteca;
7. Relatórios;
8. Pesquisas;
9. Bloqueios Governor;
10. Configurações;
11. Usuários e permissões, em fase futura.

---

# 3. Estrutura geral de IDs

Todos os registros devem ter um identificador único.

## Padrão recomendado

```text
prefixo_timestamp_random
```

## Exemplos

```text
atividade_20260616_001
projeto_20260616_001
relatorio_20260616_001
arquivo_20260616_001
pesquisa_20260616_001
```

## Prefixos recomendados

| Módulo                | Prefixo        |
| --------------------- | -------------- |
| Atividades            | `atividade_`   |
| Projetos Legislativos | `projeto_`     |
| Biblioteca            | `arquivo_`     |
| Relatórios            | `relatorio_`   |
| Calendário            | `evento_`      |
| Comissões             | `comissao_`    |
| Parlamentares         | `parlamentar_` |
| Pesquisas             | `pesquisa_`    |
| Bloqueios Governor    | `bloqueio_`    |
| Usuários              | `usuario_`     |

---

# 4. Atividades / Kanban

## 4.1. Objetivo do módulo

Registrar, acompanhar e priorizar as demandas operacionais da equipe CFTA/Belli/Governor.

Esse módulo deve concentrar:

* tarefas semanais;
* demandas de monitoramento legislativo;
* produção de relatórios;
* atualização de projetos;
* rotinas fixas;
* bloqueios operacionais;
* demandas do sistema Governor;
* atividades da Ana Paula, Vitor e equipe Belli/Governor.

---

## 4.2. Campos da atividade

| Campo                 | Tipo         | Obrigatório | Descrição                                             |
| --------------------- | ------------ | ----------- | ----------------------------------------------------- |
| `id`                  | texto        | Sim         | Identificador único da atividade                      |
| `titulo`              | texto        | Sim         | Nome curto da atividade                               |
| `descricao`           | texto longo  | Não         | Explicação detalhada da atividade                     |
| `projeto_vinculado`   | texto/id     | Não         | Projeto CFTA, pesquisa, relatório ou frente vinculada |
| `responsavel`         | texto        | Sim         | Pessoa ou equipe responsável                          |
| `status`              | lista        | Sim         | Situação atual da atividade                           |
| `prioridade`          | lista        | Sim         | Grau de urgência/importância                          |
| `tipo`                | lista        | Sim         | Natureza da atividade                                 |
| `prazo`               | data         | Não         | Data limite, quando houver                            |
| `data_criacao`        | data         | Sim         | Data em que a atividade foi criada                    |
| `data_atualizacao`    | data         | Sim         | Última atualização                                    |
| `origem`              | lista/texto  | Não         | Origem da demanda                                     |
| `tags`                | lista        | Não         | Palavras-chave                                        |
| `observacoes`         | texto longo  | Não         | Observações internas                                  |
| `links`               | lista        | Não         | Links relacionados                                    |
| `arquivos_vinculados` | lista de ids | Não         | Documentos da biblioteca associados                   |
| `historico`           | lista        | Futuro      | Histórico de alterações                               |
| `concluida_em`        | data         | Não         | Data de conclusão                                     |

---

## 4.3. Status de atividades

| Status         | Uso                                                          |
| -------------- | ------------------------------------------------------------ |
| `a_fazer`      | Atividade cadastrada, mas ainda não iniciada                 |
| `em_andamento` | Atividade em execução                                        |
| `bloqueado`    | Atividade parada por dependência, bug ou falta de informação |
| `em_validacao` | Atividade finalizada, aguardando revisão/envio               |
| `concluido`    | Atividade finalizada                                         |
| `arquivado`    | Atividade encerrada ou sem prioridade atual                  |

---

## 4.4. Prioridades

| Prioridade | Descrição                                                       |
| ---------- | --------------------------------------------------------------- |
| `urgente`  | Demanda crítica, precisa ser resolvida imediatamente            |
| `alta`     | Demanda importante, deve ser priorizada                         |
| `media`    | Demanda relevante, mas sem urgência imediata                    |
| `baixa`    | Demanda complementar                                            |
| `fixa`     | Rotina permanente sem prazo formal, mas com execução recorrente |

---

## 4.5. Tipos de atividade

| Tipo                        | Descrição                                           |
| --------------------------- | --------------------------------------------------- |
| `monitoramento_legislativo` | Acompanhamento de projetos, pautas e tramitações    |
| `relatorio`                 | Produção ou revisão de relatório                    |
| `tramitação`                | Verificação ou envio de movimentação legislativa    |
| `pauta_comissao`            | Monitoramento de pauta de comissão                  |
| `articulacao_politica`      | Atividade de contato, agenda ou estratégia política |
| `pesquisa`                  | Produção ou atualização de estudo/painel            |
| `sistema_governor`          | Correção, melhoria ou bloqueio do Governor          |
| `biblioteca`                | Cadastro, organização ou revisão de documentos      |
| `rotina_fixa`               | Rotina operacional recorrente                       |
| `agroindustria`             | Frente específica de agroindústria                  |
| `administrativo`            | Organização interna, documentação ou planejamento   |

---

## 4.6. Origens da demanda

| Origem           | Descrição                                       |
| ---------------- | ----------------------------------------------- |
| `cfta`           | Demanda originada pelo CFTA                     |
| `belli`          | Demanda interna da Belli                        |
| `governor`       | Demanda de sistema/dados                        |
| `ana_paula`      | Demanda operacional da consultoria              |
| `vitor`          | Demanda de organização, relatório ou tecnologia |
| `congresso`      | Demanda gerada por movimentação legislativa     |
| `rotina_semanal` | Demanda derivada da rotina fixa                 |
| `cliente`        | Demanda externa/institucional                   |
| `outro`          | Outra origem                                    |

---

## 4.7. Exemplo de atividade

```json
{
  "id": "atividade_20260616_001",
  "titulo": "Atualizar base de projetos de agroindústria",
  "descricao": "Revisar projetos federais e estaduais relacionados à agroindústria, inspeção, SUASA e responsabilidade técnica.",
  "projeto_vinculado": "Frente Agroindústria",
  "responsavel": "Vitor / Ana Paula",
  "status": "em_andamento",
  "prioridade": "alta",
  "tipo": "agroindustria",
  "prazo": "2026-06-19",
  "data_criacao": "2026-06-16",
  "data_atualizacao": "2026-06-16",
  "origem": "belli",
  "tags": ["agroindústria", "CFTA", "projetos legislativos"],
  "observacoes": "Priorizar matérias com impacto direto em responsabilidade técnica.",
  "links": [],
  "arquivos_vinculados": []
}
```

---

# 5. Projetos Legislativos CFTA

## 5.1. Objetivo do módulo

Organizar projetos legislativos acompanhados pela Belli/Governor para o CFTA, com foco em impacto institucional, profissional, técnico e setorial.

O módulo deve servir como base para:

* monitoramento legislativo;
* relatórios semanais;
* relatórios mensais;
* alertas de tramitação;
* análise de impacto;
* atuação política;
* priorização de matérias.

---

## 5.2. Campos do projeto legislativo

| Campo                    | Tipo        | Obrigatório | Descrição                        |
| ------------------------ | ----------- | ----------- | -------------------------------- |
| `id`                     | texto       | Sim         | Identificador único              |
| `numero`                 | texto       | Sim         | Número do projeto                |
| `ano`                    | número      | Sim         | Ano do projeto                   |
| `tipo`                   | lista       | Sim         | PL, PLP, PEC, MPV, PDL etc.      |
| `casa_legislativa`       | lista       | Sim         | Câmara, Senado, Assembleia etc.  |
| `uf`                     | texto       | Não         | UF, quando estadual              |
| `autor`                  | texto       | Não         | Autor da matéria                 |
| `partido_uf_autor`       | texto       | Não         | Partido e UF do autor            |
| `ementa`                 | texto longo | Sim         | Ementa ou resumo oficial         |
| `resumo_executivo`       | texto longo | Não         | Resumo em linguagem estratégica  |
| `tema_principal`         | lista       | Sim         | Tema dominante                   |
| `temas_secundarios`      | lista       | Não         | Temas complementares             |
| `comissao_atual`         | texto       | Não         | Comissão onde tramita            |
| `relator`                | texto       | Não         | Relator atual                    |
| `situacao_atual`         | texto       | Sim         | Situação legislativa atual       |
| `data_ultima_tramitacao` | data        | Não         | Última movimentação              |
| `link_oficial`           | link        | Não         | Link da Câmara/Senado/Assembleia |
| `impacto_cfta`           | lista       | Sim         | Classificação de impacto         |
| `prioridade`             | lista       | Sim         | Prioridade de acompanhamento     |
| `recomendacao`           | texto longo | Não         | Recomendação estratégica         |
| `proxima_acao`           | texto       | Não         | Próximo encaminhamento           |
| `responsavel_interno`    | texto       | Não         | Responsável pelo acompanhamento  |
| `status_monitoramento`   | lista       | Sim         | Situação dentro da operação      |
| `observacoes`            | texto longo | Não         | Observações internas             |
| `tags`                   | lista       | Não         | Palavras-chave                   |
| `data_cadastro`          | data        | Sim         | Data de entrada no sistema       |
| `data_ultima_checagem`   | data        | Sim         | Última revisão manual            |

---

## 5.3. Tipos de proposição

| Tipo    | Descrição                         |
| ------- | --------------------------------- |
| `PL`    | Projeto de Lei                    |
| `PLP`   | Projeto de Lei Complementar       |
| `PEC`   | Proposta de Emenda à Constituição |
| `MPV`   | Medida Provisória                 |
| `PDL`   | Projeto de Decreto Legislativo    |
| `REQ`   | Requerimento                      |
| `INC`   | Indicação                         |
| `PRC`   | Projeto de Resolução              |
| `Outro` | Outros tipos                      |

---

## 5.4. Casas legislativas

| Valor                 | Descrição                       |
| --------------------- | ------------------------------- |
| `camara_federal`      | Câmara dos Deputados            |
| `senado_federal`      | Senado Federal                  |
| `congresso_nacional`  | Congresso Nacional              |
| `assembleia_estadual` | Assembleia Legislativa estadual |
| `camara_distrital`    | Câmara Legislativa do DF        |
| `outro`               | Outro órgão legislativo         |

---

## 5.5. Temas principais

| Tema                        | Descrição                                           |
| --------------------------- | --------------------------------------------------- |
| `agroindustria`             | Agroindústria, produtos artesanais, SUASA, inspeção |
| `responsabilidade_tecnica`  | Atuação técnica, atribuições e RT                   |
| `defesa_agropecuaria`       | Sanidade, fiscalização e defesa agropecuária        |
| `assistencia_tecnica`       | ATER, assistência técnica e extensão rural          |
| `fiscalizacao_profissional` | Fiscalização de exercício profissional              |
| `bioinsumos`                | Bioinsumos e inovação no agro                       |
| `fertilizantes`             | Fertilizantes, insumos e produção                   |
| `credito_rural`             | Crédito, financiamento e renegociação               |
| `agricultura_familiar`      | Agricultura familiar e pequenos produtores          |
| `aquicultura`               | Aquicultura, pesca e produção aquícola              |
| `regularizacao`             | Regularização fundiária, ambiental ou sanitária     |
| `educacao_profissional`     | Ensino técnico, formação e certificação             |
| `outro`                     | Outro tema                                          |

---

## 5.6. Impacto para o CFTA

| Impacto                     | Descrição                                           |
| --------------------------- | --------------------------------------------------- |
| `direto_tecnicos_agricolas` | Afeta diretamente técnicos agrícolas                |
| `direto_agroindustria`      | Afeta diretamente agroindústria e RT                |
| `indireto_setorial`         | Impacta setor agropecuário de forma indireta        |
| `sistemico`                 | Impacto amplo na política agrícola ou institucional |
| `monitoramento`             | Deve ser apenas acompanhado                         |
| `baixa_aderencia`           | Pouca relação com o CFTA                            |

---

## 5.7. Status de monitoramento

| Status                  | Descrição                             |
| ----------------------- | ------------------------------------- |
| `prioritario`           | Acompanhar de perto                   |
| `monitorar`             | Manter no radar                       |
| `aguardar_movimentacao` | Sem ação imediata                     |
| `em_analise`            | Precisa de avaliação técnica/política |
| `encaminhado_relatorio` | Já entrou em relatório                |
| `arquivado`             | Sem prioridade atual                  |

---

## 5.8. Exemplo de projeto legislativo

```json
{
  "id": "projeto_20260616_001",
  "numero": "4314",
  "ano": 2016,
  "tipo": "PL",
  "casa_legislativa": "senado_federal",
  "uf": null,
  "autor": "Jerônimo Goergen",
  "partido_uf_autor": "PP/RS",
  "ementa": "Altera dispositivos do RIISPOA relacionados à inspeção industrial e sanitária de produtos de origem animal.",
  "resumo_executivo": "Projeto relevante para agroindústrias e integração entre serviços de inspeção estadual, municipal e federal.",
  "tema_principal": "agroindustria",
  "temas_secundarios": ["defesa_agropecuaria", "responsabilidade_tecnica"],
  "comissao_atual": "Senado Federal",
  "relator": "",
  "situacao_atual": "Aguardando apreciação pelo Senado Federal",
  "data_ultima_tramitacao": "",
  "link_oficial": "",
  "impacto_cfta": "direto_agroindustria",
  "prioridade": "alta",
  "recomendacao": "Acompanhar no Senado e avaliar oportunidade de manifestação institucional.",
  "proxima_acao": "Verificar tramitação atualizada e relatoria.",
  "responsavel_interno": "Belli/Governor",
  "status_monitoramento": "prioritario",
  "observacoes": "Projeto com aderência à agenda de agroindústria e responsabilidade técnica.",
  "tags": ["RIISPOA", "agroindústria", "inspeção", "POA"],
  "data_cadastro": "2026-06-16",
  "data_ultima_checagem": "2026-06-16"
}
```

---

# 6. Congresso / Comissões / Parlamentares

## 6.1. Objetivo do módulo

Mapear a atuação política relevante para a operação CFTA/Belli:

* comissões prioritárias;
* presidentes de comissão;
* relatores;
* parlamentares-chave;
* lideranças partidárias;
* oportunidades de articulação;
* riscos políticos;
* histórico de contato.

---

## 6.2. Campos de comissão

| Campo                | Tipo  | Obrigatório | Descrição                           |
| -------------------- | ----- | ----------- | ----------------------------------- |
| `id`                 | texto | Sim         | Identificador único                 |
| `sigla`              | texto | Sim         | Sigla da comissão                   |
| `nome`               | texto | Sim         | Nome completo                       |
| `casa`               | lista | Sim         | Câmara, Senado etc.                 |
| `presidente`         | texto | Não         | Presidente atual                    |
| `vice_presidentes`   | lista | Não         | Vice-presidentes                    |
| `temas_relacionados` | lista | Não         | Temas de interesse                  |
| `nivel_prioridade`   | lista | Sim         | Prioridade para o CFTA              |
| `estrategia`         | lista | Não         | Ocupar, influenciar, monitorar etc. |
| `observacoes`        | texto | Não         | Observações estratégicas            |

---

## 6.3. Estratégias para comissões

| Estratégia         | Descrição                                                   |
| ------------------ | ----------------------------------------------------------- |
| `ocupar`           | Comissão onde o CFTA deve buscar presença institucional     |
| `influenciar`      | Comissão onde é importante atuar em relatores/parlamentares |
| `monitorar`        | Comissão que exige acompanhamento frequente                 |
| `conter`           | Comissão com risco de avanço de pautas negativas            |
| `baixa_prioridade` | Apenas acompanhamento eventual                              |

---

## 6.4. Campos de parlamentar

| Campo             | Tipo  | Obrigatório | Descrição                              |
| ----------------- | ----- | ----------- | -------------------------------------- |
| `id`              | texto | Sim         | Identificador único                    |
| `nome`            | texto | Sim         | Nome parlamentar                       |
| `cargo`           | lista | Sim         | Deputado, senador etc.                 |
| `partido`         | texto | Não         | Partido                                |
| `uf`              | texto | Não         | Unidade federativa                     |
| `casa`            | lista | Sim         | Câmara, Senado etc.                    |
| `comissoes`       | lista | Não         | Comissões em que atua                  |
| `lideranca`       | texto | Não         | Governo, oposição, partido, bloco etc. |
| `relacao_cfta`    | lista | Não         | Favorável, neutro, crítico etc.        |
| `grau_influencia` | lista | Não         | Alto, médio, baixo                     |
| `temas_interesse` | lista | Não         | Temas relacionados                     |
| `proximas_acoes`  | texto | Não         | Encaminhamentos sugeridos              |
| `observacoes`     | texto | Não         | Informações políticas relevantes       |

---

# 7. Calendário

## 7.1. Objetivo do módulo

Controlar prazos, rotinas e eventos relevantes da operação.

O calendário deve abranger:

* rotinas semanais;
* reuniões;
* prazos de relatório;
* pautas de comissão;
* audiências públicas;
* entregas internas;
* eventos institucionais;
* checagens de tramitação.

---

## 7.2. Campos de evento

| Campo               | Tipo      | Obrigatório | Descrição                      |
| ------------------- | --------- | ----------- | ------------------------------ |
| `id`                | texto     | Sim         | Identificador único            |
| `titulo`            | texto     | Sim         | Nome do evento                 |
| `descricao`         | texto     | Não         | Detalhes                       |
| `data_inicio`       | data/hora | Sim         | Início                         |
| `data_fim`          | data/hora | Não         | Fim                            |
| `tipo`              | lista     | Sim         | Tipo de evento                 |
| `responsavel`       | texto     | Não         | Responsável                    |
| `projeto_vinculado` | texto/id  | Não         | Projeto associado              |
| `recorrencia`       | lista     | Não         | Diária, semanal etc.           |
| `prioridade`        | lista     | Não         | Urgente, alta etc.             |
| `status`            | lista     | Sim         | Previsto, realizado, cancelado |
| `observacoes`       | texto     | Não         | Observações                    |

---

## 7.3. Tipos de evento

| Tipo                   | Descrição                       |
| ---------------------- | ------------------------------- |
| `rotina_segunda`       | Monitoramento de pautas até 12h |
| `rotina_diaria`        | Jornalzinho e checagem diária   |
| `rotina_sexta`         | Fechamento semanal              |
| `reuniao`              | Reunião interna ou externa      |
| `pauta_comissao`       | Pauta de comissão               |
| `audiencia_publica`    | Audiência pública               |
| `prazo_relatorio`      | Entrega de relatório            |
| `checagem_tramitacao`  | Revisão de movimentações        |
| `evento_institucional` | Evento do CFTA/Belli/Congresso  |
| `outro`                | Outro evento                    |

---

# 8. Biblioteca

## 8.1. Objetivo do módulo

Organizar documentos, arquivos, links, planilhas e materiais utilizados na operação.

Enquanto o sistema for estático, a biblioteca pode guardar links e metadados. Na versão futura com banco de dados, deverá permitir upload real.

---

## 8.2. Campos de item da biblioteca

| Campo               | Tipo        | Obrigatório | Descrição                         |
| ------------------- | ----------- | ----------- | --------------------------------- |
| `id`                | texto       | Sim         | Identificador único               |
| `titulo`            | texto       | Sim         | Nome do documento ou arquivo      |
| `tipo`              | lista       | Sim         | PDF, DOCX, planilha, link etc.    |
| `categoria`         | lista       | Sim         | Categoria documental              |
| `projeto_vinculado` | texto/id    | Não         | Projeto relacionado               |
| `responsavel`       | texto       | Não         | Responsável pelo cadastro         |
| `data_inclusao`     | data        | Sim         | Data de entrada                   |
| `data_documento`    | data        | Não         | Data original do documento        |
| `link`              | link        | Não         | Link externo ou interno           |
| `resumo`            | texto longo | Não         | Resumo do conteúdo                |
| `observacoes`       | texto       | Não         | Observações internas              |
| `tags`              | lista       | Não         | Palavras-chave                    |
| `arquivo_real`      | arquivo     | Futuro      | Upload real em versão com storage |

---

## 8.3. Tipos de arquivo

| Tipo     | Descrição             |
| -------- | --------------------- |
| `pdf`    | Documento PDF         |
| `docx`   | Documento Word        |
| `xlsx`   | Planilha Excel        |
| `pptx`   | Apresentação          |
| `imagem` | PNG, JPG, SVG etc.    |
| `link`   | Link externo          |
| `html`   | Página ou painel HTML |
| `texto`  | Texto simples         |
| `outro`  | Outro formato         |

---

## 8.4. Categorias da biblioteca

| Categoria             | Descrição                           |
| --------------------- | ----------------------------------- |
| `relatorio_mensal`    | Relatórios mensais                  |
| `relatorio_semanal`   | Relatórios semanais                 |
| `projeto_legislativo` | Documentos de projetos legislativos |
| `agroindustria`       | Materiais de agroindústria          |
| `comissoes`           | Materiais de comissões              |
| `pesquisas`           | Estudos, painéis e mapas            |
| `institucional_cfta`  | Documentos institucionais do CFTA   |
| `institucional_belli` | Documentos da Belli                 |
| `governor`            | Arquivos técnicos do Governor       |
| `mapas`               | Mapas, dashboards e painéis         |
| `outro`               | Outros materiais                    |

---

# 9. Relatórios

## 9.1. Objetivo do módulo

Gerar, organizar e armazenar relatórios da operação CFTA/Belli.

O módulo deve apoiar:

* prestação de contas;
* acompanhamento semanal;
* registro de atividades;
* consolidação mensal;
* análise legislativa;
* entrega institucional.

---

## 9.2. Campos de relatório

| Campo                     | Tipo         | Obrigatório | Descrição                       |
| ------------------------- | ------------ | ----------- | ------------------------------- |
| `id`                      | texto        | Sim         | Identificador único             |
| `titulo`                  | texto        | Sim         | Nome do relatório               |
| `tipo`                    | lista        | Sim         | Semanal, mensal etc.            |
| `periodo_inicio`          | data         | Não         | Início do período               |
| `periodo_fim`             | data         | Não         | Fim do período                  |
| `resumo_executivo`        | texto longo  | Não         | Síntese principal               |
| `atividades_relacionadas` | lista de ids | Não         | Atividades usadas               |
| `projetos_relacionados`   | lista de ids | Não         | Projetos citados                |
| `tramitações_relevantes`  | texto longo  | Não         | Movimentações                   |
| `bloqueios`               | texto longo  | Não         | Gargalos                        |
| `proximos_passos`         | texto longo  | Não         | Encaminhamentos                 |
| `responsavel`             | texto        | Não         | Responsável pelo relatório      |
| `status`                  | lista        | Sim         | Rascunho, revisão, enviado etc. |
| `data_criacao`            | data         | Sim         | Data de criação                 |
| `data_envio`              | data         | Não         | Data de envio                   |
| `arquivo_vinculado`       | id/link      | Não         | Documento final                 |
| `observacoes`             | texto        | Não         | Observações internas            |

---

## 9.3. Tipos de relatório

| Tipo            | Descrição                              |
| --------------- | -------------------------------------- |
| `semanal`       | Relatório semanal                      |
| `mensal`        | Relatório mensal                       |
| `tramitacao`    | Relatório de tramitação                |
| `atividades`    | Relatório de atividades da consultoria |
| `agroindustria` | Relatório temático de agroindústria    |
| `comissao`      | Relatório sobre comissão específica    |
| `semestral`     | Relatório consolidado do semestre      |
| `executivo`     | Relatório para diretoria/cliente       |
| `pesquisa`      | Relatório de pesquisa ou painel        |
| `outro`         | Outro tipo                             |

---

## 9.4. Status de relatório

| Status       | Descrição                   |
| ------------ | --------------------------- |
| `rascunho`   | Em elaboração               |
| `em_revisao` | Aguardando revisão          |
| `validado`   | Revisado e aprovado         |
| `enviado`    | Encaminhado ao destinatário |
| `arquivado`  | Encerrado                   |

---

# 10. Pesquisas

## 10.1. Objetivo do módulo

Organizar estudos, mapas, dashboards e análises estratégicas usadas pela Belli/Governor.

A aba Pesquisas deve reunir os painéis já publicados e estudos futuros, especialmente aqueles que possam fortalecer a atuação do CFTA.

---

## 10.2. Campos de pesquisa

| Campo              | Tipo        | Obrigatório | Descrição                          |
| ------------------ | ----------- | ----------- | ---------------------------------- |
| `id`               | texto       | Sim         | Identificador único                |
| `titulo`           | texto       | Sim         | Nome da pesquisa                   |
| `tema`             | lista       | Sim         | Tema principal                     |
| `status`           | lista       | Sim         | Publicada, em desenvolvimento etc. |
| `descricao`        | texto longo | Sim         | Descrição executiva                |
| `indicadores`      | lista       | Não         | Indicadores principais             |
| `link_painel`      | link        | Não         | Link para mapa/dashboard           |
| `link_relatorio`   | link        | Não         | Link para relatório associado      |
| `responsavel`      | texto       | Não         | Responsável pelo estudo            |
| `data_criacao`     | data        | Não         | Data de criação                    |
| `data_atualizacao` | data        | Não         | Última atualização                 |
| `fontes`           | lista       | Não         | Fontes utilizadas                  |
| `observacoes`      | texto       | Não         | Observações internas               |
| `tags`             | lista       | Não         | Palavras-chave                     |

---

## 10.3. Temas de pesquisa

| Tema                  | Descrição                             |
| --------------------- | ------------------------------------- |
| `fumo`                | Produção de fumo e cadeia relacionada |
| `deficit_tecnico`     | Déficit de técnicos agrícolas         |
| `agroindustria`       | Agroindústria por UF/região           |
| `tecnicos_agricolas`  | Distribuição e atuação de técnicos    |
| `produtividade_agro`  | Produtividade agropecuária            |
| `cadeias_produtivas`  | Cadeias estratégicas                  |
| `assistencia_tecnica` | ATER e cobertura técnica              |
| `fiscalizacao`        | Fiscalização profissional             |
| `mapas`               | Mapas e análises territoriais         |
| `outro`               | Outro tema                            |

---

## 10.4. Status de pesquisa

| Status               | Descrição                          |
| -------------------- | ---------------------------------- |
| `publicada`          | Já disponível                      |
| `em_desenvolvimento` | Em produção                        |
| `planejada`          | Ideia aprovada, ainda não iniciada |
| `em_revisao`         | Aguardando validação               |
| `arquivada`          | Sem prioridade atual               |

---

## 10.5. Pesquisas iniciais recomendadas

| Pesquisa                                 | Status sugerido |
| ---------------------------------------- | --------------- |
| Mapa do Fumo                             | Publicada       |
| Déficit Técnico                          | Publicada       |
| Agroindústria por UF                     | Planejada       |
| Técnicos Agrícolas por Estado            | Planejada       |
| Produtividade Agropecuária               | Planejada       |
| Assistência Técnica e Extensão Rural     | Planejada       |
| Diagnóstico de Fiscalização Profissional | Planejada       |

---

# 11. Bloqueios Governor

## 11.1. Objetivo do módulo

Registrar e acompanhar problemas técnicos ou operacionais do Governor que impactam o monitoramento legislativo.

---

## 11.2. Campos de bloqueio

| Campo              | Tipo        | Obrigatório | Descrição                        |
| ------------------ | ----------- | ----------- | -------------------------------- |
| `id`               | texto       | Sim         | Identificador único              |
| `titulo`           | texto       | Sim         | Nome do bloqueio                 |
| `descricao`        | texto longo | Sim         | Explicação do problema           |
| `modulo_afetado`   | lista       | Sim         | Parte do sistema afetada         |
| `impacto`          | lista       | Sim         | Grau de impacto                  |
| `prioridade`       | lista       | Sim         | Urgência                         |
| `responsavel`      | texto       | Não         | Responsável pela correção        |
| `status`           | lista       | Sim         | Situação atual                   |
| `data_abertura`    | data        | Sim         | Quando o bloqueio foi registrado |
| `data_solucao`     | data        | Não         | Quando foi resolvido             |
| `solucao_esperada` | texto longo | Não         | O que precisa ser feito          |
| `contorno_manual`  | texto longo | Não         | Como operar enquanto não corrige |
| `observacoes`      | texto       | Não         | Observações internas             |

---

## 11.3. Módulos afetados

| Módulo                    | Descrição                                |
| ------------------------- | ---------------------------------------- |
| `novas_proposicoes`       | Módulo de novas matérias                 |
| `filtro_casa_legislativa` | Separação Câmara/Senado/Estados          |
| `projetos_estaduais`      | Abertura e leitura de matérias estaduais |
| `notificacoes_tramitacao` | Alertas automáticos                      |
| `base_projetos`           | Base de projetos monitorados             |
| `relatorios`              | Geração de relatórios                    |
| `outro`                   | Outro módulo                             |

---

## 11.4. Impacto do bloqueio

| Impacto   | Descrição                         |
| --------- | --------------------------------- |
| `critico` | Impede operação normal            |
| `alto`    | Gera risco de perda de informação |
| `medio`   | Exige contorno manual             |
| `baixo`   | Impacto pontual                   |

---

## 11.5. Status de bloqueio

| Status        | Descrição                             |
| ------------- | ------------------------------------- |
| `aberto`      | Bloqueio registrado                   |
| `em_analise`  | Problema sendo avaliado               |
| `em_correcao` | Correção em andamento                 |
| `resolvido`   | Solucionado                           |
| `contornado`  | Não resolvido, mas com solução manual |
| `arquivado`   | Sem ação atual                        |

---

# 12. Configurações

## 12.1. Objetivo do módulo

Guardar preferências locais, exportações, backups e configurações do painel.

---

## 12.2. Campos de configuração

| Campo                | Tipo     | Descrição                         |
| -------------------- | -------- | --------------------------------- |
| `versao_sistema`     | texto    | Versão atual da Central           |
| `ultima_exportacao`  | data     | Última exportação JSON            |
| `tema_visual`        | texto    | Tema atual                        |
| `modo_debug`         | booleano | Indica modo de testes             |
| `dados_localstorage` | objeto   | Dados salvos localmente           |
| `backup_automatico`  | booleano | Futuro recurso                    |
| `usuario_local`      | texto    | Nome do operador local, se houver |

---

# 13. Futuro módulo de usuários

## 13.1. Objetivo futuro

Quando a Central migrar para banco de dados, será necessário criar login e permissões.

---

## 13.2. Campos de usuário

| Campo           | Tipo  | Obrigatório | Descrição                  |
| --------------- | ----- | ----------- | -------------------------- |
| `id`            | texto | Sim         | Identificador              |
| `nome`          | texto | Sim         | Nome completo              |
| `email`         | email | Sim         | E-mail                     |
| `perfil`        | lista | Sim         | Tipo de acesso             |
| `organizacao`   | texto | Não         | CFTA, Belli, Governor etc. |
| `status`        | lista | Sim         | Ativo ou inativo           |
| `data_criacao`  | data  | Sim         | Data de cadastro           |
| `ultimo_acesso` | data  | Não         | Último login               |

---

## 13.3. Perfis de usuário

| Perfil                  | Permissões                                  |
| ----------------------- | ------------------------------------------- |
| `administrador`         | Acesso total                                |
| `consultor_belli`       | Gestão de atividades, relatórios e projetos |
| `operador_governor`     | Gestão de dados, bloqueios e monitoramento  |
| `visualizador_cfta`     | Visualização de dashboard e relatórios      |
| `responsavel_relatorio` | Criação e revisão de relatórios             |
| `externo_limitado`      | Acesso restrito                             |

---

# 14. Relações entre módulos

## 14.1. Atividades e projetos legislativos

Uma atividade pode estar vinculada a um projeto legislativo.

Exemplo:

```text
Atividade: Atualizar tramitação do PL 4314/2016
Projeto vinculado: PL 4314/2016
```

---

## 14.2. Atividades e relatórios

Um relatório pode usar várias atividades como base.

Exemplo:

```text
Relatório semanal de 10 a 14/06
Atividades vinculadas:
- Monitorar pauta CAPADR
- Atualizar PL 5122/2023
- Revisar matérias novas da semana
```

---

## 14.3. Projetos e comissões

Um projeto legislativo pode estar vinculado a uma comissão.

Exemplo:

```text
Projeto: PL 3981/2024
Comissão atual: CCJC
```

---

## 14.4. Biblioteca e relatórios

Um relatório finalizado pode ser cadastrado na biblioteca.

Exemplo:

```text
Relatório de Maio/2026
Categoria: Relatório mensal
Módulo relacionado: Biblioteca
```

---

## 14.5. Pesquisas e projetos

Uma pesquisa pode embasar análise legislativa ou institucional.

Exemplo:

```text
Pesquisa: Déficit Técnico
Uso: fundamentar demanda por valorização e presença dos técnicos agrícolas
```

---

# 15. Chaves recomendadas para localStorage

Enquanto o sistema for estático, os dados podem ser salvos no navegador usando chaves padronizadas.

| Chave                     | Conteúdo                       |
| ------------------------- | ------------------------------ |
| `cfta_atividades`         | Lista de atividades            |
| `cfta_projetos`           | Lista de projetos legislativos |
| `cfta_biblioteca`         | Itens da biblioteca            |
| `cfta_relatorios`         | Relatórios salvos              |
| `cfta_calendario`         | Eventos do calendário          |
| `cfta_pesquisas`          | Pesquisas cadastradas          |
| `cfta_bloqueios_governor` | Bloqueios técnicos             |
| `cfta_configuracoes`      | Configurações locais           |
| `cfta_backup`             | Backup geral                   |

---

# 16. Objeto geral de backup

O backup JSON deve reunir todos os módulos.

## Estrutura recomendada

```json
{
  "versao": "2.0",
  "data_exportacao": "2026-06-16",
  "atividades": [],
  "projetos": [],
  "biblioteca": [],
  "relatorios": [],
  "calendario": [],
  "pesquisas": [],
  "bloqueios_governor": [],
  "configuracoes": {}
}
```

---

# 17. Regras gerais de validação

## 17.1. Atividades

* Toda atividade deve ter título.
* Toda atividade deve ter status.
* Toda atividade deve ter prioridade.
* Toda atividade deve ter responsável, mesmo que seja “A definir”.
* Atividades urgentes devem aparecer no Dashboard.
* Atividades bloqueadas devem aparecer no painel de bloqueios.

---

## 17.2. Projetos legislativos

* Todo projeto deve ter número, ano e casa legislativa.
* Todo projeto deve ter classificação de impacto para o CFTA.
* Todo projeto prioritário deve ter próxima ação.
* Projetos sem checagem recente devem aparecer como pendência.
* Projetos de agroindústria devem receber tag específica.

---

## 17.3. Relatórios

* Todo relatório deve ter tipo e período.
* Relatórios em rascunho não devem ser marcados como enviados.
* Relatórios enviados devem ter data de envio.
* Relatórios semanais devem puxar atividades da semana.

---

## 17.4. Biblioteca

* Todo item deve ter título e categoria.
* Links devem ser válidos.
* Documentos importantes devem ter resumo.
* Arquivos relacionados a projetos devem ter projeto vinculado.

---

# 18. Indicadores do Dashboard

O Dashboard deve calcular automaticamente:

| Indicador              | Base de cálculo                                      |
| ---------------------- | ---------------------------------------------------- |
| Total de atividades    | Quantidade de registros em atividades                |
| Atividades urgentes    | Prioridade = urgente                                 |
| Atividades bloqueadas  | Status = bloqueado                                   |
| Atividades atrasadas   | Prazo menor que hoje e status diferente de concluído |
| Relatórios pendentes   | Relatórios com status rascunho ou revisão            |
| Projetos prioritários  | Projetos com prioridade alta ou urgente              |
| Bloqueios Governor     | Bloqueios com status aberto/em análise/em correção   |
| Documentos cadastrados | Total de itens da biblioteca                         |
| Pesquisas publicadas   | Pesquisas com status publicada                       |

---

# 19. Ordem de implementação recomendada

## Etapa 1

* Padronizar atividades;
* Padronizar projetos legislativos;
* Padronizar biblioteca;
* Padronizar relatórios.

## Etapa 2

* Ajustar Dashboard para usar esses dados;
* Melhorar filtros;
* Criar exportação CSV;
* Criar backup JSON mais organizado.

## Etapa 3

* Separar HTML, CSS e JavaScript;
* Melhorar manutenção do código;
* Preparar migração futura.

## Etapa 4

* Migrar para banco de dados;
* Criar login;
* Criar upload real;
* Criar permissões;
* Criar histórico.

---

# 20. Conclusão

Esta estrutura de dados deve orientar todas as melhorias futuras da Central Operacional CFTA • Belli • Governor.

Antes de alterar visual ou migrar tecnologia, o sistema precisa manter consistência nos dados. A prioridade deve ser padronizar atividades, projetos legislativos, relatórios, biblioteca e bloqueios do Governor.

Com essa base, a Central poderá evoluir de um painel estático para uma plataforma institucional de monitoramento, gestão legislativa e relatórios estratégicos.

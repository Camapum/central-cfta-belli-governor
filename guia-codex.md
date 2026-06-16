# Guia de Uso do Codex — Central Operacional CFTA • Belli • Governor

## 1. Objetivo deste guia

Este documento orienta como usar o Codex para melhorar a Central Operacional CFTA • Belli • Governor sem quebrar a versão estável.

O Codex deve ser usado para:

* revisar código;
* organizar arquivos;
* corrigir bugs;
* melhorar funcionalidades;
* refatorar estrutura;
* criar novas abas;
* melhorar relatórios;
* melhorar biblioteca;
* melhorar projetos legislativos;
* preparar futura migração para sistema real.

A regra principal é:

```text
Nunca pedir para o Codex “melhorar tudo de uma vez”.
```

As tarefas devem ser pequenas, objetivas e testadas localmente antes de publicar.

---

# 2. Estado atual do projeto

## Versão estável

```text
v2.0
```

## Link oficial

```text
https://camapum.github.io/central-cfta-belli-governor/
```

## Estrutura atual

O sistema ainda funciona principalmente em um arquivo:

```text
index.html
```

Com documentação em:

```text
documentacao/
```

Arquivos de documentação:

```text
roadmap.md
estrutura-de-dados.md
manual-de-uso.md
backlog.md
historico-de-versoes.md
checklist-de-publicacao.md
guia-codex.md
```

---

# 3. Regras antes de usar o Codex

Antes de pedir qualquer alteração:

* [ ] fazer backup do `index.html`;
* [ ] manter cópia `index-v2-estavel.html`;
* [ ] abrir o projeto no VS Code;
* [ ] testar com Live Server;
* [ ] ler o `backlog.md`;
* [ ] consultar o `checklist-de-publicacao.md`;
* [ ] definir uma tarefa específica;
* [ ] não aceitar mudanças grandes sem revisar.

---

# 4. Como escrever bons prompts para o Codex

## Prompt ruim

```text
Melhore o site inteiro e deixe mais profissional.
```

Problema: é amplo demais e pode quebrar funcionalidades.

## Prompt bom

```text
Leia os arquivos da pasta documentacao antes de alterar o código.

Melhore apenas a aba Biblioteca, mantendo a versão 2.0 visualmente estável.

A biblioteca deve permitir cadastrar título, tipo, categoria, projeto vinculado, responsável, data, link, resumo, observações e tags.

Não altere Dashboard, Kanban, Relatórios ou Configurações.

Mantenha compatibilidade com GitHub Pages e localStorage.
```

---

# 5. Fluxo correto de trabalho

## Etapa 1 — Planejar

Escolher uma tarefa do `backlog.md`.

Exemplo:

```text
Melhorar aba Projetos CFTA.
```

## Etapa 2 — Pedir para o Codex analisar

Antes de alterar, pedir:

```text
Leia a estrutura atual do projeto e os arquivos da pasta documentacao. Antes de alterar, explique o plano de mudança.
```

## Etapa 3 — Alterar uma parte por vez

Não alterar vários módulos ao mesmo tempo.

## Etapa 4 — Testar localmente

Rodar com Live Server:

```text
http://127.0.0.1:5500/index.html
```

Testar:

* Dashboard;
* Kanban;
* Cadastro;
* Biblioteca;
* Relatórios;
* Pesquisas;
* Configurações.

## Etapa 5 — Publicar

Só publicar depois de passar no checklist.

## Etapa 6 — Registrar

Atualizar:

```text
historico-de-versoes.md
backlog.md
```

---

# 6. Prompts recomendados

## 6.1. Prompt inicial para qualquer tarefa

```text
Leia todos os arquivos da pasta documentacao antes de alterar o código.

Considere que a versão 2.0 é a versão estável da Central Operacional CFTA Belli Governor.

Não quebre funcionalidades existentes.

Mantenha compatibilidade com GitHub Pages e localStorage.

Antes de alterar, explique rapidamente:
1. o que você entendeu;
2. quais arquivos pretende modificar;
3. quais riscos existem;
4. como pretende testar.
```

---

## 6.2. Prompt para melhorar Projetos CFTA

```text
Leia documentacao/estrutura-de-dados.md e documentacao/backlog.md.

Melhore apenas a aba Projetos CFTA.

Objetivo:
transformar a aba Projetos CFTA em uma base legislativa estratégica.

A aba deve conter campos para:
- número do projeto;
- ano;
- tipo;
- casa legislativa;
- autor;
- partido/UF;
- ementa resumida;
- tema principal;
- comissão atual;
- relator;
- situação;
- impacto para o CFTA;
- prioridade;
- recomendação;
- próxima ação;
- última checagem;
- link oficial.

Funcionalidades desejadas:
- filtro por casa legislativa;
- filtro por tema;
- filtro por prioridade;
- busca textual;
- botão para copiar resumo do projeto.

Não altere as demais abas.

Mantenha o visual da versão 2.0.
Mantenha compatibilidade com GitHub Pages e localStorage.
```

---

## 6.3. Prompt para melhorar Biblioteca

```text
Leia documentacao/estrutura-de-dados.md e documentacao/manual-de-uso.md.

Melhore apenas a aba Biblioteca.

Objetivo:
organizar documentos, links, relatórios e pesquisas da operação CFTA/Belli/Governor.

Campos obrigatórios:
- título;
- tipo;
- categoria;
- projeto vinculado;
- responsável;
- data de inclusão;
- link;
- resumo;
- observações;
- tags.

Funcionalidades:
- cadastrar item;
- editar item;
- excluir item;
- buscar por texto;
- filtrar por categoria;
- filtrar por projeto;
- abrir link;
- exportar CSV.

Não implementar upload real nesta etapa.
Não alterar outras abas.
Manter localStorage e GitHub Pages.
```

---

## 6.4. Prompt para melhorar Relatórios

```text
Leia documentacao/estrutura-de-dados.md e documentacao/manual-de-uso.md.

Melhore apenas a aba Relatórios.

Objetivo:
permitir gerar relatórios operacionais com base nas atividades cadastradas.

Tipos de relatório:
- semanal;
- mensal;
- tramitação;
- atividades;
- agroindústria;
- semestral.

Funcionalidades:
- selecionar tipo de relatório;
- selecionar período;
- gerar texto estruturado;
- copiar relatório;
- baixar relatório em .txt;
- incluir atividades concluídas;
- incluir bloqueios;
- incluir próximos passos.

Não alterar layout geral da versão 2.0.
Manter compatibilidade com localStorage e GitHub Pages.
```

---

## 6.5. Prompt para melhorar Kanban

```text
Leia documentacao/estrutura-de-dados.md.

Melhore apenas o Kanban da Central.

Objetivo:
tornar o Kanban mais útil para a rotina operacional.

Melhorias:
- padronizar colunas em A fazer, Em andamento, Bloqueado, Em validação e Concluído;
- permitir editar atividade;
- permitir excluir atividade;
- permitir duplicar atividade;
- filtrar por responsável;
- filtrar por prioridade;
- filtrar por projeto;
- destacar atividades urgentes;
- destacar atividades atrasadas.

Não alterar as demais abas.
Manter identidade visual da versão 2.0.
Manter GitHub Pages e localStorage.
```

---

## 6.6. Prompt para melhorar Dashboard

```text
Leia documentacao/backlog.md e documentacao/estrutura-de-dados.md.

Melhore apenas o Dashboard.

Objetivo:
deixar o Dashboard mais executivo e operacional.

O Dashboard deve mostrar:
- atividades urgentes;
- bloqueios críticos;
- próximos prazos;
- relatórios pendentes;
- projetos prioritários;
- resumo da semana;
- últimas atualizações.

Não colocar roadmap técnico no Dashboard.
Roadmap deve ficar apenas na documentação ou em Configurações.

Manter visual institucional em verde, branco e dourado.
Manter GitHub Pages e localStorage.
```

---

## 6.7. Prompt para melhorar Pesquisas

```text
Leia documentacao/estrutura-de-dados.md.

Melhore apenas a aba Pesquisas.

Objetivo:
organizar os painéis e estudos estratégicos da Belli/Governor.

A aba deve conter cards para:
- Mapa do Fumo;
- Déficit Técnico;
- Agroindústria por UF;
- Técnicos Agrícolas por Estado;
- Produtividade agropecuária;
- Assistência Técnica e Extensão Rural;
- Diagnóstico de Fiscalização Profissional;
- Cadeias Produtivas Estratégicas.

Cada card deve ter:
- título;
- tema;
- status;
- descrição executiva;
- indicadores principais;
- link do painel;
- responsável;
- data de atualização.

Não alterar outras abas.
Manter versão 2.0 visualmente estável.
```

---

## 6.8. Prompt para separar HTML, CSS e JavaScript

```text
Leia toda a documentação do projeto.

Objetivo:
refatorar a estrutura técnica sem alterar funcionalidades ou visual.

Atualmente o projeto está concentrado em index.html.

Separe em:
- index.html;
- assets/css/style.css;
- assets/js/app.js;
- assets/js/data.js;
- assets/js/dashboard.js;
- assets/js/kanban.js;
- assets/js/reports.js;
- assets/js/library.js.

Regras:
- manter todas as abas funcionando;
- manter localStorage;
- manter compatibilidade com GitHub Pages;
- não alterar visual significativamente;
- testar caminhos dos arquivos;
- não remover nenhuma funcionalidade existente.

Antes de alterar, explique o plano.
Depois das alterações, informe quais arquivos foram criados/modificados.
```

---

# 7. Ordem recomendada para usar o Codex

## Primeiro ciclo

1. Melhorar Projetos CFTA;
2. Melhorar Biblioteca;
3. Melhorar Relatórios;
4. Melhorar Kanban;
5. Melhorar Pesquisas;
6. Melhorar Dashboard.

## Segundo ciclo

1. Separar HTML, CSS e JavaScript;
2. Organizar arquivos;
3. Melhorar estrutura do código;
4. Criar dados iniciais separados.

## Terceiro ciclo

1. Preparar migração para React/Next.js;
2. Planejar Supabase;
3. Planejar login;
4. Planejar upload real.

---

# 8. O que não pedir ao Codex por enquanto

Evitar pedidos como:

```text
Transforme tudo em React agora.
```

```text
Crie login e banco de dados de uma vez.
```

```text
Melhore tudo do jeito que achar melhor.
```

```text
Apague o código antigo e recomece.
```

```text
Substitua o visual inteiro.
```

Esses pedidos podem quebrar a versão estável e criar retrabalho.

---

# 9. Como revisar alterações do Codex

Após qualquer alteração, verificar:

* [ ] o site abre no Live Server;
* [ ] não há erro no console;
* [ ] o Dashboard aparece;
* [ ] o Kanban funciona;
* [ ] os cadastros salvam;
* [ ] os filtros funcionam;
* [ ] a Biblioteca abre;
* [ ] os Relatórios abrem;
* [ ] Pesquisas abre;
* [ ] Configurações abre;
* [ ] o visual não piorou;
* [ ] não foram removidas funções importantes.

---

# 10. Regra de publicação

Só publicar no GitHub Pages depois de passar pelo:

```text
documentacao/checklist-de-publicacao.md
```

E registrar a alteração em:

```text
documentacao/historico-de-versoes.md
```

---

# 11. Conclusão

O Codex deve ser usado como apoio técnico para evoluir a Central Operacional com segurança.

A documentação da pasta `documentacao` deve orientar todas as alterações.

A prioridade é manter a versão 2.0 estável, melhorar funcionalidades aos poucos e só depois fazer refatorações maiores.

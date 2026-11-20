# Estrutura de dados do CORA

Os dados ficam em coleções de documentos JSON. Todos os horários são gravados em ISO 8601 (UTC) e exibidos no horário de Brasília (`America/Sao_Paulo`). Datas de calendário (`dataBR`, `nascimento`, `validade`) usam `AAAA-MM-DD` no horário de Brasília.

## `membros/{matricula}`
Alunos e colaboradores. O id do documento é a matrícula (ou o código temporário).

| Campo | Tipo | Descrição |
|---|---|---|
| `matricula` | texto | Matrícula institucional ou código `TMP-0000` |
| `nome` | texto | Nome completo |
| `tipo` | texto | `aluno`, `professor`, `rt`, `recepcao` ou `outro` |
| `periodo` | texto | Período/turma (aluno) ou setor (colaborador) |
| `ativo` | booleano | Cadastro ativo |
| `temporario` | booleano | `true` para código temporário |
| `validade` | data | Validade do código temporário |
| `convertidoDe` | texto | Código temporário de origem, após conversão |
| `criadoEm` | data e hora | |

## `pacientes/{id}`

| Campo | Tipo | Descrição |
|---|---|---|
| `nome` | texto | Nome completo |
| `prontuario` | texto | Número do prontuário (único) |
| `nascimento` | data | |
| `cpf` | texto | Validado pelos dígitos verificadores |
| `telefone` | texto | |
| `alergias` | texto | Alergias e condições sistêmicas (destaque no check-in) |
| `obs` | texto | Observações |
| `criadoEm`, `criadoPor` | | Data e matrícula de quem cadastrou |

## `atendimentos/{id}`
Um documento por visita do paciente.

| Campo | Tipo | Descrição |
|---|---|---|
| `pacienteId` | texto | Paciente |
| `dataBR` | data | Dia do check-in |
| `etapa` | texto | `recepcao`, `clinica`, `procedimento`, `provisoria` ou `alta` |
| `eventos` | lista | `{etapa, ts, por, nota}`: uma entrada por etapa, com horário e matrícula de quem registrou |
| `alunoMatricula` | texto | Aluno operador |
| `auxiliarMatricula` | texto | Aluno auxiliar (opcional) |
| `circulanteMatricula` | texto | Aluno circulante (opcional) |
| `professorMatricula` | texto | Professor supervisor |
| `procedimentos` | lista de textos | Procedimentos realizados |
| `dentes` | texto | Dentes/região (notação FDI) |
| `descricao` | texto | Descrição do procedimento |
| `retornoPrevisto` | data | Na liberação provisória |
| `criadoEm` | data e hora | |

## `config/*`

| Documento | Conteúdo |
|---|---|
| `config/procedimentos` | `{lista: [texto]}`: lista de procedimentos personalizada |
| `config/semestres` | `{lista: [{nome, inicio, fim}]}`: semestres letivos |
| `config/instituicao` | `{nome}`: nome exibido abaixo de "CORA" |

## `vinculos/{idDaConta}`
Liga a conta de quem usa o sistema a uma matrícula: `{matricula, em}`. Cada matrícula pode estar ligada a uma única conta; administradores podem liberar o vínculo.

## Regras de acesso

| Caminho | Leitura | Escrita |
|---|---|---|
| tudo | Colaborador ou acima | Colaborador ou acima |
| `membros` | Colaborador ou acima | Editor (administradores) |
| `pacientes` | Colaborador ou acima | Editor (administradores) |
| `config` | Colaborador ou acima | Editor (administradores) |
| `vinculos` | Colaborador ou acima | Editor; cada pessoa grava o próprio vínculo |

Quem tem acesso apenas de visualização não lê nenhum dado.

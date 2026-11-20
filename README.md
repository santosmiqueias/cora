# CORA

**Controle Odontológico de Registros e Atendimentos**

Sistema web para clínica-escola de odontologia. Acompanha o percurso de cada paciente, do check-in na recepção até a alta, com todos os horários registrados no horário de Brasília.

## Funcionalidades

### Check-in
Quadro do dia com o percurso do paciente em cinco etapas:

1. **Check-in na recepção:** só a recepção registra.
2. **Entrada na clínica:** define a equipe do atendimento (operador obrigatório; auxiliar e circulante opcionais, para trio, dupla ou atendimento solo).
3. **Procedimento finalizado:** procedimentos realizados, dentes/região (notação FDI), professor supervisor e descrição obrigatória.
4. **Liberação provisória:** o paciente retorna outro dia, com data prevista de retorno.
5. **Alta:** liberação final, tratamento concluído.

O tempo de espera aparece ao vivo e fica vermelho depois de 30 minutos. Alergias e condições do paciente aparecem em destaque para a equipe.

### Identificação
- **Alunos:** cadastro por matrícula institucional e nome completo. Quem ainda não tem matrícula recebe um **código temporário** (ex.: `TMP-4821`) com validade. O código pode ser convertido depois em matrícula definitiva, mantendo todo o histórico.
- **Colaboradores:** professores, responsável técnico, recepção e outros.
- **Pacientes:** cadastro feito só pela recepção. O paciente não fica ligado a um aluno fixo.

### Progresso
- **Por paciente:** histórico completo de atendimentos, etapas e descrições.
- **Por aluno:** produção no período (como operador, auxiliar e circulante; pacientes, procedimentos, altas, tempo médio em clínica).
- **Todos os registros:** linha do tempo geral com filtro por dia.

### Métricas
Visível só para professores, responsável técnico e recepção. Períodos: dia, semana, mês, semestre letivo (datas configuráveis) e ano.
- Pacientes atendidos e check-ins
- Tempo médio de espera (recepção → entrada na clínica)
- Tempo médio em clínica
- Procedimentos mais realizados
- Altas e liberações provisórias
- Atendimentos por aluno

### Configurações
- Lista de procedimentos editável, com lista padrão restaurável.
- Nome da clínica/instituição exibido abaixo de "CORA".

## Perfis de acesso

| Perfil | O que pode fazer |
|---|---|
| Recepção | Administrador. Cadastra pacientes e faz o check-in de chegada. |
| Professor / Responsável técnico | Administradores. Cadastram membros, veem Progresso e Métricas, corrigem registros. |
| Aluno | Vê apenas a aba Check-in: entrada na clínica, procedimento, liberação provisória e alta dos atendimentos de que participa. |

## Como rodar

O sistema é uma única página: abra o `index.html` em qualquer navegador.

Aberto diretamente, ele roda em **modo local**: os dados ficam salvos só no navegador de quem abriu. Serve para testar e demonstrar.

A versão em uso pela equipe roda hospedada no claude.ai, que oferece o banco de dados compartilhado, o login e as regras de acesso. Para rodar de forma independente, em servidor próprio e com login institucional, é preciso trocar a camada de dados (`local` / `remote` no início do script) por um serviço como o Supabase. A estrutura de dados está em [`docs/estrutura-de-dados.md`](docs/estrutura-de-dados.md).

## Logos

Cinco propostas de logo em `logos/`, nas cores azul, amarelo e vermelho:

| Arquivo | Conceito |
|---|---|
| `1-c-de-cuidado.svg` | A letra C envolve um dente |
| `2-coracao.svg` | Dente com coroa em forma de coração ("CORA", de coração) |
| `3-percurso.svg` | Anel de cinco segmentos, um por etapa do check-in |
| `4-trio.svg` | Coroa formada por três cúspides: operador, auxiliar e circulante |
| `5-prontuario.svg` | Prancheta com prendedor em forma de dente |

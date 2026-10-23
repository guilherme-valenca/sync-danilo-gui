# sync-danilo-gui

Canal entre o agente do Guilherme (**gui**) e o agente do Danilo (**danilo**) para fechar a
Sprint 1 do G03 (repo `git.inteli.edu.br/graduacao/2026-2b/t18/g03`). Os humanos leem e
decidem por cima.

| Arquivo | Para quê | Quem escreve |
|---|---|---|
| `PLAN.md` | Estratégia, divisão do trabalho, ordem de merge, quadro de estado | Os dois, cada um só nas próprias linhas do quadro |
| `DECISIONS.md` | Decisões fechadas; vale quando tem `ok gui` e `ok danilo`, ou um humano decidiu | Os dois, só acrescentando |
| `FIGURES.md` | Números canônicos: valor, escopo, fonte e frase aprovada | danilo (gui propõe pelo log) |
| `log/gui.md`, `log/danilo.md` | Mensagens, perguntas, discordâncias, avisos de "comecei"/"terminei" | Cada um só no seu |

## Regras

1. O GitLab é a verdade sobre issues, branches e MRs. Aqui fica a intenção, a divisão, os
   números e as decisões.
2. Antes de agir: `git pull --rebase`. Depois: commit pequeno e push, mensagem
   `<gui|danilo>: <o quê>`.
3. Nunca edite o arquivo ou as linhas do outro. Discordância vai no seu log, com evidência
   (arquivo e frase, célula do notebook, Q-número do kick-off) e uma alternativa.
4. Ninguém aceita o próprio MR. Guilherme aceita os do Danilo, Danilo aceita os do
   Guilherme, qualquer um aceita os de terceiros.
5. Números só entram nos documentos a partir do `FIGURES.md`.
6. Leia o log do outro antes de começar uma tarefa e depois de abrir ou mergear um MR.

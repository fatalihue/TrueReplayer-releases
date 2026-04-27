<p align="right">
  <sub><a href="README.md">English</a> &nbsp;·&nbsp; <b>Português (BR)</b></sub>
</p>

<p align="center">
  <img src="TrueReplayer.ico" width="84" alt="TrueReplayer" />
</p>

<h1 align="center">TrueReplayer</h1>

<p align="center">
  <b>Gravador e reprodutor de macros para Windows.</b><br/>
  Grave cliques de mouse, teclado, scroll e ações no navegador — depois reproduza com precisão.
</p>

<p align="center">
  <a href="https://github.com/fatalihue/TrueReplayer-releases/releases/latest">
    <img src="https://img.shields.io/github/v/release/fatalihue/TrueReplayer-releases?style=flat-square&color=60CDFF&label=release" alt="Última versão" />
  </a>
  <img src="https://img.shields.io/badge/windows-10%20%2F%2011-0078D4?style=flat-square" alt="Windows 10/11" />
  <img src="https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square" alt=".NET 8" />
  <img src="https://img.shields.io/badge/arch-x64-6bcb77?style=flat-square" alt="x64" />
</p>

<p align="center">
  <img src="Image%20App/Main%20Window.png" alt="Janela principal do TrueReplayer" width="900" />
</p>

---

## Download

<a href="https://github.com/fatalihue/TrueReplayer-releases/releases/latest">
  <img src="https://img.shields.io/badge/Baixar-%C3%9Altima%20vers%C3%A3o-60CDFF?style=for-the-badge&logo=windows" alt="Baixar" />
</a>

| Pacote | Quando usar |
|---|---|
| `TrueReplayer-win-Setup.exe` | Instala o app e ativa **atualizações automáticas** (recomendado) |
| `TrueReplayer-win-Portable.zip` | Extrai e roda — sem instalar, sem auto-update |
| `TrueReplayer-ChromeExtension-1.2.0.zip` | Habilita as ações de automação no navegador (carregar descompactada em `chrome://extensions`) |

> **Requer** Windows 10 (1809+) ou Windows 11 — x64

---

## Destaques

- 🎯 **Replay preciso** com suporte a Raw Input — funciona em jogos como Roblox
- 🪟 **Ciente da janela** — trava tamanho, posição e foco numa janela alvo antes do replay
- 🔗 **Profile chaining** — chama outros profiles inline com cycle detection e repeat count
- ⚡ **Trigger Modes** — OnPress, OnRelease, WhilePressed, Toggle para o comportamento da hotkey
- 🌐 **Automação de navegador** — clica, digita e navega usando seletores CSS (extensão Chrome)
- ⌨️ **Hotkeys e hotstrings** para disparar qualquer profile de qualquer lugar
- 📁 **Profiles e pastas** com target de janela herdado
- 🎨 **UI Fluent escura** com 23 temas pré-definidos e cores totalmente customizáveis

---

## Gravação e Replay

- **Mouse** — cliques esquerdo / direito / meio, scroll, arrastar (press e release capturados separadamente)
- **Teclado** — todas as teclas, modificadores, F1–F12, teclado numérico e símbolos
- **Delays** — captura o tempo real ou usa delay fixo; opcional **delay aleatório (jitter)**
- **Modo de inserção** — clique numa linha para gravar novas ações a partir daquela posição
- **Loops** — número de repetições (ou infinito) com delay opcional entre iterações
- **Feedback ao vivo** — a ação atual fica destacada; barra de status mostra progresso e tempo decorrido
- **Modo Clicker** — autoclicker com seletor de botão (esquerdo / direito / meio)

## Tabela de Ações

- **Edição inline** — duplo clique em qualquer célula para editar delay, coordenadas, tecla ou notas
- **Painel lateral** — duplo clique numa linha abre um editor detalhado
- **Arrastar e soltar** — reordena linhas individuais ou múltiplas pelas alças de grip
- **Seleção múltipla** — `Ctrl`+clique, `Shift`+clique ou `Ctrl`+A
- **Operações em lote** — atualiza delay, coordenadas ou notas em todas as linhas selecionadas
- **Skip** — exclui ações selecionadas do replay temporariamente sem deletar; linhas skipped ficam discretas e o estado é salvo junto com o profile
- **Select Similar** — seleciona todas as ações do mesmo tipo com um clique
- **Visibilidade de colunas** — mostra/esconde colunas pela toolbar
- **Copy & Paste entre profiles** — transfere ações entre quaisquer dois profiles
- **Undo / Redo** — histórico completo com `Ctrl+Z` / `Ctrl+Y`

## Window Target

Amarra um profile a uma janela específica para um replay confiável e independente de estado.

<p align="center">
  <img src="Image%20App/Target%20Configuration.png" alt="Dialog de Target Configuration" width="780" />
</p>

- **Click-to-detect** — clique em qualquer janela para capturar processo e título
- **Modos de match** — `Contains` ou regex no título da janela
- **Relative Coordinates** — grava cliques relativos à janela, replay funciona mesmo se ela mudar de posição
- **Lock Size** — salva largura/altura na gravação e restaura antes do replay
- **Lock Position** — salva X/Y e restaura junto com o tamanho
- **Bring to Focus** — traz a janela alvo para frente antes do replay, preservando estado maximizado/fullscreen
- **Update Window Size & Position** — recaptura a geometria sem precisar regravar
- **Convert Coordinates** — converte em lote entre coordenadas absolutas e relativas à janela

## Profiles e Pastas

- **Arquivos JSON** — ficam em `Documentos\TrueReplayer\Profiles`
- **Pastas** — agrupa profiles visualmente com cores; colapsa ou desabilita pasta inteira
- **Configuração herdada** — pastas podem definir target, relative coords e bring-to-focus — todos os profiles dentro herdam automaticamente
- **Hotkeys** — atalho de teclado para disparar um profile instantaneamente
- **Hotstrings** — digite uma sequência (ex: `/oi`) para executar um profile (modo instantâneo ou com terminador)
- **Trigger Modes** — escolhe como a hotkey se comporta (veja abaixo)
- **Import / Export** — compartilhe profiles como arquivos `.trprofile`, preservando organização em pastas e imagens
- **Busca** — filtra profiles pelo nome em tempo real
- **Proteção contra perda** — avisa antes de trocar ou fechar com alterações não salvas

## Trigger Modes

Cada profile escolhe como a hotkey dispara o macro.

<p align="center">
  <img src="Image%20App/Triggers.png" alt="Trigger Modes" width="780" />
</p>

| Modo | Comportamento |
|---|---|
| **On Press** | Dispara uma vez quando a hotkey é pressionada (padrão) |
| **On Release** | Dispara uma vez quando a hotkey é solta — o down event é absorvido |
| **While Pressed** | Segura a hotkey para repetir o replay em loop infinito; soltar cancela |
| **Toggle** | Primeiro toque inicia o replay, segundo toque para |

- Hotkeys combinadas (ex: `Alt+Q`) funcionam em todos os modos
- A ordem de soltar os modificadores não importa para `On Release` (`Alt↓ Q↓ Q↑ Alt↑` e `Alt↓ Q↓ Alt↑ Q↑` ambos disparam)
- Proteção contra auto-repeat impede que o repeat do teclado do SO dispare múltiplos `On Press`

## Profile Chaining

Reuso de profiles como blocos de construção. A nova ação **Run Profile** invoca outro profile inline em qualquer ponto do macro.

<p align="center">
  <img src="Image%20App/Run%20Profile.png" alt="Dialog de Run Profile" width="780" />
</p>

- **Repeat count** — chama o sub-profile de 1 a 999 vezes seguidas por ação
- **Cycle detection** — `A → B → A` é bloqueado em runtime com entrada no log diagnóstico
- **Profundidade máxima** de 5 evita recursão profunda acidental
- **Contexto auto-contido** — sub-profile usa seu próprio window target, lock position e relative-coordinates se tiver; senão herda do caller
- **Restore do caller** — após o sub-profile retornar, a janela do caller é re-focada para o resto do macro pai rodar no target certo
- **Cancelamento propagado** — Stop encerra a cadeia inteira instantaneamente
- **Status ao vivo** — barra de status mostra `Running A → B → C` enquanto sub-profile executa

## Edit Text

Insere blocos de texto como se digitasse, com conteúdo dinâmico e um transformador visual de clipboard.

<p align="center">
  <img src="Image%20App/Edit%20Text.png" alt="Dialog de Edit Text" width="780" />
</p>

- **Seletor de emoji** — busca e insere qualquer emoji
- **Variáveis dinâmicas** — `{clipboard}`, `{date}`, `{time}`, `{datetime}`
- **Teclas especiais** — `{enter}`, `{tab}`, `{backspace}`, setas de navegação, sufixo de repetição `:N`
- **Snippets** — salva e reaproveita blocos de texto frequentes
- **Syntax highlighting** — reconhecimento de tokens para variáveis conhecidas, incluindo modificadores de clipboard encadeados

### Clipboard Transform

Construa tokens complexos de clipboard visualmente — sem precisar memorizar sintaxe.

<p align="center">
  <img src="Image%20App/Clipboard.png" alt="Popover de Clipboard Transform" width="420" />
</p>

| Modificador | O que faz |
|---|---|
| **Trim** | Remove espaços nas pontas |
| **UPPERCASE / lowercase** | Força o case |
| **Line #** | Extrai uma linha específica (1-indexada) |
| **Word #** | Extrai uma palavra específica |
| **First N / Last N chars** | Pega N caracteres do início ou do fim |

- Modificadores são encadeados em ordem (`{clipboard:trim:line:1:first:8}` etc.)
- Preview ao vivo mostra o conteúdo real do clipboard com todos os transforms aplicados
- Tokens ficam destacados no editor e sobrevivem a Edit / Save sem alteração

## Automação de Navegador

Controla navegadores baseados em Chrome com a extensão do TrueReplayer. Usa seletores CSS em vez de coordenadas de tela (que quebram facilmente).

| Ação | O que faz |
|---|---|
| **Browser Click / Right Click** | Clica num elemento por seletor CSS ou texto visível |
| **Browser Input Text** | Digita num input, com placeholders `{clipboard}` / `{date}` / `{time}` / `{datetime}` |
| **Browser Wait** | Espera um elemento aparecer antes de prosseguir |
| **Browser Navigate** | Abre uma URL na aba atual ou em nova aba |

- **Pick Element visual** — clique em qualquer elemento da página para capturar um seletor CSS robusto
- **Text Match** — casa por texto visível (ex: `Enviar`) como alternativa ao seletor
- **Detecção automática de inputs** — clicar num campo de input durante a gravação cria automaticamente uma ação Input Text
- **Reconexão confiável** — keep-alive baseado em alarms, reconecta mesmo se o Chrome ficou ocioso

> 📘 Guia de configuração: veja [`docs/extension-setup/`](docs/extension-setup/)

## Aparência

Personalize a interface com 23 temas ou cores totalmente customizadas.

<p align="center">
  <img src="Image%20App/Themes.png" alt="Theme Editor" width="780" />
</p>

- **Temas organizados por matiz do accent:**
  - *Neutro* — Carbon, Slate
  - *Pink/Rose* — Rose, Sakura
  - *Laranja/Amarelo* — Copper, Amber, Gruvbox Dark
  - *Verde* — Emerald, Monokai, Neon
  - *Cyan/Azul* — Ocean, Nord, Midnight, One Dark Pro, Night Flat *(padrão)*, Tokyo Night, GitHub Dark, GitHub Default, Better Solarized
  - *Roxo/Violeta/Mauve* — Amethyst, Dracula, Catppuccin Mocha, Rosé Pine
- **Cores customizadas** — accent, semânticas (vermelho de gravação, verde de replay), cada pill por tipo de ação (mouse, key, scroll, send-text, wait-image, browser, run-profile)
- **Fonte monoespaçada** — Consolas, Cascadia Mono, Cascadia Code, Courier New, Lucida Console
- **Layout** — tamanho de fonte, raio das bordas, altura da linha, zoom
- **Import / Export** de temas como JSON
- **Preview ao vivo** — toda mudança é aplicada instantaneamente em toda a UI

## Command Palette

Pressione `Ctrl+K` para busca fuzzy em comandos, profiles e configurações — tudo acessível sem o mouse.

## Configurações

| Seção | Opções |
|---|---|
| **Execution** | Delay fixo, número de loops, intervalo entre loops, delay aleatório (jitter), botão do clicker |
| **Recording** | Liga/desliga cliques de mouse, scroll, teclado, profile keys, browser actions |
| **Hotkeys** | Gravação, replay, toggle de profile keys, bring-to-foreground |
| **Window** | Sempre no topo, system tray, iniciar com o Windows, iniciar minimizado, executar como administrador |
| **Updates** | Verificação automática ao abrir, verificação manual |

## Qualidade de Vida

- **Auto-update** com preview do changelog — você vê o que mudou antes de baixar; nada instala sem confirmação
- **Recuperação de crash do WebView2** — estratégia escalonada (Reload → Navigate → Restart) mantém a UI viva mesmo em falhas raras do WebView2
- **Logs diagnósticos** — sessão registrada em arquivo em `%LOCALAPPDATA%\TrueReplayer\Logs\` com rotação; acesso rápido pelo menu da bandeja
- **Atalho DevTools** — abre DevTools do WebView2 pela bandeja para inspeção
- **Multi-monitor** — coordenadas funcionam em qualquer display
- **System tray** — minimiza pra bandeja; hotkey **Bring to Foreground** restaura da bandeja
- **Auto-recovery** — se a UI travar, o app se recarrega em até 5 segundos
- **Escape fecha menus** — menus de contexto e dropdowns fecham com `Esc`
- **Notificações toast** — mensagens de sucesso / erro / info empilháveis
- **Proteção de alterações** — nunca perca trabalho por fechar sem querer
- **Verificação do WebView2** — avisa e redireciona para instalação se faltar

---

## Hotkeys Padrão

| Ação | Tecla |
|---|---|
| Iniciar / Parar Gravação | `Ctrl+PageUp` |
| Iniciar / Parar Replay | `Ctrl+PageDown` |
| Toggle Profile Keys | `Pause` |
| Trazer pro Foreground | `Ctrl+Insert` |
| Command Palette | `Ctrl+K` |
| Undo / Redo | `Ctrl+Z` / `Ctrl+Y` |

Todas as hotkeys podem ser remapeadas em **Settings → Hotkeys**.

---

## Requisitos

- Windows 10 versão 1809 ou superior / Windows 11 — x64 apenas
- [Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) (já vem no Windows 11; o app avisa no Windows 10 se faltar)
- ~500 MB em disco (runtime .NET 8 incluso — não precisa instalar)

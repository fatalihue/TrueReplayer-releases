<div align="center">

<img src="Assets/Square150x150Logo.png" width="104" alt="TrueReplayer logo" />

# TrueReplayer

**Grave o que você faz. Reproduza quando quiser — sob demanda ou com um atalho.**

Gravador de macros e automação para **Windows**: cliques, teclas e rolagem gravados e reproduzidos com precisão — com esperas, condições, loops, injeção de texto, auto-clicker e entrada que jogos de verdade aceitam.

[![Latest release](https://img.shields.io/github/v/release/fatalihue/TrueReplayer-releases?style=flat-square&color=60CDFF&label=download)](https://github.com/fatalihue/TrueReplayer-releases/releases/latest)
[![Windows 10/11](https://img.shields.io/badge/Windows-10%20%2F%2011%20(x64)-0078D4?style=flat-square&logo=windows)](https://github.com/fatalihue/TrueReplayer-releases/releases/latest)
[![License: MIT](https://img.shields.io/badge/license-MIT-9b8cff?style=flat-square)](LICENSE)

### ✨ **[Manual completo — ilustrado, em 15 partes →](https://fatalihue.github.io/TrueReplayer-releases/manual.html)**

<sub>Do primeiro clique gravado à automação que roda sozinha: exemplos passo a passo, diagramas e a solução de problemas.</sub>

</div>

<p align="center">
  <img src="docs/img/main.png" width="860" alt="Janela principal do TrueReplayer — a lista de ações de um perfil, com o painel de perfis à esquerda e as configurações à direita" />
</p>

---

## O que ele faz

Grava sua entrada real e reproduz exatamente — quantas vezes você quiser, inclusive com outro aplicativo em foco, por **hotkey** ou **hotstring**. E cada macro pode ir além da gravação: **esperar** uma imagem ou cor aparecer, **decidir** com blocos If/Else, **repetir** com While e For Each Data Row, **digitar** texto com tokens (`{clipboard}`, `{date}`, variáveis, prompts), preencher formulários a partir de uma **tabela de dados**, controlar o **Chrome por seletor** e disparar sozinha por **agendamento ou condição**.

Tudo organizado em **perfis** (com pastas, ícones e cores) que viajam por export/import, um **auto-clicker** dedicado com Game mode para jogos como o Roblox, **37 temas** com editor completo — e atualização automática em segundo plano.

Cada um desses assuntos é uma parte do **[manual web](https://fatalihue.github.io/TrueReplayer-releases/manual.html)**, com telas e receitas prontas.

---

## Instalar

1. Baixe o **`TrueReplayer-win-Setup.exe`** na **[página de Releases](https://github.com/fatalihue/TrueReplayer-releases/releases/latest)**.
2. Execute — instala em segundos e passa a se **atualizar sozinho** (deltas de poucos MB).

> **Requisitos:** Windows 10 ou 11 (64 bits). A interface usa o [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/) — já vem no Windows moderno; se faltar, o app se oferece para instalar.

## Primeiros 60 segundos

1. **Grave** — `Ctrl+PageUp`, faça suas ações, `Ctrl+PageUp` de novo.
2. **Reproduza** — `Ctrl+PageDown`.
3. **Salve** e **atribua um atalho** — botão direito no perfil → *Assign hotkey*.

O resto — condições, loops, tokens, data loop, clicker — está no **[manual](https://fatalihue.github.io/TrueReplayer-releases/manual.html)**, na ordem em que você vai precisar.

---

## Construído com

**WinUI 3 (.NET 8) + WebView2** no host · **React + TypeScript** na interface · `SendInput` e hooks nativos no motor · atualizações via [Velopack](https://velopack.io). Código-fonte em [`fatalihue/truereplayer`](https://github.com/fatalihue/truereplayer).

## Licença

[MIT](LICENSE) © fatalihue

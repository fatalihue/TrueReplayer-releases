<div align="center">

# TrueReplayer — Guia do Usuário

[← Voltar ao README](../README.md)

</div>

Referência completa do app. Primeira vez aqui? Faça o [Início rápido](../README.md#início-rápido) e volte.

## Conteúdo

- [Conceitos básicos](#conceitos-básicos)
- [Comece por aqui — 14 receitas](#comece-por-aqui--14-receitas)
- [Recording](#recording)
- [Reprodução e configurações de execução](#reprodução-e-configurações-de-execução)
- [A grade de ações](#a-grade-de-ações)
- [Referência de ações](#referência-de-ações)
- [Blocos condicionais (If / Else / EndIf)](#blocos-condicionais-if--else--endif)
- [Assert — exigir que algo seja verdade](#assert--exigir-que-algo-seja-verdade)
- [Perfis e pastas](#perfis-e-pastas)
- [Hotkeys e hotstrings](#hotkeys-e-hotstrings)
- [Automação (disparo sem hotkey)](#automação-disparo-sem-hotkey)
- [Remaps de tecla](#remaps-de-tecla)
- [Alvo de janela e coordenadas relativas](#alvo-de-janela-e-coordenadas-relativas)
- [Automação multi-janela (Activate Window)](#automação-multi-janela-activate-window)
- [Clicker mode (auto-clicker)](#clicker-mode-auto-clicker)
- [Game mode](#game-mode)
- [Send Text](#send-text)
- [Transformações de texto](#transformações-de-texto)
- [Variáveis, slots e prompts](#variáveis-slots-e-prompts)
- [Data Loop](#data-loop)
- [Automação de navegador](#automação-de-navegador)
- [Temas e aparência](#temas-e-aparência)
- [Referência de configurações](#referência-de-configurações)
- [Onde seus dados ficam](#onde-seus-dados-ficam)
- [Solução de problemas](#solução-de-problemas)

---

## Conceitos básicos

| Termo | O que é |
| --- | --- |
| **Perfil** | Uma macro: lista de ações + suas configurações. Um arquivo `.json`. |
| **Ação** | Um passo (um clique, uma tecla, um `If`…). Uma linha na grade. |
| **Pasta** | Grupo colorido de perfis. Um perfil fica em no máximo uma. |
| **Macro / Clicker** | *Macro* grava e reproduz listas de ações; *Clicker* é auto-clicker. Alterne com **`ScrollLock`**. |

---

## Comece por aqui — 14 receitas

Da mais fácil para a mais difícil. Faça duas ou três e você já sabe usar o app.

A maioria das macros úteis tem **uma ou duas ações**. Não ache que precisa gravar algo longo.

**1. Uma resposta pronta em qualquer lugar**
Barra → **Send Text** → escreva a mensagem → clique no chip **Enter** (isso envia) → `Ctrl+Enter` → **Save**.
Botão direito no perfil → **Assign hotstring…** → `.cp`.
Agora digitar `.cp` em qualquer chat solta a resposta inteira.

**2. Use o que você copiou**
No **Send Text**, ponha `{clipboard}` onde entra o valor copiado. Precisa só de um pedaço? `{clipboard:trim}`, `{clipboard:line:3}`, `{clipboard:words:2-4}` — veja [Transformações de texto](#transformações-de-texto).
Seu clipboard real é restaurado depois.

**3. Carimbe a hora e feche o chamado**
**Send Text** → `Finalizado em {datetime}` + `{enter}`. Depois **Send Keystroke** → `Ctrl+Alt+R`.
Duas ações, um toque de tecla.

**4. Pergunte um valor na hora**
`{input:Número do pedido}` abre uma caixa. `{input:Prioridade|menu:Baixa,Média,Alta}` abre uma lista.
Pergunta **uma vez por execução** — repetir o mesmo rótulo reusa a resposta.

**5. Funcionar só em um app**
Botão direito no perfil → **Window target…** → **Detect Window** → clique na janela → **Test front window** → ligue **Relative Coordinates** → **Set Target**.
Sem isso, mover a janela 20 px erra todos os cliques.

**6. Espere a tela, não chute**
Barra → **Wait for Image** → recorte o botão → **Test match** → confiança em **85%**.
Nunca 100%: uma tela viva nunca fica idêntica pixel a pixel, e a macro nunca acha.

**7. Clique opcional, só se aparecer**
Barra → **Conditional** → **Pixel Color Match** → escolha um ponto da cor do botão → na linha **If**, **Wait for condition** = `5000` → ponha o clique entre **If** e **EndIf**.

**8. Guarde um valor entre passos**
Barra → **Set Variable** → **Name** `cliente`, **Value** `{clipboard:trim}`. Depois use `{var:cliente}`.
Variáveis somem no fim de cada execução.

**9. Junte vários valores e cole depois**
Selecione um texto → `Win+Ctrl+C`. Repita: cai em `{clip:1}`, `{clip:2}`, `{clip:3}`…
Os slots sobrevivem entre execuções.

**10. Um item da lista por toque**
Copie a lista (`Ctrl+C`, de qualquer lugar) e escreva `{clipboard:next}` no **Send Text**.
Cada toque cola a próxima linha. Copiar outra coisa recomeça sozinho.

**11. Troque 20 passos repetidos por um loop**
Monte a macro para **um** item → **Data Loop** → cole a tabela → troque os valores fixos por `{row:item}` → ligue **Loop over data** → **On row error** = **Skip row**.
87 ações viram 5 ações e uma tabela.

**12. Reaproveite um final em várias macros**
Ponha os passos comuns num perfil `Confirmar`. Nas outras: barra → **Run Profile** → `Confirmar`.
Conserte num lugar, melhore em vinte.

**13. Clique num site pelo nome**
Instale a [extensão do Chrome](#automação-de-navegador) → barra → **Browser** → **Browser Click** → prefira o **texto** visível (`text=Enviar`).
Continua funcionando quando o layout muda.

**14. Rode sem apertar nada**
Settings → **App** → **Automation** → **Manage ›** → **+ Add automation** → escolha o gatilho → **Save** → **ligue a chave Armed**.
Salvar não é armar. Essa chave é a que todo mundo esquece.

---

## Recording

1. Tenha um perfil ativo.
2. **`Ctrl+PageUp`** (ou botão **Recording**) para começar.
3. Faça as ações.
4. **`Ctrl+PageUp`** de novo para parar.

**Onde os passos entram:** com linhas **selecionadas**, insere **antes** da primeira; **sem seleção**, acrescenta no **fim**.

**Filtros** (Settings → Profile → Recording) — todos ligados por padrão:

| Opção | Efeito |
| --- | --- |
| **Mouse Clicks** | Cliques esquerdo/direito/meio e duplos. |
| **Mouse Scroll** | Roda do mouse. |
| **Keyboard** | Teclas e modificadores. |
| **Combined Actions** | **On** → `Ctrl+C` vira uma linha. **Off** → linhas `KeyDown`/`KeyUp` separadas, necessário para arrastar ou segurar tecla. |

---

## Reprodução e configurações de execução

**`Ctrl+PageDown`** (ou **Replay**) executa; de novo (ou **Stop**) interrompe na hora, soltando o que estiver pressionado.

A reprodução agenda cada ação contra um **prazo**, não encadeia esperas: se atrasar, ressincroniza em vez de disparar uma salva de ações. Depois de ações que esperam por natureza (**WaitImage**, **WaitPixelColor**, **Pause**, **Run Profile**, **Hold Key**, ações de navegador, `If` com espera) o relógio também ressincroniza — um delay usado como acomodação nunca é comprimido.

| Configuração | O que faz | Padrão |
| --- | --- | --- |
| **Delay** | Atraso fixo antes de cada ação, contado do **início** da anterior (ação de 30 ms + delay 100 ms → a próxima começa em 100 ms, não 130). | 100 ms |
| **Loops** | Repetições da macro inteira, 1 a 999. **Pertence ao perfil.** | 1 |
| **Interval** | Pausa entre uma repetição e a seguinte. **Pertence ao perfil.** | desligado |
| **Jitter** | Variação aleatória de ± % em cada delay. | desligado |

> **Loops e Interval são do perfil**, e viajam no export/duplicar. Sem perfil carregado, valem para o app.
>
> **Não existe `0 = infinito`.** Mínimo 1. Para rodar até você mandar parar, use o modo de disparo **While Pressed** ou **Toggle**.

A pílula de loop mostra o que a **próxima execução** fará: `3×`, `por linha` (Loop over data) ou `∞`. Contorno tracejado âmbar = você mexeu e não salvou.

---

## A grade de ações

Colunas: **caixa · Action · Details · Delay · Notes**.

<p align="center">
  <img src="img/main.png" width="820" alt="A janela principal e a grade de ações do TrueReplayer" /><br>
  <sub><i>Perfis à esquerda, grade no centro, configurações à direita.</i></sub>
</p>

| Ação | Como |
| --- | --- |
| **Selecionar** | Clique · `Ctrl+Click` alterna · `Shift+Click` intervalo. |
| **Editar na linha** | Clique na célula: **Delay**, **Notes**, **coordenadas**, **Key**. `Enter` confirma, `Esc` cancela. |
| **Reordenar** | Arraste, ou **`Alt+↑` / `Alt+↓`**. |
| **Pular** | Desmarque a linha — fica na lista, não roda. |
| **Em massa** | Com várias selecionadas: **Set delay**, **Set X / Y**, **Set notes**, **Move**, **Skip**, **Delete**. |
| **Painel Sheet** | Botão direito → **Edit** para o formulário completo. |

> **Else / EndIf** não têm Delay (célula em branco). O **If** aceita: é uma **espera pré-sondagem**, antes de checar a condição.

---

## Referência de ações

| Ação | O que faz |
| --- | --- |
| **Left / Right / Middle Click** | Um clique em `(x, y)` — ou **N cliques** com intervalo, **Gap jitter** e **Position jitter**. |
| **Double Click** | Dois cliques abaixo do limiar do sistema, para o app ler como duplo real. Aceita **× N**. |
| **Keystroke** | Uma tecla ou combinação — ou **N vezes** com intervalo e **Gap jitter**. |
| **Hold Key** | Segura uma tecla por N ms (padrão 1000). Modificadores são descartados. |
| **Key Down / Key Up** | Pressionar ou soltar isolado — para arrastar ou segurar tecla. |
| **Scroll Up / Down** | Um passo da roda na posição do cursor. |
| **Send Text** | Injeta texto com tokens — veja [Send Text](#send-text). |
| **Set Variable** | Guarda um valor lido com `{var:nome}`. |
| **Copy to Slot** | Copia a seleção atual para um slot, lido com `{clip:nome}`. |
| **Pause** | Para até uma **hotkey de retomada** ou um **timeout**. Precisa de um dos dois. |
| **Wait Image** | Espera uma imagem aparecer (confiança padrão ≈ 85%). |
| **Wait Pixel Color** | Espera o pixel em `(x, y)` bater com uma cor. |
| **Run Profile** | Executa outro perfil como subpasso. Ciclos e mais de 5 níveis são bloqueados. |
| **Activate Window** | **Activate** / **Maximize** / **Minimize** / **Close** noutra janela. Muda o foco do SO, nunca o contexto de coordenadas. |
| **If / Else / EndIf** | [Blocos condicionais](#blocos-condicionais-if--else--endif). |
| **Assert** | Exige que algo seja verdade e **para nomeando a falha** — veja [Assert](#assert--exigir-que-algo-seja-verdade). |
| **Browser actions** | Click / Type / Navigate / Wait / Assert / Select no Chrome. |

### Repetição em cliques e teclas

**Keystroke** e os cliques aceitam repetição na própria linha:

- **Times to repeat** — 1 a 999. Em `1` a linha se comporta como sempre.
- **Gap between** — intervalo entre uma e a próxima (padrão 30 ms; **600 ms** no Double Click, porque um duplo precisa de folga acima da velocidade do Windows para contar como duplo *distinto*).
- **Gap jitter** — ± % aleatório em cada intervalo. Desligado por padrão; ligue no pontinho ao lado do rótulo.
- **Position jitter** *(só cliques)* — espalha o ponto em ± N px por eixo.

Os três últimos só ficam ativos com **Times to repeat** > 1.

> **Quando usar jitter.** `Click × 3` com Gap + Position jitter parece humano — é o que serve em jogos, onde repetir o mesmo pixel no mesmo ritmo é o sinal mais óbvio de macro. Para automação comum (um botão, um campo), **deixe desligado**: ali você quer o pixel exato.

<p align="center">
  <img src="img/click-repeat.png" width="360" alt="O bloco Repeat de uma linha de clique" /><br>
  <sub><i>Times · Gap · Gap jitter · Position jitter.</i></sub>
</p>

---

## Blocos condicionais (If / Else / EndIf)

Faz a macro reagir ao que está na tela.

- Verdadeiro → roda o que está entre **If** e **Else/EndIf**.
- Falso → pula para o **Else** (se houver) ou para depois do **EndIf**.
- **Negate** inverte: o ramo verdadeiro roda quando a checagem **falha**.
- **Wait for condition** (ms) — fica checando até esse tempo antes de decidir. Satisfez → verdadeiro; estourou → falso. `0` = instantâneo (padrão).
- **On Probe Error** — se a *própria checagem* falhar: **Treat as false** (padrão) ou **Halt**.
- Blocos podem ser **aninhados**, cada nível na sua cor. Para aninhar: selecione uma linha **dentro** do bloco → **Insert Conditional**.

<p align="center">
  <img src="img/conditionals.png" width="820" alt="Dois blocos If/Else/EndIf na grade de ações" /><br>
  <sub><i>Uma checagem de pixel negada e uma de imagem com ramo <code>else</code>.</i></sub>
</p>

### As 10 condições, com exemplo de cada

| Condição | Verdadeiro quando | Exemplo prático |
| --- | --- | --- |
| **Image Found** | Uma imagem está visível na tela. | *Recorte o ícone de "salvo".* Se apareceu, siga; se não, clique em Salvar de novo. |
| **Pixel Color Match** | O pixel em `(x, y)` bate com uma cor. | *Ponto no meio do botão liga/desliga.* Verde = já está ligado, então pule o clique. |
| **Window Open** | Existe janela com aquele processo/título. | *Process `notepad.exe`.* Só feche o arquivo se o Bloco de Notas estiver aberto. |
| **Clipboard** | O texto copiado casa (Contains / Equals / Regex). | *Regex `^\d{11}$`.* Se o que copiei é um CPF, preencha o campo; senão, avise. |
| **Browser Element** | Um elemento no Chrome está presente / visível / habilitado. | *`text=Enviar`, estado `enabled`.* Só clique quando o botão sair do cinza. |
| **Random** | Um sorteio cai abaixo de N%. | *30%.* Em três de cada dez voltas, faça uma pausa extra — a macro deixa de parecer um metrônomo. |
| **Variable** | `{var:nome}` compara verdadeiro. | *`{var:tentativas}` maior que `3`.* Desistiu de tentar, siga para o plano B. |
| **Process Running** | Um processo está rodando. | *`chrome.exe`.* Só rode os passos de navegador se o Chrome estiver aberto. |
| **File Exists** | Um arquivo ou pasta existe. | *`C:\Relatorios\hoje.pdf`.* Se o download terminou, anexe; senão, espere mais. |
| **Time** | O relógio está na janela de início–fim, nos dias escolhidos. | *08:00–18:00, Seg–Sex.* Fora do horário comercial, não dispare o envio. |

> Nas condições de **estado** (Clipboard, Variable, Random, Time) as opções aparecem como **Met / NOT Met**; nas de **objeto** (Image, Window, Process, File, Browser, Pixel), como **Found / NOT Found**. Mesma ideia.

### Exemplo — a janelinha que só aparece às vezes

O sistema *às vezes* abre um "Tem certeza?". Quando aparece, a macro digita por cima; quando não, uma pausa fixa de 3 s é tempo jogado fora.

1. Selecione a linha logo depois de onde o aviso costuma surgir. O bloco entra **antes** dela.
2. Barra → ícone de ramificação → **Window Open**. Entram **If** e **EndIf**.
3. Preencha **Process Name** e/ou **Title**. Com o aviso na tela, aperte **Test** — tem que dar *Found*.
4. Arraste o clique do **OK** para dentro do bloco.
5. Abra a linha **If** (passe o mouse → lápis, ou selecione e `Enter`) e ponha **Wait for condition** = `2000`.

| Linha | Quando roda |
| --- | --- |
| **If** — Window Open · `Confirmação` | sempre — é a checagem |
| Left Click (612, 428) | só se a janela existir |
| **EndIf** | fecha o bloco |

Apareceu em 200 ms → segue em 200 ms. Não apareceu em 2 s → pula o bloco.

**Quer um plano B?** Dentro do bloco, logo acima do **EndIf**, tem a linha tracejada **+ Add Else branch**. É ali que o Else nasce — não está no menu do botão direito.

### Dois tempos diferentes

| | Onde fica | Como gasta |
| --- | --- | --- |
| **Delay** | Coluna Delay da grade | Espera fixa **antes** da checagem — gasta tudo mesmo que já estivesse pronto. |
| **Wait for condition** | Editor da linha If | Gasta **só o necessário**, até o limite. |

Se preencher os dois, eles somam.

### Editando o conteúdo de um bloco

Uma operação só pega o **bloco inteiro** quando a seleção inclui um marcador (If / Else / EndIf) — assim marcadores nunca ficam órfãos.

- **Arraste** ações do corpo para dentro ou fora do bloco, livremente.
- **Delete** no corpo mantém o bloco; delete no **If** apaga o bloco inteiro.
- **`Alt+↑` / `Alt+↓`**: seleção só de corpo move sozinha; tocando um marcador, leva o bloco.
- **Duplicar** um **If** copia o bloco inteiro.

---

## Assert — exigir que algo seja verdade

Um **If** *pergunta* e segue por um dos dois caminhos. Um **Assert** *exige*: se não for verdade, **para na hora e diz qual premissa falhou**.

Uma linha só, sem ramificação e sem `EndIf`. Fica em barra → ícone de ramificação → **Insert Assert — must be true**.

| Exija que… | Exemplo prático |
| --- | --- |
| **Window Open** | *`app.exe`, foreground.* Não digite a senha se a janela de login não estiver na frente. |
| **Process Running** | *`vpn.exe`.* Não tente acessar o sistema interno sem a VPN rodando. |
| **Clipboard** | *Contains `@`.* Não preencha o campo de e-mail se o que foi copiado não parece um e-mail. |
| **Variable** | *`{var:total}` maior que `0`.* Não emita a nota com o total zerado. |
| **File Exists** | *`C:\entrada\lote.csv`.* Não rode o processamento sem o arquivo do dia. |
| **Time** | *Seg–Sex.* Não dispare o envio no fim de semana. |

São só estas seis de propósito: imagem e pixel já param sozinhos por timeout (**Wait Image** / **Wait Pixel Color**), e para página existe o **Assert Element**.

**Campos:** **Require** (Met/NOT Met) · **Wait for condition** (padrão 1500 ms; **Time** não aceita — relógio não muda de resposta se você insistir) · **On failure** (**Abort** padrão, ou **Continue** que só registra) · **Notes** (o nome que aparece na falha).

A falha aparece assim:

```
Assert failed: 'janela de login em foco' — window app.exe was not in the foreground
Assert failed: 'código copiado'          — clipboard did not match the pattern
```

Sem **Notes**, a mensagem cai para `'element'` — funciona, mas com três asserts na macro você não sabe qual foi.

> **Assert, If ou Wait?**
> **Wait** = *sincronizar* ("espere a tela ficar pronta").
> **If** = *ramificar* ("se aparecer, clique; se não, siga") — os dois caminhos são normais.
> **Assert** = *exigir* ("daqui não passa sem isto") — só um caminho é aceitável.

---

## Perfis e pastas

- **New / Save / Rename / Duplicate / Delete** no painel Profiles.
- **Pin** mantém no topo; **arraste** para dentro de uma **pasta**.
- **Pastas** — cor, renomear, recolher. Podem ter um **alvo de janela** que os perfis herdam. O botão no cabeçalho do painel recolhe/expande **todas**.
- **Info** (botão direito) — emoji, descrição e **tags** (pesquisáveis).
- **Import / Export** — arquivo `.trprofile` com ações, metadados, imagens e layout. Na importação, cada conflito recebe **Rename** (padrão — nada é sobrescrito em silêncio), **Overwrite** ou **Skip**. Um perfil que exige versão mais nova fica esmaecido com o motivo.

**Paleta de comandos (`Ctrl+K`)** — o que não tem botão próprio:

- **Profiles** — Duplicate, Reset, Import, Export all.
- **Actions** — *Copy as Table* / *Paste Actions* (mover passos entre perfis), *Convert to Relative / Absolute*, *Combined ↔ Paired*.
- **Diagnostics** — *Toggle Live Variables*, *Run report*, Automation e Theme Editor.

---

## Hotkeys e hotstrings

- **Hotkey** — botão direito no perfil → **Assign hotkey** → pressione a combinação. Dispara globalmente.
- **Hotstring** — uma sequência digitada (ex.: `qqsig`) que roda o perfil ao terminar.
- **Chave-mestra** — `Pause` liga/desliga **todas** de uma vez.

<p align="center">
  <img src="img/hotkey.png" width="320" alt="O diálogo Assign Hotkey com os seis modos de gatilho" /><br>
  <sub><i>Capture a combinação e escolha o modo.</i></sub>
</p>

| Modo | Comportamento |
| --- | --- |
| **On Press** | Uma vez, ao pressionar. |
| **On Release** | Uma vez, ao soltar. |
| **While Pressed** | Repete enquanto segurada; para ao soltar. |
| **Toggle** | Primeiro toque inicia, segundo para. |
| **Double-tap** | Dois toques rápidos (~0,4 s). Toque único não faz nada. |
| **Hold** | Uma vez após segurar ~0,6 s. **Não** para ao soltar. |

> Os modos valem só para **hotkeys**. Hotstrings sempre disparam ao serem digitadas.

**Botões laterais do mouse** (**XButton1/2**) funcionam como teclas, com todos os modos — ideais para macros de jogo. A roda também, mas sempre em On Press.

---

## Automação (disparo sem hotkey)

Dispara um perfil sozinho. **Settings → App → Automation → Manage** (ou bandeja → **Automations…**). Um gatilho por perfil.

| Tipo | Dispara |
| --- | --- |
| **Interval** | A cada N segundos (300 = 5 min). O primeiro vem um intervalo depois de armar. |
| **Schedule** | Num horário `HH:mm`, nos dias escolhidos. Nenhum dia aceso = todos os dias. |
| **Condition** | Quando a condição **fica verdadeira**: janela abre, processo inicia, arquivo aparece, pixel bate, imagem aparece, clipboard muda. |

<p align="center">
  <img src="img/automation-panel.png" width="820" alt="O painel de Automação" /><br>
  <sub><i>Lista com a chave <b>Armed</b> à esquerda, editor do gatilho à direita.</i></sub>
</p>

**Como se comporta**

- **Armed** — só automações armadas rodam, e se re-armam ao iniciar o app. Armar é **local desta máquina**: perfis importados ou duplicados chegam **desarmados**.
- **Uma execução por vez** — enquanto um replay, gravação ou diálogo está ativo, ou a grade tem edições não salvas, o disparo tenta por uma janela curta e depois é **pulado** (e contado). Uma automação nunca atropela trabalho não salvo.
- **Respeita os Loops, nunca roda para sempre** — perfil em `3×` roda 3 vezes; o infinito de While Pressed / Toggle é ignorado quando quem chama é o daemon.
- **Interval é ancorado no último disparo real** e sobrevive a fechar o app. Um "a cada 12 h" numa máquina que você desliga à noite não recomeça do zero. Se o momento passou com o app fechado, dispara 15 s depois de abrir.
- **Schedule perdido é descartado** — se a máquina estava suspensa às 08:00 e acordou às 18:00, o disparo não te embosca. Perdido por poucos minutos, ele ainda tenta (até 3 min).
- **Condição só dispara na virada** — precisa voltar a ser falsa antes do próximo (mude para **Continuous** para repetir enquanto verdadeira). **Cooldown** padrão 30 s.

**Antes de confiar numa automação**

- **Run now** (topo do editor) — dispara agora **pelo mesmo caminho do gatilho**, e diz *por que não rodou* se for o caso. Só funciona com a automação já salva.
- **Aviso de "nunca vai disparar"** — condição sem o campo obrigatório trava o **Save**, em vez de salvar e ficar com a luz acesa sem nunca disparar.
- **Armada mas não vigiando** — a linha diz o motivo: chave-mestra pausada, perfil desativado, ou o vigia parou sozinho.

**Custo de um vigia — o campo `Check every`**

Um gatilho de condição checa enquanto armado, e o custo é por checagem. **Image on screen** captura a tela inteira toda vez; **Window open** é quase de graça.

Deixe `0` para o padrão (250 ms pixel, 500 ms clipboard, 1 s o resto). Vale subir quando o que você espera é lento: um app abrindo, um download terminando. Trocar 1 s por 5 s numa vigia de imagem corta o custo em cinco e você não perde nada.

**Gatilho por imagem**

<p align="center">
  <img src="img/automation-image.png" width="440" alt="Gatilho de automação por imagem na tela" /><br>
  <sub><i>Região de busca, confiança e <b>Test match</b>.</i></sub>
</p>

- **Reference image** — **Capture** recorta na tela. Clique na miniatura para recortar mais justo.
- **Confidence** — padrão **80%**. Nunca 100%.
- **Search region** — **Configure** limita a busca a um pedaço: mais rápido e com menos falso positivo.
- **Test match** — procura agora; num acerto mostra a % e **ajusta a região** em volta do ponto.

> **O erro nº 1: salvar não é armar.** O **Save** grava o gatilho; quem faz existir é a chave na lista. Se está armada e não roda, use o **Run now** — ele escreve o motivo na tela.
>
> **A armadilha silenciosa:** deixar a grade com edição não salva e mandar o app para a bandeja. Nesse estado **nenhuma** automação dispara, e não há nada na tela lembrando. Salve antes de sair.

---

## Remaps de tecla

**Settings → Keys → Key Remaps** — camada 1:1 sempre ativa, independente de perfis.

- **Remapear** — `CapsLock → Esc` vale em todo o sistema enquanto o app roda. Botões laterais do mouse também servem de origem.
- **Desativar** uma tecla — mapeie para nada.
- Remaps **pausam durante a gravação** e podem ser pausados na bandeja (**Enable Key Remaps**) — a saída de emergência só com o mouse.
- Hotstrings seguem o fluxo **remapeado**. Uma tecla usada como origem não pode ser hotkey de perfil: o remap vence.

---

## Alvo de janela e coordenadas relativas

Prende um perfil (ou pasta) a uma janela.

<p align="center">
  <img src="img/target.png" width="360" alt="O diálogo Target Configuration" /><br>
  <sub><i>Processo / título, coordenadas relativas e opções de restauração.</i></sub>
</p>

- **Window target** — processo e/ou título (Contains ou Regex). A **hotkey só dispara com aquela janela na frente**. **Detect Window** preenche clicando na janela; **Test front window** confirma.
- **Relative Coordinates** — guarda os cliques em relação ao canto da janela, não da tela. Vale também para regiões do **WaitImage** e coordenadas do **WaitPixel**.
- **Bring to Focus** — traz a janela para frente antes de rodar (e faz a hotkey voltar a valer em qualquer janela).
- **Restore Position / Size** — encaixa a janela numa geometria salva. Grave com **Update Window Size & Position** *antes* de ligar as chaves.

### Exemplo — a macro que ontem acertava e hoje erra

Alguém arrastou a janela. Um clique gravado guarda um ponto **da tela**, então dez pixels de diferença erram tudo.

1. Botão direito no perfil → **Window target…** → **Detect Window** → clique na janela.
2. **Test front window** → tem que dar *✓ Matches*.
   Título que muda a cada atendimento? Use **Contains** com só o pedaço fixo. Se o pedaço fixo estiver no começo *e* no fim, use **Regex**:
   ```
   ^Pedidos .* — Sistema Interno$
   ```
   `^` prende no começo · `.*` aceita qualquer coisa no meio · `$` prende no fim.
3. Ligue **Relative Coordinates**. Como a macro já estava gravada, aparece o aviso *N actions captured in absolute coords* — clique em **Apply target & convert**.
   **Não clique em Skip:** ele deixa os números antigos e o app passa a lê-los como se já fossem relativos. É aí que a macro começa a clicar no canto errado.
4. **Set Target.** Nada é gravado até esse clique.

> **Relative Coordinates** faz a macro *seguir* a janela. **Restore Position / Size** *devolve* a janela para um lugar salvo. As duas juntas são segurança em dobro.
>
> Se o perfil usa coordenadas relativas e a janela não for achada, a execução **para com erro** em vez de clicar em qualquer lugar.

---

## Automação multi-janela (Activate Window)

Troca qual app está na frente *no meio da execução*. Diferente do alvo de janela do perfil (que prende o perfil inteiro), esta é uma **ação** que você coloca a cada troca.

**Ela muda só o foco do SO — nunca o contexto de coordenadas.** Os cliques continuam resolvendo contra o alvo do perfil. Por isso:

- **Multi-janela simples** — perfil **sem alvo**, cliques absolutos, uma linha **Activate Window** antes dos passos de cada app.
- **Multi-janela de precisão** — um perfil **orquestrador** sem alvo alternando **Activate Window X** → **Run Profile "passos-de-X"**, onde cada sub-perfil tem *seu próprio* alvo e coordenadas relativas.

**Campos** — **Action**: Activate / Maximize / Minimize / Close. **Process** e/ou **Title** identificam a janela (**Match #** escolhe a N-ésima). **Path / Args** abrem o app se nenhuma janela casar. **Placement** posiciona (só visual, não muda onde os cliques caem). **Timeout / On Timeout** decidem esperar quanto e se **Halt** (padrão) ou **Continue**. **Test** confere agora.

<p align="center">
  <img src="img/activate-window.png" width="360" alt="O editor da ação Activate Window" /><br>
  <sub><i>O verbo <b>Action</b> e os campos de identificação da janela.</i></sub>
</p>

---

## Clicker mode (auto-clicker)

**`ScrollLock`** alterna. O painel troca para quatro grupos.

**Clicker** — **Button** (Left/Right/Middle) e **Rate** (cliques/s ou ms). O rótulo mostra `≈ N/s` já contando Hold e Gap: a taxa real, não `1000/delay`.

**Target** *(um desliga os outros)* — **Position** (aleatoriza em volta do cursor) · **Area** (retângulo, pontos aleatórios dentro) · **Fixed** (sempre o mesmo ponto).

**Stop after** *(independentes; o primeiro encerra)* — **Clicks** e **Time**. **Ambos vêm desligados: por padrão o Clicker roda sem fim** (`∞`).

**Tuning** — **Jitter** (± % em cada atraso) · **Hold** (10 ms = normal; 50–200 para apps que perdem cliques curtos) · **Gap** (tempo extra por clique) · **Game move** (move por um caminho em vez de teletransportar, para jogos que ignoram saltos — só afeta **Area** e **Fixed**).

> **Rate e Hold são honestos com o período.** Hold e Gap entram *dentro* do ciclo: pedir 100 ms dá ciclos de 100 ms, não 110.

**`PageDown`** inicia/para, **`PageUp`** pausa/retoma. O painel ao vivo mostra contagem, taxa, tempo, progresso e ETA.

<p align="center">
  <img src="img/clicker.png" width="820" alt="O painel do Clicker enquanto roda" /><br>
  <sub><i>Contagem ao vivo, taxa, ETA — e as configurações à direita.</i></sub>
</p>

> **`SendInput` não avisa quando é bloqueado.** Se o alvo é uma janela elevada e o TrueReplayer não é, o Windows aceita a chamada e o evento simplesmente não chega — a taxa continua saudável enquanto nada acontece. Se parece rodando mas o alvo não reage, rode como administrador.

---

## Game mode

Para jogos que ignoram um teleporte instantâneo do cursor. **O cabeçalho da seção é o interruptor mestre** — ligado por padrão.

- **Fast approach** — em movimentos longos, teleporta até uma **Distance** (padrão 80 px) do alvo e percorre só o final devagar. Desligue se um jogo errar o clique.
- **Tuning** — **Click delay** (padrão 10 ms) sempre visível. Com o mestre ligado, também **Path step** (20 px) e **Step delay** (2 ms).
- **Focus-click** *(por ação, botão direito na linha)* — alguns campos minúsculos só recebem foco no *segundo* clique. **Use só em campos de texto pequenos, nunca em botões** — um botão dispararia duas vezes.

> O Clicker tem o próprio **Game move**, independente deste mestre.

---

## Send Text

O editor **Insert Text** compõe o texto injetado por colagem (para layouts e caracteres especiais sobreviverem).

<p align="center">
  <img src="img/sendtext.png" width="820" alt="O editor Insert Text" /><br>
  <sub><i>Chips editáveis, com as seções Clipboard · Values · Keys &amp; timing · Run state.</i></sub>
</p>

**Tokens disponíveis**

| Seção | Chips |
| --- | --- |
| **Clipboard** | `{clipboard}` · **Advanced…** (monta transformações) · **Clip slot…** (`{clip:nome}`) · **Clipboard history** (`{winclip:1}`) |
| **Values** | `{date}` · `{time}` · `{datetime}` · `{random:1-10}` |
| **Keys & timing** | `{enter}` · `{tab}` · `{delay:500}` · **More keys** |
| **Run state** | `{var:nome}` · `{counter}` · `{row}` · `{row:coluna}` · `{rownext:coluna}` · `{input:…}` |

Teclas repetíveis aceitam contagem: `{enter:3}`.

Confirme com **`Ctrl+Enter`** — o `Enter` sozinho pula linha. `Esc` cancela.

**Snippets** — texto reutilizável salvo por nome. Ficam **no app, não no perfil**: não viajam no export/import.

**Delivery** — como a formatação chega:

| Modo | Use em |
| --- | --- |
| **Rich** | E-mail, documentos, editores web. |
| **Markdown** | WhatsApp e afins (`*negrito*`). |
| **Discord** | Discord (`**negrito**`, `~~riscado~~`). |
| **Plain** | Busca, chat de jogo, campos de código. |

> Se a mensagem chegar mostrando os asteriscos, você mandou Markdown para um app que não entende — troque para **Rich** ou **Plain**. Se a formatação sumiu, o alvo não aceita texto rico.

---

## Transformações de texto

Qualquer token de texto aceita uma **cadeia de transformações**, separada por `:`. Vale para:

```
{clipboard:...}   {clip:nome:...}   {var:nome:...}
{winclip:N:...}   {row:coluna:...}  {rownext:coluna:...}
```

O chip **Advanced…** (ou clicar em qualquer chip desses) abre uma janela que monta a cadeia por etapas, **com prévia ao vivo** — você não precisa decorar sintaxe nenhuma.

<p align="center">
  <img src="img/advanced-clipboard.png" width="820" alt="O construtor de transformações com prévia ao vivo" /><br>
  <sub><i>As etapas à esquerda, a prévia do resultado à direita.</i></sub>
</p>

### A lista completa

Nos exemplos, o texto de partida é:

```
Pedido 4821 - Cabo HDMI 2m
```

| Transformação | O que faz | Exemplo | Resultado |
| --- | --- | --- | --- |
| `trim` | Tira espaços e quebras nas pontas | `{clipboard:trim}` sobre `␣␣Pedido 4821␣␣` | `Pedido 4821` |
| `upper` | MAIÚSCULAS | `{clipboard:upper}` | `PEDIDO 4821 - CABO HDMI 2M` |
| `lower` | minúsculas | `{clipboard:lower}` | `pedido 4821 - cabo hdmi 2m` |
| `sentence` | Só a primeira letra da frase | `{clipboard:sentence}` sobre `pedido enviado` | `Pedido enviado` |
| `title` | A Primeira De Cada Palavra | `{clipboard:title}` sobre `cabo hdmi 2m` | `Cabo Hdmi 2m` |
| `word:N` | A palavra N | `{clipboard:word:2}` | `4821` |
| **`words:a-b`** | **O intervalo de palavras a até b** | `{clipboard:words:1-2}` | `Pedido 4821` |
| **`words:a-`** | **Da palavra a até o fim** | `{clipboard:words:4-}` | `Cabo HDMI 2m` |
| **`before:X`** | **Tudo antes da primeira ocorrência de X** | `{clipboard:before: - }` | `Pedido 4821` |
| **`after:X`** | **Tudo depois da primeira ocorrência de X** | `{clipboard:after: - }` | `Cabo HDMI 2m` |
| **`beforelast:X`** / **`afterlast:X`** | **Idem, mas na última ocorrência** | `{clipboard:afterlast:/}` num caminho | o nome do arquivo |
| `first:N` | Os primeiros N **caracteres** | `{clipboard:first:6}` | `Pedido` |
| `last:N` | Os últimos N **caracteres** | `{clipboard:last:2}` | `2m` |

O intervalo de palavras **preserva o espaçamento original** entre elas — espaços duplos e quebras de linha voltam como estavam.

> **Se o delimitador não existir no texto, `before`/`after` devolvem vazio** — não devolvem o texto inteiro. É de propósito: a outra resposta colaria tudo onde você pediu um pedaço.

### Quando o texto tem várias linhas

Partindo de:

```
banana
Abacaxi
banana
manga
```

| Transformação | O que faz | Exemplo | Resultado |
| --- | --- | --- | --- |
| `line:N` | A linha N | `{clipboard:line:2}` | `Abacaxi` |
| `range:a-b` | As linhas a até b | `{clipboard:range:2-3}` | `Abacaxi` + `banana` |
| `range:a-` | Da linha a até o fim | `{clipboard:range:3-}` | `banana` + `manga` |
| `lines:i,j,k` | Escolhe e reordena | `{clipboard:lines:4,1}` | `manga` + `banana` |
| `sort` | Ordena A→Z (ignora maiúsculas) | `{clipboard:sort}` | `Abacaxi` `banana` `banana` `manga` |
| `dedupe` | Remove repetidas | `{clipboard:dedupe}` | `banana` `Abacaxi` `manga` |
| `join:sep` | Junta tudo numa linha | `{clipboard:sort:join:, }` | `Abacaxi, banana, banana, manga` |
| `reverse` | Inverte a ordem | `{clipboard:reverse}` | `manga` `banana` `Abacaxi` `banana` |

### Combinando

As transformações se aplicam **em sequência**, nesta ordem fixa:

```
trim → before/after → range/lines → sort → dedupe → reverse → join → words → line/word → first/last → caixa
```

```
{clipboard:after: - :upper}       →  CABO HDMI 2M
{clipboard:sort:dedupe:join:, }   →  Abacaxi, banana, manga
{clipboard:words:1-2:lower}       →  pedido 4821
```

### Uma linha por uso — `{clipboard:next}`

Cola **uma linha e guarda o lugar**. Copie 30 códigos de uma vez: o primeiro toque solta o código 1, o seguinte o 2.

- Copiou outra coisa → recomeça na linha 1 sozinho. Você nunca precisa resetar nada.
- Linhas em branco são puladas.
- No fim ele **para de dar valor** (vira vazio) em vez de voltar ao começo — recomeçar sozinho faria a macro reprocessar tudo sem ninguém perceber.
- Combina com os outros: `{clipboard:next:trim:upper}` pega a próxima linha e *depois* transforma **aquela linha**.
- Vários `{clipboard:next}` na mesma macro consomem uma linha cada, em ordem.

> **Qual dos três usar.** `{clipboard:line:3}` = *sempre* a terceira. `{clipboard:next}` = a **próxima**, do que está copiado. `{rownext:coluna}` = a próxima linha da **tabela do perfil** — essa sobrevive a fechar o app.

### Quando o número vem de uma variável — `@i`

Onde a transformação pede um número, ele pode vir de uma variável. Escreva `@` e o nome:

```
Set Variable   i = 3
Send Text      {clipboard:line:@i}     →  a terceira linha
```

| Você escreve | De onde vem |
| --- | --- |
| `@nome` | A variável com esse nome |
| `@counter` | A volta atual do loop — 1, 2, 3… |
| `@row` | A linha atual da tabela de dados |

Num loop, `{clipboard:line:@counter}` pega a linha 1 na primeira volta, a 2 na segunda, e assim por diante.

- Vale em **Line #**, **Word #**, **First N** e **Last N**.
- Na janela do construtor, o botãozinho **@** troca entre número fixo e variável. Com ele ligado a prévia diz *"Resolvido quando a macro roda"* — ela não teria como saber o valor.
- **Nome que não existe sai vazio**, de propósito. O contrário seria colar o clipboard inteiro por causa de um erro de digitação, dentro de uma resposta a cliente.
- No **join** o `@` não vale: ali o texto é o separador literal.

> `{clipboard:line:{var:i}}` com chaves **não funciona** e nunca funcionou. A grafia com `@` existe justamente por isso.

---

## Variáveis, slots e prompts

Três jeitos de uma macro lidar com valores que mudam.

| Ferramenta | Quanto dura | Como ler |
| --- | --- | --- |
| **Set Variable** | Até o fim da execução atual | `{var:nome}` |
| **Copy to Slot** / hotkey **Capture Slot** | Entre execuções, enquanto o app estiver aberto | `{clip:nome}` ou `{clip:1}`…`{clip:9}` |
| **`{input:Rótulo}`** | A execução atual (pergunta uma vez) | O próprio token |

### Cada token, com exemplo

| Token | Exemplo prático | O que sai |
| --- | --- | --- |
| `{var:cliente}` | Um **Set Variable** guardou `cliente = Maria Silva` | `Maria Silva` |
| `{clip:1}` … `{clip:9}` | Você apertou `Win+Ctrl+C` sobre um número de pedido | `4821` |
| `{clip:pedido}` | Uma ação **Copy to Slot** com **Slot** = `pedido` | o texto capturado |
| `{input:Número do pedido}` | Abre uma caixa perguntando | o que você digitar |
| `{input:Prioridade\|menu:Baixa,Média,Alta}` | Abre uma lista de opções | a opção clicada |
| `{counter}` | Loop na 3ª volta | `3` |
| `{clipboard}` | Você copiou um endereço | o endereço inteiro |
| `{clipboard:next}` | Você copiou 30 códigos | o próximo da lista, um por toque |
| `{winclip:1}` | Histórico do `Win+V` | o último item copiado |
| `{row:produto}` | Data Loop na linha 2 | o valor da coluna `produto` naquela linha |
| `{rownext:produto}` | Três `Send Text` seguidos | linha 1, linha 2, linha 3 |
| `{date}` `{time}` `{datetime}` | — | `17/08/2026`, `14:32`, os dois |
| `{random:1-10}` | — | um número sorteado |
| `{row}` | Ação na 5ª linha da grade | `5` (o número **da ação**, não da tabela) |

> **Regra de ouro:** token sem valor vira **texto vazio**, nunca erro. Se algo sair em branco, `Ctrl+K` → **Toggle Live Variables** e rode de novo.

### Set Variable

Dê um **Name** e um **Value**. O valor é montado antes de guardar, então aceita `{clipboard}`, `{row:col}`, `{date}` ou outro `{var:}`. Guardar vazio **apaga** a variável.

```
Name:  cliente
Value: {clipboard:trim}
```

No **Mode**, troque de **Set** para **Cycle**: o campo vira uma lista (um item por linha) e cada execução guarda a **próxima**, voltando à primeira no fim. Serve para uma hotkey percorrer uma lista.

```
Mode:  Cycle
Value: Bom dia
       Boa tarde
       Boa noite
```

A posição é **guardada em disco** — fechar o app não recomeça. Para recomeçar: botão direito na linha → **Reset cycle position**.

### Copy to Slot

<p align="center">
  <img src="img/copy-to-slot-clear.png" width="360" alt="Editor do Copy to Slot no modo Clear" /><br>
  <sub><i>O modo <b>Clear</b> esvazia um slot — ou todos, se o nome ficar em branco.</i></sub>
</p>

- **Capture** (padrão) — copia o que estiver **selecionado** para o slot. Garanta a seleção antes (um `Ctrl+A` na linha anterior, por exemplo). Se a captura falhar, o valor anterior **continua lá**.
- **Clear** — esvazia o slot. Campo **em branco** limpa **todos** (1 a 9) e devolve a hotkey para o slot 1.

**Capture Slot** *(hotkey, já em `Win+Ctrl+C`)* — a versão manual. Cada toque guarda a seleção no próximo slot numerado, de 1 a 9, e depois volta ao 1. Um aviso mostra onde caiu. **Não funciona enquanto uma macro roda** — lá dentro, use a ação **Copy to Slot**.

### `{input:Rótulo}`

Pausa e pergunta. O app **se traz para a frente** sozinho e, depois da resposta, **devolve o foco** para a janela de antes — então o texto cai no app certo.

```
{input:Número do pedido}                      →  caixa de texto
{input:Prioridade|menu:Baixa,Média,Alta}      →  lista de opções
```

<p align="center">
  <img src="img/ask-input.png" width="360" alt="A caixa Input needed durante uma execução" /><br>
  <sub><i>Com <code>|menu:…</code> ela vira uma lista para clicar.</i></sub>
</p>

Pergunta **uma vez por rótulo, por execução**. `Esc`/`Cancel` **param a macro**; sem resposta em 60 s, a execução é abortada (para uma automação sem ninguém olhando não travar).

### Exemplo — juntando três informações espalhadas

O nome do cliente está no chamado, o número do pedido no admin, o código de entrega no fornecedor.

1. Selecione o nome → `Win+Ctrl+C` → vira `{clip:1}`.
2. Selecione o pedido → `Win+Ctrl+C` → `{clip:2}`.
3. Selecione o código → `Win+Ctrl+C` → `{clip:3}`.
4. Um perfil com um **Send Text**:

```
Olá {clip:1}, seu pedido {clip:2} foi enviado!
Código de entrega: {clip:3}{enter}
```

Recolher são três toques, enviar é um só. Os slots continuam guardados — dá para recolher agora e rodar depois.

> **Os números seguem de onde pararam.** Se você já capturou duas coisas hoje, a próxima cai em `{clip:3}`. O aviso na tela sempre diz onde caiu.
>
> **Slot vazio?** As duas formas copiam mandando `Ctrl+C` para o app em foco, então **o texto precisa estar selecionado**. Se nada for copiado, o slot mantém o valor antigo e o contador **não avança**.

**Quando o dado está sempre no mesmo lugar**, automatize a coleta: use a ação **Copy to Slot** com um nome (`pedido`) dentro da própria macro e leia com `{clip:pedido}`. A hotkey serve para quando *você* escolhe o que copiar; a ação serve para quando a macro sempre acha o valor no mesmo canto — e é a única que funciona *durante* uma execução.

<p align="center">
  <img src="img/live-variables.png" width="360" alt="O painel Live Variables durante uma execução" /><br>
  <sub><i><code>Ctrl+K</code> → <b>Toggle Live Variables</b>: variáveis, slots e a linha atual, ao vivo.</i></sub>
</p>

---

## Data Loop

Roda o perfil inteiro uma vez para **cada linha** de uma tabela. Cada cabeçalho vira um token `{row:coluna}`.

Barra → ícone de tabela. A tabela é salva **dentro do perfil** e viaja no export.

<p align="center">
  <img src="img/data-loop.png" width="820" alt="O painel Data Loop" /><br>
  <sub><i>A tabela, o modo <b>Loop over data</b> e os tokens de coluna.</i></sub>
</p>

**Colocando dados**

- **Paste / bulk edit…** — cole um intervalo do Excel → **Replace table** ou **Append rows**. **First row is the header** usa a primeira linha como nomes de coluna.
- **Import CSV…** — `.csv` / `.tsv` / `.txt`, delimitador detectado sozinho (inclusive ponto e vírgula, como o Excel brasileiro escreve).
- **Editar na grade** — clique numa célula; **Add row / column**; o menu **⋯** do cabeçalho insere, move, renomeia e apaga. `Ctrl+Z` desfaz.
- **Copy table (TSV)** devolve tudo para o clipboard.

**Cabeçalhos → tokens**

| Token | Resolve para |
| --- | --- |
| `{row:coluna}` | O valor da linha **atual** — a *mesma* linha para todas as ações da execução. |
| `{rownext:coluna}` | A **próxima** linha a cada uso. Reinicia a cada execução; passou da última, sai vazio. |
| `{row}` | O número da linha **da ação na grade** — não tem relação com a tabela. |

> **A diferença que importa.** Use `{row:col}` quando cada execução preenche **um registro** (várias colunas, mesma linha) — é o par natural do Loop over data. Use `{rownext:col}` para despejar a **lista inteira** numa passada: três `Send Text` com `{rownext:nome}` digitam as linhas 1, 2 e 3 seguidas.

Cabeçalhos precisam ter só letras, números ou `_`. Um inválido ganha ⚠; a **varinha** conserta. Célula vazia ou coluna inexistente vira **texto vazio**, nunca erro.

**Executando**

| Modo | Comportamento |
| --- | --- |
| **Loop over data ligado** | Uma execução completa **por linha**. Ignora os Loops do perfil e o infinito de While-Pressed/Toggle. **Não inicia** com a tabela vazia. |
| **Desligado** (cursor) | Cada execução usa a **próxima** linha e avança; no fim volta à primeira. Botão direito → **Reset row position**. |

**On row error** *(só com o loop ligado)* — **Halt** (padrão) para na primeira falha; **Skip row** registra, solta o que ficou pressionado e continua, com um resumo no fim.

> **O lugar é guardado em disco.** O cursor de linha — e o do **Set Variable** em modo Cycle — sobrevive a fechar o app. Trabalhe 12 linhas hoje e amanhã continue da 13.

### Exemplo — cadastrar 40 produtos num formulário

1. **Monte a macro para UM produto**, digitando de verdade. Teste até rodar certo. Esse é o molde.
2. **Data Loop** → **Paste / bulk edit…** → cole do Excel com **First row is the header**:

   | product | price |
   | --- | --- |
   | Cabo HDMI 2m | 39,90 |
   | Mouse sem fio | 89,00 |

3. **Troque os valores fixos pelos tokens.** No painel **Columns · tokens**, clique no chip `{row:product}` para copiar e cole no lugar do texto fixo. Confira: cada coluna deve mostrar `×1` em vez de *unused*.
4. **Ligue Loop over data**, ponha **On row error** = **Skip row**, **Save**.

Uma hotkey cadastra a planilha inteira.

> **Cadastrou só um produto?** **Loop over data** está desmarcado — é o modo cursor, que anda uma linha por execução. Ligado, o painel mostra *"N iterations"* e aparece o **On row error**.

### Rodar um sub-perfil uma vez por linha

Uma ação **Run Profile** pode marcar **Run once per data row**: o perfil *chamado* roda uma vez por linha da tabela **dele**. Assim a macro pai faz o setup uma vez e processa um lote no meio da execução. Ligar isso esmaece o **Repeat**.

> **O sub-perfil não manda na própria repetição.** Os Loops e o Interval dele são ignorados quando é chamado — vale só o **Repeat** do diálogo Run Profile.
>
> Um perfil não pode chamar a si mesmo, e a cadeia para em 5 níveis. Nesses casos a ação é **pulada sem aviso na tela** — fica só no log da sessão.
>
> **Perfil não aparece na lista Profile to run?** Ele está **desligado**. Perfis desligados somem da escolha porque seriam pulados de qualquer jeito.

---

## Automação de navegador

Controla o Chrome por **seletor CSS** em vez de coordenadas. Requer a **extensão TrueReplayer** conectada — veja o [guia de instalação](extension-setup/README.md).

| Ação | O que faz |
| --- | --- |
| **Browser Click / Right Click** | Clica por seletor ou pelo **texto** visível. |
| **Browser Type** | Digita num campo, com os mesmos tokens do Send Text. |
| **Navigate** | Abre uma URL; opcionalmente espera a URL casar ou um elemento aparecer. |
| **Wait Element** | Espera um elemento aparecer (ou sumir). |
| **Assert Element** | Confere o estado e **para** se não estiver como esperado. É guarda, não espera. |
| **Select Option** | Escolhe num `<select>` por texto, valor ou índice. |

Um selo de **qualidade do seletor** (S → C) indica quão estável ele provavelmente será.

> **Em qual aba a macro age.** Na que estava na frente **quando a execução começou**, e fica ali até o fim. Trocar de aba no meio **não leva a macro junto**. Um **Navigate** re-fixa na página que abriu. Se a aba original for fechada, a macro para dizendo isso (`TAB_GONE`) em vez de agir em silêncio noutro lugar.
>
> **Mirando por texto**, o alvo é o **elemento clicável** que carrega o texto — o botão inteiro, não o `<span>` de dentro. No campo de texto, um padrão **sem prefixo** vale como **exato**. Para casar um pedaço: `text*=Salvar` (contém), `text~=salvar` (ignora maiúsculas), `text/^Salvar.*/i` (regex).

**Relatório de execução** — `Ctrl+K` → **Run report** mostra a execução passo a passo, com o que cada um mirou e quanto levou.

<p align="center">
  <img src="img/run-report.png" width="820" alt="O painel Run report" /><br>
  <sub><i>Cada passo, o que mirou e quanto levou.</i></sub>
</p>

Duas coisas que só o relatório mostra:

- **Casou por reserva** — o seletor que *você* escolheu já não casa; a macro está a uma mudança do site de parar. Um passo que **passou** pode trazer esse aviso, e é a hora de re-escolher o elemento.
- **Por que falhou, em texto** — não achou, achou mas invisível, achou mas desabilitado, tem algo por cima, seletor inválido, página não carregou.

> É só a **última** execução: cada nova substitui a anterior e fechar o app descarta. Para registro que dura, use o log (bandeja → **Open Logs Folder**).

---

## Temas e aparência

**Settings → App → Interface → Customise.**

<p align="center">
  <img src="img/theme.png" width="820" alt="A galeria de presets do Theme Editor" /><br>
  <sub><i>37 presets, com prévia ao vivo.</i></sub>
</p>

- **Gallery** — 37 presets por matiz (23 escuros + 14 claros), com busca. Padrão *Lavender Coal*.
- **Customise → Colors** — 29 cores em 6 grupos, via seletor, hex ou HSL, com verificador de contraste.
- **Customise → Interface** — presets de **Density**; ajustes de **Font Size**, **Border Radius**, **Row Height**, **Zoom**; fonte **Monospace**; **Match Windows theme**; **Enable animations**.
- **Import / Export** — compartilhe um tema como JSON.

<p align="center">
  <img src="img/theme-interface.png" width="360" alt="A aba Interface do Theme Editor" /><br>
  <sub><i>Densidade, fonte, cantos, altura de linha e zoom.</i></sub>
</p>

---

## Referência de configurações

Três abas, tudo **salvo automaticamente**.

**Profile** *(por perfil / modo)*
- **Execution** — Delay, Loops, Interval, Jitter. **Loops e Interval** ficam no perfil (`Ctrl+S`); Delay e Jitter valem para o app.
- **Game Mode** — o cabeçalho é o interruptor mestre.
- **Recording** — os filtros de captura, a chave **Profile Keys** e **Browser Actions**.
- **Clicker** — substitui os grupos acima no Clicker mode.

**Keys** *(tudo que intercepta tecla)*
- **Hotkeys** — Record `Ctrl+PageUp` · Replay `Ctrl+PageDown` · Profile-keys `Pause` · Foreground `Insert` · Mode `ScrollLock` · Capture Slot `Win+Ctrl+C`. Apague o campo para desativar.
- **Clicker** — Start/Pause (`PageDown` / `PageUp`), só no Clicker mode.
- **Key Remaps** — a camada sempre ativa.

**App** *(todo o aplicativo)*
- **Window** — Always On Top, System Tray.
- **Startup** — Run on Startup, Startup Minimized, Run as Administrator.
- **Notifications** — flash / som quando um replay termina em segundo plano.
- **Automation** — a chave-mestra + o botão do painel.
- **Interface** — Theme Editor e o idioma das dicas (**Português (BR)** ou English; nomes e menus seguem em inglês).
- O rodapé mostra a versão e um **Check for Updates** manual.

---

## Onde seus dados ficam

| O quê | Onde |
| --- | --- |
| **Perfis** | `Documents\TrueReplayer\Profiles\*.json` |
| **Onde cada lista parou** | `Documents\TrueReplayer\run-cursors.json` — cursor do Data Loop e do Set Variable em Cycle. Apagar (com o app fechado) faz todas recomeçarem. |
| **Histórico das automações** | `Documents\TrueReplayer\automation-stats.json` — disparos, últimos horários e pulos. Apagar zera. |
| **Configurações** | `appsettings.json` |
| **Imagens, temas, WebView2** | `%LocalAppData%\TrueReplayer\…` — fixados aqui para **sobreviverem às atualizações**. |

---

## Solução de problemas

**Uma hotkey não dispara.**
Confira: o **alvo de janela** casa com o app em foco; a chave **Profile Keys** (`Pause`) está ligada; o perfil não está desabilitado; e se o app alvo roda como administrador, o TrueReplayer também precisa rodar.

**Os cliques caem no lugar errado depois que a janela se moveu.**
Ligue **alvo de janela** + **Relative Coordinates** e faça **Convert to Relative**.

**Os cliques disparam duas vezes.**
**Focus-click** está ligado nessas linhas. Desligue — ele só serve para campos de texto pequenos, nunca para botões.

**Um jogo ignora os cliques.**
Mantenha o **Game mode** ligado. Se ainda errar, desligue o **Fast approach** ou reduza o **Path step**.

**Minha automação nunca dispara.**
Salvar não arma: ligue a chave **Armed**. Confira a chave-mestra, e lembre que um disparo é pulado enquanto um replay roda, um diálogo está aberto ou a grade tem edições não salvas. Use o **Run now** para ver o motivo.

**Um sub-perfil ignora os próprios Loops.**
É de propósito: vale só o **Repeat** do diálogo Run Profile.

**Um passo gravado foi para o lugar errado.**
A gravação insere **antes da primeira linha selecionada**. Limpe a seleção para acrescentar no fim.

**Um token não digitou nada.**
Ele resolveu para vazio — coluna inexistente, variável nunca definida. `Ctrl+K` → **Toggle Live Variables** e rode de novo. Se for `{clipboard:next}`, a lista provavelmente **acabou**: copie de novo e ele recomeça na linha 1.

**Uma transformação devolveu vazio.**
Se for `before`/`after`, o delimitador não existe no texto — é de propósito. Se for `words:` ou `line:`, o número passou do fim. A prévia do construtor mostra o resultado real antes de você salvar.

**A macro parou com `Assert failed`.**
Fez o que você mandou. O nome entre aspas é o **Notes** daquela linha. Se a premissa só demora, aumente o **Wait for condition** em vez de tirar o Assert.

**A lista não recomeçou do início.**
É de propósito: os cursores são guardados em disco. Botão direito → **Reset row position** / **Reset cycle position**.

**A interface não carrega.**
Instale o [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/).

---

<div align="center">

[← Voltar ao README](../README.md)

</div>

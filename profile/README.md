## 💻 SAP Microcontroller Simulator

Um simulador interativo construído em **Flutter** que emula o funcionamento básico de um microcontrolador **SAP (Simple As Possible)**.
Este aplicativo permite aos usuários escrever código assembly simples, compilá-lo e observar a execução passo a passo ou automaticamente, visualizando as mudanças nos registradores, memória e flags.

---

## ✨ Visão Geral

Este projeto oferece uma ferramenta educacional para entender a arquitetura de computadores e o ciclo de instrução de uma CPU de forma prática e visual.
Com uma interface de usuário intuitiva e animada, o simulador torna o aprendizado sobre o processamento de instruções e o fluxo de dados em um microcontrolador muito mais acessível.

---

## 👩 Integrantes
- Barbára Marcella Inácio da Silva
- Igor Vidal Meneghini
- Isabela Demaria Costa Braga
- Sofia Melo do Prado Rocha Duque

  ---

## 🚀 Funcionalidades Principais

- **Editor de Código Assembly**: Escreva seu próprio código assembly SAP diretamente no aplicativo.
- **Compilador Integrado**: Converte o código assembly em instruções executáveis, com validação básica de sintaxe e operandos.
- **Execução Passo a Passo**: Avance uma instrução por vez para observar detalhadamente o impacto em cada componente do microcontrolador.
- **Modo de Execução Contínua**: Execute o programa automaticamente para ver o resultado final mais rapidamente.
- **Visualização de Registradores**:
- `PC` (Program Counter)
- `IR` (Instruction Register)
- `MAR` (Memory Address Register)
- `MDR` (Memory Data Register)
- `ACC` (Accumulator)
- `OUT` (Output Register)
- **Unidade Lógica Aritmética (ULA/ALU)**: Destaque visual durante operações como `ADD` e `SUB`.
- **Memória RAM**: Visualização de 16 posições de memória, com destaque para endereços acessados.
- **Flags de Estado**: `Carry Flag` e `Zero Flag`, indicando resultados de operações aritméticas.
- **Console de Log**: Mensagens da simulação e saída da instrução `OUT`.
- **Animações e Destaques Visuais**: Blocos funcionais e endereços de memória se acendem conforme a execução.
- **Tela de Boas-Vindas (Splash Screen)**: Tela inicial estilosa com gradiente e botão para iniciar a simulação.
- **Design Responsivo**: Compatível com desktop, tablet e mobile.

---

## 🖥️ Instruções Suportadas (Assembly SAP)

| Instrução | Descrição | Exemplo |
|--------------|---------------------------------------------------------------------------|----------|
| `LDA <addr>` | Load Accumulator: Carrega o valor da memória `<addr>` no registrador ACC | LDA 14 |
| `ADD <addr>` | Soma o valor da memória `<addr>` ao ACC (Define Carry e Zero Flags) | ADD 15 |
| `SUB <addr>` | Subtrai valor da memória `<addr>` do ACC (Define Carry e Zero Flags) | SUB 10 |
| `STA <addr>` | Armazena o valor do ACC na memória `<addr>` | STA 0 |
| `JMP <addr>` | Altera o PC para `<addr>` (salto incondicional) | JMP 0 |
| `OUT` | Copia o valor de ACC para OUT e exibe no console de log | OUT |
| `HLT` | Interrompe a execução | HLT |

- **Comentários**: Linhas que começam com `//` ou contêm `//` após a instrução são ignoradas.
- **Dados**: Números sem opcode são interpretados como dados e carregados na memória.

---

## ⚙️ Como o Código Funciona

O aplicativo é desenvolvido em **Flutter**, utilizando **Dart**. A estrutura do código é modular e segue boas práticas do framework.

### 📁 Estrutura do Projeto

- `main.dart`: Ponto de entrada principal do aplicativo.
- `lib/`: Contém todo o código-fonte.
- `SAPSimulatorApp`: Widget raiz com tema global e navegação inicial.
- `SplashScreen`: Tela de boas-vindas com botão de iniciar simulação.
- `SAPHomePage`: Interface principal com lógica de emulação, editor, registradores e log.
- `ParsedInstruction`: Classe para representar instruções compiladas (`opcode` e `operand`).

---

### 🧠 Componentes Chave e Lógica

#### `SAPSimulatorApp` (Theme and Fonts)

- Define tema visual com `Colors.teal` e `Colors.deepPurple`
- Integra `google_fonts` (Source Code Pro)
- Estiliza `AppBar`, `Buttons`, `Cards`, `InputDecoration`

#### `SplashScreen` (Initial User Experience)

- Gradiente de fundo com título e descrição
- Botão “Iniciar” com navegação para `SAPHomePage`

#### `SAPHomePage` (Simulation Core)

- Estado do Microcontrolador:
- `_pc`, `_acc`, `_mar`, `_mdr`, `_out`, `_memory`, `_carryFlag`, `_zeroFlag`, `_isHalted`
- `_editorController`: Gerencia o texto do editor (com código de exemplo)
- `_compileCode()`:
- Analisa linhas do editor
- Converte para `ParsedInstruction`
- Valida sintaxe e operandos
- Simula tempo de compilação com `Future.delayed`

- `_executeStep()`:
- Executa instrução baseada em `_pc`
- Switch com lógica de cada `opcode`
- Atualiza registradores, memória e flags
- Anima interface e adiciona logs

- `_reset()`: Reinicia estado do simulador
- `_toggleRun()`: Executa o programa automaticamente
- `_sapBlock()`: Widget reutilizável para mostrar registradores com animações
- `_buildInstructionLine()`: Renderiza linha da instrução destacada
- Diálogos: `_showInfoDialogBlocks()` e `_showInfoDialogAbout()`

---

## 🎨 Estilização e Design

- **Paleta de Cores**: `teal` e `deepPurple` para visual moderno
- **Tipografia**: `Source Code Pro` (Google Fonts)
- **Animações**:
- `AnimatedContainer`
- `AnimatedSwitcher`
- `AnimatedOpacity`
- **Elementos Visuais**:
- Cartões (`Card`) com elevação e cantos arredondados
- Gradientes estilizados em botões e splash screen

---

## 📹 Vídeo Demonstrativo

<p align="center">
	<a href="https://youtube.com/shorts/TubGbwAnDkA?si=45Jl4ZbDBZQUlAhz">  <img src="https://raw.githubusercontent.com/isabeladcb/.github/main/imagens/logotipoSAP.jpeg" width="500" alt="Logotipo do Simulador SAP">
	</a>
</p>

---

> Projeto desenvolvido para **arquitetura de computadores I**.

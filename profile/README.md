💻 SAP Microcontroller Simulator

Um simulador interativo construído em Flutter que emula o funcionamento básico de um microcontrolador SAP (Simple As Possible). Este aplicativo permite aos usuários escrever código assembly simples, compilá-lo e observar a execução passo a passo ou automaticamente, visualizando as mudanças nos registradores, memória e flags.

✨ Visão Geral

Este projeto oferece uma ferramenta educacional para entender a arquitetura de computadores e o ciclo de instrução de uma CPU de forma prática e visual. Com uma interface de usuário intuitiva e animada, o simulador torna o aprendizado sobre o processamento de instruções e o fluxo de dados em um microcontrolador muito mais acessível.

🚀 Funcionalidades Principais

Editor de Código Assembly: Escreva seu próprio código assembly SAP diretamente no aplicativo.
Compilador Integrado: Converte o código assembly em instruções executáveis, com validação básica de sintaxe e operandos.
Execução Passo a Passo: Avance uma instrução por vez para observar detalhadamente o impacto em cada componente do microcontrolador.
Modo de Execução Contínua: Execute o programa automaticamente para ver o resultado final mais rapidamente.
Visualização de Registradores: Monitore em tempo real os valores de registradores cruciais como:
PC (Program Counter)
IR (Instruction Register)
MAR (Memory Address Register)
MDR (Memory Data Register)
ACC (Accumulator)
OUT (Output Register)
Unidade Lógica Aritmética (ULA/ALU): Destaque visual da ULA durante operações como ADD e SUB.
Memória RAM: Visualize o conteúdo de 16 posições de memória, com destaque para endereços acessados.
Flags de Estado: Observe o Carry Flag e o Zero Flag que indicam o resultado de operações aritméticas.
Console de Log: Um console integrado exibe mensagens de simulação e a saída da instrução OUT.
Animações e Destaques Visuais: Elementos da interface se acendem para indicar qual bloco funcional ou posição de memória está ativo durante a execução.
Tela de Boas-Vindas (Splash Screen): Uma tela inicial estilosa com gradiente e um botão para iniciar a simulação.
Design Responsivo: Interface otimizada para diferentes tamanhos de tela (desktop, tablet, mobile).

🖥️ Instruções Suportadas (Assembly SAP)

O simulador suporta um conjunto simplificado de instruções assembly, perfeito para fins didáticos:
| Instrução | Descrição | Exemplo |
| LDA <addr> | Load Accumulator: Carrega o valor da posição de memória <addr> no registrador ACC. | LDA 14 |
| ADD <addr> | Add: Adiciona o valor da posição de memória <addr> ao ACC. Define Carry Flag e Zero Flag. | ADD 15 |
| SUB <addr> | Subtract: Subtrai o valor da posição de memória <addr> do ACC. Define Carry Flag (borrow) e Zero Flag. | SUB 10 |
| STA <addr> | Store Accumulator: Armazena o valor do ACC na posição de memória <addr>. | STA 0 |
| JMP <addr> | Jump: Altera o PC para o endereço <addr>, realizando um salto incondicional no programa. | JMP 0 |
| OUT | Output: Copia o valor atual do ACC para o registrador OUT e o exibe no console de log. | OUT |
| HLT | Halt: Interrompe a execução do programa. | HLT |
Comentários: Linhas que começam com // ou que contêm // após a instrução são ignoradas (comentários).
Dados: Números sem opcode no início da linha são interpretados como dados e carregados sequencialmente na memória após as instruções.

⚙️ Como o Código Funciona

O aplicativo é desenvolvido em Flutter, utilizando a linguagem Dart. A estrutura do código é modular e segue as boas práticas do framework.
Estrutura do Projeto
main.dart: O ponto de entrada principal do aplicativo.
lib/: Contém todo o código-fonte Dart.
SAPSimulatorApp: O widget raiz que define o tema global do aplicativo e a navegação inicial para a SplashScreen.
SplashScreen: A tela de boas-vindas inicial que introduz o simulador e permite ao usuário prosseguir para a página principal.
SAPHomePage: O coração do simulador, contendo a lógica de emulação, a interface do usuário para o editor de código, os painéis de registradores e memória, e o console de log.
ParsedInstruction: Uma classe auxiliar simples para representar uma instrução assembly após a compilação, contendo o opcode e o operand (se aplicável).
Componentes Chave e Lógica
SAPSimulatorApp (Theme and Fonts):
Define um tema visual coeso usando ThemeData, com Colors.teal e Colors.deepPurple para uma paleta vibrante.
Integra google_fonts (especificamente Source Code Pro) para garantir uma tipografia adequada para um editor de código e console.
Configura estilos para AppBar, ElevatedButton, OutlinedButton, Card e InputDecoration para uma experiência de usuário consistente e agradável.
SplashScreen (Initial User Experience):
Apresenta um gradiente de fundo chamativo (LinearGradient).
Exibe o título do simulador e uma breve descrição.
Um botão "Iniciar" estilizado com gradiente permite ao usuário navegar para a SAPHomePage, controlando o início da experiência do simulador.
SAPHomePage (Simulation Core):
Estado do Microcontrolador: Variáveis de estado (_pc, _acc, _mar, _mdr, _out, _memory, _carryFlag, _zeroFlag, _isHalted) mantêm o estado atual do simulador.
_editorController: Gerencia o texto dentro do editor de código, pré-preenchido com um exemplo didático.
_compileCode():
Analisa cada linha do _editorController.text.
Diferencia instruções assembly de valores de dados numéricos.
Converte as instruções em objetos ParsedInstruction.
Preenche a _memory com os dados fornecidos.
Realiza validações básicas (e.g., operando presente para LDA, endereço dentro dos limites da memória) e exibe _showErrorDialog em caso de erros de compilação.
Inclui um Future.delayed para simular um tempo de compilação, com um indicador visual (_isCompiling).
_executeStep():
É a função principal de execução do ciclo de instrução.
Pega a instrução atual baseada no _pc.
Usa um switch para executar a lógica correspondente a cada opcode (e.g., LDA, ADD, JMP).
Atualiza os registradores, a memória e as flags conforme a instrução é processada.
Future.delayed é usado entre as etapas para criar um efeito de animação, permitindo que o usuário visualize o fluxo de dados.
Atualiza _highlightedInstructionIndex e _highlightedBlock para animar a interface.
Adiciona mensagens ao _logMessages para o console de saída.
Lida com a instrução HLT e o fim das instruções.
_reset(): Reinicia todos os registradores, memória e flags para seus valores iniciais. Também usa Future.delayed para um efeito visual de carregamento.
_toggleRun(): Controla o modo de execução contínua, chamando _executeStep recursivamente com atrasos.
_sapBlock(): Um widget reutilizável que exibe o nome e o valor de um registrador ou bloco funcional. Ele inclui lógica de animação (AnimatedContainer, AnimatedSwitcher) para destacar o bloco ativo.
_buildInstructionLine(): Renderiza cada linha de instrução compilada, destacando a instrução atualmente em execução.
Diálogos Informativos: _showInfoDialogBlocks() e _showInfoDialogAbout() fornecem informações úteis sobre os blocos funcionais e o simulador.

🎨 Estilização e Design

O aplicativo emprega um design limpo e funcional com ênfase na clareza visual para a simulação:
Paleta de Cores: Combinação de tons de teal e deepPurple para um visual moderno e educacional.
Tipografia: Source Code Pro da Google Fonts é usado para o texto principal, garantindo alta legibilidade para o código e os valores numéricos.
Animações: AnimatedContainer, AnimatedSwitcher e AnimatedOpacity são empregados para criar transições suaves e destaques visuais que guiam o usuário através do ciclo de execução.
Sombras e Arredondamento: Card e Button com elevação e cantos arredondados proporcionam uma sensação de profundidade e polimento.
Gradientes: Utilizados na SplashScreen e nos botões para um toque estético.

🛠️ Como Executar o Projeto

Para configurar e executar este projeto em sua máquina local, siga os passos abaixo:
Pré-requisitos
Flutter SDK: Certifique-se de ter o Flutter SDK instalado. Se não tiver, siga as instruções em flutter.dev/docs/get-started/install.
Editor de Código: Um editor como VS Code ou Android Studio com os plugins Flutter e Dart instalados.
Passos de Instalação
Clone o Repositório:
git clone https://github.com/Simulador-SAP
cd sap_microcontroller_simulator # Ou o nome da pasta do seu projeto

Instale as Dependências:
No diretório raiz do projeto, execute:
flutter pub get


Isso baixará todas as dependências, incluindo o pacote google_fonts.
Verifique o pubspec.yaml:
Certifique-se de que a seguinte dependência está listada em seu arquivo pubspec.yaml:
dependencies:
  flutter:
    sdk: flutter
  google_fonts: ^6.2.1 # Verifique a versão mais recente em pub.dev


E que os assets (se houver, como assets/pc.png no seu código) estão declarados:
flutter:
  uses-material-design: true
  assets:
    - assets/


Você precisará ter uma pasta assets na raiz do seu projeto e dentro dela o arquivo pc.png (ou qualquer outro asset de imagem que esteja sendo usado, embora o imagePath esteja comentado em _sapBlock na parte final do seu código, então pode ser que não seja necessário se o imagePath não for ativado).
Execute o Aplicativo:
Conecte um dispositivo Android ou iOS, ou inicie um emulador. Em seguida, execute o aplicativo:
flutter run


Ou inicie diretamente do seu IDE (VS Code: F5, Android Studio: botão "Run").

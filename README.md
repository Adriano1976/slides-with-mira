# Deck: Agent Skills (Mira Framework)

## 📌 Visão Geral
Este repositório contém a implementação do deck de apresentação "Agent Skills", construído sobre a engine do **Mira Framework**. O projeto traduz conceitos complexos de Engenharia de Agentes (como Skills, MCP, Hooks e ambientes virtuais) em 10 metáforas visuais animadas. 

O foco da arquitetura está na renderização de loops de animação vetorial perpétuos de alta performance, gerenciamento estrito de ciclo de vida do DOM e prevenção de vazamento de memória (memory leaks) durante a navegação do usuário.

## 🏗️ Arquitetura e Especificações Técnicas

A implementação técnica segue rigorosamente os padrões das skills `mira-animator` e `mira-animated-metaphor`, utilizando **HTML5**, **CSS3 (Variáveis)**, **D3.js** e **Lucide Icons**.

### Gerenciamento de Memória e Ciclo de Vida (Anti-Leak)
Como as animações em D3.js operam em loops contínuos (ad infinitum), o projeto implementa um controle rigoroso de estado para evitar degradação de performance:
* **Garbage Collection Ativo:** Utilização do objeto global `window.__animRegistry` para registrar instâncias ativas.
* **Generation Counters:** Cada slide utiliza um contador de geração (`window.__slugGen`) e `clearInterval()` no bootstrap da animação para garantir que instâncias anteriores sejam destruídas antes da nova renderização.
* **Viewport Handling:** Integração com a API nativa `IntersectionObserver` da IDE. A renderização (ou suspensão) do palco isolado ocorre dinamicamente conforme o card entra ou sai da área visível da tela.

### Renderização e Responsividade
* **Escala Vetorial Fixa:** Todos os componentes SVG operam com o atributo `viewBox="0 0 1280 720"`, garantindo proporção unificada (16:9).
* **Preenchimento Dinâmico:** Os gráficos preenchem responsivamente a `div` de contenção `.anim-stage`, que possui a diretiva `clamp` para delimitação de tamanho.
* **Tagging de Metadados:** Cada slide é estritamente demarcado no código com os marcadores de tamanho da engine (ex: `<!-- @MIRA:SIZE 3/10 -->`).

### Design System e Tematização
O projeto proíbe o uso de cores em *hardcode* (como `#FF0000`).
* A injeção de estilo é controlada pelo bloco `@MIRA:THEME`.
* O esquema de cores obedece exclusivamente à paleta semântica do tema `mira-dark`, utilizando variáveis CSS globais como `PRIMARY` e `ACCENT2`.
* Geração dinâmica de ícones SVG no carregamento (`init`) e eventos de scroll via `lucide.createIcons()`.

## 🧠 Mapeamento de Domínio (As 10 Metáforas)

O core business da apresentação mapeia os seguintes conceitos de arquitetura de agentes para loops em D3.js:

1. **Chatbot vs Agente Autônomo:** Modelo reativo (Máquina de venda) vs. Loop de Percepção-Ação (Robô aspirador em trajetória de Lissajous).
2. **Definição de Skill:** Acoplamento de módulos autônomos (Cartucho descendo em um slot com transferência de dados em onda).
3. **Skill vs MCP:** Processamento interno vs. Acesso externo (Sinapses orbitais vs. Chave destrancando porta).
4. **Frontmatter & Trigger (YAML):** Gatilhos de execução (Alarme de incêndio com propagação de ondas concêntricas).
5. **Contexto e Regras de Segurança:** Boundary testing e limites (Radar de varredura 360° em um mapa delimitado por cerca elétrica reativa).
6. **Fluxo de Execução:** Pipelines passo a passo (Esteira de montagem com braços mecânicos alterando propriedades de estado da peça).
7. **Construct / Ambientes Virtuais (.venv):** Isolamento de processos (Câmara hermética contendo reações, imune a colisões/exceções externas).
8. **PreToolUse Hooks:** Validação de segurança pré-execução (Cancela bloqueando um node/carro com onda de impacto ao detectar estado inválido).
9. **PostToolUse Hooks:** Validação e parsing de output (Inspetor de qualidade carimbando blocos na saída do pipeline).
10. **O Novo Operador (Desenvolvedor):** Orquestração de múltiplos agentes (Maestro regendo 15 nós divididos por responsabilidades em arcos concêntricos, reagindo a pulsos de dados com figurações em 8).

## 🎮 UI/UX e Navegação

A interface possui suporte completo a atalhos de teclado para controle da apresentação:
* **Avançar/Recuar:** Setas Direcionais (Up/Down, Left/Right), `PageUp` e `PageDown`.
* **Extremos:** Teclas `Home` e `End`.
* **Display:** Tecla `F` (Aciona a API de Fullscreen).
* **Controles Interativos:** Os cards contam com cabeçalhos estruturados, pílulas de atributos no rodapé, botões flutuantes dinâmicos (`#mira-next`) e botões nativos de "Replay" que reinjetam o ciclo de vida do D3.

## 🚀 Como Executar

O projeto não requer processos complexos de build, pois compila diretamente pelo navegador.
1. Clone o repositório.
2. Abra o arquivo `index.html` em qualquer navegador web moderno com suporte a ES6 e SVG.

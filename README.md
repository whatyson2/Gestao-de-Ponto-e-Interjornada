# ⏱️ Gestão de Ponto & Controle de Interjornada (CLT)

Aplicação web estática, responsiva e **100% offline** (zero dependências externas ou CDNs) desenvolvida para controle de jornada de trabalho padrão de **8 horas e 48 minutos** (regime de compensação semanal de 44h) e apuração legal do intervalo **Interjornada mínimo de 11 horas consecutivas** (Artigo 66 da CLT).

---

## 🎯 Visão Geral

Desenvolvido para atender às necessidades de colaboradores e gestores operacionais que precisam auditar com precisão o cumprimento das marcações de ponto, prevenindo horas extras involuntárias e passivos trabalhistas decorrentes da violação do descanso entre turnos consecutivos.

O projeto foi construído sob o princípio de **autonomia total**: funciona sem internet, sem compilação, sem `node_modules` e sem conexões com bibliotecas de terceiros.

---

## 🚀 Funcionalidades Principais

### 1. Calculadora de Ponto (8h48)
- **Dois Modos de Apuração:**
  - **Entrada + Duração de Intervalo:** Entrada rápida com seletor e atalhos de pausa pré-definidos (`1h00`, `1h15`, `1h30`, `2h00`) ou inserção livre em minutos.
  - **Registro de 4 Batidas:** Apuração automática do tempo efetivo despendido no almoço ($Batida_3 - Batida_2$) com projeção do minuto exato da 4ª batida.
- **Métricas Instantâneas:** Exibição clara da jornada de trabalho líquida (`08:48`), tempo de pausa e tempo total de permanência.
- **Acompanhamento ao Vivo:**
  - Relógio digital integrado sincronizado com o horário local.
  - Barra de progresso dinâmica com percentual de turno concluído, tempo decorrido e contagem regressiva para o encerramento.
- **Cópia Rápida:** Botão para transferir o horário calculado para a área de transferência com feedback visual (*Toast*).

### 2. Módulo Dedicado de Interjornada (Art. 66 CLT)
- **Isolamento de Operação:** Aba exclusiva para não misturar os dados operacionais do dia com o histórico do turno anterior.
- **Horário Mínimo Exigido:** Cartão em destaque indicando a hora exata mais cedo em que o colaborador pode bater a entrada sem violar o descanso.
- **Simulador de Entrada:** Campo interativo para prever um horário pretendido de início no dia seguinte.
- **Auditoria de Conformidade em Cores:**
  - 🟢 **Verde (Conforme):** Indica descanso regular e contabiliza as horas de intervalo cumpridas (ex.: `14h00`).
  - 🔴 **Vermelho (Violação):** Emite alerta imediato caso o intervalo seja inferior a 11 horas, calculando exatamente quantos minutos/horas faltam para atingir o limite legal.
- **Sincronização com 1 Clique:** Botão que transporta o horário de entrada legalmente validado diretamente para a calculadora de jornada.

---

## 📐 Regras de Negócio e Cálculos

### 1. Cálculo de Saída (8h48 Líquidas)

A jornada líquida é fixada em **528 minutos** ($8 \times 60 + 48$).

$$\text{Horário de Saída} = \text{Minutos de Entrada} + \text{Duração do Intervalo} + 528\text{ min}$$

*Exemplo prático:*
- Entrada: `08:00` (480 min)
- Intervalo: `1h00` (60 min)
- Total de minutos: $480 + 60 + 528 = 1068\text{ min} \rightarrow \mathbf{17:48}$

### 2. Módulo de Interjornada (Art. 66 da CLT)

Conforme o **Artigo 66 da CLT** e a **Súmula 110 do TST**, deve haver um intervalo ininterrupto de no mínimo **11 horas consecutivas** (660 minutos) entre o término de uma jornada e o início da seguinte.

$$\text{Entrada Mínima Permitida} = (\text{Saída do Dia Anterior} + 660\text{ min}) \pmod{1440}$$

$$\text{Descanso Real} = (\text{Entrada Hoje} - \text{Saída Anterior} + 1440) \pmod{1440}$$

$$\text{Status} = 
\begin{cases} 
\text{Conforme}, & \text{se Descanso Real} \ge 660 \\ 
\text{Violação da CLT}, & \text{se Descanso Real} < 660 
\end{cases}$$

---

## 🛠️ Arquitetura e Filosofia Técnica

- **Zero Dependências:** Construído unicamente com **HTML5, CSS3 nativo e Vanilla JavaScript**. Não utiliza Tailwind CDN, Bootstrap, FontAwesome ou bibliotecas externas de parsing.
- **Resiliência a Falhas de Rede:** Todas as fontes e propriedades visuais usam a pilha nativa do sistema operacional (`-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, etc.).
- **Suporte a Dark Mode:** Adaptação automática às preferências do sistema operacional (`@media (prefers-color-scheme: dark)`).
- **Tratamento de Virada de Dia:** A aritmética de minutos modular trata nativamente eventos que ultrapassam a meia-noite (23:59 $\rightarrow$ 00:00).

---

## 💻 Como Executar Localmente

Você não precisa de Node.js, servidores locais ou qualquer instalação de pacotes:

1. Clone o repositório ou faça download do arquivo `ponto_interjornada.html`:
   ```bash
   git clone https://github.com/SEU-USUARIO/Gestao-de-Ponto-e-Interjornada.git
   ```
2. Renomeie o arquivo para `index.html` caso queira usá-lo como raiz web.
3. Dê um duplo clique no arquivo `index.html` para abrir diretamente no navegador (Edge, Chrome, Firefox, Safari ou navegadores mobile), **inclusive com o dispositivo em modo avião ou sem acesso à internet**.

---

## 🌐 Como Publicar no GitHub Pages

Para disponibilizar a ferramenta online em seu domínio `github.io`:

1. No seu repositório no GitHub, certifique-se de que o arquivo principal esteja na raiz com o nome **`index.html`**.
2. No menu superior do repositório, clique em **Settings** (Configurações).
3. Na barra lateral esquerda, acesse a seção **Pages**.
4. Em **Build and deployment** > **Source**, selecione `Deploy from a branch`.
5. Em **Branch**, selecione `main` (ou `master`) e mantenha a pasta como `/ (root)`.
6. Clique em **Save**.
7. Após 1 a 2 minutos, o GitHub disponibilizará o link público:
   ```text
   https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/
   ```

---

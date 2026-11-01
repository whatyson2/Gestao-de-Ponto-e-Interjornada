# ⏱️ Gestão de Ponto & Controle de Interjornada (CLT)

Aplicação web estática, responsiva e **100% offline** (zero dependências externas ou CDNs) desenvolvida para controle de jornada de trabalho com suporte nativo a três regimes de contratação:
* **44 horas semanais:** 8 horas e 48 minutos diárias (528 minutos líquidos)
* **40 horas semanais:** 8 horas diárias (480 minutos líquidos)
* **30 horas semanais:** 6 horas diárias (360 minutos líquidos)

Além do cálculo do turno, o sistema conta com um módulo exclusivo de auditoria e conformidade com o **Intervalo Interjornada de 11 horas consecutivas** (Artigo 66 da CLT).

---

## 🎯 Visão Geral
Desenvolvido para atender a colaboradores e gestores operacionais que precisam calcular horários de saída com precisão, registrar marcações de ponto e auditar descansos mínimos obrigatórios, prevenindo erros de marcação e passivos trabalhistas.

O aplicativo opera sob o princípio de **autonomia completa**:
* **Sem internet:** Não utiliza fontes do Google, CDNs externos (como Tailwind ou FontAwesome) nem bibliotecas externas.
* **Sem build/instalação:** Funciona abrindo diretamente o arquivo `index.html` em qualquer navegador moderno no PC ou smartphone.

---

## 🚀 Funcionalidades Principais

### 1. Seletor de Carga Horária Dinâmico
* **44h (8h48/dia):** Padrão de compensação de sábado (528 min).
* **40h (8h00/dia):** Jornada regular de 5 dias na semana (480 min).
* **30h (6h00/dia):** Jornada reduzida/estágio (360 min).
* Ao selecionar qualquer carga horária, todos os cálculos, cores de realce e métricas se ajustam em tempo real.

### 2. Calculadora de Ponto
* **Modo Entrada + Intervalo:** Atalhos rápidos de pausa (`15m`, `1h00`, `1h15`, `1h30`, `2h00`) e campo numérico livre.
* **Modo 4 Batidas:** Apura o tempo real do intervalo de almoço ($Batida_3 - Batida_2$) e define o horário exato da 4ª batida.
* **Painel de Métricas:** Mostra a jornada líquida, o intervalo total e a permanência no local de trabalho.
* **Acompanhamento em Tempo Real:** Relógio ao vivo, barra de progresso com percentual cumprido, tempo decorrido e contagem regressiva.
* **Cópia Rápida:** Botão para copiar o horário de saída diretamente para a área de transferência.

### 3. Módulo Exclusivo de Interjornada (Art. 66 CLT)
* **Entrada Mínima Permitida:** Calcula o horário mais cedo permitido para o colaborador bater o ponto no dia seguinte (+11 horas de descanso contínuo).
* **Simulador de Entrada:** Permite simular a hora prevista de entrada do dia seguinte.
* **Status em Cores:**
  * 🟢 **Conforme:** Sinaliza descanso regular e informa o total de horas descansadas (ex.: `14h00`).
  * 🔴 **Violação:** Emite alerta imediato caso o intervalo seja inferior a 11 horas, detalhando quantos minutos ou horas faltam para o descanso legal.
* **Sincronização com 1 Clique:** Envia o horário validado para a calculadora de jornada instantaneamente.

---

## 📐 Regras de Negócio e Cálculos

### 1. Cargas Horárias Suportadas

| Carga Semanal | Jornada Líquida Diária | Minutos Líquidos | Intervalo Típico |
| :--- | :--- | :--- | :--- |
| **44 horas** | **8h48** | 528 min | 1h00 a 2h00 |
| **40 horas** | **8h00** | 480 min | 1h00 a 2h00 |
| **30 horas** | **6h00** | 360 min | 15 min a 1h00 |

### 2. Cálculo de Saída e Turno
$$\text{Minutos de Saída} = \text{Entrada (min)} + \text{Intervalo (min)} + \text{Jornada Líquida (min)}$$

*Exemplos práticos:*
* **44h:** Entrada `08:00` + Intervalo `1h00` + 8h48 = Saída às **`17:48`**
* **40h:** Entrada `08:00` + Intervalo `1h00` + 8h00 = Saída às **`17:00`**
* **30h:** Entrada `08:00` + Intervalo `15m` + 6h00 = Saída às **`14:15`**

### 3. Auditoria de Interjornada (Art. 66 CLT)
$$\text{Entrada Mínima} = (\text{Saída Anterior} + 660\text{ min}) \pmod{1440}$$
$$\text{Descanso Realizado} = (\text{Entrada Hoje} - \text{Saída Anterior} + 1440) \pmod{1440}$$

---

## 💻 Como Executar Localmente
1. Baixe ou salve o arquivo `index.html`.
2. Dê um duplo clique no arquivo para abrir no navegador (Chrome, Edge, Safari, Firefox).
3. Funciona em qualquer dispositivo (computador, tablet ou celular), inclusive em **Modo Avião ou sem rede**.

---

## 🌐 Como Publicar no GitHub Pages
1. Suba o arquivo `index.html` e o `README.md` no seu repositório.
2. Acesse **Settings** > **Pages** no GitHub.
3. Em **Source**, escolha `Deploy from a branch` e selecione a branch `main` com pasta `/ (root)`.
4. O link público ficará ativo em `https://seu-usuario.github.io/nome-do-repositorio/`.


# Simulador-de-paginacao# 🧠 Simulador de Paginação

## 📘 Introdução
O **Simulador de Paginação** demonstra o funcionamento do gerenciamento de memória em sistemas operacionais, ilustrando como páginas de processos são movidas entre o **disco** e a **memória RAM** através da técnica de **paginação**.

---

## ⚙️ Estrutura da Interface

### 💾 Memória RAM
Representa os **quadros físicos** da memória principal. Cada quadro pode conter uma única página. Quando não há espaço livre, o simulador aplica o algoritmo **FIFO Second Chance** (segunda chance), que utiliza um bit de referência (R):

- Se R=1, a página recebe uma segunda chance (R é zerado e ela vai para o fim da fila).
- Se R=0, a página pode ser substituída.

Observação: ao carregar uma página do disco para a RAM, o bit R é definido aleatoriamente como 0 ou 1, e em cada acesso (HIT) o R da página acessada é definido como 1.

### 🧱 Disco (Memória Secundária)
Simula o **armazenamento em disco**, onde ficam as páginas que ainda não foram carregadas na RAM. As páginas são identificadas como `p0`, `p1`, `p2`, etc.

### 📄 Tabela de Páginas
Mapa que relaciona o **endereço lógico** de cada página ao **endereço físico** (quadro) onde ela está armazenada na RAM.

### 🪶 Log de Eventos
Exibe o histórico de operações:
- 🟩 **HIT:** página já presente na RAM.
- 🟥 **FALTA:** página não estava na RAM e foi carregada.
- 🟥 **Substituição Second Chance:** página com R=0 é removida; páginas com R=1 ganham segunda chance e voltam ao fim da fila.

### ▶️ Controles
- **Inicializar:** Reinicia o simulador.
- **Próximo passo:** Executa manualmente um ciclo de acesso.
- **Auto ▶:** Executa a sequência completa automaticamente.

---

## 🎯 Funcionamento Lógico

1. **Solicitação de página:** o sistema busca a página requerida.
2. **Se já estiver na RAM**, ocorre um **HIT** (sem movimentação).
3. **Se não estiver**, ocorre uma **falta de página**:
   - Se houver **quadro livre**, a página é **carregada do disco** (R aleatório 0/1).
   - Se não houver, aplica-se **FIFO Second Chance**: percorre a fila; páginas com R=1 recebem segunda chance (R→0), e substitui a primeira com R=0.

Durante o processo, **setas animadas** indicam o movimento:
- 🔻 **Verde:** Disco → RAM (carregamento)
- 🔺 **Vermelha:** RAM → Disco (substituição)

---

## 🧩 Conceitos Envolvidos

- **Paginação por demanda:** apenas as páginas necessárias são carregadas.  
- **Memória virtual:** permite que o processo seja maior que a RAM.  
- **Substituição FIFO:** remove a página mais antiga.  
- **Falta de página:** ocorre quando a página não está na RAM e precisa vir do disco.

---

## 📊 Interpretação Visual

| Cor/Símbolo | Significado | Ação |
|--------------|-------------|------|
| 🟩 Verde | HIT | Página já está na RAM |
| 🟥 Vermelho | PAGE FAULT | Página foi carregada ou substituída |
| 🔻 Verde | Disco → RAM | Entrada de página |
| 🔺 Vermelho | RAM → Disco | Saída de página |

---

## 🔧 Parâmetros e Limites

- Quadros na RAM: valor máximo permitido no input é 6.
- Número de páginas do programa: valor mínimo permitido no input é 8.
- Botão extra: "Limpar log" remove todo o histórico de eventos exibido.

---

## 📅 Data do documento
Gerado em: 23/10/2025

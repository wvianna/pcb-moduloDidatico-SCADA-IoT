# Projeto: Esquema Eletrônico Automatizado

## Descrição do Projeto
Este repositório contém o esquema eletrônico de um sistema de controle automatizado desenvolvido no KiCad. O circuito foi projetado para processar sinais de sensores (entradas), realizar a lógica de controle por meio de um microcontrolador/processador central e atuar sobre o ambiente através de dispositivos de potência e sinalização (saídas).

---

> 🧩 **Projeto do firmware:** Este porjeto foi desenvolvido para o fimware disponível em [https://github.com/wvianna/pcb-moduloDidatico-SCADA-IoT-firmware](https://github.com/wvianna/pcb-moduloDidatico-SCADA-IoT-firmware). O firmware todos I/O, sensores e interface RS485 em um único hardware, facilitando a montagem e reprodução em sala de aula.

---

**Autor:** William da Silva Vianna  
**Software Utilizado:** KiCad (v9 ou superior)

---

## 🛠️ Arquitetura do Sistema: Entradas e Saídas

O correto funcionamento deste circuito depende da interação entre os pinos de leitura, processamento e atuação. Abaixo estão mapeadas as principais relações de I/O (Input/Output) do diagrama:

### 1. Interfaces de Entrada (Mapeamento de Sensores e Comandos)
As entradas são responsáveis por captar as grandezas físicas ou comandos do usuário e convertê-los em sinais elétricos legíveis pelo controlador:
* **Sensores de Campo:** Conectores dedicados para a recepção de sinais analógicos/digitais vindos dos sensores periféricos.
* **Barramentos de Comunicação:** Linhas de recepção de dados (RX, SDA, SCL) preparadas para comunicação com módulos externos.
* **Circuito de Feedback/Supervisão:** Malhas de leitura que monitoram o estado das próprias saídas para proteção contra sobrecarga.

### 2. Interfaces de Saída (Mapeamento de Atuadores e Sinalização)
As saídas traduzem as decisões tomadas pelo bloco de processamento em ações físicas ou feedback visual:
* **Módulos de Atuação de Potência:** Saídas digitais isoladas ou acopladas a drivers (transistores/relés) para controle de carga.
* **Indicadores Visuais (LEDs):** Sinalização de status do sistema (Ligado, Erro, Processando dados).
* **Barramentos de Transmissão:** Linhas de envio de dados (TX) para telemetria ou telas de interface (I2C/SPI).

---

## 💻 Necessidade de Firmware

> ⚠️ **Nota Importante de Implementação:** > Este hardware **não é puramente analógico**. A placa foi projetada ao redor de uma arquitetura programável, o que significa que o circuito impresso isolado não desempenhará nenhuma função sem o seu respectivo **Firmware**.

O firmware a ser desenvolvido para este projeto deve contemplar os seguintes requisitos de software:
1. **Inicialização (Setup):** Configuração correta dos registradores, direções dos pinos de I/O (Inputs como alta impedância/Pull-up e Outputs como Push-Pull) e taxas de transmissão dos barramentos (Baud Rate).
2. **Lógica de Controle (Loop principal):** Algoritmo responsável por ler as variáveis de entrada, aplicar filtros digitais (para evitar *debounce* ou ruídos) e tomar a decisão de acionamento das saídas.
3. **Malha de Segurança:** Rotinas de interrupção de hardware para desligar as saídas imediatamente caso um comportamento anômalo seja detectado nas entradas de supervisão.

---

## 📁 Estrutura de Arquivos no Repositório

```text
├── esquema.pdf             # Diagrama esquemático exportado para leitura
├── meu-projeto.kicad_pro   # Arquivo de gerenciamento do projeto KiCad
├── meu-projeto.kicad_sch   # Folha do desenho esquemático
├── meu-projeto.kicad_pcb   # Layout da placa de circuito impresso
└── .gitignore              # Filtro de arquivos temporários do KiCad

# 🤖 Autobot: Navegação Autônoma 2D com ESP32 e ROS 2

Bem-vindo ao repositório central do **Autobot**, um robô móvel autônomo de esteira com uma arquitetura híbrida e desacoplada.

Este projeto foi desenvolvido como Trabalho de Conclusão de Curso para a graduação em Engenharia de Computação na UNICAMP (Faculdade de Engenharia Elétrica e de Computação - FEEC), com o título: *"Navegação Autônoma 2D com ESP32: Projeto e Implementação em um Robô Móvel"*.

🎥 **[Assista ao robô em ação no YouTube!](https://youtu.be/cynhL9kDgR4)**

## 👥 A Equipe
* Thiago Maximo Pavão
* Vinícius Carvalho Pimpim
* Vinícius Esperança Mantovani

---

## 🏗️ Visão Geral do Sistema

O Autobot utiliza uma arquitetura híbrida que desacopla com sucesso o hardware do robô do computador hospedeiro. Ao utilizar um microcontrolador ESP32 como uma ponte Wi-Fi em tempo real, o robô opera sem fios, transferindo tarefas computacionalmente pesadas (como SLAM e planejamento de trajetória) para uma máquina hospedeira remota.

Através de uma análise comparativa de algoritmos de SLAM, este projeto demonstrou que a fusão de dados de encoder e IMU por meio de um Filtro de Kalman Estendido (EKF) corrige efetivamente o desvio rotacional, resultando em um mapa altamente robusto para navegação autônoma.

### Componentes de Hardware
* **Microcontrolador:** ESP32
* **LiDAR:** YDLiDAR X3
* **IMU:** MPU-6050
* **Atuação:** Chassi de esteira com motores DC e encoders nas rodas

---

## 📂 Estrutura do Repositório

O sistema é dividido em dois subprojetos principais. Visite seus respectivos repositórios para obter instruções detalhadas de instalação e uso:

### 1. 🧠 [autobot_controller](https://github.com/AutoBotsUnicamp/autobot_controller) (Firmware da ESP32)
O firmware embarcado de baixo nível, desenvolvido sobre o framework ESP-IDF usando FreeRTOS.
* **Controle de Hardware:** Gerencia o controle de motores em tempo real e a telemetria dos sensores.
* **Ponte de Rede:** Hospeda servidores TCP/UDP para transmitir dados do LiDAR, leituras da IMU e odometria via Wi-Fi, enquanto recebe comandos de velocidade.

### 2. 🗺️ [autobot_ws](https://github.com/AutoBotsUnicamp/autobot_ws) (Workspace ROS 2)
O stack de processamento de alto nível, projetado para ROS 2 Jazzy no Ubuntu 24.04.
* **Fusão de Sensores:** Usa `robot_localization` (EKF) para fundir a odometria dos encoders e dados da IMU.
* **Mapeamento:** Utiliza o `slam_toolbox` para gerar mapas 2D do ambiente.
* **Navegação:** Aproveita o stack `Nav2` para o planejamento e execução de trajetórias autônomas.

---

## 🚀 Como Começar

Se você estiver configurando o projeto do zero:
1. Clone o repositório do firmware e grave (flash) na sua ESP32.
2. Clone o workspace ROS 2 na sua máquina hospedeira, instale as dependências e compile usando o `colcon`.
3. Conecte sua máquina hospedeira à mesma rede da ESP32 e inicie os drivers base para começar a mapear ou navegar!

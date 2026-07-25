📊 Lab de Observabilidade — Stack Completa
![Status](https://img.shields.io/badge/status-funcional-brightgreen)
![Docker](https://img.shields.io/badge/docker-containerizado-blue)
![Plataformas](https://img.shields.io/badge/plataformas-Linux%20%2B%20Windows-orange)
![Prometheus](https://img.shields.io/badge/Prometheus-monitoramento-red)
![Grafana](https://img.shields.io/badge/Grafana-dashboards-orange)
![Loki](https://img.shields.io/badge/Loki-logs-yellow)
Ambiente de observabilidade completo montado do zero em VMs VirtualBox.  
Monitora servidor Linux Ubuntu 22.04 e Windows Server 2022 em tempo real  
com métricas, logs centralizados, alertas automáticos e dashboards profissionais.
---
🏗️ Arquitetura
```
Node Exporter   (Linux  :9100) ──┐
Windows Exporter (Windows:9182) ──┤──► Prometheus (:9090) ──► Grafana (:3000)
Loki            (:3100)  ◄── Promtail                              │
Alertmanager    (:9093)  ◄────────────────────────────────────────┘
                                                                   │
                                                              Telegram 🔔
```
Máquina	IP	Sistema	Função
Servidor Linux	192.168.100.84	Ubuntu 22.04 LTS	Prometheus + Grafana + Loki + Alertmanager
Windows Server	192.168.100.85	Windows Server 2022	Windows Exporter + Active Directory
---
🛠️ Stack de Tecnologias
Ferramenta	Versão	Função
Docker + Compose	Latest	Containerização de todos os serviços
Prometheus	Latest	Coleta e armazenamento de métricas (pull)
Grafana	Latest	Dashboards, visualização e alertas
Loki	Latest	Banco de dados de logs
Promtail	Latest	Agente de coleta de logs → Loki
Alertmanager	Latest	Roteamento e envio de alertas (Telegram)
Node Exporter	Latest	Métricas do servidor Linux
Windows Exporter	v0.25.1	Métricas do Windows Server 2022
PromQL	—	Linguagem de queries para alertas e dashboards
---
📊 Evidências do Lab
Dashboard Unificado — Linux + Windows + Logs
![Dashboard Linux](screenshots/dashboard%20linux.png)
Dashboard Windows Server 2022
![Dashboard Windows](screenshots/dashboard%20Windows.png)
Alerta de CPU Alta disparando no Grafana
![Alerta CPU Alta](screenshots/Alerta%20de%20CPU%20alta%20grafana.png)
Alerta de Disco Cheio disparando no Grafana
![Alerta Disco Cheio](screenshots/Alerta%20disco%20cheio%20grafana.png)
Notificação de alerta chegando no Telegram
![Alerta Telegram](screenshots/Alerta%20Telegram.png)
Prometheus monitorando todos os targets simultaneamente
![Prometheus Firing](screenshots/Alerta-firing%20LINUX.png)
Resultado após ajuste — disco normalizado
![Resultado Ajuste](screenshots/Resultado%20do%20ajuste%20-%20grafana.png)
---
⚙️ Métricas Monitoradas
Linux (Node Exporter):
CPU Usage % — com thresholds warning/critical
Memory Usage %
Disk Usage % — por partição
Network Traffic — bytes recebidos e enviados
System Uptime
Logs do sistema em tempo real (via Loki)
Windows Server (Windows Exporter):
CPU, Memória e Disco
Status de serviços
Métricas de rede
Disponibilidade (todos os serviços):
Status UP/DOWN de cada serviço da stack
Prometheus, Grafana, Loki, Alertmanager, Node Exporter, Windows Exporter
---
🚨 Alertas Configurados
Alerta	Threshold	Severidade	Canal
CPU Alta	> 85% por 2 min	Critical	Telegram
Memória Alta	> 90% por 2 min	Critical	Telegram
Disco Cheio	> 85% por 5 min	Warning	Telegram
Serviço Indisponível	down por 1 min	Critical	Telegram
---
🔧 Desafios Resolvidos
Disco do servidor atingiu 100% durante o lab — identificado pelo alerta, investigado com `du` e `df`, resolvido limpando logs e expandindo partição LVM de 12GB para 23GB sem perda de dados
Schema do Loki v11 incompatível com versão atual — migrado para v13 com `tsdb`
Containers antigos em `docker run` migrados para `docker compose` — padronização da stack
Rede Docker isolada impedindo scrape do Windows Server — resolvido com `extra_hosts` no docker-compose
Download de imagens Docker interrompido por instabilidade de rede — resolvido usando `docker pull` separado antes do `compose up`
Dashboard de 2021 exibindo N/A — resolvido importando versão 2024 compatível com Windows Exporter atual
Windows Exporter instalado como serviço — com regra de firewall criada manualmente via PowerShell
IP do servidor mudando ao trocar de rede — resolvido configurando IP fixo via `netplan` no Linux e configuração estática no Windows Server
---
📁 Estrutura do Repositório
```
lab-observabilidade/
├── config/
│   ├── prometheus/
│   │   ├── prometheus.yml        # Configuração de targets e alertas
│   │   └── rules/
│   │       └── alerts.yml        # Regras de alerta PromQL
│   ├── alertmanager/
│   │   └── alertmanager.yml      # Roteamento de alertas (Telegram)
│   ├── loki/
│   │   └── loki-config.yml       # Configuração do banco de logs
│   └── promtail/
│       └── promtail-config.yml   # Coleta de logs do sistema
├── screenshots/                  # Evidências do laboratório
└── README.md
```
---
🚀 Como Reproduzir
```bash
# Clonar o repositório
git clone https://github.com/Oliveira97-png/lab-observabilidade.git
cd lab-observabilidade

# Subir a stack completa
docker compose up -d

# Verificar se todos os serviços subiram
docker ps

# Acessar os serviços:
# Grafana:      http://localhost:3000  (admin/admin123)
# Prometheus:   http://localhost:9090
# Alertmanager: http://localhost:9093
# Loki:         http://localhost:3100

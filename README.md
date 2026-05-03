# Lab de Observabilidade — Prometheus + Grafana

![Status](https://img.shields.io/badge/status-funcional-brightgreen)
![Docker](https://img.shields.io/badge/docker-containerizado-blue)
![Plataformas](https://img.shields.io/badge/plataformas-Linux%20%2B%20Windows-orange)

Ambiente de monitoramento multi-plataforma montado do zero em VMs VirtualBox.
Monitora servidor Linux Ubuntu 22.04 e Windows Server 2022 em tempo real
com alertas configurados e dashboards profissionais.

## Arquitetura

\\\
Node Exporter (Linux :9100)  --+
                               |--> Prometheus (:9090) --> Grafana (:3000) --> Navegador
Win Exporter (Windows :9182) --+
\\\

| Maquina | IP | Sistema | Funcao |
|---|---|---|---|
| Servidor Linux | 192.168.15.155 | Ubuntu 22.04 LTS | Prometheus + Grafana + Node Exporter |
| Windows Server | 192.168.15.7 | Windows Server 2022 | Windows Exporter |

## Evidencias do Lab

### Dashboard Linux (Node Exporter Full)
![Dashboard Linux](screenshots/dashboard-linux.png)

### Dashboard Windows Server 2022
![Dashboard Windows](screenshots/dashboard-windows.png)

### Alerta de Disco Disparando (Firing)
![Alerta Firing](screenshots/alerta-firing.png)

### Prometheus monitorando duas maquinas simultaneamente
![Targets UP](screenshots/prometheus-targets.png)

## Tecnologias

- **Docker** — containerizacao de todos os servicos no Linux
- **Prometheus** — coleta e armazenamento de metricas (pull model)
- **Grafana** — dashboards e alertas
- **Node Exporter** — metricas do servidor Linux
- **Windows Exporter** — metricas do Windows Server 2022
- **PromQL** — linguagem de queries para alertas e dashboards

## Desafios Resolvidos

- Disco do servidor atingiu 96% durante o lab — identificado pelo alerta, resolvido removendo Zabbix e limpando logs
- Download de imagens Docker interrompido por instabilidade de rede — resolvido usando docker pull separado
- Dashboard de 2021 exibindo N/A — resolvido importando versao 2024 compativel com Windows Exporter atual

## Proximos Passos

- [ ] Elastic Stack (Elasticsearch + Logstash + Kibana)
- [ ] Kubernetes basico com Minikube
- [ ] SQL basico para analise de dados
- [ ] Windows Exporter na estacao Windows 11

# Lab de Observabilidade — Stack Completa

[![Status](https://img.shields.io/badge/status-funcional-brightgreen)](https://github.com/Oliveira97-png/lab-observabilidade)
[![Docker](https://img.shields.io/badge/docker-containerizado-blue)](https://github.com/Oliveira97-png/lab-observabilidade)
[![Plataformas](https://img.shields.io/badge/plataformas-Linux%20%2B%20Windows-orange)](https://github.com/Oliveira97-png/lab-observabilidade)

Ambiente de observabilidade completo montado do zero em VMs VirtualBox.
Monitora servidor Linux e Windows Server em tempo real com métricas, logs centralizados e alertas com notificação no Telegram.

## Stack

| Serviço | Função | Porta |
| --- | --- | --- |
| Prometheus | Coleta e armazenamento de métricas | 9090 |
| Grafana | Dashboards e visualização | 3000 |
| Node Exporter | Métricas do servidor Linux | 9100 |
| Windows Exporter | Métricas do Windows Server | 9182 |
| Loki | Armazenamento de logs | 3100 |
| Promtail | Coleta de logs | 9080 |
| Alertmanager | Roteamento de alertas | 9093 |

## Ambiente

| Máquina | IP | Sistema | Função |
| --- | --- | --- | --- |
| Servidor Linux | 192.168.15.155 | Ubuntu 22.04 LTS | Stack completa |
| Windows Server | 192.168.15.7 | Windows Server 2022 | Windows Exporter |

## Como subir

\```
git clone https://github.com/Oliveira97-png/lab-observabilidade.git
cd lab-observabilidade
docker compose up -d
\```

## Alertas configurados

- CpuAltaCritica — CPU acima de 85% por 2 minutos (critical)
- MemoriaAltaCritica — Memória acima de 90% por 2 minutos (critical)
- DiscoCheio — Disco acima de 92% por 5 minutos (warning)
- ServicoIndisponivel — Target inacessível por 1 minuto (critical)
- Notificações via Telegram

## Evidências

### Dashboard Linux
![Dashboard Linux](screenshots/dashboard%20linux.png)

### Dashboard Windows Server
![Dashboard Windows](screenshots/dashboard%20Windows.png)

### Alerta Firing no Prometheus
![Alerta Firing](screenshots/Prometheus%20-%20Disco%20cheio.png)

### Alerta de CPU Alta no Grafana
![CPU Alta](screenshots/Alerta%20de%20CPU%20alta%20grafana.png)

### Notificação no Telegram
![Telegram](screenshots/Alerta%20Telegram.png)

## Desafios Resolvidos

- Disco do servidor atingiu 100% durante o lab — identificado pelo alerta, investigado com du e resolvido
- Schema do Loki v11 incompatível com versão atual — migrado para v13 com tsdb
- Containers antigos em docker run migrados para docker compose
- Rede Docker isolada impedindo scrape do Windows Server — resolvido com extra_hosts
- Disco atingiu 96% no lab anterior — identificado pelo alerta, resolvido removendo Zabbix e limpando logs
- Download de imagens Docker interrompido por instabilidade de rede — resolvido usando docker pull separado
- Dashboard de 2021 exibindo N/A — resolvido importando versão 2024 compatível com Windows Exporter atual
- Windows Exporter instalado como serviço com regra de firewall criada manualmente

# Lab Observabilidade Completa

Stack completa de observabilidade com métricas, logs e alertas.

## Stack

- Prometheus — coleta e armazenamento de métricas
- Grafana — visualização de dashboards
- Node Exporter — métricas do servidor Linux
- Windows Exporter — métricas do Windows Server
- Loki — armazenamento de logs
- Promtail — coleta de logs
- Alertmanager — roteamento de alertas com notificação no Telegram

## Ambiente

- Ubuntu 22.04 LTS (192.168.15.155)
- Windows Server 2022 (192.168.15.7)
- VirtualBox com rede Bridge
- Docker + Docker Compose

## Como subir

git clone https://github.com/Oliveira97-png/lab-observabilidade.git
cd lab-observabilidade
docker compose up -d

## Alertas configurados

- CpuAltaCritica — CPU acima de 85% por 2 minutos
- MemoriaAltaCritica — memória acima de 90% por 2 minutos
- DiscoCheio — disco acima de 92%
- ServicoIndisponivel — target inacessível por 1 minuto

## Evidências

Ver pasta docs/

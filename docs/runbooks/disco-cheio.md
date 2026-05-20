# Runbook: DiscoCheio

## Descricao
Alerta disparado quando o uso de disco ultrapassa o threshold configurado.

## Severidade
Warning

## Impacto
Disco cheio pode causar falha em containers, perda de logs e indisponibilidade de servicos.

## Investigacao

1. Verificar uso atual do disco
   df -h /

2. Identificar o que esta ocupando espaco
   du -sh /* 2>/dev/null | sort -rh | head -10

3. Verificar logs grandes
   du -sh /var/log/* 2>/dev/null | sort -rh | head -10

4. Verificar dados do Docker
   docker system df

## Resolucao

- Limpar cache do apt: sudo apt clean
- Limpar logs antigos: sudo journalctl --vacuum-size=50M
- Limpar imagens Docker: docker system prune -f

## Validacao
Confirmar que uso de disco voltou abaixo do threshold com df -h /
Verificar que alerta saiu de FIRING em http://192.168.15.155:9090/alerts

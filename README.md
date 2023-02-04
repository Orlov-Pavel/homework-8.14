# Домашнее задание к занятию "14.Средство визуализации Grafana"
1. Сделал свой [docker-compose файл](./docker-compose/monitoring.yml) для сборки стенда.   
   Поднятый prometheus подключен в качестве источника данных:  
   ![grafana data sources](./pictures/grafana%20data%20sources.PNG)
2. Запросы:  
   Утилизация CPU: ```100 - (avg by (instance) (irate(node_cpu_seconds_total{instance="node_exporter:9100",mode="idle"}[15s])) * 100)```  
   CPULA 1: ```node_load1{instance="node_exporter:9100"}```  
   CPULA 5: ```node_load5{instance="node_exporter:9100"}```  
   CPULA 15: ```node_load15{instance="node_exporter:9100"}```  
   Свободная ОЗУ: ```node_memory_MemFree_bytes{instance="node_exporter:9100", job="prometheus"}```  
   Свободное место на файловой системе: ```node_filesystem_avail_bytes{device="/dev/sda2", instance="node_exporter:9100"}```  
   Сам дашборд:  
   ![grafana dashboard](./pictures/grafana%20dashboard.PNG)  
   Запустил команду ```dd if=/dev/zero of=/dev/null``` на вирутальной машине для того чтобы значения небыли нулевыми и было понятно что дашборд работает.
3. Дашборд с алертами:  
   ![grafana dashboard 2](./pictures/grafana%20dashboard%202.PNG)  
   Снова запустил ```dd if=/dev/zero of=/dev/null``` для загрузки процессора, получил оповещение в telegram:  
   ![telegram notification](./pictures/telegram%20notification.PNG)
4. Выгруженный дашборд [здесь](./dashboard/my_dashboard.json).
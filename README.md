# Prometheus

- Настроить дашборд с 4-мя графиками

- память;

- процессор;

- диск;

- сеть.

Настроить на одной из систем:

- zabbix (использовать screen (комплексный экран);

- prometheus - grafana.

---

Дано :

Инфраструктура с 5-ю виртуальными машинами,

![image](https://github.com/user-attachments/assets/29e42b02-720d-4a09-a021-048d260e43d5)


Т.к. дефолтный exporter не собирает метрики libvirt , устанавливаем через докер дополнительный:

https://grafana.com/grafana/dashboards/13633-libvirt/

И правим наш /etc/prometheus/prometheus.yml 

```

global:
  scrape_interval: 10s
scrape_configs:
  - job_name: 'prometheus_master'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']
  - job_name: 'node_exporter_ubuntu'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
  - job_name: 'prometheus_libvirt'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9177']

```

Получаем метрики:

![image](https://github.com/user-attachments/assets/68e43569-45d0-4a7a-99ee-a910f5c50591)


Подгружаем нужный id 13633/json


Получаем мониторинг наших виртуальных машин:

![image](https://github.com/user-attachments/assets/a3ef52fc-7181-46f7-b325-e603174b883b)

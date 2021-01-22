### Installing Prometheus, Grafana, Loki, Promtail
1. Install pre requirements

        ansible-galaxy install cloudalchemy.prometheus
        ansible-galaxy install cloudalchemy.grafana
        ansible-galaxy install cloudalchemy.node-exporter
        ansible-galaxy collection install community.grafana

2. Fix IP in hosts.yml if needed

3. Run playbook

        ansible-playbook grafana-on-premise.yml

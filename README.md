### Installing Prometheus, Grafana, Loki, Promtail via ansible-playbook
1. Install pre requirements
```sh
sudo apt-get install -y ansible
ansible-galaxy install cloudalchemy.prometheus
ansible-galaxy install cloudalchemy.grafana
ansible-galaxy install cloudalchemy.node_exporter
ansible-galaxy collection install community.grafana
```
2. Fix IP in hosts.yml if needed "on-premise" instead VM
3. Run VM in vagrant
```sh
vagrant up
```
3. Run playbook
```sh
ansible-playbook grafana-on-premise.yml
```
4. Check Loki

[varlogs link](http://192.168.99.99:3000/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22Loki%22,%7B%22expr%22:%22%7Bjob%3D%5C%22varlogs%5C%22%7D%22%7D%5D)
![cluster_1_redy](docs/loki.png)

5. Add dashboard

![dashboard_add](docs/dashboard.png)

![dashboard](docs/dashboard2.png)

### Usage grafana-image-renderer plugin
On any dashboard:

![share](docs/share.png)
![direct_link](docs/direct_link.png)

6. Add node1 to Prometheus targets for scraping
```sh
# insall node_exporter on node1
ansible-playbook node_exporter.yml
# to start scraping
vagrant ssh grafana
echo '  - 192.168.99.98:9100' | sudo tee -a /etc/prometheus/file_sd/node.yml
```

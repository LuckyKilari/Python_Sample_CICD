Prometheus installed steps: 
Install Prometheus:

wget https://github.com/prometheus/prometheus/releases/download/v2.53.5/prometheus-2.53.5.linux-amd64.tar.gz

tar -xvf prometheus-2.53.5.linux-amd64.tar.gz

mv prometheus-2.53.5.linux-amd64 prometheus

cd prometheus/

./Prometheus &

Access prometheus: http://server_ip:9090

Grafana Installed steps:

sudo apt update && sudo apt upgrade -y

sudo apt install -y software-properties-common

sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

sudo apt update

sudo apt install grafana -y

sudo apt --fix-broken install

sudo systemctl start grafana-server

sudo systemctl enable grafana-server

sudo systemctl status grafana-server

# Laboratorio de ejemplo OSPF

## Captura de paquetes

### captura con tcpdump
sudo ip netns exec clab-frrlab-router3 tcpdump -U -n -i eth1 -w capture.pcap

## captura con tshark
sudo ip netns exec clab-frrlab-router3 tshark -i eth1 -w /tmp/capture.pcap

## Visualizar capturas

### con tshark
tshark -r /tmp/tshark_capture.pcap

### con Wireshark
wireshark capture.pcap

## Interaccion con equipos

## Comandos de pruebas ping y traceroute
sudo docker exec -it clab-frrlab-PC1 traceroute 192.168.13.2
sudo docker exec -it clab-frrlab-PC1 ping -c4 192.168.13.2

### Dar de baja o alta un enlace
sudo docker exec -d clab-frrlab-router1 ip link set dev eth2 down
sudo docker exec -d clab-frrlab-router1 ip link set dev eth2 up



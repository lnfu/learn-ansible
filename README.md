# Learning Ansible 

練習使用 Ansible 做 IaC。

- `host.ini`: 主機連線的資料
- `ansible.cfg`: 設定檔

```sh
ansible-playbook -i host.ini playbook.yml -kK
ansible-playbook playbook.yml # 因為 ansible.cfg 已經都設定好了，所以不加參數也沒關係
```

如果要設定更複雜的 host 資訊，`host.ini` 可以改成 yaml 寫法 (放在 `inventory/` 目錄下 e.g., `inventory/hosts.yml`)。

## 前置作業

### 設定網卡

#### Router (ubuntu2204)
```sh
sudo ip link set enp0s8 up # Internal NIC 要開起來
sudo ip addr add 192.168.32.254/24 dev enp0s8

# sudo ip route flush all
ip route add 10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100 
ip route add 10.0.2.2 dev enp0s3 proto dhcp scope link src 10.0.2.15 metric 100 
ip route add 10.0.2.3 dev enp0s3 proto dhcp scope link src 10.0.2.15 metric 100 
ip route add 10.113.0.0/16 dev wg0 scope link 
ip route add 192.168.32.0/24 dev enp0s8 scope link 
ip route add default via 10.0.2.2 dev enp0s3 proto dhcp src 10.0.2.15 metric 100 
```

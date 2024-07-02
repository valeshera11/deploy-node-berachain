# Node Berachain'i Dağıtın
Bu depo, Linux sistemlerinde bir Berachain düğümünü kurmak, güncellemek ve kaldırmak için Ansible betikleri içerir. Playbook, bir Berachain node'u kurma, hizmetlerini yönetme ve node işlemlerine devam etmeden önce önemli işlemlerin tanınmasını sağlama sürecini basitleştirir.

## Önkoşullar
Kök erişimi olan bir Linux sistemi (Ubuntu 22.04 LTS önerilir).
Makinenizde Git ve Ansible yüklü.

## Başlarken
### Adım 1: Bağımlılıkların Kurulması
Sisteminizin paket listesini güncelleyin:

```
sudo apt update && sudo apt upgrade -y
```
Ansible ve Git'i yükleyin:
```
sudo apt install ansible git -y
```

### Adım 2: Projenin İndirilmesi
Ansible playbook'u ve gerekli tüm dosyaları almak için bu depoyu klonlayın:
```
git clone https://github.com/nodemasterpro/deploy-node-berachain.git
cd deploy-node-berachain
```

### Adım 3: Oyun Kitabının Yürütülmesi
Aşağıdaki komutu kullanarak playbook'u çalıştırın:
```
ansible-playbook bera_node.yml -e node_action="install"
```
Playbook'u root ayrıcalıklarıyla veya sudo erişimi olan bir kullanıcı aracılığıyla çalıştırdığınızdan emin olun. Kurulumdan sonra bearchain düğümü başlatılır.


### Adım 4: Günlükleri Görüntüleme
Berachain düğümünün günlüklerini görüntülemek için:
```
journalctl -u berachain-node -f -o cat
```

## Ek Not

Kurulumdan sonra, Berachain düğümünün adresi ve anımsatıcı ifadeniz /root/berachain/output.log adresinde bulunan belirtilen günlük dosyasında saklanır. Lütfen anımsatıcı ifadeniz ve düğüm adresiniz için bu konumu kontrol ettiğinizden emin olun.

Hizmetleri Durdurma:
Hizmeti durdurmak için:
```
sudo systemctl stop berachain-node
```

Hizmetleri Başlatma:
Berachain düğüm hizmetini başlatmak için:
```
sudo systemctl start berachain-node
```

berachain düğümünü kaldırın: 
berachain düğümünü kaldırmak için aşağıdaki komutu kullanarak playbook'u çalıştırın:
```
ansible-playbook berachain_node.yml -e node_action="remove"
```

# Kubernetes The Hard Way

This tutorial walks you through setting up Kubernetes the hard way. This guide is not for someone looking for a fully automated tool to bring up a Kubernetes cluster. Kubernetes The Hard Way is optimized for learning, which means taking the long route to ensure you understand each task required to bootstrap a Kubernetes cluster.

> The results of this tutorial should not be viewed as production ready, and may receive limited support from the community, but don't let that stop you from learning!


## システム構成

| 種類 | メモリ | ストレージ | HostOS | 仮想OS |
| --- | --- | --- | --- | --- |
| jumpbox | 512MB | 10GB | Windows | Debian |
| server | 2GB | 20GB | Windows | Debian |
| node 0 | 2GB | 20GB | Windows | Debian |
| node 1 | 2GB | 20GB | MacBookAir | Debian |

## 特徴
### ブリッジネットワークを使って、Windows上の仮想マシンと、Mac上の仮想マシンを同じネットワークで通信させてクラスター化を達成した

① VirtualBox > 設定 > ネットワーク > ブリッジアダプター を選択する

② /etc/ssh/sshd_config.d/permit-root.confにて、```PermitRootLogin yes```を追記する 

### DHCPを使わずにIPアドレスを固定する

① 各サーバーで `ip addr` を実行し、ネットワークインターフェース名（例: `enp0s3`）を確認する

② それぞれのサーバーの/etc/dhcpcd.confに以下を書き加える

```
interface ****
static ip_address=【任意のIPアドレス】/24
static routers=【自宅のルーターのIPアドレス】
static domain_name_servers=8.8.8.8 1.1.1.1
```
* [Provisioning Pod Network Routes](docs/11-pod-network-routes.md)
* [Smoke Test](docs/12-smoke-test.md)
* [Cleaning Up](docs/13-cleanup.md)

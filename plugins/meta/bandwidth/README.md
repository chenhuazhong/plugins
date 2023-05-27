
This document has moved to the [containernetworking/cni.dev](https://github.com/containernetworking/cni.dev) repo.

You can find it online here: https://cni.dev/plugins/current/meta/bandwidth/

```yaml
# /etc/cni/net.d/10-flannel.conflist
# 限制 1Mb/s 下行网速
{
  "name": "cbr0",
  "cniVersion": "0.3.1",
  "plugins": [
    {
      "type": "flannel",
      "delegate": {
        "hairpinMode": true,
        "isDefaultGateway": true
      }
    },
    {
      "type": "portmap",
      "capabilities": {
        "portMappings": true
      }
    },
    {
      "name": "slowdown",
      "type": "bandwidth",
      "nameSpace": "default",
      "ingressRate": 1048576,  // 1024 * 1024
      "ingressBurst": 104857
    }
  ]
}
```
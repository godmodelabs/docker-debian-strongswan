# docker-debian-strongswan
A debian:latest based Docker container running strongSwan (IPsec-based VPN)(https://www.strongswan.org/)
```
docker run -d --name "strongswan" \
  --privileged=true \
  --net=host \
  --cap-add=ALL \
  -v /root/strongswan/ipsec.conf:/etc/ipsec.conf \
  -v /root/strongswan/ipsec.secrets:/etc/ipsec.secrets \
  godmodelabs/debian-strongswan
```

Sample /root/strongswan/ipsec.conf
```
config setup
        cachecrls=yes
        strictcrlpolicy=yes
#       charondebug="ike 2, knl 3, cfg 2"

conn test1
        auto = start
        authby = psk
        ike = aes256-sha256-modp2048!
        esp = aes256-sha256-modp2048!
        keyexchange = ikev1
        ikelifetime = 28800s
        lifetime = 1h
        type = tunnel
        left=ww.ww.ww.ww
        leftsubnet=xx.xx.xx.xx/xx
        right=yy.yy.yy.yy
        rightsubnet=zz.zz.zz.zz/zz
```
Sample /root/strongswan/ipsec.secrets
```
yy.yy.yy.yy : PSK "secret key"
```

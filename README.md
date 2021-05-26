# Use Heroku to deploy Xray high-performance proxy services, (WebSocket tls, vmess, vless, trojan, shadowsocks and socks etc..)
> Reminder: Misuse may cause the account to be BAN! ! !

## Overview
Used to deploy vless+websocket+tls on Heroku, and automatically select the latest alpine linux and Xray core for each deployment.
vless has better performance and takes up less resources.

Use xray +caddy to deploy protocols such as vmess vless trojan shadowsocks socks transmitted via ws at the same time, and the camouflage website has been configured by default.
Support tor network, and you can start xray and caddy through a custom network configuration file to configure various functions on demand
Supports storage of custom files. Both directories and account passwords are UUID. The client must use TLS to connect to
Heroku. It provides us with a free container service. We should not abuse it, so this project should not be used as a long-term circumvention.
Mirror image
This image will not be blocked because it takes up a lot of resources. After registering a Heroku account and logging in, click the button below to deploy.

### Server

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/thawhakyi/HerokuXray) 

Click on the purple above `Deploy to Heroku` jump to the heroku app creation page, fill in the name of the app, select the node (European node is recommended, and the US node will automatically delete YouTube comments and likes!), modify some parameters and UUIDs as needed, and click below deployStart to create the deployment application.
If an error occurs, you can try a few more times. After the deployment is completed, the bottom of the page will be displayed `Your app was successfully deployed`

* Click Manage App to view and reset the parameters in the Config Vars item under Settings
* Click Open app to jump to the welcome page domain name to assign a domain name to heroku, the format is xxx.herokuapp.comfor client
* The default protocol password is 24b4b1e1-7a89-45f6-858c-242cf53b5bdb, the WS path is $UUID-[vmess|vless|trojan|ss|socks] format

### Client
* ** Be sure to replace all `xxx.herokuapp.com` to your project domain name assigned to heroku**
* ** Be sure to replace all `24b4b1e1-7a89-45f6-858c-242cf53b5bdb` UUIDs set during deployment, it is recommended to change, not everyone should be the same **
Latest version of XRay will be automatically installed during deployment.

For security reasons, unless you use a CDN, please don't use a custom domain name. Instead, use the second-level domain name assigned by Heroku to implement XRay vless Websocket + TLS.

<details>
<summary>V2rayN(Xray, V2ray)</summary>

```bash
* Client download：https://github.com/2dust/v2rayN/releases
* Proxy protocol：vless or vmess
* Address：xxx.herokuapp.com
* Port：443
* Default UUID：24b4b1e1-7a89-45f6-858c-242cf53b5bdb
* vmess alter ID：0
* encryption：none
* transmission protocol：ws
* camouflage type：none
* camouflage domain name：xxx.workers.dev ((CF Workers url)
* path：/24b4b1e1-7a89-45f6-858c-242cf53b5bdb-vless // default - vless (/custom UUID-vless), if you wanna use vmess (/custom UUID-vmess)
* Underlying transmission security：tls
* allow inscure：false
```
</details>

<details>
<summary>Trojan-Go</summary>

```bash
* Client download: https://github.com/p4gefau1t/trojan-go/releases
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "xxx.herokuapp.com",
    "remote_port": 443,
    "password": [
        "24b4b1e1-7a89-45f6-858c-242cf53b5bdb"
    ],
    "websocket": {
        "enabled": true,
        "path": "/24b4b1e1-7a89-45f6-858c-242cf53b5bdb-trojan",
        "host": "xxx.herokuapp.com"
    }
}
```
</details>

<details>
<summary>Shadowsocks</summary>

```bash
* Client download：https://github.com/shadowsocks/shadowsocks-windows/releases/
* Server address: xxx.herokuapp.com
* Port: 443
* Password：24b4b1e1-7a89-45f6-858c-242cf53b5bdb
* Encryption：chacha20-ietf-poly1305
* Plug-in：xray-plugin_windows_amd64.exe  //You need to download and unzip the plugin - https://github.com/shadowsocks/xray-plugin/releases and place it in the same directory
* Plugin options: tls; host= xxx.herokuapp.com; path= /24b4b1e1-7a89-45f6-858c-242cf53b5bdb-ss // (/custom UUID-ss)
```
</details>

<details>
<summary>You can use Cloudflare Workers to transfer traffic, (supporting WS mode of VLESS\VMESS\Trojan-Go) is configured as:</summary>

```js
const SingleDay = 'xxx.herokuapp.com'
const DoubleDay = 'xxx.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>

## OpenWrt preferred IP script is automatically updated：

* [CloudflareST](https://github.com/Lbingyi/CloudflareST) `OpenWrt recommand -faster`
* [cf-autoupdate](https://github.com/Lbingyi/cf-autoupdate) `OpenWrt recommand`

## About Cloudflare SpeedTest

* [CloudflareSpeedTest](https://github.com/XIU2/CloudflareSpeedTest)
*  [better-cloudflare-ip](https://github.com/badafans/better-cloudflare-ip)

### Special thanks to:

* [mixool](https://github.com/mixool/)
* [bclswl0827](https://github.com/bclswl0827/v2ray-heroku)
* [yxhit](https://github.com/yxhit)
* [badafans](https://github.com/badafans/better-cloudflare-ip/tree/20201208)

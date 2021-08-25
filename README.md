[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/manusjse/yg)  

## 1：vl+ws+tls or vm+ws+tls
* Server：ip（example：icook.tw）or：appname.herokuapp.com
* Port：443
* UUID：8f91b6a0-e8ee-11ea-adc1-0242ac120002   (create new one)
* Encryp method：none (vl) or chacha20-poly1305 (vm)
* Trans Protocol：ws
* host：****.workers.dev(CF Workers)or：appname.herokuapp.com
* SNI：****.workers.dev(CF Workers)or：appname.herokuapp.com
* Path：/UUID-vless or /UUID-vmess
* vmess alterid：0
* Security Type：tls
* Disable System Root Certificates：false

## 2：trojan-go+ws

* Server：ip（example：icook.tw）or：appname.herokuapp.com
* Port：443
* UUID：8f91b6a0-e8ee-11ea-adc1-0242ac120002   (create new one) 
* Trans Protocol：ws
* Path：/UUID-trojan
* SNI：****.workers.dev(CF Workers)or：appname.herokuapp.com
* host：****.workers.dev(CF Workers)or：appname.herokuapp.com

## 3：ss+ws+tls

* Server: appname.herokuapp.com
* Port: 443
* UUID：8f91b6a0-e8ee-11ea-adc1-0242ac120002   (create new one) 
* Encryption：chacha20-ietf-poly1305
* Optional: tls;host=appname.herokuapp.com;path=/UUID-ss


### CloudFlare Workers（sopport VL\VM\Trojan-Go WS mode）

```
const SingleDay = 'appname.herokuapp.com'
const DoubleDay = 'appname.herokuapp.com'
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
----------------------------------------------------------------------------------------------
```
const Day0 = 'app0.herokuapp.com'
const Day1 = 'app1.herokuapp.com'
const Day2 = 'app2.herokuapp.com'
const Day3 = 'app3.herokuapp.com'
const Day4 = 'app4.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        let day = nd.getDate() % 5;
        if (day === 0) {
            host = Day0
        } else if (day === 1) {
            host = Day1
        } else if (day === 2) {
            host = Day2
        } else if (day === 3){
            host = Day3
        } else if (day === 4){
            host = Day4
        } else {
            host = Day1
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

# jssdk

jssdk是专门为H5开发者准备的工具，只要会用jquery，就可以使用jssdk开发基于TrustNote的H5应用。

### 引入 trustnote.js

开发者需要在页面中引入 trustnote.js 文件。

```
<script src="/static/js/TrustNote.js"></script>
```

### 得到钱包地址

```
var address;
window.onload = function () {
    trustnote.getAddress(function (resp) {
        address = resp.message.address;
    });
}
```

### 转账

```
function pay() {
        var _to_address = "OKLGMIWBCFITVWKZF3JASA23OMZLICSH";//服务方的收款地址
        var _amount = 10*1000000;   //  1 MN = 100000 ; 10 MN = 10* 100000
        var _message = "some text" //你自己定义一些文字，可以随着交易一起上链
        var data = {
            payer: address,//这个地址，是上面用trustnote.getAddress函数得到的用户钱包地址。
            outputs: [{
                address: _to_address,
                amount: _amount
            }],
            message: _message
        }
        
        trustnote.callPay(data, function (resp) {
            if(resp.hasOwnProperty("error")){
              if(resp.error){
                //支付成功后的回调函数
              }else{
                //支付失败后的回调函数
              }
            }else{
              支付成功后的回调函数
            }
        })
    }
```

返回值:

```
{
  eventName: "payment",
  message: {
    unit: "MulUMgOU4e2ApF0Egq8R4vPt0alrz98y2JCk+gSQYiM="
  },
  error: null
}
```
### 示例

示例程序：https://github.com/TrustNoteSamples/paid_reading

演示视频：https://github.com/TrustNoteSamples/paid_reading/raw/master/demo.mp4

# jssdk

Jssdk is a tool specially prepared for H5 developers. As long as you use jquery, you can use jssdk to develop H5 applications based on TrustNote.

### Introducing trustnote.js

Developers need to introduce a trustnote.js file into the page.

```
<script src="/static/js/TrustNote.js"></script>
```

### Get the wallet address

```
var address;
window.onload = function () {
    trustnote.getAddress(function (resp) {
        address = resp.message.address;
    });
}
```

### Transfer

```
function pay() {
        var _to_address = "OKLGMIWBCFITVWKZF3JASA23OMZLICSH";//Provider's payment address.
        var _amount = 10*1000000;   //  1 MN = 100000 ; 10 MN = 10* 100000
        var _message = "some text" //You define some text yourself, which can be chained along with the transaction.
        var data = {
            payer: address,//This address is the user wallet address obtained above using the trustnote.getAddress function.
            outputs: [{
                address: _to_address,
                amount: _amount
            }],
            message: _message
        }
        
        trustnote.callPay(data, function (resp) {
            if(resp.hasOwnProperty("error")){
              if(resp.error){
                //Callback function after successful payment
              }else{
                //Callback function after payment failure
              }
            }else{
              //Callback function after successful payment
            }
        })
    }
```

return value:

```
{
  eventName: "payment",
  message: {
    unit: "MulUMgOU4e2ApF0Egq8R4vPt0alrz98y2JCk+gSQYiM="
  },
  error: null
}
```
### example

Sample program: https://github.com/TrustNoteSamples/paid_reading

Demo video: https://github.com/TrustNoteSamples/paid_reading/raw/master/demo.mp4

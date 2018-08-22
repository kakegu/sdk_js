# TrustNote JavaScript SDK

TrustNote JavaScript SDK is a tool specifically designed for web developers. If you know how to use jQuery, then you should be able to use the SDK to develop web applications running on TrustNote. 

In the first SDK release (v0.0.1), there is only two functions available, more functions will be added in the coming releases.

To demonstrate how to use the SDK, we developed a content restriction sample program that allows a website or a blog accepting its reader’s payment in TTT or TRC20 tokens before releasing the restricted contents to the reader or subscriber. We will explain how to use these 2 functions in the code snippets below.


### Setting Up TrustNote.js

TrustNote.js is a JavaScript file that you will link to your HTML. Developers need to download a local copy of the file and reference it in your HTML like below. 

```
<script src="/static/js/TrustNote.js"></script>
```

### Retrieve the Wallet Address

```
var address;
window.onload = function () {
    trustnote.getAddress(function (resp) {
        address = resp.message.address;
    });
}
```

### Transfer the Money

```
function pay() {
        var _to_address = "OKLGMIWBCFITVWKZF3JASA23OMZLICSH";// Service Provider's wallet address.
        var _amount = 10*1000000;   // 1 MN = 1,000,000 Notes; 10 MN = 10 * 1,000,000
        var _message = "some text" // Texts defined here will be stored on TrustNote network along with the transaction.
        var data = {
            payer: address,// This is the wallet address obtained using the trustnote.getAddress function as above.
            outputs: [{
                address: _to_address,
                amount: _amount
            }],
            message: _message
        }
        
        trustnote.callPay(data, function (resp) {
            if(resp.hasOwnProperty("error")){
              if(resp.error){
                //Callback function after payment failure
              }else{
                //Callback function after successful payment
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
### Sample

The sample program can be found from： https://github.com/TrustNoteSamples/paid_reading

Demo video of the sample program can be found from： https://github.com/TrustNoteSamples/paid_reading/raw/master/demo.mp4

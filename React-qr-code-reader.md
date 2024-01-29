# Access Camera and Read QR code using JavaScript

In this tutorial, we are going to create a QR Reader using JavaScript and HTML5. JavaScript enables us to access the camera and then we can easily scan the QR code to get the message in the QR Code.

We can create our own QR Code Reader using JavaScript with following 2 simple steps.

**Step 1 :** Create html5-qrcode.min.js file .
**Step 2 :** Create a HTML page with following code in it :
```<script src="html5-qrcode.min.js"></script>
<style>
  .result{
    background-color: green;
    color:#fff;
    padding:20px;
  }
  .row{
    display:flex;
  }
</style>
<div class="row">
  <div class="col">
    <div style="width:500px;" id="reader"></div>
  </div>
  <div class="col" style="padding:30px;">
    <h4>SCAN RESULT</h4>
    <div id="result">Result Here</div>
  </div>
</div>
<script type="text/javascript">
function onScanSuccess(qrCodeMessage) {
    document.getElementById('result').innerHTML = '<span class="result">'+qrCodeMessage+'</span>';
}
function onScanError(errorMessage) {
  //handle scan error
}
var html5QrcodeScanner = new Html5QrcodeScanner(
    "reader", { fps: 10, qrbox: 250 });
html5QrcodeScanner.render(onScanSuccess, onScanError);
</script>```

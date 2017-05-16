# Capabilities## Launching a session1.	Get the `receiverId````
var receiverId = " haiffjcadagjlijoggckpgfnoeiflnem ";
```!!!tip "Note" 
		In this example, receiverId indicates the store version of Citrix Receiver for Chrome. If you are using a repackaged version of Citrix Receiver for Chrome, use the appropriate `receiverId`.
		  &#50;. 	Convert ICA data from `.ini` to `JSON` format.

!!!tip "Note"
		Typically, the ICA file is retrieved from StoreFront as an `.ini` file. Use the following helper function to convert an ICA `.ini` file to `JSON`.
		
```
//Helper function to convert ica in INI format to JSONfunction convertICA_INI_TO_JSON(data){var keyVals = {};if (data) {var dataArr;if(data.indexOf('\r')==-1){dataArr = data.split('\n');}else{dataArr = data.split('\r\n');}for (var i = 0; i < dataArr.length; i++) {var nameValue = dataArr[i].split('=', 2);if (nameValue.length === 2) {keyVals[nameValue[0]] = nameValue[1];}// This is required as LaunchReference will contain '=' as well. The above split('=',2) will not provide// the complete LaunchReference. Ideally, something like the following should be used generically as well// because there can be other variables that use the '=' character as part of the value.if (nameValue[0] === "LaunchReference") {var index = dataArr[i].indexOf('=');var value = dataArr[i].substr(index + 1);keyVals[nameValue[0]] = value;}}console.log(keyVals);//to removereturn keyVals;}return null;}```

  &#51;.   Send the following message from the third-party Chrome app to Citrix Receiver for Chrome. 

```  chrome.runtime.sendMessage(receiverId , {"method" : "launchSession","icaData":icaJSON,”sessionId”:sessionId},function(response) { });```where:
* `icaJSON` indicates the ICA data in the form of JSON object created using the helper function.* `sessionId` is applicable in case of embedding receiver in appview. * `response: {"success":true,"sessionId":"Session1481109162565"}`  For further communication with the active session (for example, hide/unhide/disconnect) the Session ID needs to be stored.In case of error, response looks like below

```{"success":false,"error":"Invalid params: no icadata"}
```
## Hide a session1.	Send the following message from the third-party Chrome app to Citrix Receiver for Chrome. ```
chrome.runtime.sendMessage(receiverId, {"method" : "hide","sessionId":sessionId},function(response) { })
```
where `sessionId` is applicable in case of embedding receiver in appview. For more details, see Embedding Receiver using appview.
!!!tip "Note"
		When a session is launched in embed view, the appview attribute must be set to hidden in the third-party app.In case of error, response looks like below:```{"success":false,"error":"Invalid sessionId"}.```## Show a session

1. Send the following message from the third-party Chrome app to Citrix Receiver for Chrome.

``` chrome.runtime.sendMessage(receiverId, {"method" : "show","sessionId":sessionId,function(response) { });
```
where, `sessionId` is applicable in case of embedding receiver in appview. !!!tip "Note"
		When a session is launched in embed view, the appview attribute must be set to hidden in the third-party app.
		In case of error, response looks like below:```{"success":false,"error":"Invalid sessionId"}.```

## Disconnect the session 

Send the following message from the third-party Chrome app to Citrix Receiver for Chrome. ```chrome.runtime.sendMessage(receiverId, {"method" : "disconnect","sessionId":sessionId},function(response) { });```where `sessionId` is applicable in case of embedding receiver in appview. In case of error, response looks like below:```{"success":false,"error":"Invalid sessionId"}.```
## Launching Citrix Receiver for Chrome in embed modeA third-party app can be embedded to Citrix Receiver for Chrome using the appview attribute. 

Follow the procedure below:1. Create an appview element in the third-party app. Also, register the chrome.runtime.onMessageExternal listener in the background page of the app to receive status of embedding.For example:```var appview = document.createElement("appview");appview.id = "appView";// Appends the element to the document body.document.body.appendChild(appview);
```  &#50;.  Call connect method Call connect method can be achieved by passing the receiver id. Citrix Receiver for Chrome checks if the sender app is whitelisted and sends a message with embed state success. sessionId is posted to the sender app. Session id needs to be stored to do further interactions with the session. 

For example, 

```var appToEmbed = receiverId;//Get the citrix receiver id function embedCallback(response){//response value will be true if embedding is allowed otherwise value will be false} // Connects the appview to appToEmbed.// appToEmbed is the id of the Citrix Receiver for Chrome.appview.connect(appToEmbed,data,embedCallback);```
!!!tip "Note"
		When a third-party app is launched in KIOSK mode, the session cannot be launched in embed mode.

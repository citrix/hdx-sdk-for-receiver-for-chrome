# Capabilities
var receiverId = " haiffjcadagjlijoggckpgfnoeiflnem ";
```
		In this example, receiverId indicates the store version of Citrix Receiver for Chrome. If you are using a repackaged version of Citrix Receiver for Chrome, use the appropriate `receiverId`.
		

!!!tip "Note"
		Typically, the ICA file is retrieved from StoreFront as an `.ini` file. Use the following helper function to convert an ICA `.ini` file to `JSON`.
		
```
//Helper function to convert ica in INI format to JSON

  &#51;.   Send the following message from the third-party Chrome app to Citrix Receiver for Chrome. 

```  


```
```
## Hide a session
chrome.runtime.sendMessage(receiverId, {"method" : "hide","sessionId":sessionId},function(response) { })
```


		When a session is launched in embed view, the appview attribute must be set to hidden in the third-party app.

1. Send the following message from the third-party Chrome app to Citrix Receiver for Chrome.

``` 
```

		When a session is launched in embed view, the appview attribute must be set to hidden in the third-party app.
		

## Disconnect the session 

Send the following message from the third-party Chrome app to Citrix Receiver for Chrome. 
## Launching Citrix Receiver for Chrome in embed mode

Follow the procedure below:
```

For example, 

```
!!!tip "Note"
		When a third-party app is launched in KIOSK mode, the session cannot be launched in embed mode.

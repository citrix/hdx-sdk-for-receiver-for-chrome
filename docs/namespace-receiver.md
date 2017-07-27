# Namespace: receiver

## receiver

`citrix.receiver`

## Members

`(readonly) apiVersion`

## Properties

| Name | Type | Description |
|---|---|---|
| `apiVersion` |	String | HDX SDK for Chrome version. |

## Methods

### (static) createSession(id, connectionParams, onSessionCreated)

Creates a new session and returns session instance through callback. Use session instance to start the session, register and handle events and to disconnect the session.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `id` | string	| Receiver for Chrome ID. For example, id of the store version is "haiffjcadagjlijoggckpgfnoeiflnem". |
| `connectionParams` |	connectionParams	| Configuration options to create the session.|
| `onSessionCreated` |	onSessionCreated | Callback containing the session object created. Signature sample: `function <function_name>(session_object){…}` |

#### Throws

Unable to create session object.
##### Type

ReceiverError

#### Examples

**Example 1:** Following code launches an app/desktop in a new window (similar to the session launch using Receiver for Chrome).

```
//Use appropriate citrix receiver id. This sample uses store version.
// EAR = lbfgjakkeeccemhonnolnmglmfmccaag , store version = haiffjcadagjlijoggckpgfnoeiflnem
var citrixReceiverId = "haiffjcadagjlijoggckpgfnoeiflnem";

try{
	var connectionParams = {
		"launchType" : "message"
	};

	function sessionCreated(sessionObject){
		//Handle session interactions like events, start, disconnect here.
		// Adding onConnection event handler
		function connectionHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onConnection",connectionHandler);

		// Adding onConnectionClosed event handler
		function connectionClosedHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onConnectionClosed",connectionClosedHandler);

		// Adding onError event handler
		function onErrorHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onError",onErrorHandler);

		//Adding onURLRedirection event handler
		function onURLRedirectionHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onURLRedirection",onURLRedirectionHandler);
	}

	citrix.receiver.createSession(citrixReceiverId,connectionParams,sessionCreated);
}catch(ex){
	console.log(ex);
}
```

**Example 2:** Following code launches an app/desktop in an appview element inside third party Chrome app.

```
function createAppview() {
	if (!appView) {
		appView = document.createElement("appview");
		appView.id = "appView";
		// Appends the element to the document body.
		document.body.appendChild(appView);

		// Sample code for setting appview properties. Modify as needed.
		appView.style.width = "800px";
		appView.style.height = "800px";
		appView.style.left = "0px";
		appView.style.top = "100px";
		appView.style.position = "absolute";
	} else {
		appView.style.display = "block";
	}
}

//Use appropriate citrix receiver id. This sample uses store version.
// EAR = lbfgjakkeeccemhonnolnmglmfmccaag , store version = haiffjcadagjlijoggckpgfnoeiflnem
var citrixReceiverId = "haiffjcadagjlijoggckpgfnoeiflnem";

try{
	createAppview();
	var connectionParams = {
		"launchType" : "embed",
		"container": appView
	};

	function sessionCreated(sessionObject){
		//Handle session interactions like events, start, disconnect here.
		// Adding onConnection event handler
		function connectionHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onConnection",connectionHandler);

		// Adding onConnectionClosed event handler
		function connectionClosedHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onConnectionClosed",connectionClosedHandler);

		// Adding onError event handler
		function onErrorHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onError",onErrorHandler);

		//Adding onURLRedirection event handler
		function onURLRedirectionHandler(event){
			console.log("Event Received : " + event.type);
			console.log(event.data);
		}
		sessionObject.addListener("onURLRedirection",onURLRedirectionHandler);
	}

	citrix.receiver.createSession(citrixReceiverId,connectionParams,sessionCreated);
}catch(ex){
	console.log(ex);
}
```
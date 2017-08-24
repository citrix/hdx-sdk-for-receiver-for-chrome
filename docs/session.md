# Class: Session

## Session

`new Session()`

## Members

### (readonly) receiverId

#### Properties

| Name | Type | Description |
|---|---|---|
| `receiverId	` | String | Receiver for Chrome ID. |

### (readonly) sessionId

#### Properties

| Name | Type | Description |
|---|---|---|
| `sessionId` | String	| ID of the session. |

## Methods

### (inner) addListener(eventType, eventListener)

Registers the eventListener on the eventType.

#### Parameters

| Name | Type | Description |
|---|---|---| 
| `eventType` | String | Type of the event for which the listener needs to be attached. Supported event types: <br> - [onConnection](./events#onconnection) <br> - [onConnectionClosed](./events#onconnectionclosed) <br> - [onURLRedirection](./events#onurlredirection) <br> - [onError](./events#onerror) |
| `eventListener` | [eventListener](./global#eventlistener) | Listener to handle the event |

#### Example

```
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
```

### (inner) changeResolution(bounds, responseCallback)

Changes the resolution of the session.

#### Parameters

| Name | Type | Description |
|---|---|---| 
| `bounds` |	Object	| Contain session resolution settings. |
| `responseCallback` |	[responseCallback](./global/#responsecallback) | Callback that handles the response. |

#### Properties

| Name | Type | Description |
|---|---|---|
| `bounds.autoresize` | boolean | Should be set to false to give fixed width and height to session. By default, this value is set to true in which case the session is resized to match the size of appView element inside third party Chrome app or the new window. |
| `bounds.width` |	Number |	Width of the session specified in pixels. This value will be set only when autoresize is set to false. |
| `bounds.height` |	Number | Height of the session specified in pixels. This value will be set only when autoresize is set to false. |

#### Examples 

**Example 1:** To change resolution to fixed width and height.

```
var bounds = {
	"autoresize":false,
	"width": "800",
	"height":"600"
}

function fixedResolutionCallback(response){
	 console.log("changeResolution", response);
}
sessionObject.changeResolution(bounds,fixedResolutionCallback);
```

**Example 2:** To change the session resolution to match the size of appview element inside third party Chrome app or the window size.

```
var bounds = {
	"autoresize": true
}

function autoResizeCallback(response){
	 console.log("changeResolution", response);
}
sessionObject.changeResolution(bounds,autoResizeCallback);
```

### (inner) hide(responseCallback)

Hides the session.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `responseCallback` | [responseCallback](./global/#responsecallback) | Callback that handles the response. |

### (inner) logoff(responseCallback)

Sends logoff to the session.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `responseCallback` | [responseCallback](./global/#responsecallback) | Callback that handles the response. |

### (inner) removeListener(eventType, eventListener)

Removes the eventListener on the eventType.

#### Parameters

| Name | Type | Description |
|---|---|---| 
| `eventType` | String | Type of the event for which the listener needs to be attached. Supported event types: <br> - [onConnection](./events#onconnection) <br> - [onConnectionClosed](./events#onconnectionclosed) <br> - [onURLRedirection](./events#onurlredirection) <br> - [onError](./events#onerror) |
| `eventListener` | [eventListener](./global#eventlistener) | Listener to handle the event |

#### Example

```
//Removing the event handler for onConnection event
function connectionHandler(eventObj){
	console.log("Event Received : " + event.type);
	console.log(event.data);
}
sessionObject.removeListener("onConnection",connectionHandler);
```

### (inner) sendSpecialKeys(keys, responseCallback)

Sends a key combination to the session.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `keys` | Array	| Array of strings with each one representing a key. Supported keys Alt, Control, Shift, ArrowDown, ArrowLeft, ArrowRight, ArrowUp, Home, End, PageUp, PageDown, Backspace, Delete, F5, PrintScreen,Insert, Escape, Tab. |
| `responseCallback` |	[responseCallback](./global/#responsecallback)	 | Callback that handles the response. |

#### Examples

**Example 1:** Sends Ctrl+alt+delete to the session.

```
function sendKeysCallback(response){
	 console.log("sendSpecialKeys", response);
}
var keys = ["Control","Alt","Delete"];
sessionObject.sendSpecialKeys(keys,sendKeysCallback);
```

**Example 2:** To preview different apps running inside session, Ctrl+alt+tab can be sent.
```
function sendKeysCallback(response){
	 console.log("sendSpecialKeys", response);
}
var keys = ["Control","Alt","Tab"];
sessionObject.sendSpecialKeys(keys,sendKeysCallback);
```
### (inner) show(responseCallback)

Shows the session.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `responseCallback` | [responseCallback](./global/#responsecallback) | Callback that handles the response. |

### (inner) start(launchData, responseCallback)

Starts the session.

#### Parameters

| Name | Type | Description |
|---|---|---|
| `launchData` | Object | Contains the type and value of the ICA |
| `responseCallback` | [responseCallback](./global/#responsecallback) | Callback that handles the response. |

#### Properties

| Name	| Type | Description |
|---|---|---|
| `launchData.type` | String | Specifies the data type of ICA data. Allowed values are "json" or "ini". |
| `launchData.value` | String | ICA data to start the session. It should be a JSON object when type is "json" or a string read from a .ini file when type is "ini". |

#### Examples

**Example 1:** When ICA data is in JSON format

```
var icaObj = {
	"ClientName":"Chrome-Receiver",
	"Domain":"<domain_name>",
	"ClearPassword":"<password>",
	"InitialProgram":"<initial program",
	"Title":"<title>",
	"Address":"<ip address>",
	"Username":"<user name>",
	"wsPort":"<port val>"
}
var launchData = {"type" : "json",value : icaObj};
function sessionResponseCallback(response){
	console.log("start", response);
}
sessionObject.start(launchData,sessionResponseCallback);
```

**Example 2:** When ICA data is in INI format.

```
var launchData = {"type" :"ini",value :"<ica data in ini format>"};
function sessionResponseCallback(response){
	console.log("start", response);
}
sessionObject.start(launchData,sessionResponseCallback);
```

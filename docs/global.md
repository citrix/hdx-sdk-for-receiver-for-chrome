# Global

**Type Definitions**

<a name="connectionparams"></a>

## connectionParams

Configuration options to create the session.

### Type

* Object

### Properties

<table>
<thead>
<tr><th>Name</th><th>Type</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td><code>connectionParams</code></td>
<td>Object</td>
<td>
<h6>Properties</h6>
<table>
<thead>
<tr><th>Name</th><th>Type</th><th>Attributes</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td><code>launchType</code></td>
<td>String</td>
<td>&lt;optional&gt;</td>
<td>Takes "message" or "embed" as value. Defaults to "message". <br /><br />"message" - launches the session in a new window (similar to session launch using Receiver for Chrome). <br /> "embed" - Embeds the session inside third party Chrome app.</td>
</tr>
<tr>
<td><code>container</code></td>
<td>Object</td>
<td>&lt;optional&gt;</td>
<td><a href="https://developer.chrome.com/apps/tags/appview">Appview</a> element created inside third party Chrome app.<br /><br /> Applicable only when launchType is "embed".</td>
</tr>
<tr>
<td><code>bounds</code></td>
<td>Object</td>
<td>&lt;optional&gt;</td>
<td>Sets a fixed width and height to the session.
<h6>Properties</h6>
<table>
<thead>
<tr><th>Name</th><th>Type</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td><code>autoresize</code></td>
<td>boolean</td>
<td>Should be set to false to give fixed width and height to session. By default, this value is set to true in which case the session is resized to match the size of appView element inside third party Chrome app or the new window.</td>
</tr>
<tr>
<td><code>width</code></td>
<td>Number</td>
<td>Width of the session specified in pixels. This value will be set only when autoresize is set to false.</td>
</tr>
<tr>
<td><code>height</code></td>
<td>Number</td>
<td>Height of the session specified in pixels. This value will be set only when autoresize is set to false.</td>
</tr>
</tbody>
</table>
</td>
</tr>
<tr>
<td><code>preferredLang</code></td>
<td>String</td>
<td>&lt;optional&gt;</td>
<td>Specifies the preferred language code to be used inside the session. If the language code specified is either invalid or unsupported then it falls back to "en". <br /><br /> Supported language codes : en, de, es, fr, ja, ko, ru, zh, zh-cn, zh-tw. <br /><br /> If the value is unspecified then the browser"s language code is used.</td>
</tr>
</tbody>
</table>
</td>
</tr>
</tbody>
</table>

### Example

`connectionParams` full example:

```
	var appView = document.createElement("appview");

	var connectionParams = {
		"launchType" : "embed",
		"container": appView,
		"bounds" :{
			"autoresize":false,
			"width": "800",
			"height":"600"
		},
		"preferredLang" : "ja" //Setting to Japanese
	}
```	


<a name="eventlistener"></a>

## eventListener (event)

Listener to handle the events.

### Parameters

| Name | Type | Description |
|---|---|---| 
| `event` |	Object |	Object as appropriate to the `eventType` registered. |

### Properties

<table>
	<tr>
		<th>Name</th>
		<th>Type</th>
		<th>Description</th>
	</tr>
	<tr>
		<td><code>event.id</code></td>
		<td>String</td>
		<td>Id of the session object.</td>
	</tr>
	<tr>
		<td><code>event.type</code></td>
		<td>String</td>
		<td>Event type triggered.</td>
	</tr>
	<tr>
		<td><code>event.data</code></td>
		<td>Object</td>
		<td><p>Data as appropriate to the event triggered</p>
			<ul>
				<li><a href="./events#onconnection">onConnection</a></li>
				<li><a href="./events#onconnectionclosed">onConnectionClosed</a></li>
				<li><a href="./events#onurlredirection">onURLRedirection</a></li>
				<li><a href="./events#onerror">onError</a></li>
			</ul>
		</td>
	</tr>
</table>

<a name="onsessioncreated"></a>

## onSessionCreated(sessionObject)

Callback having the session object created.

### Parameters

| Name | Type | Description |
|---|---|---|
| `sessionObject` |	[Session](./session) |	Session object to interact with the session like register and handle events, start and disconnect. |

### Example

```
function sessionCreated(sessionObject) {
//Handle session interactions like events, start, disconnect here.
//ICADATA has been constructed for example. Recommending to use StoreFront/WebInterface SDK to get ICA.
//Refer session.start() for more details.
	var icaData = {
		"Domain":"abcd",
		"ClearPassword":"xxxxxxxxx",
		"InitialProgram":"#Desktop",
		"Title":"Desktop",
		"Address":"xx.xx.xx.xx",
		"Username":"xyz"
	};
	var launchData = {"type" :"json",value :icaData};

	function sessionResponseCallback(response) {
		console.log("start", response);
	}

	sessionObject.start(launchData,sessionResponseCallback);
}
```

<a name="responsecallback"></a>

## responseCallback(response)

Callback that handles the response.

### Parameters

| Name | Type | Description |
|---|---|---|
| `response` | Object | Response object |


### Properties

| Name | Type | Description |
|---|---|---|
| `response.success` |	boolean | Status of the method call. Holds the value true in case of success and false in case of failure. In case of failure, details of the error is set in the response object. |
| `response.sessionId` | String |	Id of the session. |
| `response.error` | String | Reason for the failure of the method call. |


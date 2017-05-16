# HDX SDK for Citrix Receiver for Chrome Citrix Receiver for Chrome introduces an API (Experimental API) that allow third-party Chrome apps to lock, unlock and disconnect from a XenApp and XenDesktop session. Using this API, Citrix Receiver for Chrome can be launched in both embedded mode and KIOSK mode. Sessions launched in embedded mode function  in ways similar to sessions launched KIOSK mode.Sessions launched in embed mode functions in ways similar to sessions launched in KIOSK mode. 

!!!danger "Important"
		 This feature has been verified with the launch of a single app or desktop only.

## Prerequisites 

Citrix Receiver for Chrome supports only the whitelisted third-party Chrome apps. You can whitelist a third-party Chrome app by adding the policy file for Citrix Receiver for Chrome using Chrome management settings
To whitelist a third-party Chrome app, do the following: 
1.	Install the latest version of Citrix Receiver for Chrome. See Citrix downloads page for details.2.	Whitelist the third-party Chrome app by adding the policy file for Citrix Receiver for Chrome using Chrome management settings.
The sample policy.txt file to whitelist the third-party Chrome app is as below:

```
{
	"settings": {

		 "Value": {

			 "settings_version": "1.0",

			 "store_settings": {

					"externalApps": [“<3rdParty_App1_ExtnID>”,“<3rdParty_App2_ExtnID>”]


            }


        }


    }


}
```
!!!tip "Note"
		&lt;3rdParty_App1_ExtnID&gt; is used as an example for the name of externalApps and can send messages to Citrix Receiver for Chrome. Get your appid from the `chrome://extensions` site.

## Additional references:Citrix Receiver for Chrome uses message communication provided by Chrome OS. For more details, see the following links:
* [https://developer.chrome.com/apps/tags/appview](https://developer.chrome.com/apps/tags/appview) 2.	[https://developer.chrome.com/extensions/runtime#event-onMessageExternal](https://developer.chrome.com/extensions/runtime#event-onMessageExternal) 3.	[https://developer.chrome.com/extensions/runtime#method-sendMessage](https://developer.chrome.com/extensions/runtime#method-sendMessage)4.	For more details, see Manage Chrome Apps by organizational unit on Google support.  5.	For more information on whitelisting, see [https://support.google.com/chrome/a/answer/6177431?hl=en](https://support.google.com/chrome/a/answer/6177431?hl=en)

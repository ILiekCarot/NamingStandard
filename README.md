# External Naming Convention
aka ENC, is an organization between executor developers to provide a unified scripting API for our scripters.
---   
**Please go to our official website for better styled information: https://scriptenc.org/** (coming soon)

## Why?
Over the years scripting has gotten more and more complex to support multiple executors. And with many people moving on from Roblox, there is a new market for Lua External Executors for other games. (like [Minecraft](https://elysium.wtf/))

Consider the following scenario. You want to know if a function belongs to the executor or not. In order for this code to be cross compatiable with all executors code like this is needed:
```lua
local is_executor_closure = is_syn_closure or is_fluxus_closure or is_sentinel_closure or is_krnl_closure or is_proto_closure or is_calamari_closure or is_electron_closure or is_elysian_closure
```
This is reality for scripters who want cross compatibilty in their scripts. Scripters shouldn't have to do such laborous work just to attain cross compatability. The ENC seeks to solve this problem using naming conventions everyone agrees upon and follows.

One variant of a script should naturally work on all script executors which have their environment properly fitted to the ENC. 

## How?
The ENC provides standards for naming conventions as well as API functionality. The standard is written in markdown on this GitHub. Edits or additions are done through pull requests. Edits and additions are manually approved by the ENC council and discussed by everyone.

## Supporting ENC
As a product owner, your support of ENC by following the API will result in a far smoother experience for scripters, as they are able to work on scripts that they can confidently say will work on **most** products. Once you have implemented ENC's API, you can display so by adding the badge to your website, thread or application.

Here are a few examples for badges at 100%. You can use the HTML one for websites, and the markdown one for repositories.
```html
<i>Dash badge</i>

<a href="https://roblox.scriptenc.org"><img src="https://img.shields.io/badge/ENC-100%25-blueviolet" alt="ENC - 100%"></a>

<i>Query parameter badge</i>

<a href="https://roblox.scriptenc.org"><img src="https://img.shields.io/static/v1?label=ENC&message=100%25&color=blueviolet" alt="ENC - 100%"></a>```
```   
```md
_Dash badge_

[![ENC - 100%](https://img.shields.io/badge/ENC-100%-blueviolet)](https://roblox.scriptenc.org)

_Query parameter badge_

[![ENC - 100%](https://img.shields.io/static/v1?label=ENC&message=100%&color=blueviolet)](https://roblox.scriptenc.org)
```

This will notify people of your alliance in providing scripters with an easier method of engineering scripts that your consumers can enjoy.

NOTICE: If you, as a product owner, do not have all of these functions but yet support the ones you do - you then support ENC! You are more than able to display the badge on your website.

## Checking your environment

You can run the ENC environment checking script to see how well your executor environment supports the ENC standard. Find the script [here.](ENCCheckEnv.lua) The script determines what is missing, and writes the results to file under workspace.

## Contributing
Go [here](CONTRIBUTING.md) for a guide on contributing.

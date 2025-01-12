# Get Agent Information

Get the Livechat agent data according to the path variables.

<table><thead><tr><th width="163">HTTP Method</th><th width="250">URL</th><th>Requires Auth</th></tr></thead><tbody><tr><td><code>GET</code></td><td><code>/api/v1/livechat/agent.info/:rid/:token</code></td><td><code>no</code></td></tr></tbody></table>

## Path Variables

<table><thead><tr><th width="135">Key</th><th width="218">Example Value</th><th>Description</th></tr></thead><tbody><tr><td><code>rid</code><mark style="color:red;"><code>*</code></mark></td><td><code>zRAeTszXor8CCPceB</code></td><td>The room <code>_id</code>.</td></tr><tr><td><code>token</code><mark style="color:red;"><code>*</code></mark></td><td><code>iNKE8a6k6cjbqWhWd</code></td><td>The visitor <code>token</code>.</td></tr></tbody></table>

{% hint style="info" %}
To get the `rid` and `token` values, call the [Get Rooms](https://developer.rocket.chat/reference/api/rest-api/endpoints/omnichannel/livechat-endpoints/livechat-room/get-rooms) endpoint to retrieve the details of all rooms.
{% endhint %}

## Example Call

{% swagger method="get" path="/api/v1/livechat/agent.info/:rid/:token" baseUrl="http://localhost:3000" summary="Get agent information" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" required="true" name="rid" %}
The room id.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="token" required="true" %}
The visitor token.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}

{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}

{% endswagger-response %}
{% endswagger %}

## Example Response

```json
{
    "agent": {
        "_id": "XycfA5CetCPuEjqxw",
        "emails": [
            {
                "address": "agent@rocket.chat",
                "verified": true
            }
        ],
        "status": "online",
        "name": "testAgent",
        "username": "test.agent",
        "livechat": {
            "maxNumberSimultaneousChat": "5"
        }
    },
    "success": true
}
```

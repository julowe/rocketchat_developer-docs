---
description: List all sessions on the workspace.
---

# LDAP SyncNow

<figure><img src="../../../../../.gitbook/assets/enterprise.jpg" alt=""><figcaption></figcaption></figure>

Syncs your [LDAP data](https://docs.rocket.chat/use-rocket.chat/workspace-administration/settings/ldap) based on the[ data sync configurations](https://docs.rocket.chat/use-rocket.chat/workspace-administration/settings/ldap/ldap-data-sync-settings).

{% hint style="info" %}
* It requires the `sync-auth-services-users` [permission](https://docs.rocket.chat/use-rocket.chat/workspace-administration/permissions).
* It requires [two-factor authentication.](../other-important-endpoints/2fa.md#calling-an-endpoint-with-two-factor)
{% endhint %}

| URL                    | Requires Auth | HTTP Method |
| ---------------------- | ------------- | ----------- |
| `/api/v1/ldap.syncNow` | `yes`         | `GET`       |

## Headers

<table><thead><tr><th width="179">Argument</th><th width="239">Example</th><th width="136">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>X-User-Id</code></td><td><code>myuser-name</code></td><td>Required</td><td>The authenticated  user ID.</td></tr><tr><td><code>X-Auth-Token</code></td><td><code>myauth-token</code></td><td>Required</td><td>Auth token.</td></tr><tr><td><code>x-2fa-code</code></td><td><code>148750</code></td><td>Required</td><td>The 2fa code.</td></tr></tbody></table>

## Example Call

```bash
curl --location --request POST 'http://localhost:3000/api/v1/ldap.syncNow' \
--header 'x-auth-token: 0ueGH0dyW5ewtemsyiBlrC8pU4yBbRUtReXiglvisoZ' \
--header 'x-user-id: 2tTEqR7ZNMJ4HGGNa' \
--header 'x-2fa-code: 773917'
```

## Example Result

```json
{
    "message": "Sync_in_progress",
    "success": true
}
```

### Error

Any of the following errors can occur on the endpoint.

* **Authorization**: Requires an authentication token for the request to be made.
* **No Permission**: This occurs when the authenticated user doesn't have the  `sync-auth-services-users` permission.
* **LDAP Disabled**: This occurs when the [LDAP connection](https://docs.rocket.chat/use-rocket.chat/workspace-administration/settings/ldap/ldap-connection-setting) is disabled.
* **TOTP Required:** Requires two-factor authentication for the request to be made.
* **Invalid TOTP:** Requires a valid two-factor authentication code.

{% tabs %}
{% tab title="Authorization" %}
```json
{
    "status": "error",
    "message": "You must be logged in to do this."
}
```
{% endtab %}

{% tab title="No Permission" %}
```json
{
    "success": false,
    "error": "error-not-authorized"
}
```
{% endtab %}

{% tab title="LDAP Disabled" %}
```json
{
    "success": false,
    "error": "LDAP_disabled"
}
```
{% endtab %}

{% tab title="TOTP Required" %}
```json
{
    "success": false,
    "error": "TOTP Required [totp-required]",
    "errorType": "totp-required",
    "details": {
        "method": "totp",
        "codeGenerated": false,
        "availableMethods": [
            "totp"
        ]
    }
}
```
{% endtab %}

{% tab title="Invalid TOTP" %}
```json
{
    "success": false,
    "error": "TOTP Invalid [totp-invalid]",
    "errorType": "totp-invalid",
    "details": {
        "method": "totp",
        "codeGenerated": false
    }
}
```
{% endtab %}
{% endtabs %}

## Change Log

| Version | Description                             |
| ------- | --------------------------------------- |
| 4.0.0   | Added                                   |
| 5.2.0   | Include `syncAvatars` on `ldap.syncNow` |
# HubSpot API connection check from a Linux terminal

Use this quick test to confirm that your Linux terminal can reach the HubSpot API and that your HubSpot access token works.

## 1. Set the real HubSpot API host

HubSpot API requests use `https://api.hubapi.com`.

```bash
export HUBSPOT_API_BASE_URL="https://api.hubapi.com"
```

## 2. Load your HubSpot access token

Use a real HubSpot private app token or OAuth access token.

```bash
read -rsp "HubSpot access token: " HUBSPOT_ACCESS_TOKEN && echo
```

## 3. Run the simplest possible HubSpot request

Run this as a single line:

```bash
curl -i --request GET --url "$HUBSPOT_API_BASE_URL/account-info/v3/details" --header "Authorization: Bearer $HUBSPOT_ACCESS_TOKEN"
```

If you copy this from a chat or document, do not include literal `\n` characters.

## 4. Check the result

What to look for:

- `200` means the connection worked and the token was accepted.
- `401` usually means the token is missing, expired, malformed, or invalid.
- `403` usually means the token is valid but does not have access to the resource.
- `400` usually means the command was pasted incorrectly or the request was malformed.
- A timeout, DNS error, or connection refused message usually means a network or hostname problem.

A successful response will return HubSpot account data such as `portalId`, `timeZone`, and `uiDomain`.

## 5. Optional: print only the status code

Run this as a single line:

```bash
curl -s -o /dev/null -w "%{http_code}\n" --request GET --url "$HUBSPOT_API_BASE_URL/account-info/v3/details" --header "Authorization: Bearer $HUBSPOT_ACCESS_TOKEN"
```

A `200` confirms the HubSpot API connection test succeeded.

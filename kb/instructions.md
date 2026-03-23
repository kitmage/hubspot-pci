# API connection check from a Linux terminal

Use this quick test to confirm that your API host is reachable and that your API key or token works.

## 1. Set your values

Replace the example values with your real API host and token.

```bash
export API_BASE_URL="https://api.example.com"
export API_TOKEN="replace-with-real-token"
```

## 2. Run the simplest possible request

Use `curl` to call a lightweight endpoint such as `/health`, `/status`, or `/ping`.

```bash
curl -i \
  -H "Authorization: Bearer $API_TOKEN" \
  "$API_BASE_URL/health"
```

## 3. Check the result

What to look for:

- `HTTP/1.1 200 OK` or `HTTP/2 200` means the connection worked.
- `401` or `403` usually means the host is reachable, but the token is missing, expired, or invalid.
- `404` means the host is reachable, but the endpoint path is probably wrong.
- A timeout, DNS error, or connection refused message usually means a network, hostname, or server issue.

## 4. Optional: print only the status code

If you want a very small success/fail check:

```bash
curl -s -o /dev/null -w "%{http_code}\n" \
  -H "Authorization: Bearer $API_TOKEN" \
  "$API_BASE_URL/health"
```

A `200` confirms the simplest test connection succeeded.

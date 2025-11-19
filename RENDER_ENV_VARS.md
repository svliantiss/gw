# Render.com Environment Variables

Copy these values into your Render dashboard for each service.

## API Service (llmgateway-api)

### API_URL
```
https://dev.emby.ai
```

### UI_URL
```
https://ui-dev.emby.ai
```

### ORIGIN_URLS
```
https://dev.emby.ai,https://ui-dev.emby.ai
```

### PASSKEY_RP_ID
```
emby.ai
```
*(Note: Use the root domain for passkeys, not subdomain)*

### COOKIE_DOMAIN
```
.emby.ai
```
*(Note: The leading dot allows cookies to work across subdomains)*

---

## UI Service (llmgateway-ui)

### API_URL
```
https://dev.emby.ai
```

### NEXT_PUBLIC_API_URL
```
https://dev.emby.ai
```

---

## Notes

- All URLs use `https://` (required for production)
- `PASSKEY_RP_ID` uses the root domain `emby.ai` (passkeys require root domain)
- `COOKIE_DOMAIN` uses `.emby.ai` (leading dot enables cross-subdomain cookies)
- `ORIGIN_URLS` includes both API and UI URLs for CORS


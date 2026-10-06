# Sudani Fast Pool Checker

A small web application for diagnosing which Netflix/Fast.com CDN targets are visible from the current connection.

## What it does

- Retrieves the current Fast.com JavaScript token server-side.
- Calls `https://api.fast.com/netflix/speedtest/v2`.
- Reads Fast.com `client` information (public IP/ISP/ASN/location when returned).
- Reads the returned Netflix CDN `targets`.
- Probes each target and displays application-level response time.
- Highlights targets identified as Paris.
- Does not change APN, IP, routing, VPN, DNS, or phone settings.

## Run

Requires Node.js 18+.

```bash
npm install
npm start
```

Open:

`http://localhost:3000`

## Important

Fast.com is an unofficially documented interface and can change its JavaScript/token/API behavior. This project dynamically extracts the token from the current Fast.com bundle instead of hard-coding it.

The "Paris detected" label is based on the target metadata/hostname returned by Fast.com. It is a CDN-pool diagnostic, not proof of the exact BGP path or every router hop between the phone and Paris.

## PWA support
This version can be installed as a Progressive Web App from a supported browser.

- The live `/api/pool` endpoint is never cached by the service worker.
- Static app files are cached for faster startup/offline shell support.
- For installation on a phone from the Internet, serve the app over HTTPS.
- On Android Chrome, open the site and use **Install app** / **Add to Home screen**.

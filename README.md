# IP 地址查询工具

A lightweight, self‑contained web app that lets you instantly
discover the geographic and network information of any public IP
address (or your own machine).  
It uses public APIs such as **ipwho.is** and **ipapi.co** for data
lookup and also performs a reverse‑DNS lookup to show the hostname.

> **Live demo** – [https://your‑domain.com/ip‑lookup](https://your‑domain.com/ip-lookup)  
> *(Replace with the URL where you host the `index.html` file)*

---

## Features

| Feature | Description |
|---------|-------------|
| **IP lookup** | Query an arbitrary IP or the IP of the client by leaving the field empty. |
| **Geolocation** | Country, city, region, continent, latitude, longitude, timezone. |
| **Network details** | IPv6 address, autonomous system number (ASN), ISP / organization. |
| **Hostname** | Reverse‑DNS lookup to display the FQDN. |
| **Currency** | Local currency symbol returned where available. |
| **Country flag** | Dynamic country flag fetched from Flag‑Icon‑CSS. |
| **Responsive** | Works on desktop and mobile (≤ 680 px). |
| **No JavaScript dependencies** | Only plain vanilla JS + a single Font‑Awesome CDN import. |
| **Lightweight** | < 30 KB gzipped, no external build tools. |

---

## Demo

![Screenshot of the IP lookup page](./screenshot.png)

*The screenshot shows the UI with an example lookup for `8.8.8.8`.*

---

## Installation / Hosting

1. Clone or download the repo.  
2. Place the `index.html` file in your web‑root (e.g. `/var/www/html/`).  
3. (Optional) Rename `index.html` to `ip-lookup.html` or similar.  
4. Open the page in a browser:  
   `http://your‑server.com/index.html`

The app is **completely client‑side**, so any static hosting service
( GitHub Pages, Netlify, Vercel, etc.) works out of the box.

---

## Usage

| Input | Action |
|-------|--------|
| **Leave the field empty** | Retrieves the IP & network information of the current machine (both IPv4 & IPv6). |
| **Enter an IP address** | Queries the provided address. |
| **Refresh button** | Re‑fetches the current machine’s IP and all its properties. |
| **Query button** | Sends a lookup request for the typed address. |

All interactions are performed via AJAX using the public APIs mentioned
in the **API Usage** section below.

---

## API Usage

The app talks to two services:

| Service | URL | Fallback | Notes |
|---------|-----|----------|-------|
| **ipwho.is** | `https://ipwho.is/<IP>` or `https://ipwho.is/?format=json` | Returns: `country`, `city`, `region`, `continent`, `latitude`, `longitude`, `timezone`, `asn`, `isp`, `hostname`, `currency`, etc. | First try. If unavailable, fallback to ipapi.co. |
| **ipapi.co** | `https://ipapi.co/<IP>/json/` or `https://ipapi.co/json/` | Returns a subset of the above. | Light weight alternative. |
| **Google DNS‑Over‑HTTPS (PTR)** | `https://dns.google/resolve?name=<reverse>.in-addr.arpa&type=PTR` | Follows reverse‑DNS spec. | Used to resolve hostnames. |

No API key is needed – the services allow a generous rate‑limit for
personal use.

---

## File Structure


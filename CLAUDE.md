# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**R&E Produções - Convites Personalizados** is a single-page e-commerce application for a custom invitation design business. The entire project lives in a single file: `index.html` (~1,800 lines), which contains all HTML, CSS (in a `<style>` tag), and JavaScript (in a `<script>` tag).

No build system, package manager, or external dependencies are needed — the file runs by opening it directly in any web browser.

## Running the Project

Open `index.html` in a browser. No build step, server, or installation required.

For local development with live reload, you can use any static file server, e.g.:
```bash
npx serve .
# or
python -m http.server 8080
```

## GitHub Repository Setup

This project is synced to GitHub automatically via GitHub Actions.

### Initial Setup

1. Create a new repository on GitHub (without README, .gitignore, or license)
2. Add the remote origin:
```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

3. **Generate a Personal Access Token (PAT):**
   - Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Create a new token with `repo` scope
   - Copy the token

4. **Configure GitHub Secrets:**
   - Go to your repository → Settings → Secrets and variables → Actions
   - Create a new secret named `GITHUB_TOKEN` with your PAT value

### Automatic Syncing

- Every change to `index.html` or `CLAUDE.md` is automatically committed and pushed to GitHub
- GitHub Actions runs automatically on push and checks every 2 hours
- All commits include timestamps for tracking modifications

To disable auto-sync, turn off GitHub Actions in repository settings.

## Architecture  

All logic is in `index.html`. The JavaScript is organized into named modules via comments:

- **AUTH MODULE** — Registration/login/logout using `localStorage`. Users stored under key `re_users`, active session under `re_session`. Passwords are stored in plaintext (client-side prototype only, not production-ready).
- **CART MODULE** — Per-user cart stored under `re_cart_[userId]`. Key functions: `addToCart()`, `removeFromCart()`, `changeQty()`, `finalizeOrder()` (sends order to WhatsApp).
- **ORDER HISTORY MODULE** — Per-user history under `re_history_[userId]`.
- **PRODUCT FILTERING** — `filterProducts(category)` filters `.product-card` elements by their `data-category` attribute. Categories: `interativo`, `tecnologico`, `simples`, `com-video`, `artes-festa`, `animado-plus`, `infinity`.
- **CART BUTTON INJECTION** — `injectCartButtons()` runs on DOMContentLoaded to replace WhatsApp anchor links inside product cards with dual-action buttons (Add to Cart + direct WhatsApp).
- **UI/ANIMATION** — IntersectionObserver drives card entrance animations; `showToast()` handles all user feedback notifications.

## LocalStorage Keys

| Key | Contents |
|-----|----------|
| `re_users` | JSON array of `{ name, email, password }` |
| `re_session` | JSON object of the currently logged-in user |
| `re_cart_[userId]` | JSON array of cart items `{ name, price, emoji, qty }` |
| `re_history_[userId]` | JSON array of past orders |

## Key Customization Points

Hardcoded values to update for a real deployment:
- WhatsApp number in `finalizeOrder()` (currently `+55 11 99999-9999`)
- Instagram handle in the footer
- Product names, prices, and `data-category` attributes on `.product-card` elements

## External CDN Dependencies

- Google Fonts: Playfair Display, Poppins, Dancing Script
- Font Awesome 6.5.0 (icons)

Both require an internet connection to load.

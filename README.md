# AURA
### AI-Powered Image Transformer

A lightweight, fully serverless, single-file image transformation web tool. Upload a photo, choose an artistic or photographic style, and generate a restyled image instantly — powered by Google's Gemini image generation model.

No backend server, no deployment pipeline, no installation. Just open the HTML file and go.

---

**🌐 Live Demo** → [https://aurashift.github.io/AURA/image-transformer.html](https://aurashift.github.io/AURA/image-transformer.html)

---

## 📸 Screenshots

| Workspace Interface | Transformation Result |
| :---: | :---: |
| <img width="2056" height="1201" alt="image" src="https://github.com/user-attachments/assets/0d22b656-322c-470a-b5cd-971e4bb155b5" /> | <img width="2056" height="1201" alt="image" src="https://github.com/user-attachments/assets/f1d734d4-6a4d-40cd-bfc2-b01a9ef03ffb" /> |

---

## ⚡ Architecture Highlights

| Property | Detail |
|---|---|
| **Deployment** | Single `.html` file — zero server required |
| **AI Model** | Google Gemini image generation (auto-discovered) |
| **SDK** | `@google/genai` v2.5.0 bundled inline (no CDN) |
| **Transport** | Google GenAI SDK — CORS-compatible, works from `file://` |
| **API Key** | Runtime input only — never hardcoded or stored |
| **Timeout** | 90 seconds hard cutoff per request |
| **Model Discovery** | Dynamic `ListModels` call — always uses best available model |

---

## 🔑 API Key & Billing

### Getting Your API Key
1. Go to [https://aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. Create or select a project
3. Copy your API key
4. Paste it into the AURA key field at runtime — it is stored only in your browser session

### Free Tier vs Paid Tier

| Tier | Images/Day | Images/Min | Cost |
|---|---|---|---|
| **Free** | ~50 (resets midnight PT) | 2 RPM | $0 |
| **Paid** | Unlimited | 15 RPM | ~$0.04/image (~₹3.30) |

> **Note:** As of December 2025, the free tier has `limit: 0` for image generation by default. You must enable billing to use the API reliably.

### Enabling Paid Tier (India)
1. Go to [https://aistudio.google.com/projects](https://aistudio.google.com/projects)
2. Click **Set up billing** next to your project
3. Add a payment method and complete setup
4. Your existing API key immediately gains paid-tier quota

> **India-specific:** If you see error `OR_BACR2_44`, your card type may be unsupported. Use a Visa/Mastercard international credit card, or a virtual card from [Wise](https://wise.com) as a reliable workaround. Indian debit cards and some domestic credit cards are blocked by Google's billing system.

---

## 🤖 Model

AURA uses **dynamic model discovery** — on first generate, it calls `ListModels` with your API key and automatically selects the best available image generation model.

### Priority Order
```
1. gemini-2.5-flash-image      ← fastest, preferred (~5–15s)
2. gemini-3.1-flash-image      ← fallback
3. gemini-2.0-flash-exp-image-generation ← legacy fallback
```

If none of the preferred models are available, AURA picks any model whose name contains `"image"` and supports `generateContent`. The resolved model name is logged to the browser console as `[AURA] Using model: ...`.

> Model names change frequently as Google releases and deprecates versions. Dynamic discovery ensures the app never breaks due to a renamed model.

---

## 🔒 Security

### API Key Handling
- Your key is entered at runtime into a password-masked input field
- It is stored only as a JavaScript variable in the current browser session
- It is **never** embedded in the HTML file, written to disk, or sent to any third-party server
- Closing the browser tab destroys the key — it must be re-entered each session

### Browser-to-API Architecture
```
Your Browser → Google Gemini API (direct)
```
The request goes directly from your browser to Google's servers. No intermediate server touches your image or key.

### ⚠️ Public Hosting Warning
If you host AURA on a public website, **do not hardcode your API key** in the HTML. Anyone can view page source and steal it. For public deployments, implement a backend proxy:

```
Your Browser → Your Server (holds API key securely) → Google Gemini API
```

Example proxy stack: Node.js + Express, Python + FastAPI, or Next.js API routes.

---

## ⏱️ Timeout & Performance

| Scenario | Expected Time |
|---|---|
| Normal (paid tier, gemini-2.5-flash-image) | 5–20 seconds |
| Busy server | 20–60 seconds |
| Timeout cutoff | **90 seconds** |

AURA enforces a **90-second hard timeout** using `AbortController`. If the API doesn't respond within 90 seconds, the request is cancelled and a clear error is shown. This prevents the UI from hanging indefinitely.

The loading screen shows:
- A **live elapsed timer** (e.g. `23s`)
- An **animated progress bar** calibrated to expected response time
- **Contextual status messages** that update as time progresses

> Newly upgraded accounts (free → paid) may experience 60–150s response times for the first few hours due to a known Google quota propagation delay. This resolves itself automatically.

---

## ✨ Transformation Styles

### 🔍 Depth & Lighting
| Style | Description |
|---|---|
| **Soft Focus** | Gently blurs the background while keeping the subject pin-sharp with backlighting. Pristine clarity, no grain. |
| **Dark Stage** | Places the subject against a solid black studio wall with intense flash and sharp, well-defined shadows. |
| **Studio Dark** | Deep muted gradient backdrop with powerful flash and a glowing rim light around the subject. |

### 🌀 Aura & Glow Effects
| Style | Description |
|---|---|
| **Outline Glow** | Adds a subtle white-stroke digital glow radiating off the subject's outline. Background stays photorealistic. |
| **Sparkle Aura** | Traces the subject's silhouette with sparkling glitter and light particles. Background stays photorealistic. |

### 🎞️ Vintage & Analog
| Style | Description |
|---|---|
| **Lofi Dusk** | Night-flash aesthetic with a deep grainy background, rim light, and warm peachy skin tones. |
| **Dreamy Film** | Soft nostalgic focus with golden-hour warmth, film grain, and an earthy organic palette. |
| **Red Glow** | 35mm tungsten film look with split-tone cyan/amber, organic grain, and red-orange halation blooms. |
| **90s Summer** | Classic editorial with warm analog film grading and high contrast between peachy skin and cool blue tones. |

### 🎨 Creative Frameworks
| Style | Description |
|---|---|
| **Seasonal Grid** | 4-panel edge-to-edge grid of the same image with hand-drawn crayon seasonal overlays: ❄️ Winter · 🌸 Spring · 🔥 Summer · 🍂 Autumn |

---

## 🚀 How to Run

### Option 1 — Open directly (local use)
```bash
git clone https://github.com/aurashift/AURA.git
cd AURA
open image-transformer.html   # macOS
# or double-click the file in Windows/Linux
```
The bundled SDK handles all networking — no local server needed.

### Option 2 — GitHub Pages (already live)
The repo is configured to serve via GitHub Pages. Any push to `main` automatically updates the live site.

### Option 3 — Any static host
Drop `image-transformer.html` onto Netlify, Vercel, Cloudflare Pages, or any static host. No build step required.

---

## 🛠️ Error Reference

| Error | Cause | Fix |
|---|---|---|
| `429 Quota exceeded` | Daily or per-minute limit hit | Wait for reset, or create a new API key |
| `OR_BACR2_44` | Indian billing account blocked | Use a Wise virtual Visa card |
| `Failed to fetch` | Opening file from `file://` with old version | Use current version — SDK is bundled inline |
| `No image model found` | Key has no image model access | Enable billing on your Google Cloud project |
| `Request timed out after 90s` | Server overloaded or slow | Retry in 30s; check [status.cloud.google.com](https://status.cloud.google.com) |
| `No image returned` | Model blocked the prompt | Try a different style |

---

## 📦 Dependencies

| Dependency | Version | How included |
|---|---|---|
| `@google/genai` | 2.5.0 | Bundled inline via esbuild IIFE — no CDN required |
| Google Fonts (Syne, DM Mono) | — | Loaded from CDN (requires internet) |

No `npm install`, no `node_modules`, no build step.

---

## 📄 License

MIT — free to use, modify, and distribute.

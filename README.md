# AURA
image-transformer tool

A lightweight, fully serverless, single-page image processing web tool. AURA lets you upload a photo, choose an artistic or photographic style, and generate high-fidelity, restyled images on the fly. 

Because the entire application is bundled directly inside a client-side layout, there is no backend server deployment required—just bring your API key and start transforming!

---

**Website** - https://haneel-kumar.github.io/AURA/image-transformer.html

## 📸 Screenshots

| Workspace Interface | Transformation Gallery |
| :---: | :---: |
| <img width="1438" height="838" alt="image" src="https://github.com/user-attachments/assets/e59f3fce-f7a4-4033-8c40-efca82432a9f" /> | <img width="1438" height="838" alt="image" src="https://github.com/user-attachments/assets/20ae5eaf-0744-42ac-acaa-01e12110a115" /> |

---

## ⚡ Key Architecture Highlights

* **Zero Infrastructure:** Built entirely inside a single-file document (`image-transformer.html`). No server, database, or heavy deployment pipelines required.
* **Direct API Integration:** Communication happens straight from your web browser to the image model endpoints.
* **Privacy-First Processing:** Your uploaded media and API secrets never touch third-party server environments.

---

## ✨ Features & Transformation Styles

Select from 9 fine-tuned rendering pipelines designed to manipulate context, exposure, filters, and textures while keeping absolute subject identity intact:

### 🔍 Depth & Lighting Styles
* **Soft Focus:** Blurs everything behind the subject with a gentle, back-lit soft focus, maintaining digital clarity without visual grain.
* **Dark Stage:** Drops the subject into a stark minimalist studio setting with a solid black wall, leveraging intense flash to form sharp, well-defined shadows.
* **Studio Dark:** Pairs powerful studio flash with a glowing back-lit rim effect over a deep, dark gradient backdrop.

### 🌀 Aura & Glow Effects
* **Outline Glow:** Adds a subtle white stroke digital glow outlining and radiating right off the subject, leaving the surrounding background photorealistic.
* **Sparkle Aura:** Traces the subject’s silhouette and applies a sparkling, photorealistic glitter radiation effect.

### 🎞️ Vintage & Analog Aesthetics
* **Lofi Dusk:** A high-contrast aesthetic combining night-flash elements, gentle peachy skin tones, and a deep, grainy, shadowed background.
* **Dreamy Film:** Implements an intentionally soft, nostalgic focus warmed by a diffused golden-hour glow and rich organic palette shadows.
* **Red Glow:** Recreates a 35mm flash snapshot on tungsten film with split-tone cyan shadows, amber highlights, and red-orange halation blooms around reflective surfaces.
* **90's Summer:** Recreates classic editorial lookups by pairing bright natural sunlight with a high contrast between warm skin tones and cool blue environments.

### 🎨 Creative Frameworks
* **Seasonal Grid:** Builds an edge-to-edge 4-panel grid keeping the original photorealistic subject intact but layered with custom hand-drawn crayon elements:
    * *Top-Left:* Snowflakes (Winter)
    * *Top-Right:* Flowers (Spring)
    * *Bottom-Left:* Flames (Summer)
    * *Bottom-Right:* Falling Leaves (Autumn)

---

## 🚀 How to Run the App

Since the core framework resides inside a standalone document, you can execute it instantly.

### Quick Start
1. Clone this repository:
   ```bash
   git clone [https://github.com/haneel-kumar/AURA.git](https://github.com/haneel-kumar/AURA.git)

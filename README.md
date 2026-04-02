# 🛏️ Paint My Bed

> An interactive bed colorizer built with React + Vite.  
> Click any section of the bed to fill it with color, or let the app generate beautiful color combinations automatically.

---

## What is Paint My Bed?

**Paint My Bed** is an interactive web app that lets you color a stylized bed illustration. You can:

- **Click** any part of the bed (pillow, duvet, bolster, throw) to fill it with your chosen color
- **Auto-generate** harmonious color combinations from curated Sanzo Wada palettes
- **Lock** individual items to keep their color while regenerating the rest
- **Undo** up to 30 steps or **clear** everything at once
- **Enter custom HEX codes** for any color you want

---

## 📁 Project Structure

```
paint-my-bed-main/
├── src/
│   └── main.jsx            # React entry point
├── assets/                 # SVG assets (bed, character, buttons)
│   ├── paint-my-bed-title.svg
│   ├── mr.jodigo.svg
│   ├── paint-button.svg
│   ├── paint-button-hover.svg
│   └── throw.svg
├── paint-my-bed-fixed.jsx  # Main app component
├── index.html
├── package.json
└── vite.config.js
```

---

## ⚙️ Installation & Setup

**Prerequisites:** [Node.js](https://nodejs.org/) v18+

```bash
# 1. Navigate to the project folder
cd paint-my-bed-main

# 2. Install dependencies
npm install

# 3. Start the development server
npm run dev
```

Open your browser at **http://localhost:5173**.

To build for production:
```bash
npm run build
```

---

## 🎨 How to Use

### Manual coloring
1. Pick a color from the **color palette** on the left
2. Click any zone on the bed (pillow, duvet, throw, bolster)
3. The fill animates as an expanding circle from your click point (Procreate-style)

### Auto-color ("Paint" button)
- Press the **PAINT** button for an automatic harmonious color scheme
- Filter palettes by **vibe**: `warm`, `cool`, `earth`, `jewel`, `pastel`, and more
- **Lock 🔒** any item to keep its color when regenerating the others

### Controls summary

| Action | How |
|---|---|
| Undo | ↩ button (up to 30 steps) |
| Clear all | 🗑 trash button |
| Custom color | Type a HEX code in the input field |
| Toggle throw blanket | Toggle in the Throw panel |
| Browse all palettes | "Browse" button |

---

## 🧠 How It Works (Technical)

### SVG-based Flood Fill

The core of the app is a custom JavaScript **flood fill** algorithm:

1. The bed SVG (embedded as base64) is drawn onto a hidden `<canvas>`
2. Dark pixels become **boundary walls** that constrain fill regions
3. On click, the algorithm spreads color from that pixel to all adjacent light pixels, stopping at boundaries
4. Results are drawn on a second canvas overlaid on the SVG
5. The throw (blanket) uses an **inverse flood-fill mask** — color floods outward from all edges to determine what is "inside"

### ColorDrop Animation

Each fill triggers an expanding-circle animation:
- A pixel diff is computed between the before/after canvas states
- The diff image is revealed with an animated `clip-path: circle()` expanding from the click origin

### Sanzo Wada Palettes

Color combinations come from the classic *Dictionary of Color Combinations* by Sanzo Wada — a foundational design reference. The app includes dozens of 2-, 3-, and 4-color combinations, filterable by mood/vibe.

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [React](https://react.dev/) | 18.x | UI framework |
| [Vite](https://vitejs.dev/) | 5.x | Build tool / dev server |
| HTML Canvas API | — | Flood fill & rendering |
| Inline SVG (base64) | — | Bed illustration & masks |

---

*Built with ❤️ — inspired by interior design and color theory.*

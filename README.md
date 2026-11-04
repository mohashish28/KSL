# KSL

An interactive 3D poster studio that runs in a single HTML file. Drop in an image and it becomes a piece of paper you can bend, crumple, fold, light, set on fire and shred. Add your own `.glb` 3D models next to it, spin them, resize them and let them fall and pile up under gravity.

No build step, no install, no backend. Everything lives in `KSL.html`.

## Features

**Poster**
- Drag and drop any image (or use **Choose image**) to replace the poster.
- Grab the paper and drag to bend it. It springs back when you let go.
- **Crumple** slider with three crease styles (Zigzag, Accordion, Fan) and a **Random crumple** button for a new pattern.
- **Fold in half / Unfold**, up to 7 folds, each one folds the stack again.
- **Flatten paper** resets every fold and crease.
- **Ripping mode** tears the paper. Turn it on, then grab the poster and pull: the part you grab rips off along a random ragged edge and falls to the bottom edge of the canvas. The **Grab size** slider sets how big the tear is, from a small scrap to a large chunk, and a dashed ring shows the size under your pointer. Torn pieces come to rest on the floor, and **Restore paper** puts everything back. Up to 40 loose pieces are kept, and the oldest is removed beyond that.
- **Spray mode** lets you vandalize the poster like a street wall. Turn it on, pick a color (ten street colors or any color from the picker), set the **Spray radius**, then hold and drag over the poster. The paint is fine speckle with a soft mist, and it builds up if you keep the can on one spot. Stay put long enough and it runs in drips (the **Drips** slider sets how readily). The paint sits on the paper, so it bends, folds, burns and tears with it. **Clear paint** wipes it, and ripping and spraying can't be on at the same time.
- **Shred poster** feeds the poster through a shredder, and the strips fall into a pile on the bottom of the canvas.
- **Fire** burns the poster from the bottom up, with an adjustable flame length.
- **Wind**, **Paper softness**, **Pixel filter** and **Halftone** (with dot size) change how the paper moves and looks.

**Lighting**
- Light position pad, light intensity, ambient light and paper gloss.

**3D models (.glb)**
- Add as many `.glb` files as you like, by drag and drop or the **Add 3D model** button.
- Click or drag a model to select it. A list in the panel also selects by name.
- Per-model **size** and **depth** sliders, drag to move on X and Y, hold Shift while dragging or scroll to move in depth.
- **Spin / stop spinning** toggle.
- **Drop models** makes them fall under gravity onto the bottom edge of the canvas. They collide with each other, the floor and the side walls, and you can pick one up and drop it again.
- **Remove selected** deletes the current model.

**Camera and controls**
- Drag the background to turn the whole scene. Scroll or pinch (touch) to zoom.
- **Hand control** uses your webcam: pinch thumb and index finger to grab and drag, pinch with both hands and spread to zoom, or hold up two fingers and move your hand toward or away from the camera.

## Running it

Open `KSL.html` in a modern browser. That's it.

Some browsers restrict the webcam on `file://` pages, so if **Hand control** says the camera is blocked, serve the folder locally instead:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/KSL.html
```

An internet connection is needed on first load, because the libraries come from a CDN.

## Notes and limits

- Only single-file `.glb` models work. A `.gltf` that points to separate texture files will not load.
- Model collisions use each model's bounding box, so L-shaped or ring-shaped models touch earlier than their outline would.
- Models collide in the visible plane only, not in depth.
- Hand control downloads a hand-tracking model the first time you turn it on, so it needs network access.
- Everything runs in the browser. Images and models you add are never uploaded anywhere.

## Built with

- [three.js](https://threejs.org/) r128, loaded from a CDN, with its `GLTFLoader` for `.glb` files
- [MediaPipe Tasks Vision](https://developers.google.com/mediapipe) (hand landmarker) for webcam hand control
- A position-based paper simulation and fold/crease poses adapted from kaik's `paper.js` and `pose.js`

## License

No license has been chosen yet. Add a `LICENSE` file before publishing if you want others to be able to reuse the code.

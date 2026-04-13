# Image Padding Tool Requirements & Plan

## 1. Core Functionality
- **Goal**: Convert a 4:5 aspect ratio image (4 width, 5 height) into a 9:16 aspect ratio image.
- **Method**: Add a transparent background evenly to the top and bottom of the original image without altering its width or distorting its contents.
- **Input**: User-uploaded image (e.g., `20260413-140946.png`).
- **Output**: A new `.png` image (to support transparency) with the 9:16 ratio.

## 2. Proposed Technical Stack & Open Source Options
Since the goal is to host a **public site** for free on **GitHub Pages**, we need to change our approach. GitHub Pages only hosts *static* files (HTML, CSS, JavaScript) and cannot run a Python or Node.js server.

### Option C: Pure HTML/JS with HTML5 Canvas (Selected Approach)
- **Image Processing**: We will use the browser's built-in **HTML5 `<canvas>`** to manipulate the image. All processing happens locally on the user's device, which is fast, private, and requires zero server costs.
- **Web UI**: A simple, lightweight HTML/CSS interface.
- **Deployment**: Can be hosted completely for free on **GitHub Pages**. You just push the HTML file to a GitHub repository and turn on Pages.

## 3. Implementation Steps (Plan)
1. **Frontend**: Create a single `index.html` file that contains the layout, styles, and the file upload logic.
2. **Core Logic (Client-Side JavaScript)**:
   - Read the user's uploaded image using the `FileReader` API.
   - Calculate the target height based on the original width to achieve a 9:16 ratio: `target_height = current_width * (16 / 9)`.
   - Create an invisible HTML5 `<canvas>` with dimensions `(current_width, target_height)`.
   - Draw the original image onto the canvas at the exact vertical center: `y_offset = (target_height - original_height) / 2`.
   - Export the canvas as a transparent `.png` data URL.
3. **Download**: Provide a button for the user to download the final padded image.
4. **Testing**: Open `index.html` locally in the browser and test it with `20260413-140946.png`.

## 4. Next Steps
- Please review this updated plan.
- Let me know which stack you prefer (Option A is recommended for speed and simplicity). Once aligned, we can begin the implementation!
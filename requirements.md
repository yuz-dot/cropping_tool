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
1. **Frontend**: Create a single `index.html` file that contains the layout, styles, and the file/folder upload logic. Include the `JSZip` library via CDN for bulk downloading.
2. **Core Logic (Client-Side JavaScript)**:
   - Allow users to upload a whole folder of images using `<input type="file" webkitdirectory multiple>`.
   - Read the uploaded images using the `FileReader` API.
   - Preview the first image so the user can adjust the scaling slider (default 91.1%).
   - Loop through all uploaded images:
     - Calculate the target height based on the original width to achieve a 9:16 ratio.
     - Create an invisible HTML5 `<canvas>` with dimensions `(current_width, target_height)`.
     - Draw the original image onto the canvas at the exact vertical center.
     - Export the canvas as a transparent `.png` data URL.
     - Add the image to a ZIP file.
3. **Bulk Download**: Provide a button that triggers the bulk processing, compresses all padded images into a `.zip` file using JSZip, and prompts the user to download it.
4. **Testing**: Open `index.html` locally in the browser and test it with a folder of 4:5 images.

## 4. Next Steps
- Please review this updated plan.
- Let me know which stack you prefer (Option A is recommended for speed and simplicity). Once aligned, we can begin the implementation!
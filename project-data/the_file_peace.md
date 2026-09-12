### Project Description

> `The File Peace` is a privacy-first browser-based utility suite for working with PDFs and other files without uploading them to a remote server. The application performs document processing directly on the user's device, combining a responsive interface with client-side file processing and background workers.

### Why I Built It

> Many online file-processing tools require users to upload documents to external servers. `The File Peace` was built around a different approach: keep the processing in the browser whenever possible, so users can work with their files without depending on a backend service.

### Tech Stack & Architecture

- **Frontend:** React, Vite
- **PDF Processing:** `pdf-lib`, `pdf.js`
- **Background Processing:** Web Workers
- **Architecture:** Client-side, offline-capable processing
- **UI:** Custom CSS, CSS variables, light/dark themes

---

### Application Walkthrough

#### 1. Tool Dashboard

The application starts with a centralized dashboard where users can discover and access the available file utilities.

The interface is organized by functionality so users can quickly find the tool they need.

![The File Peace Dashboard](/project-assets/the-file-peace/file-peace-dashboard.png)

---

#### 2. Light & Dark Themes

The application supports both light and dark themes, allowing the interface to adapt to user preference while maintaining the same workflows and functionality.

![The File Peace Light Theme](/project-assets/the-file-peace/file-peace-lightmode.jpg)

![The File Peace Dark Theme](/project-assets/the-file-peace/file-peace-darkmode.jpg)

---

#### 3. PDF Organization

The PDF organization workflow allows users to work with individual pages visually rather than managing page numbers manually.

Using `pdf.js` and a Web Worker, PDF pages are rendered into interactive thumbnails that can be reordered, removed, and appended directly in the browser.

![PDF Organization](/project-assets/the-file-peace/file-peace-organize.jpg)

---

#### 4. PDF Watermarking

The watermarking tool allows users to add custom text to PDF pages while controlling properties such as:

- Text content
- Opacity
- Rotation
- Size
- Color
- Position

The final PDF is generated locally using `pdf-lib`.

![PDF Watermarking](/project-assets/the-file-peace/file-peace-watermark.jpg)

---

### Key Capabilities

The current application includes utilities for:

- **Merge PDF** — combine multiple PDF documents into one
- **Split PDF** — extract selected pages or page ranges
- **Rotate PDF** — change page orientation
- **Compress PDF** — optimize PDF output
- **PDF to Image** — convert PDF pages into images
- **Image to PDF** — create PDF documents from images
- **Image Conversion** — convert between supported image formats
- **PDF Page Organization** — visually reorder, remove, and append pages
- **Watermark PDF** — add configurable text watermarks to documents
- **Video Compression** — browser-based media processing using WebAssembly

---

### Engineering Highlights

- **Client-side processing:** Files can be processed directly in the browser instead of being uploaded to a backend.
- **Web Worker integration:** Heavy PDF processing can run outside the main UI thread to keep the interface responsive.
- **Interactive document workflows:** PDF pages are rendered as visual thumbnails to make complex operations easier to understand.
- **Local file handling:** File data is handled within the browser during processing.
- **Performance-conscious processing:** The application uses browser memory and binary data handling techniques to support multi-file workflows.

---

### Project Links

- **Live Application:** [The File Peace](https://mnk17arts.github.io/the_file_peace/)
- **Public Repository:** [GitHub Repository](https://github.com/mnk17arts/the_file_peace)

### Project Status

> Actively maintained and evolving with additional file-processing utilities and improvements to the client-side experience.
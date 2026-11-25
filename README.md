# PDF Merger

A single-file, offline browser tool to merge PDFs and turn scanned images (JPEG/PNG) into full PDF pages – with live preview, page selection, compression and AES-256 password protection.

Everything runs locally in your browser. No upload, no server, no installation.

---

## Why?

Many scanners only produce JPEG or PNG files. PDF Merger combines those scans with existing PDFs into one clean PDF document – quickly and without sending your documents to an online service.

## Features

**Input**
- PDF, JPEG, PNG, WebP, BMP, GIF – via drag & drop, file dialog or paste (Ctrl+V)
- Detects the real image format by file content (e.g. a JPEG saved as `.png`)
- Respects EXIF orientation of photos/scans
- Password-protected PDFs can be unlocked and used as input

**Arranging**
- Reorder by drag & drop or ↑/↓ buttons, sort A→Z, reverse order
- Rotate images and PDFs in 90° steps
- Insert blank pages
- Pick individual pages from a PDF – visually (click thumbnails, Shift+click for ranges, All/None/Invert/Odd/Even) or by typing ranges such as `1-3, 5, 8-`

**Page size & layout (images)**
- A3, A4, A5, US Letter, US Legal, custom size (mm) or “fit page to image”
- Orientation: auto, portrait, landscape
- Scaling: fit, fill (crop), stretch, actual size (by scan DPI)
- Image size on page (10–100 %), vertical position, margin, background color
- Optional: scale PDF pages to the same page size

**Quality & file size**
- Keep original quality or compress as JPEG (quality slider)
- Limit resolution (300 / 200 / 150 / 100 / 72 DPI)
- Grayscale conversion
- Convert PDF pages to images – shrinks scanned PDFs
- The preview header shows the exact resulting file size while you adjust settings

**Preview**
- Live thumbnails of the final PDF, updated automatically
- Zoomable page viewer: +/−, Ctrl+mouse wheel, Fit, Width, 100 %, pan by dragging, arrow keys to flip pages
- “Open ↗” opens the result in the browser’s built-in PDF viewer

**Extras**
- Page numbers: position, format (`1`, `1 / 12`, `Page 1 of 12`, `- 1 -`), start number, font size, skip first page, white background box
- Document info: title, author, subject, keywords, file name
- Password protection with AES-256, optional permission restrictions (printing, copying, editing) and owner password
- Settings are remembered in the browser (passwords are **never** stored)

## Usage

1. Open `pdf-merger.html` in a current browser (Chrome, Edge, Firefox, Safari) – a double-click is enough.
2. Drop files onto the drop zone (or click it / paste with Ctrl+V).
3. Arrange the list; for PDFs use **Select pages…** if you only need some pages.
4. Adjust settings and check the preview on the right.
5. Click **Download PDF**.

### Keyboard shortcuts (page viewer)

| Key | Action |
|---|---|
| ← / → | Previous / next page |
| + / − | Zoom in / out |
| 0 | Fit whole page |
| 1 | Actual size (100 %) |
| Esc | Close viewer / page picker |

## Typical settings

| Goal | Settings |
|---|---|
| Scans as A4 document, original quality | Page size A4, Orientation Auto, Scaling Fit |
| Small file for email | Images: Compress (JPEG), quality 60–75, max. 150 DPI |
| Text documents, very small | additionally Grayscale |
| Shrink an existing scanned PDF | PDF files: Convert to images, 150 DPI, compression on |
| Scan pages without white borders | Page size: Fit page to image, Scan resolution = scanner DPI |

## Security & privacy

- All processing happens locally in the browser; the file makes no network requests.
- Encryption uses **AES-256** (PDF 2.0 / revision 6 security handler).
- Encryption is applied only when downloading; the preview shows the unprotected content.
- Permission restrictions (no printing/copying/editing) are honored by most PDF readers but are **not** a hard barrier – only the open password actually protects the content.
- Choose a strong password (12+ characters); the tool shows a simple strength hint.

## Limitations

- HEIC/HEIF images (iPhone) are only readable in Safari – otherwise export them as JPEG first.
- “Scale to page size” and “Convert to images” drop links and form fields of the affected PDFs; “Convert to images” also makes text non-selectable.
- Very large images are downscaled to about 16.7 megapixels where needed (canvas limit of Safari/iOS).
- Very large jobs (hundreds of high-resolution scans) are limited by the browser’s available memory.
- The preview thumbnails are rendered from a lightweight copy; compression artifacts are only visible in the zoomable viewer.

## Technical details

- One self-contained HTML file (~2.2 MB), no dependencies at runtime
- PDF creation: [@cantoo/pdf-lib](https://github.com/cantoo-scribe/pdf-lib) 2.11.1 (fork of pdf-lib with encryption support), MIT license
- Rendering/preview: [PDF.js](https://github.com/mozilla/pdf.js) 3.11.174 (legacy build), Apache-2.0 license – the worker is loaded from an embedded blob
- Performance: processed images, parsed PDFs and rasterized pages are cached; outdated preview builds are aborted; thumbnails are built from a downscaled proxy document


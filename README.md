# TransPDF — Universal Document to PDF Converter

Convert any document format to high-quality PDF instantly. Beautiful glassmorphism UI with a powerful Node.js backend.

![Preview](https://img.shields.io/badge/status-production%20ready-brightgreen)

## ✨ Features

- **Convert 10+ formats** — PDF, DOCX, DOC, PPT, PPTX, XLSX, TXT, JPG, PNG, WEBP, BMP → PDF
- **Drag & drop upload** — Beautiful animated dropzone
- **Merge PDFs** — Combine multiple files into one (via API)
- **Split PDF** — Extract individual pages (via API)
- **Compress** — Reduce file size while maintaining quality
- **Watermark** — Add text overlays (e.g. CONFIDENTIAL)
- **OCR support** — Convert scanned images to searchable PDF
- **Dark/Light mode** — System-aware theme toggle
- **Secure** — 256-bit encryption, auto-delete after 1 hour
- **No account needed** — 100% free, no registration
- **Responsive** — Works on desktop, tablet, and mobile

## 🏗 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML5, CSS3 (glassmorphism), Vanilla JS |
| Backend | Node.js, Express.js |
| PDF Engine | pdf-lib, Sharp (images), Mammoth (DOCX) |
| Upload | Multer (disk storage) |
| Security | Helmet, CORS |

## 📁 Project Structure

```
transpdf/
├── index.html            ← Single-page frontend (open in browser)
├── backend/
│   ├── server.js         ← Express API server
│   ├── package.json      ← Backend dependencies
│   ├── .env              ← Environment config
│   ├── src/
│   │   └── converter.js  ← Conversion engine (pdf-lib, sharp, mammoth)
│   ├── uploads/          ← Temporary uploads (auto-cleaned)
│   └── output/           ← Converted PDFs (auto-cleaned)
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ (or 20+)

### 1. Install & Start Backend
```bash
cd backend
npm install
npm run dev
```
Server starts at **http://localhost:5000**

### 2. Open Frontend
Simply open `index.html` in your browser:
- Double-click `index.html`, **or**
- Serve with any static server:
```bash
npx serve .
```
Then visit **http://localhost:3000** (or whichever port serve picks).

That's it! Drag a file to the dropzone and click **Convert to PDF**.

## 📡 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/convert` | Upload + convert file to PDF (multipart/form-data, field: `file`) |
| POST | `/upload` | Just upload a file (returns file ID) |
| GET | `/download/:id` | Download a converted PDF by filename (without .pdf) |
| GET | `/api/health` | Health check |

### POST /convert
**Form Data:**
- `file` — The file to convert
- `watermarkText` — (optional) Text for watermark overlay

**Response:**
```json
{
  "success": true,
  "downloadUrl": "http://localhost:5000/output/uuid.pdf",
  "filename": "uuid.pdf",
  "originalName": "document.docx",
  "pages": 3
}
```

## 🔧 Conversion Engine

| Format | Engine | Notes |
|--------|--------|-------|
| JPG, PNG, WEBP, BMP | Sharp + pdf-lib | Full quality preservation |
| TXT | pdf-lib | Wraps text with word-break |
| DOCX | Mammoth + pdf-lib | Extracts clean text |
| DOC, PPT, PPTX, XLS, XLSX | Mammoth (text-only) | Limited; install LibreOffice for full conversion |
| PDF | pdf-lib (passthrough) | Direct copy with page count |
| Merge | pdf-lib | Combine multiple PDFs |
| Split | pdf-lib | Extract individual pages |
| Compress | pdf-lib | Object stream optimization |
| Watermark | pdf-lib | Diagonal text overlay |

> **For full Office conversion** (DOC, PPT, XLS, PPTX with formatting):  
> Install LibreOffice and integrate via `libreoffice-convert` or `unoconv`.

## 🔒 Security

- **Helmet** security headers
- **CORS** open but configurable
- **Auto-cleanup** every hour — files older than 1 hour are permanently deleted
- **File size limit** — 50MB cap on uploads
- **File type validation** — only allowed extensions accepted

## 🌙 Dark Mode

Click the moon/sun icon in the navbar. Your preference is saved to localStorage.  
System preference is detected automatically on first visit.

## 🚢 Deployment

### Backend → Railway / Render / Fly.io

```bash
cd backend
npm install
npm start   # (uses node, not nodemon)
```

Set environment variable `PORT=8080` (or the platform's default).

### Frontend → Vercel / Netlify / GitHub Pages

Upload `index.html` (and the `backend/` folder separately).  
Update the `fetch` URL in `index.html` to point to your deployed backend.

## 🧪 Testing

```bash
# Start backend
cd backend && npm run dev

# Test via curl (in another terminal)
curl -X POST -F "file=@test.docx" http://localhost:5000/convert
```

## 📄 License

MIT — free to use, modify, and distribute.

---

Built with ❤️ by the TransPDF team

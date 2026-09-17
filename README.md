# 📄 PDF SaaS — All-in-One PDF, Image & Developer Tools Suite

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-16.2.6-black?style=for-the-badge&logo=next.js" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React 19" />
  <img src="https://img.shields.io/badge/TypeScript-5.x-blue?style=for-the-badge&logo=typescript" alt="TypeScript" />
  <img src="https://img.shields.io/badge/TailwindCSS-v4-38B2AC?style=for-the-badge&logo=tailwind-css" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License MIT" />
</p>

<p align="center">
  A modern, high-performance, and privacy-first SaaS platform offering <b>50+ professional tools</b> for PDFs, office documents, images, text, and developer utilities — all wrapped in an interactive, responsive UI.
</p>

---

## ⚡ Key Highlights

- 🔒 **Privacy-First Architecture:** Files processed locally in the browser whenever possible. Server-side jobs process files purely **in-memory** with immediate return and **zero persistent file storage**.
- 🚀 **50+ Integrated Tools:** PDF suite, document format conversions, image manipulation, OCR engine, and developer calculators.
- 🎨 **Modern Interactive Workspaces:** Dual-pane visual previewers, drag-and-drop page organizers, PDF signature canvas, live diff comparison, and Monaco-powered code editors.
- 🐳 **Docker-Ready Production Engine:** Containerized setup bundled with LibreOffice, Ghostscript, Poppler, qpdf, and Tesseract OCR for seamless deployment.
- 📊 **Built-in SaaS & Admin Hub:** Complete admin portal for contact messages, newsletter subscriptions, feedback & suggestion pipelines, and analytics.

---

## 🛠️ Complete Feature Matrix

### 1. 📑 PDF Core & Manipulation
| Tool | Execution | Description |
| :--- | :--- | :--- |
| **Merge PDF** | 🌐 Client (`pdf-lib`) | Combine multiple PDF documents in custom order. |
| **Split PDF** | 🌐 Client (`pdf-lib`) | Extract individual pages or ranges into separate PDFs. |
| **Organize PDF** | 🌐 Client | Drag-and-drop visual page reordering and layout manager. |
| **Remove Pages** | 🌐 Client | Select and delete unwanted pages with live visual preview. |
| **Extract Pages** | 🌐 Client | Isolate specific pages and save them into a new document. |
| **Rotate PDF** | 🌐 Client | Rotate pages by 90°, 180°, or 270° individually or in bulk. |
| **Scan to PDF** | 🌐 Client | Capture documents using device camera and package as PDF. |

---

### 2. 🔄 Document & Office Conversions
| Tool | Execution | Engine / Requirements |
| :--- | :--- | :--- |
| **PDF to Word (DOCX)** | 🖥️ Server | LibreOffice / Image-based zero-margin precision |
| **PDF to Excel (XLSX)** | 🖥️ Server | LibreOffice (`soffice`) spreadsheet engine |
| **PDF to PowerPoint (PPTX)** | 🖥️ Server | LibreOffice presentation converter |
| **Word to PDF** | 🖥️ Server | Document format rendering to PDF |
| **Excel to PDF** | 🖥️ Server | Sheet-to-PDF layout engine |
| **PowerPoint to PDF** | 🖥️ Server | Presentation slide vector rendering |
| **HTML to PDF** | 🖥️ Server | Web page & HTML markup to PDF converter |
| **PDF to PDF/A** | 🖥️ Server | Archival compliance via Ghostscript |
| **PDF to Text** | 🖥️ Server | Plaintext extraction pipeline |

---

### 3. 🛡️ Security, Annotation & Advanced PDF
| Tool | Execution | Engine / Details |
| :--- | :--- | :--- |
| **OCR PDF** | 🖥️ Server | Tesseract OCR engine with searchable text layers |
| **Compare PDF** | 🖥️ Server | Side-by-side visual diff and pixel comparison report |
| **Repair PDF** | 🖥️ Server | Fix corrupt or damaged PDF trees using `qpdf` |
| **Compress PDF** | 🖥️ Server | Multi-tier size optimization via Ghostscript |
| **Sign PDF** | 🌐 Client | Interactive canvas signature pad and placement tool |
| **Watermark PDF** | 🌐 Client | Custom text/image watermarks with opacity & rotation |
| **Page Numbers** | 🌐 Client | Positioned page number formatting (top/bottom/margins) |
| **Redact PDF** | 🌐 Client | Visual black-box rectangle redaction tool |
| **Crop PDF** | 🌐 Client | Interactive crop box margin adjustments |
| **Protect PDF** | 🖥️ Server | 128-bit / 256-bit AES password encryption |
| **Unlock PDF** | 🖥️ Server | Remove password security with authorized credential |

---

### 4. 🖼️ Image Suite & Format Converters
| Tool | Types Supported |
| :--- | :--- |
| **Format Converters** | JPG ⇄ PNG, WebP ⇄ JPG, HEIC → JPG, AVIF → JPG, SVG → PNG, BMP → JPG, GIF → PNG |
| **PDF ⇄ Image** | PDF to JPG, PDF to PNG, JPG/PNG to PDF, Batch Image to PDF with live sorting |
| **Image Optimization** | Compress Image, Resize by Dimensions/Percentage, Crop Image, Rotate Image |
| **Image Editor** | Visual filter, brightness, contrast, and enhancement adjustments |

---

### 5. ✍️ Text, Academic & Document Tools
- **Markdown to PDF & Word:** Live markdown previewer with export to PDF or DOCX.
- **LaTeX to Word:** Convert mathematical & scientific TeX formulas and documents.
- **RTF to PDF:** Rich Text Format parsing and conversion.
- **EPUB to PDF:** Digital eBook parsing and reflowable page rendering.
- **Pages to Word:** Apple Pages document conversion.

---

### 6. 💻 Developer Utilities & Calculators
- 🔍 **JSON Formatter & Inspector:** Dual-tab Monaco editor and visual tree inspector matching `jsonviewer`.
- 🔤 **Encoders & Decoders:** Base64 Encode/Decode, URL Encode/Decode, Hash Generator (MD5, SHA-1, SHA-256, SHA-512).
- 🧮 **Calculators:** Percentage Calculator, Age Calculator, BMI Calculator, Unit Converter.

---

## 🏛️ Architecture & Privacy Design

```
                     ┌──────────────────────────────────────────────┐
                     │              Client (Browser)                │
                     │  Next.js 16 + React 19 + Tailwind CSS        │
                     └───────┬──────────────────────────────┬───────┘
                             │                              │
         [Client-Side Tools] │                              │ [Heavy Server Tasks]
      (pdf-lib, Canvas, Web Worker)                         │ (Multipart Stream)
                             ▼                              ▼
                 Processed Locally                ┌──────────────────┐
                 No data leaves device            │  Next.js Engine  │
                                                  │   /api/process   │
                                                  └────────┬─────────┘
                                                           │
                                             ┌─────────────┴─────────────┐
                                             ▼                           ▼
                                     Docker Worker Binaries        Express API
                                    (soffice, gs, qpdf, etc.)    (Auth, CRM, Mail)
                                             │
                                     In-Memory Stream
                                    No File Persistence
```

- **Zero Permanent Storage:** Incoming files are held in temporary memory during conversion and destroyed as soon as the response stream closes.
- **Client Processing First:** Lightweight operations (splitting, merging, canvas signing, watermarking, image manipulation) happen entirely within the browser via WebAssembly and HTML5 Canvas.

---

## 🚀 Quick Start (Local Development)

### 1. Prerequisites
- **Node.js:** v20.x or higher
- **npm:** v10.x or higher
- **Docker Desktop:** (Optional, recommended for testing server CLI tools locally)

### 2. Clone Repository
```bash
git clone https://github.com/razeejafri/pdf-saas.git
cd pdf-saas
```

### 3. Setup Environment Variables
```bash
cp .env.example apps/web/.env
```

### 4. Install Dependencies
```bash
npm run install:optional
```

### 5. Start Development Server
```bash
# Runs Next.js frontend on http://localhost:3000
npm run dev
```

> **Note:** Server tools like LibreOffice conversion or Ghostscript compression require either Docker or local CLI binaries installed on your host.

---

## 🐳 Running with Docker (Recommended)

Docker packages all system tools (`soffice`, `ghostscript`, `qpdf`, `pdftoppm`, `tesseract`) out of the box:

```bash
# 1. Build Docker image
npm run docker:build

# 2. Start container in background
npm run docker:up

# 3. View live server logs
npm run docker:logs

# 4. Stop containers
npm run docker:down
```

Check that all system dependencies are recognized:
```bash
curl http://localhost:3000/api/health
# Response: {"status":"ok","serverToolsReady":true}
```

---

## 📦 Host-Side CLI Installation (Without Docker)

If you prefer running without Docker, install the required binaries natively:

### macOS (Homebrew)
```bash
brew install libreoffice ghostscript qpdf poppler tesseract
```

### Ubuntu / Debian
```bash
sudo apt-get update && sudo apt-get install -y \
  ghostscript \
  poppler-utils \
  qpdf \
  tesseract-ocr \
  tesseract-ocr-eng \
  libreoffice-writer \
  libreoffice-calc \
  libreoffice-impress \
  libreoffice-core-nogui \
  fonts-dejavu-core \
  fonts-liberation
```

Verify your setup:
```bash
npm run tools:check
```

---

## 📁 Project Structure

```text
pdf-saas/
├── apps/
│   ├── web/                     # Next.js 16 App Router UI & Process API routes
│   │   ├── src/app/             # Pages, categories & tool workspaces
│   │   ├── src/components/      # Interactive tool UI components & layouts
│   │   └── src/lib/             # Processing pipeline & security utilities
│   └── api/                     # Express.js microservice (Auth, CRM, Feedback)
│       └── src/                 # Models, controllers, routes & mailers
├── packages/
│   └── shared/                  # Shared types, tool registry & constants
├── docs/
│   └── VPS_DEPLOYMENT_GUIDE.md  # Step-by-step VPS production deployment guide
├── scripts/                     # Dependency checker & setup scripts
├── Dockerfile                   # Multi-stage production container
├── docker-compose.yml           # Production Docker Compose orchestration
└── package.json                 # Monorepo workspace configuration
```

---

## 🌐 Production VPS Deployment

For a complete walkthrough on deploying this project to a cloud VPS (Ubuntu, Hostinger, DigitalOcean, AWS, Hetzner) with Nginx reverse proxy, Docker, and free SSL:

👉 See the comprehensive [VPS Deployment Guide](docs/VPS_DEPLOYMENT_GUIDE.md).

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!
Feel free to check the [issues page](https://github.com/razeejafri/pdf-saas/issues).

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'feat: add some amazing feature'`)
4. Push to the branch (`git push -u origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

<p align="center">
  Built with ❤️ by <a href="https://github.com/razeejafri">Razee Jafri</a>
</p>

---
name: study-hub-builder
description: "Trigger: nueva unidad, armar unidad, apunte maestro, study hub, tracker de lectura, resumen facultad. Build interactive academic study hubs with KaTeX apunte maestro, postMessage PDF page jump diagrams, live note studio, and reading tracker."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Activate this skill whenever the user requests:
- Creating or structuring a new university study unit (e.g., *Unidad 1, Unidad 2, Unidad 3, Unidad 6, etc.*).
- Building an interactive **Studio Hub** (`index.html`) with dark mode, PDF reader, and note-taking tools.
- Generating an exhaustive **Apunte Maestro** (`APUNTE_MAESTRO_UNIDAD_X.html` / `.md`) with KaTeX equations and high-res cropped book diagrams.
- Implementing the **Reading & Study Tracker** with direct action buttons (`📖 Leer en Apunte`, `📄 Abrir PDF`, `📝 Ver Resolución`).
- Ensuring all embedded diagrams have interactive click-to-jump navigation to the exact page of the textbook/PDF using `postMessage`.

## Hard Rules

1. **Folder Architecture**: Every unit MUST follow the standard directory structure:
   - `0_General_y_Libros/`: Official textbooks, theory slides, and questionnaires + resolved markdown files (`RESOLUCION_Cuestionario_*.md`).
   - `1_Submodulo_A/` & `2_Submodulo_B/`: Sub-modules containing consignas, PDFs, datasets, and complete step-by-step resolutions (`RESOLUCION_TP*.md`).
   - `imagenes_apunte/`: HD cropped figures extracted directly from textbook PDFs with PyMuPDF (`fitz`).
   - `index.html`: Central Studio Hub interface.
   - `APUNTE_MAESTRO_UNIDAD_X.html` & `.md`: Master textbook-grade study guide.
   - `README.md`: Centralized index of files and resources.

2. **Interactive Diagram Navigation (Mandatory `postMessage`)**:
   - Every diagram in `APUNTE_MAESTRO_UNIDAD_X.html` MUST be wrapped in an interactive `.img-container` with an `openPdfPage(pdfPath, pageNum, event)` trigger.
   - The trigger MUST use HTML5 `window.parent.postMessage({ type: 'LOAD_PDF', url: fullUrl, page: pageNum }, '*')` so clicking inside the iframe switches the Hub to the `📑 Visor de PDFs` tab at the exact page.
   - MUST include a direct `<a href="..." target="_blank">` fallback with the badge `📑 Abrir en PDF (Pág. X) ↗️`.

3. **Reading Tracker with Action Buttons**:
   - Tracker rows MUST include individual action buttons next to each checkbox (Apunte anchor, PDF file, or TP resolution markdown).
   - Tracker progress MUST persist in `localStorage`.

4. **Live Note Studio**:
   - Must include real-time Markdown preview, character count, auto-save to `localStorage`, and one-click `.md` download.

5. **Theoretical Rigor**:
   - Master guides MUST be exhaustive, university-grade, incorporating all mathematical formulas in **KaTeX** (`$$...$$` and `$..$`), exact citations (Author, Year, Chapter, Page), and zero placeholder text.

## Execution Steps

1. **Extract & Crop Diagrams**: Use PyMuPDF (`fitz`) to crop all referenced figures from official textbook PDFs into `imagenes_apunte/` at `2.5x` matrix scale.
2. **Resolve All TPs & Questionnaires**: Create `RESOLUCION_*.md` files with 100% complete theoretical answers and verified mathematical calculations.
3. **Generate Apunte Maestro (`.html` & `.md`)**:
   - Include KaTeX CDN and auto-render.
   - Add Table of Contents with jump anchors.
   - Embed all cropped diagrams with `openPdfPage(...)` and `#page=N` links.
4. **Generate Studio Hub (`index.html`)**:
   - 5 Tabs: `📌 Panel de Recursos`, `📖 Lector de Apunte Maestro`, `📝 Bloc de Apuntes en Vivo`, `✅ Tracker de Lectura`, `📑 Visor de PDFs`.
   - Setup `window.addEventListener('message', ...)` to handle `LOAD_PDF`.
   - Render tracker with `trackerItems` containing action shortcuts.

## References

- Base templates: [assets/index_template.html](assets/index_template.html) and [assets/apunte_template.html](assets/apunte_template.html).
- Reference implementations: [Unidad 4 Studio](file:///Users/santi/Desktop/Facultad/Unidad_4_Desarrollo_y_Mantenimiento/index.html) and [Unidad 5 Studio](file:///Users/santi/Desktop/Facultad/Unidad_5_Seguimiento/index.html).

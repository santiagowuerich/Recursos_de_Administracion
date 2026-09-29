# 📚 Recursos de Administración de Sistemas de Información (AdmSI)
### Universidad Tecnológica Nacional — Facultad Regional Resistencia (UTN FRRe)

Bienvenido al repositorio central de recursos, apuntes maestros, trabajos prácticos y guías interactivas para la cátedra de **Administración de Sistemas de Información**.

---

## 🏛️ Estructura del Repositorio

```
Recursos_de_Administracion/
├── .agents/
│   └── skills/
│       └── study-hub-builder/          # Skill autónoma para construir nuevas unidades
│           ├── SKILL.md
│           └── assets/
│               ├── index_template.html
│               └── apunte_template.html
│
├── Unidad_4_Desarrollo_y_Mantenimiento/ # 👥 Unidad 4: Desarrollo y Mantenimiento de RRHH
│   ├── index.html                      # Studio Hub interactivo con dark mode, PDF viewer y notas
│   ├── APUNTE_MAESTRO_UNIDAD_4.html    # Libro de estudio completo con KaTeX y diagramas HD
│   ├── APUNTE_MAESTRO_UNIDAD_4.md      # Versión Markdown completa
│   ├── 0_General_y_Libros/             # Chiavenato 5ta Ed., Cuestionarios y resoluciones integrales
│   ├── 1_Desarrollo_RRHH/              # Guías TP 4.1 y resolución Caso CORASA (Asistente Jr.)
│   ├── 2_Mantenimiento_RRHH/           # Guías TP 4.2, Compensaciones, Personio, Ergonomía PPV
│   ├── imagenes_apunte/                # 15 diagramas HD recortados del libro oficial
│   └── README.md                       # Índice y referencias externas
│
└── Unidad_5_Seguimiento/               # 📊 Unidad 5: Seguimiento de RRHH, SW y HW
    ├── index.html                      # Studio Hub interactivo con visor modal y auto-guardado
    ├── APUNTE_MAESTRO_UNIDAD_5.html    # Libro de estudio completo (Control, Amdahl, Molero, Sar)
    ├── APUNTE_MAESTRO_UNIDAD_5.md      # Versión Markdown completa
    ├── 0_General_y_Libros/             # Chiavenato Cap. 9/16/Parte VII, Molero et al.
    ├── 1_Seguimiento_RRHH/             # TP 5.1.A y TP 5.1.B (Taller Simulación y Evaluaciones)
    ├── 2_Seguimiento_SW_HW/            # TP 5.2 (Técnicas Analíticas, Benchmarking, SysBench)
    ├── imagenes_apunte/                # 16 diagramas HD recortados de Chiavenato y Molero
    └── README.md                       # Índice y referencias externas
```

---

## 🚀 Características del Ecosistema de Estudio

1. **Interactive Studio Hub (`index.html`)**:
   - Selector dinámico de PDFs y visor integrado.
   - Lector embebido del Apunte Maestro.
   - Bloc de apuntes en vivo con Markdown renderizado en tiempo real, contador de palabras y descarga automática de archivos `.md`.
   - Tracker de lectura y estudio con persistencia en `localStorage` y botones de acción directa (`[📖 Leer en Apunte]`, `[📄 Abrir PDF]`, `[📝 Ver Resolución]`).

2. **Libros Maestros de Estudio (`APUNTE_MAESTRO_*.html`)**:
   - Rigor conceptual y académico universitario al 100%.
   - Renderizado matemático perfecto con **KaTeX**.
   - Diagramas oficiales HD vinculados con **HTML5 `postMessage`**: al hacer clic en cualquier imagen, el visor salta directamente al número de página exacto del PDF de cátedra.

3. **Skill Automatizada (`.agents/skills/study-hub-builder`)**:
   - Permite generar instantáneamente y con los mismos estándares de diseño cualquier nueva unidad temática (*Unidad 1, Unidad 2, Unidad 3, Unidad 6, etc.*).

---

## 🛠️ Cómo Iniciar
Para abrir cualquier unidad, simplemente abre su archivo `index.html` en tu navegador:
- **Unidad 4**: Abrir [`Unidad_4_Desarrollo_y_Mantenimiento/index.html`](Unidad_4_Desarrollo_y_Mantenimiento/index.html)
- **Unidad 5**: Abrir [`Unidad_5_Seguimiento/index.html`](Unidad_5_Seguimiento/index.html)

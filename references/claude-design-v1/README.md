# References — Claude Design v1

Este folder contiene los artefactos del primer ciclo de exploración de marca y producto BaW realizado con Claude. Se conserva como referencia histórica — **no es código vivo del sistema de diseño**.

## Estructura

```
claude-design-v1/
├── README.md                          ← este archivo
├── *.html                             (10 archivos)  prototipos visuales y exploraciones de UI
└── uploads/                           (research material original)
    ├── *.pdf                          research PDF de partida
    └── *.png                          (8 capturas)   referencias visuales y mood
```

## Qué hay aquí

- **HTMLs**: prototipos navegables generados durante la fase de exploración. Cubren landing, dashboard, agent fleet view, approval hub, owner portal, tenant portal, brand site y variantes.
- **uploads/**: el material de entrada original — research en PDF + capturas de pantalla y referencias visuales que sirvieron para informar las decisiones tempranas.

## Qué NO es

- **No es** la implementación de referencia. La implementación viva está en `~/Developer/zxy-ventures/baw-os`.
- **No es** el sistema de diseño actual. Los tokens canónicos viven en `/tokens/` de este repo (`baw-design`).
- **No es** documentación normativa. La documentación normativa es `BRAND_FOUNDATIONS.md` + los ADRs en `/decisions/`.

## Por qué se conserva

Tres razones:

1. **Trazabilidad**: muchas decisiones registradas en los ADRs (especialmente 0001–0005) hacen referencia a patrones explorados aquí. Conservar los artefactos originales facilita auditar de dónde viene cada decisión.
2. **Mood y dirección visual**: las capturas en `uploads/` siguen siendo material útil para discutir dirección visual con colaboradores externos (agencia, contratistas de marca, diseñadores invitados).
3. **Anti-revisionismo**: si en el futuro alguien propone "volvamos al look de la primera versión", aquí está la primera versión, completa y sin filtros, para revisar.

## Reglas de uso

- **No editar los HTMLs**. Si surge una idea derivada de uno, se documenta como propuesta nueva en el sistema vivo, no como edición del histórico.
- **No referenciar desde producción**. Nada en `baw-os` debe importar de aquí — ni CSS, ni componentes, ni assets.
- **Sí extraer aprendizajes**. Cualquier patrón que valga la pena conservar se promueve formalmente: tokens al `/tokens/`, principios al `BRAND_FOUNDATIONS.md`, decisiones al `/decisions/`.

## Cómo abrir los HTMLs

Localmente, basta con abrirlos en el navegador. Algunos asumen que las imágenes de `uploads/` están en la ruta relativa esperada — si una imagen no carga, verificar paths.

## Contexto temporal

Este folder es un snapshot del trabajo previo a la formalización del design system. La fecha efectiva de "cierre" es cuando se creó `baw-design` como repo independiente con tokens canónicos. A partir de ese punto, este folder queda congelado.

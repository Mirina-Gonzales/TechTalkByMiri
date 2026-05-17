# 🎤 Tech Talks By Miri

Repositorio personal con mis presentaciones y charlas técnicas a lo largo de los años.

## 📂 Estructura

Las charlas se organizan por año. Cada año contiene:
- **README.md**: Lista visual de charlas del año
- **talks.json**: Metadatos estructurados en formato JSON

## 🎯 Formatos soportados

- 🎨 **Canva**: Presentaciones compartidas como embed interactivo
- 📄 **PDF**: Documentos descargables
- 🎥 **YouTube**: Videos embebidos

## 📝 Formato JSON

Cada `talks.json` contiene un array de objetos con la siguiente estructura:

```json
{
  "id": "identificador-único",
  "titulo": "Título de la charla",
  "descripcion": "Descripción breve de la charla",
  "tipo": "canva|pdf|youtube",
  "url": "https://...",
  "autor": "Nombre del evento/organizador"
}
```

### Ejemplos de URLs

- **Canva**: `https://www.canva.com/design/DAXXX/view?utm_content=DAXXX`
- **PDF**: Ruta relativa como `./archivo.pdf` 
- **YouTube**: `https://www.youtube.com/watch?v=VIDEO_ID`

## 🗺️ Navegación

Usa el menú lateral para explorar charlas por año.

---

*Última actualización: 17 de mayo de 2026*

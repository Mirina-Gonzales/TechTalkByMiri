# 2024 - Charlas Técnicas

<div id="talks-container"></div>

<script>
  async function loadTalks() {
    try {
      const response = await fetch('./talks.json');
      const talks = await response.json();
      renderTalks(talks);
    } catch (error) {
      console.error('Error al cargar talks.json:', error);
      document.getElementById('talks-container').innerHTML = '<p>No hay charlas registradas para este año.</p>';
    }
  }

  function renderTalks(talks) {
    const container = document.getElementById('talks-container');
    
    if (talks.length === 0) {
      container.innerHTML = '<p>No hay charlas registradas para este año.</p>';
      return;
    }

    const html = talks.map(talk => `
      <div style="border: 1px solid #ddd; border-radius: 8px; padding: 20px; margin-bottom: 20px; background: #f9f9f9;">
        <h3 style="margin-top: 0; color: #333;">${talk.titulo}</h3>
        <p style="color: #666; margin: 8px 0;"><strong>Fecha:</strong> ${new Date(talk.fecha).toLocaleDateString('es-ES', { year: 'numeric', month: 'long', day: 'numeric' })}</p>
        <p style="color: #666; margin: 8px 0;"><strong>Evento:</strong> ${talk.autor}</p>
        <p style="color: #555; margin: 12px 0;">${talk.descripcion}</p>
        ${talk.tags ? `<p style="margin: 8px 0;"><strong>Tags:</strong> ${talk.tags.map(tag => `<span style="background: #e0e0e0; padding: 2px 8px; border-radius: 4px; margin-right: 4px; font-size: 0.9em;">${tag}</span>`).join('')}</p>` : ''}
        <div style="margin-top: 12px;">
          ${renderContentLink(talk)}
        </div>
      </div>
    `).join('');

    container.innerHTML = html;
  }

  function renderContentLink(talk) {
    switch(talk.tipo) {
      case 'canva':
        return `
          <details>
            <summary style="cursor: pointer; color: #0066cc; text-decoration: underline;">Ver presentación Canva</summary>
            <div style="margin-top: 12px;">
              <iframe loading="lazy" style="border-radius:4px" src="${talk.url}" width="100%" height="600"></iframe>
            </div>
          </details>
        `;
      case 'pdf':
        return `<a href="${talk.url}" style="color: #0066cc; text-decoration: none; padding: 8px 16px; background: #e3f2fd; border-radius: 4px; display: inline-block;">📄 Descargar PDF</a>`;
      case 'youtube':
        return `
          <details>
            <summary style="cursor: pointer; color: #0066cc; text-decoration: underline;">Ver video</summary>
            <div style="margin-top: 12px; position: relative; width: 100%; padding-bottom: 56.25%;">
              <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border-radius: 4px;" src="${talk.url}" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            </div>
          </details>
        `;
      default:
        return `<a href="${talk.url}" style="color: #0066cc; text-decoration: none; padding: 8px 16px; background: #e3f2fd; border-radius: 4px; display: inline-block;">🔗 Acceder</a>`;
    }
  }

  // Cargar charlas cuando el DOM está listo
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', loadTalks);
  } else {
    loadTalks();
  }
</script>

# 2025 - Charlas Técnicas

<style>
  #talks-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    margin: 20px 0;
  }
  
  .talk-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 12px;
    padding: 24px;
    color: white;
    display: flex;
    flex-direction: column;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    cursor: pointer;
  }
  
  .talk-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 20px rgba(0,0,0,0.2);
  }
  
  .talk-card h3 {
    margin: 0 0 12px 0;
    font-size: 18px;
    font-weight: 600;
    line-height: 1.4;
  }
  
  .talk-card .evento {
    font-size: 13px;
    opacity: 0.9;
    margin-bottom: 12px;
    font-weight: 500;
  }
  
  .talk-card .descripcion {
    font-size: 14px;
    line-height: 1.5;
    margin-bottom: 16px;
    flex-grow: 1;
    opacity: 0.95;
  }
  
  .talk-card .btn {
    align-self: flex-start;
    padding: 8px 16px;
    background: rgba(255,255,255,0.2);
    border: 2px solid white;
    color: white;
    border-radius: 6px;
    font-size: 13px;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.3s ease;
    cursor: pointer;
  }
  
  .talk-card .btn:hover {
    background: white;
    color: #667eea;
  }
  
  .empty-state {
    grid-column: 1 / -1;
    text-align: center;
    padding: 40px;
    color: #999;
  }
</style>

<div id="talks-container"></div>

<script>
  async function loadTalks() {
    try {
      const response = await fetch('./talks.json');
      const talks = await response.json();
      renderTalks(talks);
    } catch (error) {
      console.error('Error al cargar talks.json:', error);
      document.getElementById('talks-container').innerHTML = '<div class="empty-state">No hay charlas registradas para este año.</div>';
    }
  }

  function renderTalks(talks) {
    const container = document.getElementById('talks-container');
    
    if (talks.length === 0) {
      container.innerHTML = '<div class="empty-state">No hay charlas registradas para este año.</div>';
      return;
    }

    const html = talks.map(talk => `
      <div class="talk-card">
        <h3>${talk.titulo}</h3>
        <p class="evento">🎤 ${talk.autor}</p>
        <p class="descripcion">${talk.descripcion}</p>
        ${renderButton(talk)}
      </div>
    `).join('');

    container.innerHTML = html;
  }

  function renderButton(talk) {
    const icons = { canva: '🎨', pdf: '📄', youtube: '🎥', default: '🔗' };
    const labels = { canva: 'Ver Canva', pdf: 'Descargar', youtube: 'Ver Video', default: 'Acceder' };
    const icon = icons[talk.tipo] || icons.default;
    const label = labels[talk.tipo] || labels.default;
    
    if (talk.tipo === 'canva') {
      return `<a href="${talk.url}" target="_blank" class="btn">${icon} ${label}</a>`;
    } else if (talk.tipo === 'pdf') {
      return `<a href="${talk.url}" class="btn">${icon} ${label}</a>`;
    } else if (talk.tipo === 'youtube') {
      return `<a href="${talk.url}" target="_blank" class="btn">${icon} ${label}</a>`;
    }
    return `<a href="${talk.url}" target="_blank" class="btn">${icon} ${label}</a>`;
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', loadTalks);
  } else {
    loadTalks();
  }
</script>

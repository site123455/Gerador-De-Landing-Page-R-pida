<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Gerador de Landing Page</title>
  <style>
    :root {
      --primary:#2563eb; --primary-dark:#1d4ed8;
      --bg:#f9fafb; --card:#ffffff; --text:#111827; --muted:#6b7280;
      --radius:14px;
    }
    *{box-sizing:border-box;margin:0;padding:0}
    body{font-family:"Inter",system-ui,sans-serif;background:var(--bg);color:var(--text);padding:36px;line-height:1.5;}
    .container{max-width:1080px;margin:0 auto;animation:fadeIn .6s ease}
    header{text-align:center;margin-bottom:32px;}
    header h1{font-size:26px;font-weight:700;}
    header p{font-size:15px;color:var(--muted);margin-top:6px;}
    .panel{background:var(--card);padding:28px;border-radius:var(--radius);box-shadow:0 6px 24px rgba(0,0,0,.08);animation:slideUp .6s ease;}
    .grid{display:grid;grid-template-columns:1fr 1fr;gap:24px;}
    label{font-size:13px;font-weight:500;color:var(--muted);display:block;margin-bottom:6px;}
    input,textarea,select{width:100%;padding:12px;border:1px solid #e5e7eb;border-radius:10px;font-size:14px;margin-bottom:14px;transition:border .2s,box-shadow .2s;}
    input:focus,textarea:focus,select:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 2px rgba(37,99,235,0.2);}
    textarea{resize:vertical;}
    button{background:var(--primary);color:#fff;font-weight:600;padding:12px 20px;border:none;border-radius:10px;cursor:pointer;transition:.2s;}
    button:hover{background:var(--primary-dark);transform:translateY(-1px);}
    .actions{display:flex;gap:12px;flex-wrap:wrap;margin-top:10px;}
    .preview{margin-top:28px;height:540px;border-radius:12px;overflow:hidden;border:1px solid #e5e7eb;box-shadow:inset 0 0 8px rgba(0,0,0,.05);animation:fadeIn .8s ease;}
    iframe{width:100%;height:100%;border:0;}
    footer{text-align:center;font-size:13px;color:var(--muted);margin-top:28px;}
    @media(max-width:860px){.grid{grid-template-columns:1fr}}
    @keyframes fadeIn{from{opacity:0}to{opacity:1}}
    @keyframes slideUp{from{transform:translateY(12px);opacity:0}to{transform:translateY(0);opacity:1}}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>⚡ Gerador de Landing Page</h1>
      <p>Crie uma landing page responsiva, moderna e exporte em HTML com apenas alguns cliques.</p>
    </header>

    <div class="panel">
      <div class="grid">
        <div>
          <label>Título principal</label>
          <input id="title" value="Transforme visitantes em clientes" />

          <label>Subtítulo</label>
          <input id="subtitle" value="Uma landing page simples, rápida e eficaz." />

          <label>Texto do botão CTA</label>
          <input id="cta" value="Começar agora" />

          <label>Imagem de fundo (URL)</label>
          <input id="bg" value="https://images.unsplash.com/photo-1521737604893-d14cc237f11d?q=80&w=1600&auto=format&fit=crop" />

          <label>Campo de captura</label>
          <select id="capture">
            <option value="email">E-mail</option>
            <option value="telefone">Telefone</option>
            <option value="whatsapp">WhatsApp</option>
          </select>

          <div class="actions">
            <button id="generate">Gerar preview</button>
            <button id="download">Baixar HTML</button>
            <button id="copy">Copiar HTML</button>
          </div>
        </div>

        <div>
          <label>Prova social / texto extra</label>
          <textarea id="extra" rows="4">Mais de 10.000 clientes satisfeitos</textarea>

          <label>Logo (URL)</label>
          <input id="logo" placeholder="Opcional" />

          <label>Rodapé</label>
          <input id="footer" value="© 2025 Minha Empresa" />

          <label>Tema</label>
          <select id="theme">
            <option value="light">Claro</option>
            <option value="dark">Escuro</option>
            <option value="gradient">Gradiente</option>
          </select>
        </div>
      </div>

      <div class="preview"><iframe id="frame" sandbox="allow-forms allow-scripts"></iframe></div>
    </div>

    <footer>Gerador de Landing Page — design simples, elegante e moderno</footer>
  </div>

  <script>
    function buildHTML({title,subtitle,cta,bg,capture,extra,logo,theme,footer}){
      let bgStyle;
      if(theme==='gradient') bgStyle="background:linear-gradient(135deg,#2563eb,#06b6d4);";
      else if(bg) bgStyle=`background:url('${bg}') center/cover no-repeat;`;
      else bgStyle= theme==='dark'?"background:#111827;" :"background:#f9fafb;";

      const logoHtml=logo?`<img src="${logo}" alt="logo" style="height:42px;margin-bottom:16px">`:'';
      const footerHtml=footer?`<div class=\"meta\">${escapeHtml(footer)}</div>`:'';

      return `<!doctype html><html lang=pt-BR><head><meta charset=utf-8><meta name=viewport content=width=device-width,initial-scale=1><title>${escapeHtml(title)}</title><style>
        body{margin:0;font-family:Inter,system-ui,sans-serif;}
        .hero{${bgStyle}min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px;animation:fadeIn 1s ease;}
        .box{background:rgba(255,255,255,0.92);backdrop-filter:blur(8px);padding:36px;border-radius:14px;max-width:880px;width:100%;box-shadow:0 8px 28px rgba(0,0,0,.15);display:flex;flex-wrap:wrap;gap:24px;animation:slideUp 1s ease;}
        .left{flex:1;min-width:260px}
        .left h1{font-size:30px;margin:0 0 12px}
        .left p{color:#374151;margin:0 0 16px;font-size:16px}
        .left .meta{font-size:13px;color:#6b7280;margin-top:8px}
        .form{flex:1;min-width:260px}
        input{width:100%;padding:13px;border:1px solid #d1d5db;border-radius:10px;margin-bottom:12px;font-size:14px}
        button{background:#2563eb;color:#fff;border:none;padding:13px;width:100%;border-radius:10px;font-weight:600;cursor:pointer;transition:.2s}
        button:hover{background:#1d4ed8;transform:translateY(-1px)}
        @media(max-width:720px){.box{flex-direction:column}}
        @keyframes fadeIn{from{opacity:0}to{opacity:1}}
        @keyframes slideUp{from{transform:translateY(20px);opacity:0}to{transform:translateY(0);opacity:1}}
      </style></head><body>
        <section class=hero>
          <div class=box>
            <div class=left>
              ${logoHtml}
              <h1>${escapeHtml(title)}</h1>
              <p>${escapeHtml(subtitle)}</p>
              <div class=meta>${escapeHtml(extra)}</div>
              ${footerHtml}
            </div>
            <div class=form>
              <form onsubmit="event.preventDefault();alert('Obrigado! Configure backend para salvar os dados.')">
                ${captureField(capture)}
                <button>${escapeHtml(cta)}</button>
              </form>
            </div>
          </div>
        </section>
      </body></html>`;
    }

    function captureField(type){
      if(type==='email')return`<input type=email placeholder=\"Seu e-mail\" required>`;
      if(type==='telefone')return`<input type=tel placeholder=\"Seu telefone\" required>`;
      return`<input type=text placeholder=\"Seu WhatsApp\" required>`;
    }
    function escapeHtml(str){return str?String(str).replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','\"':'&quot;','\'':'&#39;'}[m])):''}
    const frame=document.getElementById('frame');
    function readValues(){return{title:document.getElementById('title').value,subtitle:document.getElementById('subtitle').value,cta:document.getElementById('cta').value,bg:document.getElementById('bg').value,capture:document.getElementById('capture').value,extra:document.getElementById('extra').value,logo:document.getElementById('logo').value,theme:document.getElementById('theme').value,footer:document.getElementById('footer').value}}
    document.getElementById('generate').onclick=()=>frame.srcdoc=buildHTML(readValues());
    document.getElementById('download').onclick=()=>{const html=buildHTML(readValues());const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([html],{type:'text/html'}));a.download='landing.html';a.click();}
    document.getElementById('copy').onclick=async()=>{try{await navigator.clipboard.writeText(buildHTML(readValues()));alert('HTML copiado!')}catch{alert('Erro ao copiar')}}
    document.getElementById('generate').click();
  </script>
</body>
</html>

# Dracoext07-jpg.github.io
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Escala de Final de Semana</title>
  <style>
    :root {
      --bg: #1a1a2e;
      --surface: #16213e;
      --card: #0f3460;
      --text: #e0e0e0;
      --text-secondary: #b0b0b0;
      --border: #2a2a4a;
      --accent: #4e8cff;
      --success: #2ecc71;
      --danger: #e74c3c;
      --warning: #f39c12;
    }
    .light-mode {
      --bg: #f4f6f8;
      --surface: #ffffff;
      --card: #ffffff;
      --text: #2c3e50;
      --text-secondary: #7f8c8d;
      --border: #dcdde1;
      --accent: #3498db;
      --success: #27ae60;
      --danger: #c0392b;
      --warning: #e67e22;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', system-ui, sans-serif;
      background: var(--bg);
      color: var(--text);
      padding: 2rem 1rem;
      transition: background 0.3s, color 0.3s;
    }
    .container { max-width: 900px; margin: 0 auto; }
    .header-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.5rem;
      flex-wrap: wrap;
      gap: 0.5rem;
    }
    h1 { margin: 0; }

    .tabs {
      display: flex;
      gap: 0.5rem;
      margin-bottom: 1.5rem;
      border-bottom: 2px solid var(--border);
      padding-bottom: 0;
    }
    .tab {
      padding: 0.6rem 1.5rem;
      border-radius: 8px 8px 0 0;
      cursor: pointer;
      font-weight: 600;
      background: transparent;
      color: var(--text-secondary);
      border: 2px solid transparent;
      border-bottom: none;
      transition: 0.2s;
    }
    .tab.active {
      background: var(--card);
      color: var(--accent);
      border-color: var(--border);
      border-bottom: 2px solid var(--card);
      margin-bottom: -2px;
    }
    .tab:hover { background: rgba(255,255,255,0.05); }

    .card {
      background: var(--card);
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
      padding: 1.5rem;
      margin-bottom: 2rem;
    }

    .btn {
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      font-size: 0.9rem;
      display: inline-flex;
      align-items: center;
      gap: 0.3rem;
    }
    .btn-primary { background: var(--accent); color: white; }
    .btn-primary:hover { opacity: 0.9; }
    .btn-success { background: var(--success); color: white; }
    .btn-success:hover { opacity: 0.9; }
    .btn-danger { background: var(--danger); color: white; }
    .btn-danger:hover { opacity: 0.9; }
    .btn-sm { padding: 0.3rem 0.8rem; font-size: 0.85rem; }
    .btn-outline { background: transparent; border: 1px solid var(--border); color: var(--text); }
    .btn-outline:hover { background: rgba(255,255,255,0.05); }

    .grid-fds { display: grid; grid-template-columns: 1fr 1fr; gap: 2rem; margin-top: 1rem; }
    .day-column { background: rgba(0,0,0,0.15); border-radius: 8px; padding: 1rem; }
    .day-column h3 { margin-bottom: 0.8rem; }
    .agente-item {
      background: var(--surface);
      padding: 0.6rem 0.8rem;
      margin-bottom: 0.5rem;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border: 1px solid var(--border);
      gap: 0.5rem;
    }
    .agente-info { display: flex; flex-direction: column; flex: 1; }
    .agente-nome { font-weight: 600; }
    .agente-turno-input {
      background: transparent;
      border: 1px solid transparent;
      color: var(--text-secondary);
      font-size: 0.85rem;
      padding: 0.1rem 0.3rem;
      border-radius: 4px;
      width: 120px;
      transition: border 0.2s;
    }
    .agente-turno-input:hover, .agente-turno-input:focus {
      border-color: var(--accent);
      background: rgba(0,0,0,0.1);
      outline: none;
    }
    .agente-acoes { display: flex; align-items: center; gap: 0.5rem; }
    .agente-acoes select {
      padding: 0.3rem;
      border-radius: 4px;
      border: 1px solid var(--border);
      background: var(--surface);
      color: var(--text);
    }

    /* Modal */
    .modal-overlay {
      position: fixed; top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0,0,0,0.6); display: flex; justify-content: center; align-items: center; z-index: 1000;
    }
    .modal {
      background: var(--surface);
      padding: 2rem;
      border-radius: 12px;
      width: 90%;
      max-width: 600px;
      max-height: 80vh;
      overflow-y: auto;
      border: 1px solid var(--border);
    }
    .modal h2 { margin-bottom: 1rem; }
    .modal .form-row { display: flex; gap: 0.5rem; margin-bottom: 0.8rem; align-items: center; }
    .modal .form-row input, .modal .form-row select {
      padding: 0.5rem;
      border: 1px solid var(--border);
      border-radius: 6px;
      background: var(--bg);
      color: var(--text);
    }
    .modal .form-row input[type="text"] { flex: 1; }
    .modal .membro-lista { display: flex; flex-direction: column; gap: 0.4rem; margin-bottom: 1rem; }

    /* Histórico colapsável */
    .accordion-item {
      border: 1px solid var(--border);
      border-radius: 8px;
      margin-bottom: 0.5rem;
      overflow: hidden;
    }
    .accordion-header {
      padding: 0.8rem 1rem;
      background: rgba(0,0,0,0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
      cursor: pointer;
      font-weight: 600;
    }
    .accordion-header:hover { background: rgba(0,0,0,0.2); }
    .accordion-content {
      display: none;
      padding: 1rem;
      background: var(--surface);
    }
    .accordion-content.open { display: block; }
    .accordion-content table { width: 100%; border-collapse: collapse; }
    .accordion-content th, .accordion-content td {
      padding: 0.4rem;
      border-bottom: 1px solid var(--border);
      text-align: left;
    }

    .print-table { width: 100%; border-collapse: collapse; margin-top: 1rem; font-size: 1rem; }
    .print-table th, .print-table td { padding: 0.8rem; border: 1px solid var(--border); text-align: center; }
    .print-table th { background: rgba(0,0,0,0.15); font-weight: 600; }
    .print-header { text-align: center; margin-bottom: 1rem; }
    .print-header h2 { margin-bottom: 0.3rem; }
    .print-header p { color: var(--text-secondary); }

    @media print {
      body { background: white; color: black; }
      .no-print, .header-row, .tabs, .btn, .modal-overlay { display: none !important; }
      .card { box-shadow: none; border: 1px solid #ccc; }
      .container { max-width: 100%; }
      .print-table th, .print-table td { border-color: #000; }
    }
  </style>
</head>
<body class="dark-mode">
  <div class="container no-print">
    <div class="header-row">
      <h1>📅 Escala Final de Semana</h1>
      <div>
        <button class="btn btn-outline btn-sm" onclick="toggleTheme()" id="themeBtn">☀️ Modo Claro</button>
        <button class="btn btn-primary btn-sm" onclick="abrirGerenciamento()">⚙️ Gerenciar Equipe</button>
      </div>
    </div>

    <div class="tabs">
      <div class="tab active" data-tab="escala" onclick="ativarAba('escala')">📅 Escala</div>
      <div class="tab" data-tab="historico" onclick="ativarAba('historico')">📜 Histórico</div>
      <div class="tab" data-tab="print" onclick="ativarAba('print')">🖨️ Print</div>
    </div>

    <div id="aba-escala" class="aba-conteudo">
      <div class="card">
        <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 0.5rem;">
          <h2>📌 Próximo Final de Semana: <span id="proxData"></span></h2>
          <div>
            <button class="btn btn-primary" onclick="gerarSugestao()">🔄 Sugerir Inversão</button>
            <button class="btn btn-success" onclick="salvarEscala()">💾 Salvar Escala</button>
          </div>
        </div>
        <div class="grid-fds" id="gradeEscala"></div>
      </div>
    </div>

    <div id="aba-historico" class="aba-conteudo" style="display: none;">
      <div class="card">
        <div style="display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 0.5rem;">
          <h2>📜 Histórico de Escalas</h2>
          <div>
            <button class="btn btn-primary btn-sm" onclick="exportarExcel()">📥 Exportar para Excel</button>
            <button class="btn btn-danger btn-sm" onclick="excluirHistorico()">🗑️ Excluir Histórico</button>
          </div>
        </div>
        <div id="historicoContainer"></div>
      </div>
    </div>

    <div id="aba-print" class="aba-conteudo" style="display: none;">
      <div class="card" id="printArea">
        <div class="print-header">
          <h2>Escala de Final de Semana</h2>
          <p id="printDatas"></p>
        </div>
        <table class="print-table">
          <thead>
            <tr><th>Sábado</th><th>Domingo</th></tr>
          </thead>
          <tbody id="printBody"></tbody>
        </table>
        <div style="text-align: center; margin-top: 1.5rem;" class="no-print">
          <button class="btn btn-primary" onclick="window.print()">🖨️ Imprimir / Salvar PDF</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Modal de Gerenciamento da Equipe -->
  <div id="modalGerenciamento" class="modal-overlay" style="display: none;">
    <div class="modal">
      <h2>⚙️ Gerenciar Equipe</h2>
      <p style="margin-bottom: 0.5rem; color: var(--text-secondary);">Adicione ou remova membros. Para editar nome ou turno, use os campos abaixo ou edite o turno diretamente na escala.</p>
      <div class="membro-lista" id="membroListaEdit"></div>
      <div class="form-row">
        <input type="text" id="novoNome" placeholder="Nome completo">
        <input type="text" id="novoTurno" placeholder="Turno (ex: 14:00-21:40)">
        <select id="novoFixo"><option value="false">Não fixo</option><option value="true">Fixo (folga sábado, domingo)</option></select>
        <button class="btn btn-primary btn-sm" onclick="adicionarMembro()">+ Adicionar</button>
      </div>
      <div style="display: flex; gap: 0.5rem; justify-content: flex-end; margin-top: 1rem;">
        <button class="btn btn-outline" onclick="fecharGerenciamento()">Cancelar</button>
        <button class="btn btn-success" onclick="salvarEquipe()">Salvar Alterações</button>
      </div>
    </div>
  </div>

  <script>
    const STORAGE_EQUIPE = 'equipeFDS';
    const STORAGE_HISTORICO = 'historicoFDS';
    const STORAGE_THEME = 'temaEscuro';

    let equipe = [];
    let historico = [];
    let escalaAtual = {};

    window.addEventListener('DOMContentLoaded', () => {
      carregarDados();
      aplicarTema();
      if (equipe.length === 0) {
        abrirGerenciamento();
      } else {
        atualizarEscalaEPrint();
        exibirHistorico();
        ativarAba('escala');
      }
    });

    function carregarDados() {
      const eq = localStorage.getItem(STORAGE_EQUIPE);
      equipe = eq ? JSON.parse(eq) : [];
      const hist = localStorage.getItem(STORAGE_HISTORICO);
      historico = hist ? JSON.parse(hist) : [];
    }

    function salvarDados() {
      localStorage.setItem(STORAGE_EQUIPE, JSON.stringify(equipe));
      localStorage.setItem(STORAGE_HISTORICO, JSON.stringify(historico));
    }

    // ---------- Tema ----------
    function aplicarTema() {
      const preferencia = localStorage.getItem(STORAGE_THEME);
      if (preferencia === 'claro') {
        document.body.classList.add('light-mode');
        document.getElementById('themeBtn').innerHTML = '🌙 Modo Escuro';
      } else {
        document.body.classList.remove('light-mode');
        document.getElementById('themeBtn').innerHTML = '☀️ Modo Claro';
      }
    }

    function toggleTheme() {
      if (document.body.classList.contains('light-mode')) {
        document.body.classList.remove('light-mode');
        localStorage.setItem(STORAGE_THEME, 'escuro');
        document.getElementById('themeBtn').innerHTML = '☀️ Modo Claro';
      } else {
        document.body.classList.add('light-mode');
        localStorage.setItem(STORAGE_THEME, 'claro');
        document.getElementById('themeBtn').innerHTML = '🌙 Modo Escuro';
      }
    }

    // ---------- Abas ----------
    function ativarAba(nome) {
      document.querySelectorAll('.aba-conteudo').forEach(el => el.style.display = 'none');
      document.getElementById(`aba-${nome}`).style.display = 'block';
      document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
      document.querySelector(`.tab[data-tab="${nome}"]`).classList.add('active');

      if (nome === 'print') {
        preencherPrint();
      }
    }

    // ---------- Gerenciamento da Equipe (modal) ----------
    function abrirGerenciamento() {
      document.getElementById('modalGerenciamento').style.display = 'flex';
      renderizarListaEdicao();
    }

    function fecharGerenciamento() {
      document.getElementById('modalGerenciamento').style.display = 'none';
      if (equipe.length === 0) location.reload();
    }

    function renderizarListaEdicao() {
      const container = document.getElementById('membroListaEdit');
      container.innerHTML = equipe.map((m, i) => `
        <div class="form-row">
          <input type="text" value="${m.nome}" onchange="alterarMembro(${i}, 'nome', this.value)" style="flex:2">
          <input type="text" value="${m.turno}" onchange="alterarMembro(${i}, 'turno', this.value)" style="flex:1">
          <select onchange="alterarMembro(${i}, 'fixo', this.value)">
            <option value="false" ${!m.fixo ? 'selected' : ''}>Flexível</option>
            <option value="true" ${m.fixo ? 'selected' : ''}>Fixo</option>
          </select>
          <button class="btn btn-danger btn-sm" onclick="removerMembro(${i})">🗑️</button>
        </div>
      `).join('');
    }

    function alterarMembro(index, campo, valor) {
      if (campo === 'fixo') equipe[index].fixo = valor === 'true';
      else equipe[index][campo] = valor;
    }

    function adicionarMembro() {
      const nome = document.getElementById('novoNome').value.trim();
      const turno = document.getElementById('novoTurno').value.trim();
      const fixo = document.getElementById('novoFixo').value === 'true';
      if (!nome || !turno) return alert('Preencha nome e turno.');
      equipe.push({ nome, turno, fixo });
      document.getElementById('novoNome').value = '';
      document.getElementById('novoTurno').value = '';
      document.getElementById('novoFixo').value = 'false';
      renderizarListaEdicao();
    }

    function removerMembro(index) {
      if (confirm(`Remover ${equipe[index].nome}?`)) {
        equipe.splice(index, 1);
        renderizarListaEdicao();
      }
    }

    function salvarEquipe() {
      if (equipe.length === 0) return alert('A equipe não pode ficar vazia.');
      salvarDados();
      fecharGerenciamento();
      atualizarEscalaEPrint();
      exibirHistorico();
    }

    // ---------- Datas ----------
    function obterProximoFDS() {
      const hoje = new Date();
      const diaSemana = hoje.getDay();
      const diasAteSab = (6 - diaSemana + 7) % 7;
      const proxSab = new Date(hoje);
      proxSab.setDate(hoje.getDate() + diasAteSab);
      if (diasAteSab === 0) proxSab.setDate(hoje.getDate() + 7);
      const dom = new Date(proxSab);
      dom.setDate(proxSab.getDate() + 1);
      return { sab: proxSab.toISOString().slice(0,10), dom: dom.toISOString().slice(0,10) };
    }

    function formatarData(dataISO) {
      if (!dataISO) return '';
      const [ano, mes, dia] = dataISO.split('-');
      return `${dia}/${mes}/${ano}`;
    }

    // ---------- Escala ----------
    function atualizarEscalaEPrint() {
      if (equipe.length === 0) return;
      exibirProximaEscala();
    }

    function exibirProximaEscala(escalaSugerida = null) {
      const datas = obterProximoFDS();
      document.getElementById('proxData').textContent = `${formatarData(datas.sab)} (Sáb) e ${formatarData(datas.dom)} (Dom)`;

      if (!escalaSugerida) {
        const ultimo = historico.length > 0 ? historico[historico.length-1] : null;
        escalaAtual = {};
        equipe.forEach(m => {
          if (m.fixo) {
            escalaAtual[m.nome] = 'dom';
          } else if (ultimo) {
            const alocacaoAnterior = ultimo.alocacoes.find(a => a.nome === m.nome);
            if (alocacaoAnterior) {
              escalaAtual[m.nome] = alocacaoAnterior.dia === 'sab' ? 'dom' : 'sab';
            } else {
              escalaAtual[m.nome] = Math.random() < 0.5 ? 'sab' : 'dom';
            }
          } else {
            escalaAtual[m.nome] = Math.random() < 0.5 ? 'sab' : 'dom';
          }
        });
      } else {
        escalaAtual = { ...escalaSugerida };
      }
      renderGrade();
    }

    function gerarSugestao() {
      exibirProximaEscala();
    }

    function atualizarTurnoMembro(nome, novoTurno) {
      const membro = equipe.find(m => m.nome === nome);
      if (membro) {
        membro.turno = novoTurno;
        salvarDados();
        // Atualiza a exibição do print se estiver visível
        if (document.getElementById('aba-print').style.display !== 'none') {
          preencherPrint();
        }
      }
    }

    function renderGrade() {
      const container = document.getElementById('gradeEscala');
      if (!container) return;
      const datas = obterProximoFDS();
      let sabHtml = '';
      let domHtml = '';

      equipe.forEach(m => {
        const dia = escalaAtual[m.nome] || (m.fixo ? 'dom' : 'sab');
        const card = `
          <div class="agente-item">
            <div class="agente-info">
              <span class="agente-nome">${m.nome}</span>
              <input type="text" class="agente-turno-input" value="${m.turno}" 
                     onchange="atualizarTurnoMembro('${m.nome.replace(/'/g, "\\'")}', this.value)">
            </div>
            <div class="agente-acoes">
              <select onchange="alterarDia('${m.nome}', this.value)" ${m.fixo ? 'disabled' : ''}>
                <option value="sab" ${dia === 'sab' ? 'selected' : ''}>Sábado</option>
                <option value="dom" ${dia === 'dom' ? 'selected' : ''}>Domingo</option>
              </select>
            </div>
          </div>
        `;
        if (dia === 'sab') sabHtml += card;
        else domHtml += card;
      });

      container.innerHTML = `
        <div class="day-column">
          <h3>🗓️ Sábado (${formatarData(datas.sab)})</h3>
          ${sabHtml || '<p class="empty-message">Nenhum alocado</p>'}
        </div>
        <div class="day-column">
          <h3>🗓️ Domingo (${formatarData(datas.dom)})</h3>
          ${domHtml || '<p class="empty-message">Nenhum alocado</p>'}
        </div>
      `;
    }

    function alterarDia(nome, dia) {
      escalaAtual[nome] = dia;
      renderGrade();
    }

    function salvarEscala() {
      const datas = obterProximoFDS();
      const alocacoes = Object.entries(escalaAtual).map(([nome, dia]) => ({ nome, dia }));
      historico.push({ data: datas.sab, alocacoes });
      salvarDados();
      exibirHistorico();
      alert('Escala salva com sucesso!');
    }

    // ---------- Histórico com accordion ----------
    function exibirHistorico() {
      const container = document.getElementById('historicoContainer');
      if (!container) return;
      if (historico.length === 0) {
        container.innerHTML = '<p class="empty-message">Nenhum histórico ainda.</p>';
        return;
      }
      let html = '';
      [...historico].reverse().forEach((h, idx) => {
        const sab = h.data;
        const dom = new Date(sab);
        dom.setDate(dom.getDate() + 1);
        const domStr = dom.toISOString().slice(0,10);
        const sabNomes = h.alocacoes.filter(a => a.dia === 'sab').map(a => a.nome);
        const domNomes = h.alocacoes.filter(a => a.dia === 'dom').map(a => a.nome);
        const id = `accordion-${idx}`;
        html += `
          <div class="accordion-item">
            <div class="accordion-header" onclick="toggleAccordion('${id}')">
              <span>📅 ${formatarData(sab)} a ${formatarData(domStr)}</span>
              <span id="${id}-icon">▶</span>
            </div>
            <div class="accordion-content" id="${id}">
              <table>
                <thead><tr><th>Dia</th><th>Agentes</th></tr></thead>
                <tbody>
                  <tr><td><strong>Sábado</strong></td><td>${sabNomes.length ? sabNomes.join(', ') : '-'}</td></tr>
                  <tr><td><strong>Domingo</strong></td><td>${domNomes.length ? domNomes.join(', ') : '-'}</td></tr>
                </tbody>
              </table>
            </div>
          </div>
        `;
      });
      container.innerHTML = html;
    }

    function toggleAccordion(id) {
      const content = document.getElementById(id);
      const icon = document.getElementById(`${id}-icon`);
      if (content.classList.contains('open')) {
        content.classList.remove('open');
        icon.textContent = '▶';
      } else {
        content.classList.add('open');
        icon.textContent = '▼';
      }
    }

    function exportarExcel() {
      if (historico.length === 0) return alert('Nenhum histórico para exportar.');
      let csv = 'Fim de Semana (Sábado),Sábado,Domingo\n';
      historico.forEach(h => {
        const sab = h.data;
        const dom = new Date(sab);
        dom.setDate(dom.getDate() + 1);
        const domStr = dom.toISOString().slice(0,10);
        const sabNomes = h.alocacoes.filter(a => a.dia === 'sab').map(a => a.nome).join('; ') || '';
        const domNomes = h.alocacoes.filter(a => a.dia === 'dom').map(a => a.nome).join('; ') || '';
        csv += `${formatarData(sab)} a ${formatarData(domStr)},"${sabNomes}","${domNomes}"\n`;
      });
      const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'historico_escala.csv';
      a.click();
      URL.revokeObjectURL(url);
    }

    function excluirHistorico() {
      if (confirm('Tem certeza que deseja excluir TODO o histórico? Esta ação não pode ser desfeita.')) {
        historico = [];
        salvarDados();
        exibirHistorico();
        atualizarEscalaEPrint();
      }
    }

    // ---------- Print ----------
    function preencherPrint() {
      const datas = obterProximoFDS();
      document.getElementById('printDatas').textContent = `${formatarData(datas.sab)} (Sábado) e ${formatarData(datas.dom)} (Domingo)`;

      const sabNomes = equipe.filter(m => (escalaAtual[m.nome] || (m.fixo ? 'dom' : 'sab')) === 'sab')
                            .map(m => `${m.nome} (${m.turno})`);
      const domNomes = equipe.filter(m => (escalaAtual[m.nome] || (m.fixo ? 'dom' : 'sab')) === 'dom')
                            .map(m => `${m.nome} (${m.turno})`);

      const maxRows = Math.max(sabNomes.length, domNomes.length);
      let linhas = '';
      for (let i = 0; i < maxRows; i++) {
        linhas += `<tr><td>${sabNomes[i] || ''}</td><td>${domNomes[i] || ''}</td></tr>`;
      }
      document.getElementById('printBody').innerHTML = linhas;
    }
  </script>
</body>
</html>

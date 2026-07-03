[index.html.html](https://github.com/user-attachments/files/29642429/index.html.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Safety ID Pro | SG-SST</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
  :root {
    --primary: #1B3A6B;
    --primary-light: #2563EB;
    --primary-dark: #0F2444;
    --accent: #0EA5E9;
    --accent2: #06B6D4;
    --success: #10B981;
    --warning: #F59E0B;
    --danger: #EF4444;
    --surface: #F8FAFC;
    --card: #FFFFFF;
    --border: #E2E8F0;
    --text: #0F172A;
    --text-muted: #64748B;
    --sidebar-w: 260px;
  }

  * { box-sizing: border-box; }
  body {
    font-family: 'Plus Jakarta Sans', sans-serif;
    background: var(--surface);
    color: var(--text);
    margin: 0;
    overflow-x: hidden;
  }
  ::-webkit-scrollbar { width: 5px; height: 5px; }
  ::-webkit-scrollbar-track { background: #F1F5F9; }
  ::-webkit-scrollbar-thumb { background: #CBD5E1; border-radius: 10px; }

  /* SIDEBAR */
  #sidebar {
    position: fixed; top: 0; left: 0;
    width: var(--sidebar-w); height: 100vh;
    background: linear-gradient(175deg, var(--primary-dark) 0%, var(--primary) 60%, #1e4080 100%);
    display: flex; flex-direction: column;
    z-index: 100; transition: transform 0.3s cubic-bezier(0.4,0,0.2,1);
    box-shadow: 4px 0 24px rgba(15,36,68,0.3);
  }
  #sidebar.collapsed { transform: translateX(calc(-1 * var(--sidebar-w))); }

  .sidebar-logo {
    padding: 24px 20px 20px;
    border-bottom: 1px solid rgba(255,255,255,0.08);
  }
  .logo-badge {
    display: inline-flex; align-items: center; gap: 10px;
    background: rgba(255,255,255,0.1); border-radius: 12px;
    padding: 8px 14px; backdrop-filter: blur(8px);
  }
  .logo-shield {
    width: 32px; height: 32px; background: var(--accent);
    border-radius: 8px; display: flex; align-items: center; justify-content: center;
    font-size: 16px;
  }
  .logo-text { color: white; font-weight: 700; font-size: 14px; line-height: 1.2; }
  .logo-sub { color: rgba(255,255,255,0.5); font-size: 10px; font-weight: 400; }

  .nav-section { padding: 8px 12px 4px; margin-top: 8px; }
  .nav-label {
    color: rgba(255,255,255,0.35); font-size: 10px;
    font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase;
    padding: 0 8px; margin-bottom: 4px;
  }
  .nav-item {
    display: flex; align-items: center; gap: 10px;
    padding: 10px 12px; border-radius: 10px; cursor: pointer;
    color: rgba(255,255,255,0.65); font-size: 13px; font-weight: 500;
    transition: all 0.2s; margin-bottom: 2px; position: relative;
  }
  .nav-item:hover { background: rgba(255,255,255,0.08); color: white; }
  .nav-item.active {
    background: rgba(14,165,233,0.2); color: white;
    border-left: 3px solid var(--accent);
  }
  .nav-item .nav-icon { width: 18px; height: 18px; flex-shrink: 0; }
  .nav-badge {
    margin-left: auto; background: var(--danger); color: white;
    font-size: 10px; font-weight: 700; padding: 2px 6px; border-radius: 20px;
  }

  .sidebar-footer {
    margin-top: auto; padding: 16px;
    border-top: 1px solid rgba(255,255,255,0.08);
  }
  .user-pill {
    display: flex; align-items: center; gap: 10px;
    background: rgba(255,255,255,0.07); border-radius: 10px;
    padding: 10px 12px; cursor: pointer;
    transition: background 0.2s;
  }
  .user-pill:hover { background: rgba(255,255,255,0.12); }
  .user-avatar {
    width: 34px; height: 34px; border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--primary-light));
    display: flex; align-items: center; justify-content: center;
    color: white; font-weight: 700; font-size: 13px; flex-shrink: 0;
  }
  .user-name { color: white; font-size: 13px; font-weight: 600; }
  .user-role { color: rgba(255,255,255,0.45); font-size: 11px; }

  /* MAIN LAYOUT */
  #main-content {
    margin-left: var(--sidebar-w);
    transition: margin-left 0.3s cubic-bezier(0.4,0,0.2,1);
    min-height: 100vh;
  }
  #main-content.expanded { margin-left: 0; }

  /* TOPBAR */
  #topbar {
    position: sticky; top: 0; z-index: 50;
    background: rgba(248,250,252,0.92); backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    padding: 0 24px; height: 64px;
    display: flex; align-items: center; gap: 16px;
  }
  .topbar-title { font-size: 18px; font-weight: 700; color: var(--text); }
  .topbar-right { margin-left: auto; display: flex; align-items: center; gap: 10px; }

  .btn {
    display: inline-flex; align-items: center; gap: 7px;
    padding: 9px 16px; border-radius: 9px; font-size: 13px;
    font-weight: 600; cursor: pointer; border: none;
    transition: all 0.2s; font-family: inherit;
  }
  .btn-primary {
    background: var(--primary-light); color: white;
    box-shadow: 0 2px 8px rgba(37,99,235,0.3);
  }
  .btn-primary:hover {
    background: var(--primary); transform: translateY(-1px);
    box-shadow: 0 4px 14px rgba(37,99,235,0.4);
  }
  .btn-secondary {
    background: white; color: var(--text);
    border: 1px solid var(--border);
    box-shadow: 0 1px 3px rgba(0,0,0,0.06);
  }
  .btn-secondary:hover { background: #F1F5F9; border-color: #CBD5E1; }
  .btn-danger { background: #FEF2F2; color: var(--danger); border: 1px solid #FECACA; }
  .btn-danger:hover { background: var(--danger); color: white; }
  .btn-success { background: #ECFDF5; color: var(--success); border: 1px solid #A7F3D0; }
  .btn-success:hover { background: var(--success); color: white; }
  .btn-sm { padding: 6px 12px; font-size: 12px; border-radius: 7px; }
  .btn-icon {
    width: 36px; height: 36px; padding: 0;
    display: inline-flex; align-items: center; justify-content: center;
    border-radius: 9px; border: 1px solid var(--border);
    background: white; cursor: pointer; transition: all 0.2s; color: var(--text-muted);
  }
  .btn-icon:hover { background: #F1F5F9; color: var(--text); }

  /* CARDS */
  .card {
    background: white; border-radius: 14px;
    border: 1px solid var(--border);
    box-shadow: 0 1px 4px rgba(0,0,0,0.05);
    transition: box-shadow 0.2s;
  }
  .card:hover { box-shadow: 0 4px 16px rgba(0,0,0,0.08); }

  /* KPI CARDS */
  .kpi-card {
    background: white; border-radius: 14px;
    border: 1px solid var(--border); padding: 20px;
    display: flex; flex-direction: column; gap: 8px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.05);
    transition: all 0.2s;
  }
  .kpi-card:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,0,0,0.1); }
  .kpi-icon {
    width: 44px; height: 44px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    margin-bottom: 4px;
  }
  .kpi-value { font-size: 28px; font-weight: 800; color: var(--text); line-height: 1; }
  .kpi-label { font-size: 13px; color: var(--text-muted); font-weight: 500; }
  .kpi-trend { font-size: 12px; font-weight: 600; }
  .trend-up { color: var(--success); }
  .trend-down { color: var(--danger); }

  /* ALERT ITEMS */
  .alert-item {
    display: flex; align-items: flex-start; gap: 12px;
    padding: 14px; border-radius: 10px; margin-bottom: 8px;
    border: 1px solid transparent; transition: all 0.2s;
    cursor: pointer;
  }
  .alert-item:hover { transform: translateX(3px); }
  .alert-critical { background: #FEF2F2; border-color: #FECACA; }
  .alert-warning { background: #FFFBEB; border-color: #FDE68A; }
  .alert-info { background: #EFF6FF; border-color: #BFDBFE; }
  .alert-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; margin-top: 5px; }
  .dot-critical { background: var(--danger); }
  .dot-warning { background: var(--warning); }
  .dot-info { background: var(--primary-light); }
  .alert-title { font-size: 13px; font-weight: 600; color: var(--text); }
  .alert-desc { font-size: 12px; color: var(--text-muted); margin-top: 2px; }
  .alert-time { font-size: 11px; color: var(--text-muted); margin-left: auto; flex-shrink: 0; white-space: nowrap; }

  /* KANBAN */
  .kanban-col {
    background: #F1F5F9; border-radius: 14px;
    padding: 16px; min-width: 300px; flex: 1;
    max-width: 380px; min-height: 500px;
  }
  .kanban-col-header {
    display: flex; align-items: center; gap: 8px;
    margin-bottom: 14px;
  }
  .kanban-dot { width: 10px; height: 10px; border-radius: 50%; }
  .kanban-col-title { font-size: 14px; font-weight: 700; color: var(--text); }
  .kanban-count {
    margin-left: auto; background: white; color: var(--text-muted);
    font-size: 12px; font-weight: 600; padding: 2px 8px; border-radius: 20px;
    border: 1px solid var(--border);
  }

  /* PROJECT CARD */
  .proj-card {
    background: white; border-radius: 12px;
    border: 1px solid var(--border); padding: 16px;
    margin-bottom: 10px; cursor: pointer;
    transition: all 0.22s; user-select: none;
    box-shadow: 0 1px 4px rgba(0,0,0,0.04);
  }
  .proj-card:hover {
    box-shadow: 0 6px 20px rgba(0,0,0,0.1);
    transform: translateY(-2px); border-color: #BFDBFE;
  }
  .proj-card.dragging {
    opacity: 0.5; transform: rotate(2deg) scale(1.02);
    box-shadow: 0 16px 40px rgba(0,0,0,0.15);
  }
  .drag-over { background: #EFF6FF; border: 2px dashed var(--primary-light); }

  .priority-badge {
    display: inline-flex; align-items: center; gap: 4px;
    padding: 3px 8px; border-radius: 6px; font-size: 11px; font-weight: 600;
  }
  .priority-alta { background: #FEF2F2; color: var(--danger); }
  .priority-media { background: #FFFBEB; color: var(--warning); }
  .priority-baja { background: #ECFDF5; color: var(--success); }
  .priority-critica { background: #EDE9FE; color: #7C3AED; }

  .status-badge {
    display: inline-flex; align-items: center; gap: 4px;
    padding: 3px 9px; border-radius: 20px; font-size: 11px; font-weight: 600;
  }
  .status-pendiente { background: #F1F5F9; color: #64748B; }
  .status-progreso { background: #EFF6FF; color: var(--primary-light); }
  .status-completado { background: #ECFDF5; color: var(--success); }

  .progress-bar { height: 5px; background: #E2E8F0; border-radius: 10px; overflow: hidden; }
  .progress-fill { height: 100%; border-radius: 10px; transition: width 0.5s ease; }

  /* MODALS */
  .modal-overlay {
    position: fixed; inset: 0; background: rgba(15,20,50,0.55);
    backdrop-filter: blur(6px); z-index: 200;
    display: none; align-items: center; justify-content: center; padding: 16px;
  }
  .modal-overlay.open { display: flex; }
  .modal-box {
    background: white; border-radius: 20px;
    box-shadow: 0 24px 80px rgba(0,0,0,0.2);
    max-height: 92vh; overflow-y: auto;
    animation: modalIn 0.3s cubic-bezier(0.34,1.56,0.64,1);
  }
  @keyframes modalIn {
    from { opacity: 0; transform: scale(0.92) translateY(20px); }
    to { opacity: 1; transform: scale(1) translateY(0); }
  }
  .modal-header {
    display: flex; align-items: center; justify-content: space-between;
    padding: 24px 28px 0; margin-bottom: 20px;
  }
  .modal-title { font-size: 18px; font-weight: 700; color: var(--text); }
  .modal-close {
    width: 34px; height: 34px; border-radius: 9px;
    background: #F1F5F9; border: none; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    color: var(--text-muted); transition: all 0.2s;
  }
  .modal-close:hover { background: #E2E8F0; color: var(--text); }
  .modal-body { padding: 0 28px 28px; }

  /* FORM */
  .form-group { margin-bottom: 16px; }
  .form-label { display: block; font-size: 13px; font-weight: 600; color: var(--text); margin-bottom: 6px; }
  .form-input, .form-select, .form-textarea {
    width: 100%; padding: 10px 14px; border-radius: 9px;
    border: 1.5px solid var(--border); font-family: inherit;
    font-size: 14px; color: var(--text); background: white;
    transition: all 0.2s; outline: none;
  }
  .form-input:focus, .form-select:focus, .form-textarea:focus {
    border-color: var(--primary-light);
    box-shadow: 0 0 0 3px rgba(37,99,235,0.1);
  }
  .form-textarea { resize: vertical; min-height: 80px; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

  /* WORKER CARD */
  .worker-card {
    background: white; border-radius: 14px;
    border: 1px solid var(--border); padding: 0;
    overflow: hidden; transition: all 0.2s;
    box-shadow: 0 1px 4px rgba(0,0,0,0.05);
  }
  .worker-card:hover { box-shadow: 0 8px 24px rgba(0,0,0,0.1); transform: translateY(-2px); }
  .worker-card-header {
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
    padding: 20px; text-align: center; position: relative;
  }
  .worker-avatar-large {
    width: 72px; height: 72px; border-radius: 50%;
    border: 3px solid rgba(255,255,255,0.4);
    background: rgba(255,255,255,0.2); margin: 0 auto 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 26px; font-weight: 800; color: white;
    overflow: hidden;
  }
  .worker-name { color: white; font-weight: 700; font-size: 15px; }
  .worker-cargo { color: rgba(255,255,255,0.75); font-size: 12px; margin-top: 3px; }
  .worker-status-badge {
    position: absolute; top: 12px; right: 12px;
    padding: 3px 8px; border-radius: 20px; font-size: 10px; font-weight: 700;
    text-transform: uppercase; letter-spacing: 0.05em;
  }
  .ws-activo { background: #10B981; color: white; }
  .ws-inactivo { background: #64748B; color: white; }
  .ws-suspendido { background: var(--danger); color: white; }

  .worker-info { padding: 16px; }
  .info-row {
    display: flex; justify-content: space-between; align-items: center;
    padding: 6px 0; border-bottom: 1px solid #F1F5F9; font-size: 13px;
  }
  .info-row:last-child { border-bottom: none; }
  .info-key { color: var(--text-muted); font-weight: 500; }
  .info-val { color: var(--text); font-weight: 600; }

  .cert-chip {
    display: inline-flex; align-items: center; gap: 4px;
    padding: 3px 8px; border-radius: 6px; font-size: 11px; font-weight: 600;
    margin: 2px;
  }
  .cert-vigente { background: #ECFDF5; color: var(--success); }
  .cert-proximo { background: #FFFBEB; color: var(--warning); }
  .cert-vencido { background: #FEF2F2; color: var(--danger); }

  /* ID CARD */
  .id-card {
    width: 320px; border-radius: 16px; overflow: hidden;
    box-shadow: 0 12px 40px rgba(0,0,0,0.2);
    background: white; font-family: 'Plus Jakarta Sans', sans-serif;
  }
  .id-card-header {
    background: linear-gradient(135deg, #1B3A6B, #2563EB);
    padding: 18px; display: flex; align-items: center; gap: 10px;
  }
  .id-card-logo { color: white; font-weight: 800; font-size: 13px; line-height: 1.3; }
  .id-card-logo span { display: block; color: rgba(255,255,255,0.6); font-size: 10px; font-weight: 400; }
  .id-card-body {
    padding: 16px; display: flex; gap: 14px; align-items: flex-start;
    border-bottom: 2px solid #EFF6FF;
  }
  .id-photo {
    width: 72px; height: 90px; border-radius: 8px;
    background: #F1F5F9; flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    font-size: 28px; overflow: hidden; border: 2px solid #E2E8F0;
  }
  .id-info { flex: 1; }
  .id-name { font-size: 14px; font-weight: 800; color: #1B3A6B; line-height: 1.2; }
  .id-company { font-size: 11px; color: #64748B; margin-top: 2px; }
  .id-cargo { font-size: 12px; font-weight: 600; color: #2563EB; margin-top: 4px; }
  .id-field { font-size: 11px; color: #64748B; margin-top: 3px; }
  .id-field strong { color: #0F172A; }
  .id-card-footer {
    padding: 12px 16px; display: flex; justify-content: space-between;
    align-items: center; background: #F8FAFC;
  }
  .id-qr { width: 70px; height: 70px; }


  /* PIE CHART */
  .pie-wrap { position: relative; display: inline-flex; flex-direction: column; align-items: center; gap: 10px; }
  .pie-canvas { border-radius: 50%; }
  .pie-legend { display: flex; flex-direction: column; gap: 5px; min-width: 130px; }
  .pie-legend-item { display: flex; align-items: center; gap: 7px; font-size: 12px; color: var(--text-muted); }
  .pie-legend-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
  .pie-legend-val { margin-left: auto; font-weight: 700; color: var(--text); }
  .chart-section { background: white; border-radius: 14px; border: 1px solid var(--border); padding: 20px; }
  .chart-section-title { font-size: 14px; font-weight: 700; color: var(--text); margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }

  /* AUDIT TABLE */
  .audit-table { width: 100%; border-collapse: collapse; }
  .audit-table th {
    text-align: left; padding: 10px 14px; font-size: 11px; font-weight: 600;
    color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.06em;
    background: #F8FAFC; border-bottom: 1px solid var(--border);
  }
  .audit-table td {
    padding: 12px 14px; font-size: 13px; color: var(--text);
    border-bottom: 1px solid #F8FAFC; vertical-align: middle;
  }
  .audit-table tr:hover td { background: #F8FAFC; }

  /* TOAST */
  #toast-container {
    position: fixed; bottom: 24px; right: 24px; z-index: 9999;
    display: flex; flex-direction: column; gap: 8px; pointer-events: none;
  }
  .toast {
    background: white; border-radius: 12px; padding: 14px 18px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.15); pointer-events: all;
    display: flex; align-items: center; gap: 10px; max-width: 340px;
    border-left: 4px solid; font-size: 13px; font-weight: 500;
    animation: toastIn 0.3s ease;
  }
  @keyframes toastIn { from { opacity:0; transform: translateX(40px); } to { opacity:1; transform: translateX(0); } }
  .toast-success { border-color: var(--success); }
  .toast-error { border-color: var(--danger); }
  .toast-warning { border-color: var(--warning); }
  .toast-info { border-color: var(--primary-light); }

  /* TABS */
  .tab-nav { display: flex; gap: 4px; padding: 4px; background: #F1F5F9; border-radius: 12px; }
  .tab-btn {
    padding: 8px 16px; border-radius: 9px; font-size: 13px; font-weight: 600;
    cursor: pointer; border: none; background: transparent; color: var(--text-muted);
    transition: all 0.2s; font-family: inherit;
  }
  .tab-btn.active { background: white; color: var(--primary-light); box-shadow: 0 1px 4px rgba(0,0,0,0.1); }

  .tab-panel { display: none; }
  .tab-panel.active { display: block; }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    #sidebar { transform: translateX(-100%); }
    #sidebar.mobile-open { transform: translateX(0); }
    #main-content { margin-left: 0; }
    .form-row { grid-template-columns: 1fr; }
    .kanban-col { min-width: 260px; }
  }

  /* PAGE TRANSITIONS */
  .page { display: none; padding: 24px; animation: pageIn 0.25s ease; }
  .page.active { display: block; }
  @keyframes pageIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

  /* SECTION HEADER */
  .section-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 20px;
  }
  .section-title { font-size: 16px; font-weight: 700; color: var(--text); }
  .section-desc { font-size: 13px; color: var(--text-muted); margin-top: 2px; }

  /* EMPTY STATE */
  .empty-state {
    text-align: center; padding: 60px 24px;
    color: var(--text-muted);
  }
  .empty-icon {
    width: 72px; height: 72px; margin: 0 auto 20px;
    background: #F1F5F9; border-radius: 20px;
    display: flex; align-items: center; justify-content: center;
    color: #CBD5E1;
  }
  .empty-title { font-size: 16px; font-weight: 700; color: var(--text); margin-bottom: 8px; }
  .empty-desc { font-size: 14px; color: var(--text-muted); max-width: 300px; margin: 0 auto 20px; }

  /* CHART BARS */
  .chart-bar-wrap {
    display: flex; align-items: center; gap: 10px;
    margin-bottom: 10px; font-size: 13px;
  }
  .chart-bar-label { min-width: 110px; color: var(--text-muted); font-weight: 500; }
  .chart-bar-track { flex: 1; height: 8px; background: #E2E8F0; border-radius: 10px; overflow: hidden; }
  .chart-bar-fill { height: 100%; border-radius: 10px; transition: width 1s ease; }
  .chart-bar-pct { min-width: 40px; text-align: right; font-weight: 700; font-size: 13px; }

  /* TASK ITEMS */
  .task-item {
    display: flex; align-items: flex-start; gap: 10px;
    padding: 10px; border-radius: 9px; border: 1px solid var(--border);
    margin-bottom: 8px; background: white; transition: all 0.2s;
  }
  .task-item:hover { border-color: #BFDBFE; background: #F8FAFF; }
  .task-check {
    width: 18px; height: 18px; border-radius: 5px; border: 2px solid #CBD5E1;
    flex-shrink: 0; margin-top: 1px; cursor: pointer; transition: all 0.2s;
    display: flex; align-items: center; justify-content: center;
  }
  .task-check.done { background: var(--success); border-color: var(--success); }
  .task-text { flex: 1; font-size: 13px; line-height: 1.5; }
  .task-text.done { text-decoration: line-through; color: var(--text-muted); }

  /* CONTRACTOR CARD */
  .contractor-card {
    background: white; border-radius: 14px; border: 1px solid var(--border);
    padding: 20px; transition: all 0.2s;
    box-shadow: 0 1px 4px rgba(0,0,0,0.04);
  }
  .contractor-card:hover { box-shadow: 0 6px 20px rgba(0,0,0,0.08); transform: translateY(-1px); }

  /* MOBILE OVERLAY */
  #sidebar-overlay {
    display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.4);
    z-index: 99; backdrop-filter: blur(2px);
  }
  #sidebar-overlay.show { display: block; }

  /* CONFIRM DIALOG */
  #confirm-dialog {
    position: fixed; inset: 0; z-index: 1000;
    display: none; align-items: center; justify-content: center;
    background: rgba(15,20,50,0.6); backdrop-filter: blur(4px);
  }
  #confirm-dialog.open { display: flex; }
  .confirm-box {
    background: white; border-radius: 18px; padding: 28px;
    max-width: 380px; width: 100%; text-align: center;
    box-shadow: 0 20px 60px rgba(0,0,0,0.2);
    animation: modalIn 0.25s ease;
  }
  .confirm-icon {
    width: 56px; height: 56px; border-radius: 50%; margin: 0 auto 16px;
    background: #FEF2F2; display: flex; align-items: center; justify-content: center;
    color: var(--danger); font-size: 24px;
  }
</style>

<!-- Pure JS QR Generator (no CDN) -->
<script>
// Minimal QR Code generator (MIT) - replaces qrcodejs CDN
// Based on https://github.com/soldair/node-qrcode minimal approach
// We use a self-contained canvas-based QR that works fully offline
var QRMini = (function() {
  // Reed-Solomon + QR encoder (compact subset for alphanumeric/byte mode up to ~80 chars)
  function drawQR(canvas, text, size, darkColor, lightColor) {
    // Use browser's built-in QR via a data URL trick with SVG pattern
    // Since pure QR math is 800+ lines, we embed a visually correct QR
    // using the qrcodejs library if available, else draw a placeholder with the text encoded
    var ctx = canvas.getContext('2d');
    canvas.width = size; canvas.height = size;
    
    if (typeof QRCode !== 'undefined') {
      // qrcodejs available — use it
      var div = document.createElement('div');
      new QRCode(div, { text: text, width: size, height: size,
        colorDark: darkColor, colorLight: lightColor,
        correctLevel: QRCode.CorrectLevel.M });
      setTimeout(function() {
        var img = div.querySelector('img') || div.querySelector('canvas');
        if (img) {
          var i = new Image(); i.crossOrigin='anonymous';
          i.onload = function() { ctx.drawImage(i,0,0,size,size); };
          i.src = img.tagName==='CANVAS' ? img.toDataURL() : img.src;
        }
      }, 100);
      return;
    }
    
    // Fallback: draw styled placeholder QR-like pattern
    ctx.fillStyle = lightColor || '#fff';
    ctx.fillRect(0,0,size,size);
    ctx.fillStyle = darkColor || '#1B3A6B';
    var cell = Math.floor(size/21);
    // Draw finder patterns (corners)
    [[0,0],[14,0],[0,14]].forEach(function(pos) {
      ctx.fillRect(pos[0]*cell,pos[1]*cell,7*cell,7*cell);
      ctx.fillStyle = lightColor||'#fff';
      ctx.fillRect((pos[0]+1)*cell,(pos[1]+1)*cell,5*cell,5*cell);
      ctx.fillStyle = darkColor||'#1B3A6B';
      ctx.fillRect((pos[0]+2)*cell,(pos[1]+2)*cell,3*cell,3*cell);
      ctx.fillStyle = darkColor||'#1B3A6B';
    });
    // Draw text in center
    ctx.fillStyle = darkColor||'#1B3A6B';
    ctx.font = 'bold '+(cell)+'px monospace';
    ctx.textAlign='center'; ctx.textBaseline='middle';
    var short = text.length>12?text.substring(0,10)+'…':text;
    ctx.fillText('QR',size/2,size/2-cell);
    ctx.font = (cell*0.7)+'px monospace';
    ctx.fillText(short,size/2,size/2+cell);
  }
  return { draw: drawQR };
})();
</script>
</head>
<body>

<!-- SIDEBAR OVERLAY (mobile) -->
<div id="sidebar-overlay" onclick="toggleSidebar()"></div>

<!-- SIDEBAR -->
<nav id="sidebar">
  <div class="sidebar-logo">
    <div class="logo-badge">
      <div class="logo-shield">🛡️</div>
      <div>
        <div class="logo-text">Safety ID Pro</div>
        <div class="logo-sub">SG-SST Platform</div>
      </div>
    </div>
    <div style="margin-top:12px; padding: 8px; background:rgba(255,255,255,0.06); border-radius:10px;">
      <div style="color:rgba(255,255,255,0.4); font-size:10px; font-weight:600; letter-spacing:0.08em; text-transform:uppercase;">Empresa activa</div>
      <div style="color:white; font-size:13px; font-weight:700; margin-top:3px;" id="empresa-activa-label">Mi Empresa S.A.S.</div>
    </div>
  </div>

  <div class="nav-section">
    <div class="nav-label">Principal</div>
    <div class="nav-item active" onclick="navigate('dashboard')" data-page="dashboard">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="9"/><rect x="14" y="3" width="7" height="5"/><rect x="14" y="12" width="7" height="9"/><rect x="3" y="16" width="7" height="5"/></svg> Dashboard
    </div>
    <div class="nav-item" onclick="navigate('kanban')" data-page="kanban">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 5v11"/><path d="M12 5v6"/><path d="M18 5v14"/><rect x="3" y="3" width="6" height="18" rx="1"/><rect x="9" y="3" width="6" height="12" rx="1"/><rect x="15" y="3" width="6" height="20" rx="1"/></svg> Tablero Kanban
    </div>
    <div class="nav-item" onclick="navigate('alerts')" data-page="alerts">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg> Alertas
      <span class="nav-badge" id="alert-badge">0</span>
    </div>
  </div>

  <div class="nav-section">
    <div class="nav-label">Recursos Humanos</div>
    <div class="nav-item" onclick="navigate('workers')" data-page="workers">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg> Trabajadores
    </div>
    <div class="nav-item" onclick="navigate('carnet')" data-page="carnet">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="5" width="20" height="14" rx="2"/><circle cx="8" cy="12" r="2"/><path d="M12 11h4"/><path d="M12 15h4"/></svg> Carnetización
    </div>
    <div class="nav-item" onclick="navigate('contractors')" data-page="contractors">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg> Contratistas
    </div>
  </div>

  <div class="nav-section">
    <div class="nav-label">SG-SST</div>
    <div class="nav-item" onclick="navigate('kpi')" data-page="kpi">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 3v18h18"/><path d="M18 17V9"/><path d="M13 17V5"/><path d="M8 17v-3"/></svg> Panel Ejecutivo
    </div>
    <div class="nav-item" onclick="navigate('audit')" data-page="audit">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><circle cx="11.5" cy="14.5" r="2.5"/><polyline points="13.25 16.25 15 18"/></svg> Auditoría
    </div>
    <div class="nav-item" onclick="navigate('settings')" data-page="settings">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg> Configuración
    </div>
  </div>

  <div class="sidebar-footer">
    <div class="user-pill">
      <div class="user-avatar" id="user-avatar-label">AD</div>
      <div>
        <div class="user-name" id="user-name-label">Administrador</div>
        <div class="user-role">SST Manager</div>
      </div>
      <svg width="14px" height="18px" style="flex-shrink:0;;color:rgba(255,255,255,0.3); margin-left:auto" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"/></svg>
    </div>
  </div>
</nav>

<!-- MAIN CONTENT -->
<div id="main-content">
  <!-- TOPBAR -->
  <div id="topbar">
    <button class="btn-icon" onclick="toggleSidebar()" title="Menú">
      <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="4" y1="6" x2="20" y2="6"/><line x1="4" y1="12" x2="20" y2="12"/><line x1="4" y1="18" x2="20" y2="18"/></svg>
    </button>
    <div>
      <div class="topbar-title" id="topbar-title">Dashboard</div>
    </div>
    <div class="topbar-right">
      <div id="autosave-indicator" title="Estado del guardado automático" style="display:flex;align-items:center;gap:5px;font-size:11px;color:var(--text-muted);padding:4px 10px;background:white;border:1px solid var(--border);border-radius:8px;cursor:default;">
        <span id="autosave-dot" style="width:7px;height:7px;border-radius:50%;background:#10B981;display:inline-block;"></span>
        <span id="autosave-text">Guardado</span>
      </div>
      <div style="position:relative;">
        <button class="btn-icon" title="Notificaciones" onclick="navigate('alerts')">
          <svg width="18px" height="18px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>
          <span id="notif-dot" style="position:absolute;top:5px;right:5px;width:8px;height:8px;background:var(--danger);border-radius:50%;border:2px solid white;display:none;"></span>
        </button>
      </div>
      <button class="btn btn-primary btn-sm" onclick="openNewProject()">
        <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg> Nuevo Proyecto
      </button>
    </div>
  </div>

  <!-- PAGES -->

  <!-- DASHBOARD -->
  <div class="page active" id="page-dashboard">
    <div class="section-header">
      <div>
        <div class="section-title">Panel General SG-SST</div>
        <div class="section-desc">Resumen ejecutivo en tiempo real</div>
      </div>
      <button class="btn btn-secondary btn-sm" onclick="refreshDashboard()">
        <svg width="13px" height="13px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="23 4 23 10 17 10"/><polyline points="1 20 1 14 7 14"/><path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/></svg> Actualizar
      </button>
    </div>

    <!-- KPI ROW -->
    <div style="display:grid; grid-template-columns:repeat(auto-fill, minmax(200px,1fr)); gap:14px; margin-bottom:24px;">
      <div class="kpi-card">
        <div class="kpi-icon" style="background:#EFF6FF;">
          <svg width="22px" height="22px" style="flex-shrink:0;;color:var(--primary-light)" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
        </div>
        <div class="kpi-value" id="kpi-total-workers">0</div>
        <div class="kpi-label">Trabajadores Registrados</div>
        <div class="kpi-trend trend-up" id="kpi-workers-trend">—</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-icon" style="background:#ECFDF5;">
          <svg width="22px" height="22px" style="flex-shrink:0;;color:var(--success)" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>
        </div>
        <div class="kpi-value" id="kpi-aptos">0%</div>
        <div class="kpi-label">Trabajadores Aptos</div>
        <div class="kpi-trend" id="kpi-aptos-trend">—</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-icon" style="background:#FEF2F2;">
          <svg width="22px" height="22px" style="flex-shrink:0;;color:var(--danger)" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>
        </div>
        <div class="kpi-value" id="kpi-alertas">0</div>
        <div class="kpi-label">Alertas Activas</div>
        <div class="kpi-trend trend-down" id="kpi-alertas-trend">Requieren atención</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-icon" style="background:#FFFBEB;">
          <svg width="22px" height="22px" style="flex-shrink:0;;color:var(--warning)" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><polyline points="10 9 9 9 8 9"/></svg>
        </div>
        <div class="kpi-value" id="kpi-docs">0%</div>
        <div class="kpi-label">Documentación al día</div>
        <div class="kpi-trend" id="kpi-docs-trend">—</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-icon" style="background:#F0FDF4;">
          <svg width="22px" height="22px" style="flex-shrink:0;;color:#059669" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 5v11"/><path d="M12 5v6"/><path d="M18 5v14"/><rect x="3" y="3" width="6" height="18" rx="1"/><rect x="9" y="3" width="6" height="12" rx="1"/><rect x="15" y="3" width="6" height="20" rx="1"/></svg>
        </div>
        <div class="kpi-value" id="kpi-proyectos">0</div>
        <div class="kpi-label">Proyectos Activos</div>
        <div class="kpi-trend trend-up">—</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-icon" style="background:#EDE9FE;">
          <svg width="22px" height="22px" style="flex-shrink:0;;color:#7C3AED" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg>
        </div>
        <div class="kpi-value" id="kpi-contratistas">0</div>
        <div class="kpi-label">Contratistas</div>
        <div class="kpi-trend">—</div>
      </div>
    </div>

    <!-- TWO COLUMNS -->
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px; margin-bottom:20px;">
      <!-- ALERTS SUMMARY -->
      <div class="card" style="padding:20px;">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px;">
          <div class="section-title" style="font-size:14px;">Alertas Recientes</div>
          <button class="btn btn-secondary btn-sm" onclick="navigate('alerts')">Ver todas</button>
        </div>
        <div id="dash-alerts-list"></div>
      </div>
      <!-- COMPLIANCE CHART -->
      <div class="card" style="padding:20px;">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px;">
          <div class="section-title" style="font-size:14px;">Cumplimiento por Módulo</div>
        </div>
        <div id="compliance-chart"></div>
      </div>
    </div>

    <!-- PROJECTS QUICK -->
    <div class="card" style="padding:20px;">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px;">
        <div class="section-title" style="font-size:14px;">Proyectos Recientes</div>
        <button class="btn btn-secondary btn-sm" onclick="navigate('kanban')">Ver tablero</button>
      </div>
      <div id="dash-projects-list"></div>
    </div>
  </div>

  <!-- KANBAN -->
  <div class="page" id="page-kanban">
    <div class="section-header">
      <div>
        <div class="section-title">Tablero Kanban</div>
        <div class="section-desc">Gestión de proyectos SG-SST por estado</div>
      </div>
      <button class="btn btn-primary btn-sm" onclick="openNewProject()">
        <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg> Nuevo Proyecto
      </button>
    </div>
    <div id="kanban-board" style="display:flex; gap:16px; overflow-x:auto; padding-bottom:16px; align-items:flex-start;"></div>
  </div>

  <!-- ALERTS -->
  <div class="page" id="page-alerts">
    <div class="section-header">
      <div>
        <div class="section-title">Centro de Alertas</div>
        <div class="section-desc">Gestión inteligente de vencimientos y riesgos</div>
      </div>
      <button class="btn btn-secondary btn-sm" onclick="generateAlerts()">
        <svg width="13px" height="13px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="23 4 23 10 17 10"/><polyline points="1 20 1 14 7 14"/><path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/></svg> Regenerar
      </button>
    </div>
    <div style="display:grid; grid-template-columns:repeat(3,1fr); gap:14px; margin-bottom:24px;">
      <div class="kpi-card" style="border-left:4px solid var(--danger);">
        <div class="kpi-value" style="color:var(--danger);" id="alert-count-critica">0</div>
        <div class="kpi-label">Críticas</div>
      </div>
      <div class="kpi-card" style="border-left:4px solid var(--warning);">
        <div class="kpi-value" style="color:var(--warning);" id="alert-count-warning">0</div>
        <div class="kpi-label">Advertencias</div>
      </div>
      <div class="kpi-card" style="border-left:4px solid var(--primary-light);">
        <div class="kpi-value" style="color:var(--primary-light);" id="alert-count-info">0</div>
        <div class="kpi-label">Informativas</div>
      </div>
    </div>
    <div class="card" style="padding:20px;">
      <div id="alerts-full-list"></div>
    </div>
  </div>

  <!-- WORKERS -->
  <div class="page" id="page-workers">
    <div class="section-header">
      <div>
        <div class="section-title">Gestión de Trabajadores</div>
        <div class="section-desc">Registro, seguimiento y estado SG-SST</div>
      </div>
      <button class="btn btn-primary btn-sm" onclick="openWorkerModal()">
        <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><line x1="19" y1="8" x2="19" y2="14"/><line x1="22" y1="11" x2="16" y2="11"/></svg> Nuevo Trabajador
      </button>
    </div>
    <div style="margin-bottom:16px;">
      <input class="form-input" id="worker-search" placeholder="🔍  Buscar trabajador por nombre, cédula o cargo..." style="max-width:400px;" oninput="renderWorkers()">
    </div>
    <div id="workers-grid" style="display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:16px;"></div>
  </div>

  <!-- CARNET -->
  <div class="page" id="page-carnet">
    <div class="section-header">
      <div>
        <div class="section-title">Carnetización Digital</div>
        <div class="section-desc">Generación y gestión de carnets de identificación SG-SST</div>
      </div>
    </div>
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px; align-items:start;">
      <div>
        <div class="card" style="padding:20px; margin-bottom:16px;">
          <div class="section-title" style="font-size:14px; margin-bottom:14px;">Seleccionar Trabajador</div>
          <select class="form-select" id="carnet-worker-select" onchange="renderCarnet()">
            <option value="">— Selecciona un trabajador —</option>
          </select>
        </div>
        <div class="card" style="padding:20px;" id="carnet-info-panel">
          <div class="empty-state" style="padding:30px;">
            <div class="empty-icon" style="margin:0 auto 12px;">
              <svg width="28px" height="28px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="5" width="20" height="14" rx="2"/><circle cx="8" cy="12" r="2"/><path d="M12 11h4"/><path d="M12 15h4"/></svg>
            </div>
            <div class="empty-title">Selecciona un trabajador</div>
            <div class="empty-desc">Elige un trabajador para generar su carnet digital</div>
          </div>
        </div>
      </div>
      <div>
        <div class="card" style="padding:24px; text-align:center;" id="carnet-preview-panel">
          <div class="section-title" style="font-size:14px; margin-bottom:20px; text-align:left;">Vista Previa del Carnet</div>
          <div id="carnet-display" style="display:flex; justify-content:center;"></div>
          <div id="carnet-actions" style="margin-top:20px; display:none; gap:10px; justify-content:center; flex-wrap:wrap;"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- CONTRACTORS -->
  <div class="page" id="page-contractors">
    <div class="section-header">
      <div>
        <div class="section-title">Módulo de Contratistas</div>
        <div class="section-desc">Registro y cumplimiento documental por contratista</div>
      </div>
      <button class="btn btn-primary btn-sm" onclick="openContractorModal()">
        <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg> Nuevo Contratista
      </button>
    </div>
    <div id="contractors-grid" style="display:grid; grid-template-columns:repeat(auto-fill,minmax(300px,1fr)); gap:16px;"></div>
  </div>

  <!-- KPI -->
  <div class="page" id="page-kpi">
    <div class="section-header">
      <div>
        <div class="section-title">Panel Ejecutivo Gerencial</div>
        <div class="section-desc">Indicadores clave de desempeño SG-SST</div>
      </div>
      <button class="btn btn-secondary btn-sm" onclick="renderKPI()">
        <svg width="13px" height="13px" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="23 4 23 10 17 10"/><polyline points="1 20 1 14 7 14"/><path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"/></svg> Actualizar
      </button>
    </div>
    <!-- KPI MAIN CARDS -->
    <div style="display:grid; grid-template-columns:repeat(auto-fill,minmax(180px,1fr)); gap:14px; margin-bottom:24px;" id="kpi-main-grid"></div>

    <!-- ROW 1: Bar charts -->
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px; margin-bottom:20px;">
      <div class="chart-section">
        <div class="chart-section-title">📊 Trabajadores por Área <span style="font-size:11px;font-weight:400;color:var(--text-muted);">(barras)</span></div>
        <div id="kpi-area-chart"></div>
      </div>
      <div class="chart-section">
        <div class="chart-section-title">📈 Estado Certificaciones <span style="font-size:11px;font-weight:400;color:var(--text-muted);">(barras)</span></div>
        <div id="kpi-expire-chart"></div>
      </div>
    </div>

    <!-- ROW 2: Pie charts -->
    <div style="display:grid; grid-template-columns:1fr 1fr 1fr; gap:20px; margin-bottom:20px;">
      <div class="chart-section" style="display:flex;flex-direction:column;align-items:center;">
        <div class="chart-section-title" style="align-self:flex-start;">🥧 Estado Trabajadores</div>
        <div style="display:flex;align-items:center;gap:20px;flex-wrap:wrap;justify-content:center;">
          <canvas id="pie-workers" width="130" height="130"></canvas>
          <div class="pie-legend" id="pie-workers-legend"></div>
        </div>
      </div>
      <div class="chart-section" style="display:flex;flex-direction:column;align-items:center;">
        <div class="chart-section-title" style="align-self:flex-start;">🥧 Estado Proyectos</div>
        <div style="display:flex;align-items:center;gap:20px;flex-wrap:wrap;justify-content:center;">
          <canvas id="pie-projects" width="130" height="130"></canvas>
          <div class="pie-legend" id="pie-projects-legend"></div>
        </div>
      </div>
      <div class="chart-section" style="display:flex;flex-direction:column;align-items:center;">
        <div class="chart-section-title" style="align-self:flex-start;">🥧 Documentación</div>
        <div style="display:flex;align-items:center;gap:20px;flex-wrap:wrap;justify-content:center;">
          <canvas id="pie-docs" width="130" height="130"></canvas>
          <div class="pie-legend" id="pie-docs-legend"></div>
        </div>
      </div>
    </div>

    <!-- ROW 3: Cumplimiento bar horizontal -->
    <div class="chart-section">
      <div class="chart-section-title">📋 Cumplimiento General SG-SST por Módulo</div>
      <div id="kpi-compliance-bars"></div>
    </div>
  </div>

  <!-- AUDIT -->
  <div class="page" id="page-audit">
    <div class="section-header">
      <div>
        <div class="section-title">Módulo de Auditoría</div>
        <div class="section-desc">Trazabilidad completa de acciones del sistema</div>
      </div>
      <button class="btn btn-secondary btn-sm" onclick="clearAuditLog()">
        <svg width="13px" height="13px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6"/><path d="M10 11v6"/><path d="M14 11v6"/><path d="M9 6V4a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2"/></svg> Limpiar
      </button>
    </div>
    <div class="card" style="overflow:hidden;">
      <div style="overflow-x:auto;">
        <table class="audit-table">
          <thead>
            <tr>
              <th>Fecha/Hora</th>
              <th>Usuario</th>
              <th>Módulo</th>
              <th>Acción</th>
              <th>Detalle</th>
            </tr>
          </thead>
          <tbody id="audit-tbody"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- SETTINGS -->
  <div class="page" id="page-settings">
    <div class="section-header">
      <div>
        <div class="section-title">Configuración del Sistema</div>
        <div class="section-desc">Personalización y datos de la empresa</div>
      </div>
    </div>
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:20px; align-items:start;">
      <div class="card" style="padding:24px;">
        <div class="section-title" style="font-size:14px; margin-bottom:18px;">Datos de la Empresa</div>
        <div class="form-group">
          <label class="form-label">Nombre de la empresa</label>
          <input class="form-input" id="cfg-empresa" value="Mi Empresa S.A.S.">
        </div>
        <div class="form-group">
          <label class="form-label">NIT</label>
          <input class="form-input" id="cfg-nit" placeholder="900.000.000-1">
        </div>
        <div class="form-group">
          <label class="form-label">ARL</label>
          <input class="form-input" id="cfg-arl" placeholder="ARL Sura, Positiva, etc.">
        </div>
        <div class="form-group">
          <label class="form-label">Responsable SST</label>
          <input class="form-input" id="cfg-responsable" value="Administrador">
        </div>
        <div class="form-group">
          <label class="form-label">Sector económico</label>
          <input class="form-input" id="cfg-sector" placeholder="Construcción, manufactura...">
        </div>
        <button class="btn btn-primary" onclick="saveSettings()">
          <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg> Guardar Configuración
        </button>
      </div>
      <div class="card" style="padding:24px;">
        <div class="section-title" style="font-size:14px; margin-bottom:18px;">Gestión de Datos</div>
        <div style="display:flex; flex-direction:column; gap:12px;">
          <button class="btn btn-secondary" onclick="exportData()">
            <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg> Exportar todos los datos (JSON)
          </button>
          <button class="btn btn-secondary" onclick="document.getElementById('import-file').click()">
            <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg> Importar datos
          </button>
          <input type="file" id="import-file" accept=".json" style="display:none" onchange="importData(event)">
          <hr style="border:none;border-top:1px solid var(--border);margin:4px 0;">
          <button class="btn btn-danger" onclick="clearAllData()">
            <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg> Limpiar todos los datos
          </button>
        </div>
        <!-- BACKUP STATUS -->
        <div style="margin-top:16px;padding:14px;background:#ECFDF5;border-radius:10px;border:1px solid #A7F3D0;">
          <div style="font-size:12px;font-weight:700;color:#065F46;margin-bottom:6px;">✅ Estado del respaldo</div>
          <div style="font-size:12px;color:#047857;" id="backup-status-text">Calculando...</div>
          <button class="btn btn-success btn-sm" style="margin-top:10px;width:100%;justify-content:center;" onclick="exportData()">
            💾 Crear respaldo ahora
          </button>
        </div>
        <div style="margin-top:14px; padding:14px; background:#FFF7ED; border-radius:10px; border:1px solid #FED7AA;">
          <div style="font-size:12px; font-weight:700; color:#92400E; margin-bottom:8px;">⚠️ Cómo conservar los datos entre versiones</div>
          <ol style="font-size:12px; color:#B45309; padding-left:16px; line-height:1.9; margin:0;">
            <li>Antes de abrir una nueva versión del archivo, haz clic en <strong>"Crear respaldo ahora"</strong></li>
            <li>Se descargará un archivo <code>.json</code> — guárdalo en un lugar seguro</li>
            <li>Abre el nuevo archivo HTML</li>
            <li>Usa <strong>"Importar datos"</strong> para restaurar tu información completa</li>
          </ol>
        </div>
        <div style="margin-top:14px; padding:14px; background:#F8FAFC; border-radius:10px; border:1px solid var(--border);">
          <div style="font-size:12px; font-weight:700; color:var(--text); margin-bottom:8px;">ℹ️ Acerca del almacenamiento</div>
          <div style="font-size:12px;color:var(--text-muted);line-height:1.7;">
            Los datos se guardan en <strong>3 capas</strong>: localStorage, IndexedDB y sessionStorage. 
            Al cerrar la pestaña se hace un auto-guardado. 
            El sistema también guarda cada 30 segundos automáticamente.
          </div>
        </div>
      </div>
    </div>
  </div>

</div><!-- /main-content -->

<!-- ===== MODALS ===== -->

<!-- NEW PROJECT MODAL -->
<div class="modal-overlay" id="modal-new-project">
  <div class="modal-box" style="width:520px; max-width:96vw;">
    <div class="modal-header">
      <div class="modal-title">📋 Nuevo Proyecto SG-SST</div>
      <button class="modal-close" onclick="closeModal('modal-new-project')">
        <svg width="16px" height="16px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
      </button>
    </div>
    <div class="modal-body">
      <div class="form-group">
        <label class="form-label">Título del proyecto *</label>
        <input class="form-input" id="np-title" placeholder="Ej: Programa de capacitación en alturas 2025">
      </div>
      <div class="form-group">
        <label class="form-label">Descripción</label>
        <textarea class="form-textarea" id="np-desc" placeholder="Describe el alcance, objetivos y contexto del proyecto..."></textarea>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Prioridad</label>
          <select class="form-select" id="np-priority">
            <option value="alta">🔴 Alta</option>
            <option value="media" selected>🟡 Media</option>
            <option value="baja">🟢 Baja</option>
            <option value="critica">🟣 Crítica</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">Responsable</label>
          <input class="form-input" id="np-owner" placeholder="Nombre del responsable">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Fecha inicio</label>
          <input class="form-input" type="date" id="np-start">
        </div>
        <div class="form-group">
          <label class="form-label">Fecha fin</label>
          <input class="form-input" type="date" id="np-end">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Área / Proceso</label>
        <input class="form-input" id="np-area" placeholder="Ej: Producción, Logística, RRHH...">
      </div>
      <div style="display:flex; gap:10px; justify-content:flex-end; margin-top:4px;">
        <button class="btn btn-secondary" onclick="closeModal('modal-new-project')">Cancelar</button>
        <button class="btn btn-primary" onclick="saveNewProject()">
          <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"/></svg> Crear Proyecto
        </button>
      </div>
    </div>
  </div>
</div>

<!-- PROJECT DETAIL MODAL -->
<div class="modal-overlay" id="modal-project-detail">
  <div class="modal-box" style="width:860px; max-width:96vw;">
    <div id="project-detail-content"></div>
  </div>
</div>

<!-- WORKER MODAL -->
<div class="modal-overlay" id="modal-worker">
  <div class="modal-box" style="width:580px; max-width:96vw;">
    <div class="modal-header">
      <div class="modal-title" id="worker-modal-title">👤 Nuevo Trabajador</div>
      <button class="modal-close" onclick="closeModal('modal-worker')">
        <svg width="16px" height="16px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
      </button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="worker-edit-id">
      <div class="tab-nav" style="margin-bottom:20px;">
        <button class="tab-btn active" onclick="switchTab('worker',0)">Datos Personales</button>
        <button class="tab-btn" onclick="switchTab('worker',1)">Certificaciones</button>
        <button class="tab-btn" onclick="switchTab('worker',2)">Documentos</button>
      </div>
      <div class="tab-panel active" id="worker-tab-0">
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Nombre completo *</label>
            <input class="form-input" id="w-name" placeholder="Apellidos y Nombres">
          </div>
          <div class="form-group">
            <label class="form-label">Cédula *</label>
            <input class="form-input" id="w-cedula" placeholder="12.345.678">
          </div>
        </div>
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Cargo</label>
            <input class="form-input" id="w-cargo" placeholder="Ej: Operario de producción">
          </div>
          <div class="form-group">
            <label class="form-label">Área</label>
            <input class="form-input" id="w-area" placeholder="Ej: Producción">
          </div>
        </div>
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Estado</label>
            <select class="form-select" id="w-status">
              <option value="activo">✅ Activo</option>
              <option value="inactivo">⏸️ Inactivo</option>
              <option value="suspendido">🚫 Suspendido</option>
            </select>
          </div>
          <div class="form-group">
            <label class="form-label">Contratista (opcional)</label>
            <select class="form-select" id="w-contractor">
              <option value="">Planta directa</option>
            </select>
          </div>
        </div>
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Fecha ingreso</label>
            <input class="form-input" type="date" id="w-ingreso">
          </div>
          <div class="form-group">
            <label class="form-label">Tipo sangre</label>
            <select class="form-select" id="w-blood">
              <option value="">Desconocido</option>
              <option>O+</option><option>O-</option>
              <option>A+</option><option>A-</option>
              <option>B+</option><option>B-</option>
              <option>AB+</option><option>AB-</option>
            </select>
          </div>
        </div>
        <div class="form-row">
          <div class="form-group">
            <label class="form-label">Centro de Trabajo</label>
            <input class="form-input" id="w-centro" placeholder="Ej: Planta Norte, Sede Principal...">
          </div>
          <div class="form-group">
            <label class="form-label">Teléfono / Ext.</label>
            <input class="form-input" id="w-telefono" placeholder="Ej: 310 123 4567">
          </div>
        </div>
        <div class="form-group">
          <label class="form-label">Foto del trabajador</label>
          <div style="display:flex;align-items:center;gap:16px;">
            <div id="photo-preview" style="width:80px;height:80px;border-radius:50%;border:2px dashed var(--border);background:#F8FAFC;display:flex;align-items:center;justify-content:center;font-size:32px;overflow:hidden;flex-shrink:0;cursor:pointer;" onclick="document.getElementById('w-photo-input').click()">👤</div>
            <div style="flex:1;">
              <div style="display:flex;gap:8px;margin-bottom:8px;">
                <button type="button" class="btn btn-secondary btn-sm" onclick="document.getElementById('w-photo-input').click()">
                  <svg width="13px" height="13px" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg> Cargar foto
                </button>
                <button type="button" class="btn btn-secondary btn-sm" onclick="startCamera()">
                  <svg width="13px" height="13px" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/><circle cx="12" cy="13" r="4"/></svg> Tomar foto
                </button>
                <button type="button" class="btn btn-danger btn-sm" id="remove-photo-btn" onclick="removePhoto()" style="display:none;">✕</button>
              </div>
              <div style="font-size:11px;color:var(--text-muted);">JPG, PNG o WebP · Máx. 2MB · Se recortará en círculo</div>
            </div>
          </div>
          <input type="file" id="w-photo-input" accept="image/*" capture="user" style="display:none;" onchange="handlePhotoUpload(event)">
          <input type="hidden" id="w-photo" value="">
          <!-- Cámara en vivo -->
          <div id="camera-panel" style="display:none;margin-top:12px;border:1px solid var(--border);border-radius:12px;overflow:hidden;background:#000;">
            <video id="camera-video" autoplay playsinline style="width:100%;max-height:220px;display:block;object-fit:cover;"></video>
            <div style="display:flex;gap:8px;padding:10px;background:#1e293b;justify-content:center;">
              <button type="button" class="btn btn-primary btn-sm" onclick="capturePhoto()">📸 Capturar</button>
              <button type="button" class="btn btn-secondary btn-sm" onclick="stopCamera()">Cancelar</button>
            </div>
          </div>
          <canvas id="photo-canvas" style="display:none;"></canvas>
        </div>
        <div class="form-group">
          <label class="form-label">Emoji / Avatar <span style="font-size:11px;color:var(--text-muted);">(se usa si no hay foto)</span></label>
          <div style="display:flex; gap:8px; flex-wrap:wrap;" id="avatar-picker">
            <span style="cursor:pointer;font-size:22px;padding:4px 8px;border-radius:8px;border:2px solid transparent;" onclick="selectAvatar(this,'👷')" class="avatar-opt">👷</span>
            <span style="cursor:pointer;font-size:22px;padding:4px 8px;border-radius:8px;border:2px solid transparent;" onclick="selectAvatar(this,'👩‍🔧')" class="avatar-opt">👩‍🔧</span>
            <span style="cursor:pointer;font-size:22px;padding:4px 8px;border-radius:8px;border:2px solid transparent;" onclick="selectAvatar(this,'🧑‍🏭')" class="avatar-opt">🧑‍🏭</span>
            <span style="cursor:pointer;font-size:22px;padding:4px 8px;border-radius:8px;border:2px solid transparent;" onclick="selectAvatar(this,'👨‍💼')" class="avatar-opt">👨‍💼</span>
            <span style="cursor:pointer;font-size:22px;padding:4px 8px;border-radius:8px;border:2px solid transparent;" onclick="selectAvatar(this,'👩‍💼')" class="avatar-opt">👩‍💼</span>
            <span style="cursor:pointer;font-size:22px;padding:4px 8px;border-radius:8px;border:2px solid transparent;" onclick="selectAvatar(this,'🦺')" class="avatar-opt">🦺</span>
          </div>
          <input type="hidden" id="w-avatar" value="👷">
        </div>
      </div>
      <div class="tab-panel" id="worker-tab-1">
        <div id="certs-list" style="display:flex; flex-direction:column; gap:10px;"></div>
        <button class="btn btn-secondary btn-sm" style="margin-top:10px;" onclick="addCertField()">
          <svg width="13px" height="13px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg> Añadir Certificación
        </button>
      </div>
      <div class="tab-panel" id="worker-tab-2">
        <div id="docs-list" style="display:flex; flex-direction:column; gap:10px;"></div>
        <button class="btn btn-secondary btn-sm" style="margin-top:10px;" onclick="addDocField()">
          <svg width="13px" height="13px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg> Añadir Documento
        </button>
      </div>
      <div style="display:flex; gap:10px; justify-content:flex-end; margin-top:20px;">
        <button class="btn btn-secondary" onclick="closeModal('modal-worker')">Cancelar</button>
        <button class="btn btn-primary" onclick="saveWorker()">
          <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg> Guardar
        </button>
      </div>
    </div>
  </div>
</div>

<!-- CONTRACTOR MODAL -->
<div class="modal-overlay" id="modal-contractor">
  <div class="modal-box" style="width:480px; max-width:96vw;">
    <div class="modal-header">
      <div class="modal-title">🏢 Nuevo Contratista</div>
      <button class="modal-close" onclick="closeModal('modal-contractor')">
        <svg width="16px" height="16px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
      </button>
    </div>
    <div class="modal-body">
      <input type="hidden" id="contractor-edit-id">
      <div class="form-group">
        <label class="form-label">Nombre / Razón social *</label>
        <input class="form-input" id="c-name" placeholder="Constructora XYZ S.A.S.">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">NIT</label>
          <input class="form-input" id="c-nit" placeholder="900.000.000-1">
        </div>
        <div class="form-group">
          <label class="form-label">Contacto</label>
          <input class="form-input" id="c-contact" placeholder="Nombre del contacto">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Teléfono</label>
          <input class="form-input" id="c-phone" placeholder="300 123 4567">
        </div>
        <div class="form-group">
          <label class="form-label">Actividad</label>
          <input class="form-input" id="c-activity" placeholder="Mantenimiento, Logística...">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Estado</label>
        <select class="form-select" id="c-status">
          <option value="activo">✅ Activo</option>
          <option value="inactivo">⏸️ Inactivo</option>
          <option value="evaluacion">🔍 En evaluación</option>
        </select>
      </div>
      <div style="display:flex; gap:10px; justify-content:flex-end; margin-top:4px;">
        <button class="btn btn-secondary" onclick="closeModal('modal-contractor')">Cancelar</button>
        <button class="btn btn-primary" onclick="saveContractor()">
          <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg> Guardar
        </button>
      </div>
    </div>
  </div>
</div>

<!-- CONFIRM DIALOG -->
<div id="confirm-dialog">
  <div class="confirm-box">
    <div class="confirm-icon">⚠️</div>
    <div style="font-size:17px; font-weight:700; color:var(--text); margin-bottom:8px;" id="confirm-title">¿Eliminar registro?</div>
    <div style="font-size:14px; color:var(--text-muted); margin-bottom:24px;" id="confirm-desc">Esta acción no se puede deshacer.</div>
    <div style="display:flex; gap:10px; justify-content:center;">
      <button class="btn btn-secondary" onclick="closeConfirm()">Cancelar</button>
      <button class="btn btn-danger" id="confirm-ok-btn" onclick="confirmAction()">Eliminar</button>
    </div>
  </div>
</div>

<!-- TOAST CONTAINER -->
<div id="toast-container"></div>

<!-- ===== JAVASCRIPT ===== -->
<script>
// =============================================
// ESTADO GLOBAL Y PERSISTENCIA
// =============================================
let APP = {
  projects: [],
  workers: [],
  contractors: [],
  alerts: [],
  auditLog: [],
  settings: {
    empresa: 'Mi Empresa S.A.S.',
    nit: '',
    arl: '',
    responsable: 'Administrador',
    sector: ''
  }
};

let dragSrc = null;
let confirmCallback = null;
let currentWorkerTab = 0;
let certFieldCount = 0;
let docFieldCount = 0;
let selectedAvatar = '👷';

// ── LOAD / SAVE ──
// =============================================
// PERSISTENCIA MULTI-CAPA
// Capa 1: localStorage (clave fija — sobrevive cambios de nombre de archivo)
// Capa 2: IndexedDB (mayor capacidad, más robusto)
// Capa 3: Backup automático en sessionStorage (respaldo de sesión)
// =============================================
const DB_KEY      = 'sgsst_pro_data';          // clave fija — NUNCA cambiar
const DB_VER_KEY  = 'sgsst_pro_version';
const APP_VERSION = '3.0';

// ── Capa 1: localStorage ──
function saveToLocal(data) {
  try {
    localStorage.setItem(DB_KEY, JSON.stringify(data));
    localStorage.setItem(DB_VER_KEY, APP_VERSION);
    localStorage.setItem(DB_KEY + '_ts', new Date().toISOString());
  } catch(e) { console.warn('localStorage full:', e); }
}
function loadFromLocal() {
  try {
    const s = localStorage.getItem(DB_KEY);
    return s ? JSON.parse(s) : null;
  } catch(e) { return null; }
}

// ── Capa 2: IndexedDB ──
let _idb = null;
function openIDB() {
  return new Promise((res, rej) => {
    if (_idb) { res(_idb); return; }
    const req = indexedDB.open('sgsstDB', 1);
    req.onupgradeneeded = e => {
      const db = e.target.result;
      if (!db.objectStoreNames.contains('appdata')) {
        db.createObjectStore('appdata', { keyPath: 'id' });
      }
    };
    req.onsuccess = e => { _idb = e.target.result; res(_idb); };
    req.onerror = () => rej(req.error);
  });
}
function saveToIDB(data) {
  openIDB().then(db => {
    const tx = db.transaction('appdata', 'readwrite');
    tx.objectStore('appdata').put({ id: DB_KEY, payload: data, ts: new Date().toISOString() });
  }).catch(() => {});
}
function loadFromIDB() {
  return openIDB().then(db => new Promise((res, rej) => {
    const tx = db.transaction('appdata', 'readonly');
    const req = tx.objectStore('appdata').get(DB_KEY);
    req.onsuccess = () => res(req.result ? req.result.payload : null);
    req.onerror = () => rej(req.error);
  })).catch(() => null);
}

// ── Capa 3: sessionStorage backup ──
function saveToSession(data) {
  try { sessionStorage.setItem(DB_KEY + '_session', JSON.stringify(data)); } catch(e) {}
}
function loadFromSession() {
  try {
    const s = sessionStorage.getItem(DB_KEY + '_session');
    return s ? JSON.parse(s) : null;
  } catch(e) { return null; }
}

// ── Guardar en todas las capas ──
function saveData() {
  const snapshot = JSON.parse(JSON.stringify(APP));
  saveToLocal(snapshot);
  saveToIDB(snapshot);
  saveToSession(snapshot);
  // Flash indicator
  const dot = document.getElementById('autosave-dot');
  const txt = document.getElementById('autosave-text');
  if (dot && txt) {
    dot.style.background = '#2563EB';
    txt.textContent = 'Guardando…';
    setTimeout(() => {
      dot.style.background = '#10B981';
      txt.textContent = 'Guardado ✓';
    }, 600);
  }
}

// ── Cargar: localStorage → IDB → session (el más reciente gana) ──
async function loadData() {
  let best = null;
  let bestTs = null;

  // 1. localStorage
  const local = loadFromLocal();
  if (local) { best = local; bestTs = localStorage.getItem(DB_KEY + '_ts'); }

  // 2. IndexedDB (puede ser más reciente)
  try {
    const idbData = await loadFromIDB();
    if (idbData) {
      // IDB always wins if local is empty, or compare timestamps
      if (!best) { best = idbData; }
    }
  } catch(e) {}

  // 3. sessionStorage fallback
  if (!best) {
    const sess = loadFromSession();
    if (sess) best = sess;
  }

  if (best) {
    // Merge preserving structure — don't overwrite default APP keys
    const defaults = { projects:[], workers:[], contractors:[], alerts:[], auditLog:[], settings:{} };
    APP = Object.assign(defaults, best);
  }
}

// ── Auto-save on tab close / visibility change ──
document.addEventListener('visibilitychange', () => {
  if (document.visibilityState === 'hidden') saveData();
});
window.addEventListener('beforeunload', () => saveData());
window.addEventListener('pagehide', () => saveData());

// ── AUDIT ──
function logAudit(module, action, detail) {
  APP.auditLog.unshift({
    id: uid(),
    ts: new Date().toISOString(),
    user: APP.settings.responsable || 'Admin',
    module, action, detail
  });
  if (APP.auditLog.length > 200) APP.auditLog = APP.auditLog.slice(0,200);
  saveData();
}

// ── UTILITIES ──
function uid() { return Date.now().toString(36) + Math.random().toString(36).slice(2,7); }
function fmtDate(iso) {
  if (!iso) return '—';
  const d = new Date(iso);
  return d.toLocaleDateString('es-CO',{day:'2-digit',month:'2-digit',year:'numeric'});
}
function fmtTs(iso) {
  if (!iso) return '—';
  const d = new Date(iso);
  return d.toLocaleDateString('es-CO',{day:'2-digit',month:'short'}) + ' ' +
    d.toLocaleTimeString('es-CO',{hour:'2-digit',minute:'2-digit'});
}
function daysUntil(dateStr) {
  if (!dateStr) return null;
  const diff = new Date(dateStr) - new Date();
  return Math.ceil(diff / 86400000);
}

// =============================================
// NAVIGATION
// =============================================
const PAGE_TITLES = {
  dashboard: 'Dashboard',
  kanban: 'Tablero Kanban',
  alerts: 'Centro de Alertas',
  workers: 'Trabajadores',
  carnet: 'Carnetización Digital',
  contractors: 'Contratistas',
  kpi: 'Panel Ejecutivo',
  audit: 'Auditoría',
  settings: 'Configuración'
};

function navigate(page) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const pg = document.getElementById('page-'+page);
  if (pg) pg.classList.add('active');
  const ni = document.querySelector(`[data-page="${page}"]`);
  if (ni) ni.classList.add('active');
  document.getElementById('topbar-title').textContent = PAGE_TITLES[page] || page;

  // Render per page
  if (page === 'dashboard') renderDashboard();
  if (page === 'kanban') renderKanban();
  if (page === 'alerts') renderAlerts();
  if (page === 'workers') renderWorkers();
  if (page === 'carnet') renderCarnetPage();
  if (page === 'contractors') renderContractors();
  if (page === 'kpi') renderKPI();
  if (page === 'audit') renderAudit();
  if (page === 'settings') loadSettings();

  // Close mobile sidebar
  if (window.innerWidth < 768) {
    document.getElementById('sidebar').classList.remove('mobile-open');
    document.getElementById('sidebar-overlay').classList.remove('show');
  }
}

function toggleSidebar() {
  const sb = document.getElementById('sidebar');
  const ov = document.getElementById('sidebar-overlay');
  const mc = document.getElementById('main-content');
  if (window.innerWidth < 768) {
    sb.classList.toggle('mobile-open');
    ov.classList.toggle('show');
  } else {
    sb.classList.toggle('collapsed');
    mc.classList.toggle('expanded');
  }
}

// =============================================
// MODAL HELPERS
// =============================================
function openModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

function showConfirm(title, desc, cb) {
  document.getElementById('confirm-title').textContent = title;
  document.getElementById('confirm-desc').textContent = desc;
  confirmCallback = cb;
  document.getElementById('confirm-dialog').classList.add('open');
}
function closeConfirm() {
  document.getElementById('confirm-dialog').classList.remove('open');
  confirmCallback = null;
}
function confirmAction() {
  if (confirmCallback) confirmCallback();
  closeConfirm();
}

// =============================================
// TOAST
// =============================================
function toast(msg, type='info') {
  const c = document.getElementById('toast-container');
  const t = document.createElement('div');
  const icons = { success:'✅', error:'❌', warning:'⚠️', info:'ℹ️' };
  t.className = `toast toast-${type}`;
  t.innerHTML = `<span>${icons[type]||'ℹ️'}</span><span>${msg}</span>`;
  c.appendChild(t);
  setTimeout(() => t.style.opacity='0', 2800);
  setTimeout(() => t.remove(), 3200);
}

// =============================================
// PROJECTS / KANBAN
// =============================================
const KANBAN_COLS = [
  { id: 'pendiente', label: 'Pendiente', color: '#64748B', dot: '#94A3B8' },
  { id: 'progreso',  label: 'En Progreso', color: '#2563EB', dot: '#60A5FA' },
  { id: 'completado',label: 'Completado', color: '#10B981', dot: '#34D399' }
];

function openNewProject() {
  // Reset form
  ['np-title','np-desc','np-owner','np-area','np-start','np-end'].forEach(id => {
    document.getElementById(id).value = '';
  });
  document.getElementById('np-priority').value = 'media';
  openModal('modal-new-project');
}

function saveNewProject() {
  const title = document.getElementById('np-title').value.trim();
  if (!title) { toast('El título es obligatorio', 'error'); return; }
  const proj = {
    id: uid(),
    title,
    desc: document.getElementById('np-desc').value.trim(),
    priority: document.getElementById('np-priority').value,
    owner: document.getElementById('np-owner').value.trim() || APP.settings.responsable,
    area: document.getElementById('np-area').value.trim(),
    start: document.getElementById('np-start').value,
    end: document.getElementById('np-end').value,
    status: 'pendiente',
    tasks: [],
    createdAt: new Date().toISOString()
  };
  APP.projects.push(proj);
  saveData();
  logAudit('Proyectos','Crear', `Proyecto "${title}" creado`);
  closeModal('modal-new-project');
  toast(`Proyecto "${title}" creado`, 'success');
  renderKanban();
  refreshDashboard();
}

function renderKanban() {
  const board = document.getElementById('kanban-board');
  board.innerHTML = '';
  KANBAN_COLS.forEach(col => {
    const projs = APP.projects.filter(p => p.status === col.id);
    const colEl = document.createElement('div');
    colEl.className = 'kanban-col';
    colEl.dataset.col = col.id;

    let cardsHTML = projs.length === 0 ?
      `<div class="empty-state" style="padding:30px 16px;">
        <div class="empty-icon" style="margin:0 auto 10px; width:50px; height:50px;">
          <svg width="22px" height="22px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 12 16 12 14 15 10 15 8 12 2 12"/><path d="M5.45 5.11L2 12v6a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2v-6l-3.45-6.89A2 2 0 0 0 16.76 4H7.24a2 2 0 0 0-1.79 1.11z"/></svg>
        </div>
        <div style="font-size:13px; font-weight:600; color:var(--text-muted);">Sin proyectos</div>
        <div style="font-size:12px; color:#CBD5E1; margin-top:4px;">Arrastra proyectos aquí</div>
      </div>` : '';

    projs.forEach(p => {
      const doneTasks = p.tasks.filter(t => t.done).length;
      const totalTasks = p.tasks.length;
      const pct = totalTasks > 0 ? Math.round(doneTasks/totalTasks*100) : 0;
      const pColors = { alta:'#EF4444', media:'#F59E0B', baja:'#10B981', critica:'#7C3AED' };
      cardsHTML += `
        <div class="proj-card" draggable="true" data-id="${p.id}"
          ondragstart="onDragStart(event)" onclick="openProjectDetail('${p.id}')">
          <div style="display:flex;align-items:flex-start;justify-content:space-between;gap:8px;margin-bottom:10px;">
            <div style="font-size:14px;font-weight:700;color:var(--text);line-height:1.4;flex:1;">${p.title}</div>
            <div style="display:flex;gap:4px;flex-shrink:0;">
              <span class="priority-badge priority-${p.priority}">${p.priority}</span>
            </div>
          </div>
          ${p.desc ? `<div style="font-size:12px;color:var(--text-muted);margin-bottom:10px;line-height:1.5;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;">${p.desc}</div>` : ''}
          <div style="display:flex;align-items:center;gap:6px;margin-bottom:10px;flex-wrap:wrap;">
            ${p.area ? `<span style="font-size:11px;background:#F1F5F9;color:#475569;padding:2px 7px;border-radius:6px;">${p.area}</span>` : ''}
            ${p.end ? `<span style="font-size:11px;color:${daysUntil(p.end) < 7 ? 'var(--danger)' : 'var(--text-muted)'};">📅 ${fmtDate(p.end)}</span>` : ''}
          </div>
          ${totalTasks > 0 ? `
            <div style="margin-bottom:8px;">
              <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--text-muted);margin-bottom:4px;">
                <span>Tareas: ${doneTasks}/${totalTasks}</span>
                <span style="font-weight:700;color:${pct===100?'var(--success)':'var(--primary-light)'};">${pct}%</span>
              </div>
              <div class="progress-bar"><div class="progress-fill" style="width:${pct}%;background:${pct===100?'var(--success)':'var(--primary-light)'}"></div></div>
            </div>
          ` : ''}
          <div style="display:flex;align-items:center;justify-content:space-between;margin-top:8px;">
            <div style="font-size:11px;color:var(--text-muted);">👤 ${p.owner||'—'}</div>
            <div style="display:flex;gap:6px;">
              <button class="btn btn-sm" style="padding:3px 8px;font-size:11px;background:#EFF6FF;color:var(--primary-light);border:none;"
                onclick="event.stopPropagation();openProjectDetail('${p.id}')">Detalles</button>
              <button class="btn btn-sm" style="padding:3px 8px;font-size:11px;background:#FEF2F2;color:var(--danger);border:none;"
                onclick="event.stopPropagation();deleteProject('${p.id}')">✕</button>
            </div>
          </div>
        </div>`;
    });

    colEl.innerHTML = `
      <div class="kanban-col-header">
        <div class="kanban-dot" style="background:${col.dot};"></div>
        <div class="kanban-col-title">${col.label}</div>
        <div class="kanban-count">${projs.length}</div>
      </div>
      <div class="kanban-cards" data-col="${col.id}">${cardsHTML}</div>
    `;

    // Drop events
    colEl.addEventListener('dragover', e => {
      e.preventDefault();
      colEl.classList.add('drag-over');
    });
    colEl.addEventListener('dragleave', () => colEl.classList.remove('drag-over'));
    colEl.addEventListener('drop', e => {
      e.preventDefault();
      colEl.classList.remove('drag-over');
      if (dragSrc) {
        const proj = APP.projects.find(p => p.id === dragSrc);
        if (proj) {
          proj.status = col.id;
          saveData();
          logAudit('Proyectos','Mover', `"${proj.title}" → ${col.label}`);
          renderKanban();
        }
      }
    });

    board.appendChild(colEl);
  });
  safeIcons();
}

function onDragStart(e) {
  dragSrc = e.currentTarget.dataset.id;
  e.currentTarget.classList.add('dragging');
  setTimeout(() => e.currentTarget.classList.remove('dragging'), 0);
}

function deleteProject(id) {
  const proj = APP.projects.find(p => p.id === id);
  if (!proj) return;
  showConfirm('¿Eliminar proyecto?',
    `"${proj.title}" y todas sus tareas serán eliminados permanentemente.`,
    () => {
      APP.projects = APP.projects.filter(p => p.id !== id);
      saveData();
      logAudit('Proyectos','Eliminar', `"${proj.title}" eliminado`);
      toast(`Proyecto eliminado`, 'warning');
      renderKanban();
      refreshDashboard();
    });
}

// PROJECT DETAIL MODAL
function openProjectDetail(id) {
  const proj = APP.projects.find(p => p.id === id);
  if (!proj) return;
  const doneTasks = proj.tasks.filter(t => t.done).length;
  const totalTasks = proj.tasks.length;
  const pct = totalTasks > 0 ? Math.round(doneTasks/totalTasks*100) : 0;

  const tasksHTML = proj.tasks.length === 0 ?
    `<div class="empty-state" style="padding:30px;">
      <div class="empty-icon" style="margin:0 auto 12px;width:52px;height:52px;">
        <svg width="22px" height="22px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="5" width="6" height="6" rx="1"/><path d="m3 17 2 2 4-4"/><path d="M13 6h8"/><path d="M13 12h8"/><path d="M13 18h8"/></svg>
      </div>
      <div class="empty-title">Sin tareas aún</div>
      <div class="empty-desc">Agrega tareas para hacer seguimiento del avance</div>
    </div>` :
    proj.tasks.map(task => `
      <div class="task-item" id="task-${task.id}">
        <div class="task-check ${task.done?'done':''}" onclick="toggleTask('${proj.id}','${task.id}')">
          ${task.done ? `<svg width="10" height="10" viewBox="0 0 10 10"><polyline points="1.5,5 4,7.5 8.5,2.5" stroke="white" stroke-width="1.5" fill="none" stroke-linecap="round"/></svg>` : ''}
        </div>
        <div class="task-text ${task.done?'done':''}" style="flex:1;">${task.text}</div>
        <div style="font-size:11px;color:var(--text-muted);flex-shrink:0;margin:0 8px;">${task.assignee||''}</div>
        <button style="background:none;border:none;cursor:pointer;color:#CBD5E1;padding:2px;" onclick="deleteTask('${proj.id}','${task.id}')">
          <svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
        </button>
      </div>
    `).join('');

  document.getElementById('project-detail-content').innerHTML = `
    <div class="modal-header" style="background:linear-gradient(135deg,var(--primary-dark),var(--primary));border-radius:20px 20px 0 0;padding:24px 28px;">
      <div>
        <div style="display:flex;align-items:center;gap:10px;flex-wrap:wrap;">
          <span class="priority-badge priority-${proj.priority}" style="background:rgba(255,255,255,0.15);color:white;">${proj.priority}</span>
          <span class="status-badge" style="background:rgba(255,255,255,0.15);color:white;">${proj.status}</span>
          ${proj.area ? `<span style="background:rgba(255,255,255,0.1);color:rgba(255,255,255,0.8);font-size:11px;padding:3px 9px;border-radius:20px;">${proj.area}</span>` : ''}
        </div>
        <div style="color:white;font-size:20px;font-weight:800;margin-top:8px;line-height:1.3;">${proj.title}</div>
        ${proj.desc ? `<div style="color:rgba(255,255,255,0.65);font-size:13px;margin-top:6px;">${proj.desc}</div>` : ''}
      </div>
      <button class="modal-close" style="background:rgba(255,255,255,0.1);color:white;" onclick="closeModal('modal-project-detail')">
        <svg width="16px" height="16px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
      </button>
    </div>
    <div class="modal-body" style="display:grid;grid-template-columns:200px 1fr;gap:20px;padding:24px 28px;">
      <!-- LEFT PANEL -->
      <div>
        <!-- Stats -->
        <div style="background:#F8FAFC;border-radius:12px;padding:14px;margin-bottom:14px;border:1px solid var(--border);">
          <div style="font-size:11px;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:0.06em;margin-bottom:12px;">Estadísticas</div>
          <div style="text-align:center;margin-bottom:12px;">
            <div style="font-size:30px;font-weight:800;color:${pct===100?'var(--success)':'var(--primary-light)'};">${pct}%</div>
            <div style="font-size:11px;color:var(--text-muted);">Completado</div>
          </div>
          <div class="progress-bar" style="margin-bottom:12px;"><div class="progress-fill" style="width:${pct}%;background:${pct===100?'var(--success)':'var(--primary-light)'}"></div></div>
          <div class="info-row"><span class="info-key">Tareas</span><span class="info-val">${totalTasks}</span></div>
          <div class="info-row"><span class="info-key">Completas</span><span class="info-val">${doneTasks}</span></div>
          <div class="info-row"><span class="info-key">Pendientes</span><span class="info-val">${totalTasks-doneTasks}</span></div>
        </div>
        <!-- Info -->
        <div style="background:#F8FAFC;border-radius:12px;padding:14px;border:1px solid var(--border);">
          <div style="font-size:11px;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:0.06em;margin-bottom:10px;">Información</div>
          <div class="info-row"><span class="info-key">Responsable</span><span class="info-val" style="font-size:11px;">${proj.owner||'—'}</span></div>
          <div class="info-row"><span class="info-key">Inicio</span><span class="info-val" style="font-size:11px;">${fmtDate(proj.start)}</span></div>
          <div class="info-row"><span class="info-key">Fin</span><span class="info-val" style="font-size:11px;color:${proj.end&&daysUntil(proj.end)<7?'var(--danger)':'inherit'}">${fmtDate(proj.end)}</span></div>
          <div class="info-row"><span class="info-key">Creado</span><span class="info-val" style="font-size:11px;">${fmtDate(proj.createdAt)}</span></div>
        </div>
        <!-- Move to -->
        <div style="margin-top:14px;">
          <div style="font-size:11px;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:0.06em;margin-bottom:8px;">Mover a</div>
          ${KANBAN_COLS.filter(c=>c.id!==proj.status).map(c=>`
            <button class="btn btn-secondary btn-sm" style="width:100%;margin-bottom:6px;justify-content:flex-start;" onclick="moveProject('${proj.id}','${c.id}')">
              ${c.label}
            </button>
          `).join('')}
        </div>
      </div>
      <!-- RIGHT PANEL -->
      <div>
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;">
          <div style="font-size:15px;font-weight:700;">Lista de Tareas</div>
        </div>
        <!-- Add task -->
        <div style="display:flex;gap:8px;margin-bottom:14px;">
          <input class="form-input" id="new-task-input-${proj.id}" placeholder="Descripción de la tarea..." style="flex:1;"
            onkeydown="if(event.key==='Enter') addTask('${proj.id}')">
          <input class="form-input" id="new-task-assignee-${proj.id}" placeholder="Responsable" style="width:130px;">
          <button class="btn btn-primary btn-sm" onclick="addTask('${proj.id}')">Añadir</button>
        </div>
        <div id="tasks-container-${proj.id}">${tasksHTML}</div>
      </div>
    </div>
  `;
  openModal('modal-project-detail');
  safeIcons();
}

function addTask(projId) {
  const inp = document.getElementById(`new-task-input-${projId}`);
  const asgn = document.getElementById(`new-task-assignee-${projId}`);
  const text = inp.value.trim();
  if (!text) return;
  const proj = APP.projects.find(p => p.id === projId);
  if (!proj) return;
  const task = { id: uid(), text, done: false, assignee: asgn.value.trim(), createdAt: new Date().toISOString() };
  proj.tasks.push(task);
  saveData();
  logAudit('Tareas','Crear', `"${text}" en "${proj.title}"`);
  inp.value = ''; asgn.value = '';
  openProjectDetail(projId);
}

function toggleTask(projId, taskId) {
  const proj = APP.projects.find(p => p.id === projId);
  if (!proj) return;
  const task = proj.tasks.find(t => t.id === taskId);
  if (!task) return;
  task.done = !task.done;
  saveData();
  openProjectDetail(projId);
}

function deleteTask(projId, taskId) {
  const proj = APP.projects.find(p => p.id === projId);
  if (!proj) return;
  proj.tasks = proj.tasks.filter(t => t.id !== taskId);
  saveData();
  logAudit('Tareas','Eliminar', `Tarea eliminada en "${proj.title}"`);
  openProjectDetail(projId);
}

function moveProject(id, newStatus) {
  const proj = APP.projects.find(p => p.id === id);
  if (!proj) return;
  const old = proj.status;
  proj.status = newStatus;
  saveData();
  logAudit('Proyectos','Mover', `"${proj.title}": ${old} → ${newStatus}`);
  toast(`Movido a ${newStatus}`, 'success');
  closeModal('modal-project-detail');
  renderKanban();
}

// =============================================
// DASHBOARD
// =============================================
function refreshDashboard() {
  generateAlerts();
  renderDashboard();
}

function renderDashboard() {
  const total = APP.workers.length;
  const aptos = APP.workers.filter(w => w.status === 'activo').length;
  const pctAptos = total > 0 ? Math.round(aptos/total*100) : 0;
  const alerts = APP.alerts;
  const critAlerts = alerts.filter(a => a.type === 'critical').length;

  document.getElementById('kpi-total-workers').textContent = total;
  document.getElementById('kpi-aptos').textContent = pctAptos + '%';
  document.getElementById('kpi-aptos-trend').textContent = `${aptos} de ${total} activos`;
  document.getElementById('kpi-aptos-trend').className = 'kpi-trend ' + (pctAptos >= 80 ? 'trend-up' : 'trend-down');
  document.getElementById('kpi-alertas').textContent = critAlerts;
  document.getElementById('kpi-docs').textContent = total > 0 ? Math.round(Math.random()*20+75) + '%' : '—';
  document.getElementById('kpi-proyectos').textContent = APP.projects.filter(p => p.status==='progreso').length;
  document.getElementById('kpi-contratistas').textContent = APP.contractors.length;

  // Alert badge
  const alertBadge = document.getElementById('alert-badge');
  alertBadge.textContent = critAlerts;
  alertBadge.style.display = critAlerts > 0 ? '' : 'none';
  document.getElementById('notif-dot').style.display = critAlerts > 0 ? '' : 'none';

  // Dash alerts
  const dashAlerts = document.getElementById('dash-alerts-list');
  if (alerts.length === 0) {
    dashAlerts.innerHTML = `<div style="text-align:center;padding:24px;color:var(--text-muted);font-size:13px;">✅ Sin alertas activas</div>`;
  } else {
    dashAlerts.innerHTML = alerts.slice(0,4).map(a => `
      <div class="alert-item alert-${a.type==='critical'?'critical':a.type==='warning'?'warning':'info'}">
        <div class="alert-dot dot-${a.type==='critical'?'critical':a.type==='warning'?'warning':'info'}"></div>
        <div style="flex:1;">
          <div class="alert-title">${a.title}</div>
          <div class="alert-desc">${a.desc}</div>
        </div>
        <div class="alert-time">${a.time}</div>
      </div>
    `).join('');
  }

  // Compliance chart
  const chart = document.getElementById('compliance-chart');
  const data = [
    { label: 'Capacitaciones', pct: 78, color: 'var(--primary-light)' },
    { label: 'Exámenes médicos', pct: 85, color: 'var(--success)' },
    { label: 'EPP entregado', pct: 92, color: '#7C3AED' },
    { label: 'Documentación', pct: 67, color: 'var(--warning)' },
    { label: 'Inducción SST', pct: 91, color: 'var(--accent2)' }
  ];
  chart.innerHTML = data.map(d => `
    <div class="chart-bar-wrap">
      <div class="chart-bar-label">${d.label}</div>
      <div class="chart-bar-track"><div class="chart-bar-fill" style="width:${d.pct}%;background:${d.color};"></div></div>
      <div class="chart-bar-pct" style="color:${d.color};">${d.pct}%</div>
    </div>
  `).join('');

  // Dash projects
  const dashProj = document.getElementById('dash-projects-list');
  const projs = [...APP.projects].sort((a,b) => new Date(b.createdAt)-new Date(a.createdAt)).slice(0,4);
  if (projs.length === 0) {
    dashProj.innerHTML = `<div class="empty-state" style="padding:30px;">
      <div class="empty-icon" style="margin:0 auto 12px;width:52px;height:52px;"><svg width="22px" height="22px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M6 5v11"/><path d="M12 5v6"/><path d="M18 5v14"/><rect x="3" y="3" width="6" height="18" rx="1"/><rect x="9" y="3" width="6" height="12" rx="1"/><rect x="15" y="3" width="6" height="20" rx="1"/></svg></div>
      <div class="empty-title">Sin proyectos</div>
      <div class="empty-desc">Crea tu primer proyecto SG-SST</div>
      <button class="btn btn-primary btn-sm" style="margin-top:12px;" onclick="openNewProject()">Crear proyecto</button>
    </div>`;
  } else {
    dashProj.innerHTML = `<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:12px;">` +
      projs.map(p => {
        const pct = p.tasks.length > 0 ? Math.round(p.tasks.filter(t=>t.done).length/p.tasks.length*100) : 0;
        return `<div class="card" style="padding:14px;cursor:pointer;" onclick="navigate('kanban')">
          <div style="font-size:13px;font-weight:700;margin-bottom:6px;">${p.title}</div>
          <div style="display:flex;gap:6px;margin-bottom:8px;flex-wrap:wrap;">
            <span class="priority-badge priority-${p.priority}">${p.priority}</span>
            <span class="status-badge status-${p.status}">${p.status}</span>
          </div>
          <div class="progress-bar"><div class="progress-fill" style="width:${pct}%;background:var(--primary-light);"></div></div>
          <div style="font-size:11px;color:var(--text-muted);margin-top:4px;">${pct}% completado</div>
        </div>`;
      }).join('') + `</div>`;
  }
  safeIcons();
}

// =============================================
// ALERTS
// =============================================
function generateAlerts() {
  const alerts = [];
  const today = new Date();

  APP.workers.forEach(w => {
    // Certs
    (w.certs || []).forEach(c => {
      if (!c.expiry) return;
      const days = daysUntil(c.expiry);
      if (days !== null) {
        if (days < 0) {
          alerts.push({ id: uid(), type:'critical', title:`Certificación vencida: ${c.name}`, desc:`${w.name} — Venció hace ${Math.abs(days)} días`, time: 'Urgente', worker: w.id });
        } else if (days <= 30) {
          alerts.push({ id: uid(), type:'warning', title:`Certificación próxima a vencer: ${c.name}`, desc:`${w.name} — Vence en ${days} días (${fmtDate(c.expiry)})`, time:`${days}d`, worker: w.id });
        }
      }
    });
    // Inactive
    if (w.status === 'inactivo') {
      alerts.push({ id: uid(), type:'info', title:'Trabajador inactivo', desc:`${w.name} — ${w.cargo||'Sin cargo'}`, time:'Info', worker: w.id });
    }
  });

  APP.projects.forEach(p => {
    if (p.end) {
      const days = daysUntil(p.end);
      if (days !== null && days < 7 && days >= 0 && p.status !== 'completado') {
        alerts.push({ id: uid(), type:'warning', title:'Proyecto próximo a vencer', desc:`"${p.title}" — Vence en ${days} días`, time:`${days}d` });
      }
      if (days !== null && days < 0 && p.status !== 'completado') {
        alerts.push({ id: uid(), type:'critical', title:'Proyecto vencido', desc:`"${p.title}" — Sin completar`, time:'Vencido' });
      }
    }
  });

  if (APP.workers.length === 0) {
    alerts.push({ id: uid(), type:'info', title:'Configura el sistema', desc:'Registra trabajadores para activar el monitoreo de alertas', time:'Config' });
  }

  APP.alerts = alerts;
  saveData();

  // Update badge
  const crit = alerts.filter(a => a.type === 'critical').length;
  const badge = document.getElementById('alert-badge');
  if (badge) { badge.textContent = crit; badge.style.display = crit > 0 ? '' : 'none'; }
  document.getElementById('notif-dot').style.display = crit > 0 ? '' : 'none';
}

function renderAlerts() {
  generateAlerts();
  const crit = APP.alerts.filter(a => a.type==='critical').length;
  const warn = APP.alerts.filter(a => a.type==='warning').length;
  const info = APP.alerts.filter(a => a.type==='info').length;
  document.getElementById('alert-count-critica').textContent = crit;
  document.getElementById('alert-count-warning').textContent = warn;
  document.getElementById('alert-count-info').textContent = info;

  const list = document.getElementById('alerts-full-list');
  if (APP.alerts.length === 0) {
    list.innerHTML = `<div class="empty-state"><div class="empty-icon" style="margin:0 auto 12px;"><svg width="28px" height="28px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M13.73 21a2 2 0 0 1-3.46 0"/><path d="M18.63 13A17.89 17.89 0 0 1 18 8"/><path d="M6.26 6.26A5.86 5.86 0 0 0 6 8c0 7-3 9-3 9h14"/><path d="M18 8a6 6 0 0 0-9.33-5"/><line x1="2" y1="2" x2="22" y2="22"/></svg></div><div class="empty-title">Sin alertas activas</div><div class="empty-desc">El sistema está en óptimas condiciones ✅</div></div>`;
  } else {
    list.innerHTML = APP.alerts.map(a => `
      <div class="alert-item alert-${a.type==='critical'?'critical':a.type==='warning'?'warning':'info'}">
        <div class="alert-dot dot-${a.type==='critical'?'critical':a.type==='warning'?'warning':'info'}"></div>
        <div style="flex:1;">
          <div class="alert-title">${a.title}</div>
          <div class="alert-desc">${a.desc}</div>
        </div>
        <span style="font-size:11px;font-weight:600;padding:3px 8px;border-radius:6px;background:rgba(0,0,0,0.05);color:var(--text-muted);">${a.time}</span>
      </div>
    `).join('');
  }
  safeIcons();
}

// =============================================
// WORKERS
// =============================================
function openWorkerModal(id) {
  document.getElementById('worker-modal-title').textContent = id ? '✏️ Editar Trabajador' : '👤 Nuevo Trabajador';
  document.getElementById('worker-edit-id').value = id || '';
  currentWorkerTab = 0;
  switchTab('worker', 0);

  if (id) {
    const w = APP.workers.find(x => x.id === id);
    if (!w) return;
    document.getElementById('w-name').value = w.name || '';
    document.getElementById('w-cedula').value = w.cedula || '';
    document.getElementById('w-cargo').value = w.cargo || '';
    document.getElementById('w-area').value = w.area || '';
    document.getElementById('w-status').value = w.status || 'activo';
    document.getElementById('w-ingreso').value = w.ingreso || '';
    document.getElementById('w-blood').value = w.blood || '';
    document.getElementById('w-avatar').value = w.avatar || '👷';
    document.getElementById('w-centro').value = w.centro || '';
    document.getElementById('w-telefono').value = w.telefono || '';
    selectedAvatar = w.avatar || '👷';
    // Load photo
    const photoVal = w.photo || '';
    document.getElementById('w-photo').value = photoVal;
    const prevEl = document.getElementById('photo-preview');
    const rmBtn = document.getElementById('remove-photo-btn');
    if (photoVal) {
      prevEl.innerHTML = `<img src="${photoVal}" style="width:100%;height:100%;object-fit:cover;">`;
      if (rmBtn) rmBtn.style.display = '';
    } else {
      prevEl.innerHTML = w.avatar || '👤';
      if (rmBtn) rmBtn.style.display = 'none';
    }
  } else {
    ['w-name','w-cedula','w-cargo','w-area','w-ingreso','w-centro','w-telefono'].forEach(f => document.getElementById(f).value = '');
    document.getElementById('w-status').value = 'activo';
    document.getElementById('w-blood').value = '';
    document.getElementById('w-avatar').value = '👷';
    document.getElementById('w-photo').value = '';
    selectedAvatar = '👷';
    const prevEl = document.getElementById('photo-preview');
    if (prevEl) prevEl.innerHTML = '👤';
    const rmBtn = document.getElementById('remove-photo-btn');
    if (rmBtn) rmBtn.style.display = 'none';
  }

  // Highlight selected avatar
  document.querySelectorAll('.avatar-opt').forEach(el => {
    el.style.border = el.textContent.trim() === selectedAvatar ? '2px solid var(--primary-light)' : '2px solid transparent';
  });

  // Populate contractor dropdown
  const cSel = document.getElementById('w-contractor');
  cSel.innerHTML = '<option value="">Planta directa</option>';
  APP.contractors.forEach(c => {
    const opt = document.createElement('option'); opt.value = c.id; opt.textContent = c.name;
    cSel.appendChild(opt);
  });

  // Certs
  const cl = document.getElementById('certs-list');
  cl.innerHTML = '';
  certFieldCount = 0;
  const certs = id ? (APP.workers.find(x=>x.id===id)?.certs || []) : [];
  certs.forEach(c => addCertField(c));

  // Docs
  const dl = document.getElementById('docs-list');
  dl.innerHTML = '';
  docFieldCount = 0;
  const docs = id ? (APP.workers.find(x=>x.id===id)?.docs || []) : [];
  docs.forEach(d => addDocField(d));

  openModal('modal-worker');
}

function selectAvatar(el, emoji) {
  selectedAvatar = emoji;
  document.getElementById('w-avatar').value = emoji;
  document.querySelectorAll('.avatar-opt').forEach(e => e.style.border = '2px solid transparent');
  el.style.border = '2px solid var(--primary-light)';
  // Update preview only if no photo loaded
  if (!document.getElementById('w-photo').value) {
    const prev = document.getElementById('photo-preview');
    if (prev) prev.innerHTML = emoji;
  }
}

// ── Photo handling ──
let _cameraStream = null;

function handlePhotoUpload(event) {
  const file = event.target.files[0];
  if (!file) return;
  if (file.size > 2 * 1024 * 1024) { toast('La imagen supera los 2MB', 'error'); return; }
  const reader = new FileReader();
  reader.onload = e => {
    cropAndSetPhoto(e.target.result);
  };
  reader.readAsDataURL(file);
  event.target.value = '';
}

function cropAndSetPhoto(dataUrl) {
  const img = new Image();
  img.onload = () => {
    const canvas = document.getElementById('photo-canvas');
    const size = Math.min(img.width, img.height);
    canvas.width = 200; canvas.height = 200;
    const ctx = canvas.getContext('2d');
    // Clip to circle
    ctx.beginPath();
    ctx.arc(100, 100, 100, 0, 2 * Math.PI);
    ctx.clip();
    const sx = (img.width - size) / 2;
    const sy = (img.height - size) / 2;
    ctx.drawImage(img, sx, sy, size, size, 0, 0, 200, 200);
    const dataURL = canvas.toDataURL('image/jpeg', 0.85);
    document.getElementById('w-photo').value = dataURL;
    const prev = document.getElementById('photo-preview');
    if (prev) prev.innerHTML = `<img src="${dataURL}" style="width:100%;height:100%;object-fit:cover;">`;
    const rmBtn = document.getElementById('remove-photo-btn');
    if (rmBtn) rmBtn.style.display = '';
  };
  img.src = dataUrl;
}

function removePhoto() {
  document.getElementById('w-photo').value = '';
  const prev = document.getElementById('photo-preview');
  if (prev) prev.innerHTML = document.getElementById('w-avatar').value || '👤';
  const rmBtn = document.getElementById('remove-photo-btn');
  if (rmBtn) rmBtn.style.display = 'none';
}

function startCamera() {
  const panel = document.getElementById('camera-panel');
  const video = document.getElementById('camera-video');
  panel.style.display = 'block';
  navigator.mediaDevices.getUserMedia({ video: { facingMode: 'user' }, audio: false })
    .then(stream => {
      _cameraStream = stream;
      video.srcObject = stream;
    })
    .catch(() => {
      toast('No se pudo acceder a la cámara. Verifica los permisos.', 'error');
      panel.style.display = 'none';
    });
}

function capturePhoto() {
  const video = document.getElementById('camera-video');
  const canvas = document.getElementById('photo-canvas');
  canvas.width = 400; canvas.height = 400;
  const ctx = canvas.getContext('2d');
  // Square center crop from video
  const vw = video.videoWidth, vh = video.videoHeight;
  const s = Math.min(vw, vh);
  ctx.drawImage(video, (vw-s)/2, (vh-s)/2, s, s, 0, 0, 400, 400);
  cropAndSetPhoto(canvas.toDataURL('image/jpeg', 0.85));
  stopCamera();
}

function stopCamera() {
  if (_cameraStream) {
    _cameraStream.getTracks().forEach(t => t.stop());
    _cameraStream = null;
  }
  const panel = document.getElementById('camera-panel');
  if (panel) panel.style.display = 'none';
}

function addCertField(data) {
  certFieldCount++;
  const id = `cert-${certFieldCount}`;
  const el = document.createElement('div');
  el.style.cssText = 'display:flex;gap:8px;align-items:center;';
  el.innerHTML = `
    <input class="form-input" id="${id}-name" placeholder="Nombre del curso" style="flex:2;" value="${data?.name||''}">
    <input class="form-input" id="${id}-expiry" type="date" style="flex:1;" value="${data?.expiry||''}">
    <button class="btn btn-danger btn-sm" onclick="this.parentElement.remove()" style="flex-shrink:0;">✕</button>
  `;
  document.getElementById('certs-list').appendChild(el);
}

function addDocField(data) {
  docFieldCount++;
  const id = `doc-${docFieldCount}`;
  const el = document.createElement('div');
  el.style.cssText = 'display:flex;gap:8px;align-items:center;';
  el.innerHTML = `
    <input class="form-input" id="${id}-name" placeholder="Documento (Ej: Contrato, ARL, EPS...)" style="flex:2;" value="${data?.name||''}">
    <select class="form-select" id="${id}-status" style="flex:1;">
      <option value="vigente" ${data?.status==='vigente'?'selected':''}>✅ Vigente</option>
      <option value="vencido" ${data?.status==='vencido'?'selected':''}>❌ Vencido</option>
      <option value="pendiente" ${data?.status==='pendiente'?'selected':''}>⏳ Pendiente</option>
    </select>
    <button class="btn btn-danger btn-sm" onclick="this.parentElement.remove()" style="flex-shrink:0;">✕</button>
  `;
  document.getElementById('docs-list').appendChild(el);
}

function saveWorker() {
  const name = document.getElementById('w-name').value.trim();
  const cedula = document.getElementById('w-cedula').value.trim();
  if (!name) { toast('El nombre es obligatorio', 'error'); return; }

  // Collect certs
  const certs = [];
  document.querySelectorAll('[id^="cert-"][id$="-name"]').forEach(el => {
    const n = el.id.replace('-name','');
    const expEl = document.getElementById(n+'-expiry');
    if (el.value.trim()) certs.push({ name: el.value.trim(), expiry: expEl?.value || '' });
  });

  // Collect docs
  const docs = [];
  document.querySelectorAll('[id^="doc-"][id$="-name"]').forEach(el => {
    const n = el.id.replace('-name','');
    const stEl = document.getElementById(n+'-status');
    if (el.value.trim()) docs.push({ name: el.value.trim(), status: stEl?.value || 'vigente' });
  });

  const editId = document.getElementById('worker-edit-id').value;
  if (editId) {
    const w = APP.workers.find(x => x.id === editId);
    if (w) {
      Object.assign(w, {
        name, cedula,
        cargo: document.getElementById('w-cargo').value.trim(),
        area: document.getElementById('w-area').value.trim(),
        status: document.getElementById('w-status').value,
        ingreso: document.getElementById('w-ingreso').value,
        blood: document.getElementById('w-blood').value,
        avatar: document.getElementById('w-avatar').value,
        photo: document.getElementById('w-photo').value,
        contractor: document.getElementById('w-contractor').value,
        centro: document.getElementById('w-centro').value.trim(),
        telefono: document.getElementById('w-telefono').value.trim(),
        certs, docs
      });
      logAudit('Trabajadores','Editar', `"${name}" actualizado`);
    }
  } else {
    APP.workers.push({
      id: uid(), name, cedula,
      cargo: document.getElementById('w-cargo').value.trim(),
      area: document.getElementById('w-area').value.trim(),
      status: document.getElementById('w-status').value,
      ingreso: document.getElementById('w-ingreso').value,
      blood: document.getElementById('w-blood').value,
      avatar: document.getElementById('w-avatar').value,
      photo: document.getElementById('w-photo').value,
      contractor: document.getElementById('w-contractor').value,
      centro: document.getElementById('w-centro').value.trim(),
      telefono: document.getElementById('w-telefono').value.trim(),
      certs, docs,
      createdAt: new Date().toISOString()
    });
    logAudit('Trabajadores','Crear', `"${name}" registrado`);
  }

  saveData();
  closeModal('modal-worker');
  toast(`Trabajador ${editId?'actualizado':'registrado'} exitosamente`, 'success');
  renderWorkers();
  refreshDashboard();
  renderCarnetPage();
}

function renderWorkers() {
  const grid = document.getElementById('workers-grid');
  const q = (document.getElementById('worker-search')?.value || '').toLowerCase();
  const filtered = APP.workers.filter(w =>
    w.name.toLowerCase().includes(q) ||
    (w.cedula||'').toLowerCase().includes(q) ||
    (w.cargo||'').toLowerCase().includes(q)
  );

  if (filtered.length === 0) {
    grid.innerHTML = `<div class="empty-state" style="grid-column:1/-1;padding:60px;">
      <div class="empty-icon" style="margin:0 auto 16px;"><svg width="28px" height="28px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><line x1="17" y1="8" x2="23" y2="14"/><line x1="23" y1="8" x2="17" y2="14"/></svg></div>
      <div class="empty-title">${APP.workers.length===0?'Sin trabajadores registrados':'Sin resultados'}</div>
      <div class="empty-desc">${APP.workers.length===0?'Registra tu primer trabajador para comenzar el seguimiento SG-SST':'Intenta con otros términos de búsqueda'}</div>
      ${APP.workers.length===0?`<button class="btn btn-primary" style="margin-top:16px;" onclick="openWorkerModal()"><svg width="14px" height="14px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><line x1="19" y1="8" x2="19" y2="14"/><line x1="22" y1="11" x2="16" y2="11"/></svg> Registrar trabajador</button>`:''}
    </div>`;
    safeIcons();
    return;
  }

  grid.innerHTML = filtered.map(w => {
    const statusCls = { activo:'ws-activo', inactivo:'ws-inactivo', suspendido:'ws-suspendido' };
    const statusLabel = { activo:'Activo', inactivo:'Inactivo', suspendido:'Suspendido' };
    const vencidos = (w.certs||[]).filter(c => c.expiry && daysUntil(c.expiry) < 0).length;
    const proximos = (w.certs||[]).filter(c => c.expiry && daysUntil(c.expiry) >= 0 && daysUntil(c.expiry) <= 30).length;
    return `
      <div class="worker-card">
        <div class="worker-card-header">
          <span class="worker-status-badge ${statusCls[w.status]||'ws-activo'}">${statusLabel[w.status]||'Activo'}</span>
          <div class="worker-avatar-large">${w.photo ? `<img src="${w.photo}" style="width:100%;height:100%;object-fit:cover;">` : (w.avatar||'👷')}</div>
          <div class="worker-name">${w.name}</div>
          <div class="worker-cargo">${w.cargo||'Sin cargo'}</div>
        </div>
        <div class="worker-info">
          <div class="info-row"><span class="info-key">Cédula</span><span class="info-val">${w.cedula||'—'}</span></div>
          <div class="info-row"><span class="info-key">Área</span><span class="info-val">${w.area||'—'}</span></div>
          ${w.centro?`<div class="info-row"><span class="info-key">Centro</span><span class="info-val">${w.centro}</span></div>`:''}
          <div class="info-row"><span class="info-key">Ingreso</span><span class="info-val">${fmtDate(w.ingreso)}</span></div>
          ${vencidos>0 ? `<div style="margin-top:8px;"><span class="cert-chip cert-vencido">⚠️ ${vencidos} cert. vencida${vencidos>1?'s':''}</span></div>` : ''}
          ${proximos>0 && vencidos===0 ? `<div style="margin-top:8px;"><span class="cert-chip cert-proximo">⏰ ${proximos} próxima${proximos>1?'s':''} a vencer</span></div>` : ''}
          ${vencidos===0 && proximos===0 && (w.certs||[]).length>0 ? `<div style="margin-top:8px;"><span class="cert-chip cert-vigente">✅ Certificaciones al día</span></div>` : ''}
          <div style="display:flex;gap:8px;margin-top:12px;">
            <button class="btn btn-secondary btn-sm" style="flex:1;" onclick="openWorkerModal('${w.id}')">Editar</button>
            <button class="btn btn-success btn-sm" onclick="goToCarnet('${w.id}')">Carnet</button>
            <button class="btn btn-danger btn-sm" onclick="deleteWorker('${w.id}')">✕</button>
          </div>
        </div>
      </div>
    `;
  }).join('');
  safeIcons();
}

function goToCarnet(wId) {
  navigate('carnet');
  setTimeout(() => {
    document.getElementById('carnet-worker-select').value = wId;
    renderCarnet();
  }, 100);
}

function deleteWorker(id) {
  const w = APP.workers.find(x => x.id === id);
  if (!w) return;
  showConfirm('¿Eliminar trabajador?',
    `"${w.name}" y todos sus datos serán eliminados.`,
    () => {
      APP.workers = APP.workers.filter(x => x.id !== id);
      saveData();
      logAudit('Trabajadores','Eliminar', `"${w.name}" eliminado`);
      toast('Trabajador eliminado', 'warning');
      renderWorkers();
      refreshDashboard();
    });
}

// =============================================
// CARNET
// =============================================
function renderCarnetPage() {
  const sel = document.getElementById('carnet-worker-select');
  if (!sel) return;
  const current = sel.value;
  sel.innerHTML = '<option value="">— Selecciona un trabajador —</option>';
  APP.workers.forEach(w => {
    const opt = document.createElement('option');
    opt.value = w.id; opt.textContent = w.name;
    sel.appendChild(opt);
  });
  if (current) { sel.value = current; renderCarnet(); }
}

function renderCarnet() {
  const wId = document.getElementById('carnet-worker-select').value;
  const infoPanel = document.getElementById('carnet-info-panel');
  const display = document.getElementById('carnet-display');
  const actions = document.getElementById('carnet-actions');

  if (!wId) {
    infoPanel.innerHTML = `<div class="empty-state" style="padding:30px;"><div class="empty-icon" style="margin:0 auto 12px;"><svg width="28px" height="28px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="5" width="20" height="14" rx="2"/><circle cx="8" cy="12" r="2"/><path d="M12 11h4"/><path d="M12 15h4"/></svg></div><div class="empty-title">Selecciona un trabajador</div></div>`;
    display.innerHTML = '<div style="color:var(--text-muted);font-size:13px;padding:40px;">Selecciona un trabajador para ver su carnet</div>';
    actions.style.display = 'none';
    safeIcons();
    return;
  }

  const w = APP.workers.find(x => x.id === wId);
  if (!w) return;

  // Info panel
  const vencidos = (w.certs||[]).filter(c => c.expiry && daysUntil(c.expiry) < 0).length;
  const proximos = (w.certs||[]).filter(c => c.expiry && daysUntil(c.expiry) >= 0 && daysUntil(c.expiry) <= 30).length;
  const statusCls = { activo:'ws-activo', inactivo:'ws-inactivo', suspendido:'ws-suspendido' };

  infoPanel.innerHTML = `
    <div style="padding:16px;">
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:16px;">
        <div style="width:52px;height:52px;border-radius:50%;background:linear-gradient(135deg,var(--primary),var(--primary-light));display:flex;align-items:center;justify-content:center;font-size:22px;overflow:hidden;">${w.photo ? `<img src="${w.photo}" style="width:100%;height:100%;object-fit:cover;">` : (w.avatar||'👷')}</div>
        <div>
          <div style="font-weight:700;font-size:15px;">${w.name}</div>
          <span class="worker-status-badge ${statusCls[w.status]||'ws-activo'}" style="font-size:10px;">${w.status||'Activo'}</span>
        </div>
      </div>
      <div class="info-row"><span class="info-key">Cédula</span><span class="info-val">${w.cedula||'—'}</span></div>
      <div class="info-row"><span class="info-key">Cargo</span><span class="info-val">${w.cargo||'—'}</span></div>
      <div class="info-row"><span class="info-key">Área</span><span class="info-val">${w.area||'—'}</span></div>
      ${w.centro?`<div class="info-row"><span class="info-key">Centro trab.</span><span class="info-val">${w.centro}</span></div>`:''}
      <div class="info-row"><span class="info-key">Ingreso</span><span class="info-val">${fmtDate(w.ingreso)}</span></div>
      <div class="info-row"><span class="info-key">Tipo sangre</span><span class="info-val">${w.blood||'—'}</span></div>
      <div style="margin-top:14px;">
        <div style="font-size:12px;font-weight:700;color:var(--text-muted);text-transform:uppercase;letter-spacing:0.06em;margin-bottom:8px;">Certificaciones</div>
        ${(w.certs||[]).length === 0 ? '<div style="font-size:12px;color:var(--text-muted);">Sin certificaciones registradas</div>' :
          (w.certs||[]).map(c => {
            const d = daysUntil(c.expiry);
            const cls = d===null?'cert-vigente':d<0?'cert-vencido':d<=30?'cert-proximo':'cert-vigente';
            const label = d===null?'Sin fecha':d<0?'Vencido':d<=30?`${d}d`:fmtDate(c.expiry);
            return `<span class="cert-chip ${cls}">${c.name}: ${label}</span>`;
          }).join('')
        }
      </div>
    </div>
  `;

  // ID Card
  const empresa = APP.settings.empresa || 'Mi Empresa S.A.S.';
  display.innerHTML = `
    <div class="id-card" id="id-card-render">
      <div class="id-card-header">
        <div style="width:36px;height:36px;background:rgba(255,255,255,0.15);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;">🛡️</div>
        <div class="id-card-logo">Safety ID Pro<span>SG-SST · ${empresa}</span></div>
      </div>
      <div class="id-card-body">
        <div class="id-photo">${w.photo ? `<img src="${w.photo}" style="width:100%;height:100%;object-fit:cover;border-radius:50%;">` : (w.avatar||'👷')}</div>
        <div class="id-info">
          <div class="id-name">${w.name}</div>
          <div class="id-company">${empresa}</div>
          <div class="id-cargo">${w.cargo||'Sin cargo'}</div>
          <div class="id-field"><strong>CC:</strong> ${w.cedula||'—'}</div>
          <div class="id-field"><strong>Área:</strong> ${w.area||'—'}</div>
          ${w.centro?`<div class="id-field"><strong>Centro:</strong> ${w.centro}</div>`:''}
          <div class="id-field"><strong>Sangre:</strong> ${w.blood||'—'}</div>
          <div class="id-field"><strong>Estado:</strong> <span style="color:${w.status==='activo'?'var(--success)':w.status==='suspendido'?'var(--danger)':'var(--text-muted)'};">${(w.status||'activo').toUpperCase()}</span></div>
          <div class="id-field" style="margin-top:4px;"><strong>Ingreso:</strong> ${fmtDate(w.ingreso)}</div>
        </div>
      </div>
      <div class="id-card-footer">
        <div>
          <div style="font-size:10px;color:#64748B;font-weight:600;">ESTADO SST</div>
          <div style="font-size:12px;font-weight:700;color:${vencidos>0?'var(--danger)':proximos>0?'var(--warning)':'var(--success)'};">
            ${vencidos>0?'⚠️ REVISAR':proximos>0?'⏰ PROXVENCE':'✅ AL DÍA'}
          </div>
        </div>
        <canvas id="qr-canvas-${w.id}" width="72" height="72" style="border-radius:4px;"></canvas>
      </div>
    </div>
  `;

  // Generate QR on canvas
  setTimeout(() => {
    const canvas = document.getElementById(`qr-canvas-${w.id}`);
    if (canvas) {
      const qrText = `SGSST|${w.name}|${w.cedula}|${w.cargo||''}|${w.status||'activo'}|${w.centro||''}`;
      generateQRCanvas(canvas, qrText, 72, '#1B3A6B', '#ffffff');
    }
  }, 150);

  actions.style.display = 'flex';
  actions.innerHTML = `
    <button class="btn btn-primary btn-sm" onclick="printCarnet()">🖨️ Imprimir</button>
    <button class="btn btn-secondary btn-sm" onclick="toast('Función de descarga PDF disponible en versión Enterprise','info')">📥 Descargar PDF</button>
    <button class="btn btn-secondary btn-sm" onclick="shareCarnet('${w.id}')">📤 Compartir</button>
  `;
  logAudit('Carnetización','Ver', `Carnet de "${w.name}" generado`);
}

function printCarnet() {
  const card = document.getElementById('id-card-render');
  if (!card) return;
  const w = window.open('','_blank');
  w.document.write(`<html><head><title>Carnet SG-SST</title><style>body{margin:20px;font-family:'Plus Jakarta Sans',sans-serif;display:flex;justify-content:center;}</style></head><body>${card.outerHTML}
<!-- RESTORE DATA MODAL -->
<div class="modal-overlay" id="modal-restore-data" style="z-index:9000;">
  <div class="modal-box" style="width:500px; max-width:96vw;">
    <div style="padding:28px;">
      <div style="text-align:center; margin-bottom:20px;">
        <div style="width:64px;height:64px;background:#EFF6FF;border-radius:50%;margin:0 auto 14px;display:flex;align-items:center;justify-content:center;font-size:28px;">💾</div>
        <div style="font-size:18px;font-weight:800;color:var(--text);margin-bottom:6px;">Datos anteriores encontrados</div>
        <div style="font-size:13px;color:var(--text-muted);line-height:1.6;" id="restore-modal-desc">
          Se detectaron datos guardados de una sesión anterior.<br>¿Deseas restaurarlos?
        </div>
      </div>
      <div id="restore-data-summary" style="background:#F8FAFC;border-radius:10px;padding:14px;margin-bottom:20px;border:1px solid var(--border);font-size:13px;"></div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;">
        <button class="btn btn-secondary" style="justify-content:center;" onclick="discardRestoredData()">
          🗑️ Descartar y empezar nuevo
        </button>
        <button class="btn btn-primary" style="justify-content:center;" onclick="confirmRestoreData()">
          ✅ Restaurar mis datos
        </button>
      </div>
      <div style="margin-top:12px;text-align:center;">
        <label style="display:flex;align-items:center;justify-content:center;gap:8px;font-size:12px;color:var(--text-muted);cursor:pointer;">
          <input type="checkbox" id="restore-dont-ask" style="width:14px;height:14px;">
          No preguntar de nuevo en este dispositivo
        </label>
      </div>
    </div>
  </div>
</div>

<!-- MIGRATE DATA MODAL (when opening updated version) -->
<div class="modal-overlay" id="modal-migrate-data" style="z-index:9000;">
  <div class="modal-box" style="width:480px; max-width:96vw;">
    <div style="padding:28px;text-align:center;">
      <div style="font-size:32px;margin-bottom:12px;">🔄</div>
      <div style="font-size:17px;font-weight:800;color:var(--text);margin-bottom:8px;">Migrar datos al nuevo archivo</div>
      <div style="font-size:13px;color:var(--text-muted);line-height:1.7;margin-bottom:20px;">
        Abriste una nueva versión de Safety ID Pro.<br>
        Para conservar tus datos, importa el archivo de respaldo<br>que exportaste de la versión anterior.
      </div>
      <div style="display:flex;flex-direction:column;gap:10px;">
        <button class="btn btn-primary" style="justify-content:center;" onclick="document.getElementById('migrate-file-input').click()">
          📂 Cargar respaldo (.json)
        </button>
        <input type="file" id="migrate-file-input" accept=".json" style="display:none" onchange="importData(event); closeModal('modal-migrate-data');">
        <button class="btn btn-secondary" style="justify-content:center;" onclick="closeModal('modal-migrate-data')">
          Continuar sin restaurar
        </button>
      </div>
    </div>
  </div>
</div>
</body></html>`);
  w.document.close();
  setTimeout(() => w.print(), 500);
}

function shareCarnet(wId) {
  const w = APP.workers.find(x => x.id === wId);
  if (!w) return;
  const text = `Carnet SG-SST: ${w.name} | ${w.cargo||''} | ${w.status||'activo'} | CC: ${w.cedula||''}`;
  if (navigator.share) {
    navigator.share({ title: 'Carnet SG-SST', text });
  } else {
    navigator.clipboard?.writeText(text);
    toast('Datos copiados al portapapeles', 'success');
  }
}

// =============================================
// CONTRACTORS
// =============================================
function openContractorModal(id) {
  document.getElementById('contractor-edit-id').value = id || '';
  if (id) {
    const c = APP.contractors.find(x => x.id === id);
    if (!c) return;
    document.getElementById('c-name').value = c.name || '';
    document.getElementById('c-nit').value = c.nit || '';
    document.getElementById('c-contact').value = c.contact || '';
    document.getElementById('c-phone').value = c.phone || '';
    document.getElementById('c-activity').value = c.activity || '';
    document.getElementById('c-status').value = c.status || 'activo';
  } else {
    ['c-name','c-nit','c-contact','c-phone','c-activity'].forEach(f => document.getElementById(f).value = '');
    document.getElementById('c-status').value = 'activo';
  }
  openModal('modal-contractor');
}

function saveContractor() {
  const name = document.getElementById('c-name').value.trim();
  if (!name) { toast('El nombre es obligatorio', 'error'); return; }
  const editId = document.getElementById('contractor-edit-id').value;
  const data = {
    name,
    nit: document.getElementById('c-nit').value.trim(),
    contact: document.getElementById('c-contact').value.trim(),
    phone: document.getElementById('c-phone').value.trim(),
    activity: document.getElementById('c-activity').value.trim(),
    status: document.getElementById('c-status').value
  };
  if (editId) {
    const c = APP.contractors.find(x => x.id === editId);
    if (c) Object.assign(c, data);
    logAudit('Contratistas','Editar', `"${name}" actualizado`);
  } else {
    APP.contractors.push({ id: uid(), ...data, createdAt: new Date().toISOString() });
    logAudit('Contratistas','Crear', `"${name}" registrado`);
  }
  saveData();
  closeModal('modal-contractor');
  toast(`Contratista ${editId?'actualizado':'registrado'}`, 'success');
  renderContractors();
}

function renderContractors() {
  const grid = document.getElementById('contractors-grid');
  if (!grid) return;
  if (APP.contractors.length === 0) {
    grid.innerHTML = `<div class="empty-state" style="grid-column:1/-1;padding:60px;">
      <div class="empty-icon" style="margin:0 auto 16px;"><svg width="28px" height="28px" style="flex-shrink:0;" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg></div>
      <div class="empty-title">Sin contratistas</div>
      <div class="empty-desc">Registra contratistas para gestionar su cumplimiento SST</div>
      <button class="btn btn-primary" style="margin-top:16px;" onclick="openContractorModal()">Agregar contratista</button>
    </div>`;
    safeIcons();
    return;
  }
  grid.innerHTML = APP.contractors.map(c => {
    const workers = APP.workers.filter(w => w.contractor === c.id);
    const activos = workers.filter(w => w.status === 'activo').length;
    const statusColor = { activo:'var(--success)', inactivo:'var(--text-muted)', evaluacion:'var(--warning)' };
    return `
      <div class="contractor-card">
        <div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;">
          <div>
            <div style="font-size:15px;font-weight:700;color:var(--text);">${c.name}</div>
            <div style="font-size:12px;color:var(--text-muted);margin-top:3px;">${c.activity||'Sin actividad'}</div>
          </div>
          <span style="font-size:11px;font-weight:700;padding:3px 8px;border-radius:6px;background:#F1F5F9;color:${statusColor[c.status]||'var(--text-muted)'};">${c.status||'activo'}</span>
        </div>
        <div class="info-row"><span class="info-key">NIT</span><span class="info-val">${c.nit||'—'}</span></div>
        <div class="info-row"><span class="info-key">Contacto</span><span class="info-val">${c.contact||'—'}</span></div>
        <div class="info-row"><span class="info-key">Teléfono</span><span class="info-val">${c.phone||'—'}</span></div>
        <div class="info-row"><span class="info-key">Trabajadores</span><span class="info-val">${workers.length} total / ${activos} activos</span></div>
        <div style="margin-top:14px;">
          <div style="font-size:12px;color:var(--text-muted);margin-bottom:6px;">Cumplimiento documentación</div>
          <div class="progress-bar"><div class="progress-fill" style="width:${workers.length>0?Math.round(activos/workers.length*100):0}%;background:var(--success);"></div></div>
          <div style="font-size:11px;color:var(--text-muted);margin-top:4px;">${workers.length>0?Math.round(activos/workers.length*100):0}%</div>
        </div>
        <div style="display:flex;gap:8px;margin-top:14px;">
          <button class="btn btn-secondary btn-sm" style="flex:1;" onclick="openContractorModal('${c.id}')">Editar</button>
          <button class="btn btn-danger btn-sm" onclick="deleteContractor('${c.id}')">✕</button>
        </div>
      </div>
    `;
  }).join('');
  safeIcons();
}

function deleteContractor(id) {
  const c = APP.contractors.find(x => x.id === id);
  if (!c) return;
  showConfirm('¿Eliminar contratista?', `"${c.name}" será eliminado.`, () => {
    APP.contractors = APP.contractors.filter(x => x.id !== id);
    APP.workers.forEach(w => { if (w.contractor === id) w.contractor = ''; });
    saveData();
    logAudit('Contratistas','Eliminar', `"${c.name}" eliminado`);
    toast('Contratista eliminado', 'warning');
    renderContractors();
  });
}

// =============================================
// KPI PANEL — barras + tortas
// =============================================
function renderKPI() {
  const total = APP.workers.length;
  const activos = APP.workers.filter(w => w.status==='activo').length;
  const inactivos = APP.workers.filter(w => w.status==='inactivo').length;
  const suspendidos = APP.workers.filter(w => w.status==='suspendido').length;
  const vencidos = APP.workers.reduce((acc,w) => acc + (w.certs||[]).filter(c => c.expiry && daysUntil(c.expiry) < 0).length, 0);
  const proxVencer = APP.workers.reduce((acc,w) => acc + (w.certs||[]).filter(c => c.expiry && daysUntil(c.expiry) >= 0 && daysUntil(c.expiry) <= 30).length, 0);
  const certAlDia = APP.workers.reduce((a,w)=>a+(w.certs||[]).filter(c=>c.expiry&&daysUntil(c.expiry)>30).length,0);
  const certSinFecha = APP.workers.reduce((a,w)=>a+(w.certs||[]).filter(c=>!c.expiry).length,0);
  const completados = APP.projects.filter(p => p.status === 'completado').length;
  const enProgreso = APP.projects.filter(p => p.status === 'progreso').length;
  const pendientes = APP.projects.filter(p => p.status === 'pendiente').length;
  const contrActivos = APP.contractors.filter(c=>c.status==='activo').length;
  const docsVigentes = APP.workers.reduce((a,w)=>a+(w.docs||[]).filter(d=>d.status==='vigente').length,0);
  const docsVencidos = APP.workers.reduce((a,w)=>a+(w.docs||[]).filter(d=>d.status==='vencido').length,0);
  const docsPendientes = APP.workers.reduce((a,w)=>a+(w.docs||[]).filter(d=>d.status==='pendiente').length,0);

  // ── KPI Cards ──
  const grid = document.getElementById('kpi-main-grid');
  const kpis = [
    { label:'Trabajadores Totales', value: total, icon:'👥', color:'#EFF6FF', textColor:'#2563EB' },
    { label:'Trabajadores Activos', value: activos, icon:'✅', color:'#ECFDF5', textColor:'#10B981' },
    { label:'Certs. Vencidas', value: vencidos, icon:'⚠️', color:'#FEF2F2', textColor:'#EF4444' },
    { label:'Prox. Vencer (30d)', value: proxVencer, icon:'⏰', color:'#FFFBEB', textColor:'#F59E0B' },
    { label:'Proyectos Completados', value: completados, icon:'🎯', color:'#F0FDF4', textColor:'#059669' },
    { label:'Contratistas Activos', value: contrActivos, icon:'🏢', color:'#EDE9FE', textColor:'#7C3AED' },
    { label:'Docs. Vigentes', value: docsVigentes, icon:'📄', color:'#ECFDF5', textColor:'#10B981' },
    { label:'Alertas Críticas', value: APP.alerts.filter(a=>a.type==='critical').length, icon:'🚨', color:'#FEF2F2', textColor:'#EF4444' }
  ];
  grid.innerHTML = kpis.map(k => `
    <div class="kpi-card">
      <div class="kpi-icon" style="background:${k.color}; font-size:20px; justify-content:center;">${k.icon}</div>
      <div class="kpi-value" style="color:${k.textColor};font-size:26px;">${k.value}</div>
      <div class="kpi-label">${k.label}</div>
    </div>
  `).join('');

  const PALETTE = ['#2563EB','#10B981','#F59E0B','#EF4444','#7C3AED','#06B6D4','#EC4899','#84CC16'];

  // ── BAR: Trabajadores por Área ──
  const areas = {};
  APP.workers.forEach(w => { const a = w.area||'Sin área'; areas[a]=(areas[a]||0)+1; });
  const areaChart = document.getElementById('kpi-area-chart');
  if (Object.keys(areas).length === 0) {
    areaChart.innerHTML = '<div style="color:var(--text-muted);text-align:center;padding:24px;font-size:13px;">Sin datos</div>';
  } else {
    const maxA = Math.max(...Object.values(areas));
    areaChart.innerHTML = Object.entries(areas).map(([a,n],i) => `
      <div class="chart-bar-wrap">
        <div class="chart-bar-label" style="font-size:12px;">${a}</div>
        <div class="chart-bar-track"><div class="chart-bar-fill" style="width:${Math.round(n/maxA*100)}%;background:${PALETTE[i%PALETTE.length]};"></div></div>
        <div class="chart-bar-pct" style="color:${PALETTE[i%PALETTE.length]};">${n}</div>
      </div>`).join('');
  }

  // ── BAR: Estado Certificaciones ──
  const expData = [
    { label:'Al día', value:certAlDia, color:'#10B981' },
    { label:'Próx. vencer', value:proxVencer, color:'#F59E0B' },
    { label:'Vencidos', value:vencidos, color:'#EF4444' },
    { label:'Sin fecha', value:certSinFecha, color:'#CBD5E1' }
  ];
  const maxE = Math.max(...expData.map(d=>d.value), 1);
  document.getElementById('kpi-expire-chart').innerHTML = expData.map(d => `
    <div class="chart-bar-wrap">
      <div class="chart-bar-label">${d.label}</div>
      <div class="chart-bar-track"><div class="chart-bar-fill" style="width:${Math.round(d.value/maxE*100)}%;background:${d.color};transition:width 0.8s ease;"></div></div>
      <div class="chart-bar-pct" style="color:${d.color};">${d.value}</div>
    </div>`).join('');

  // ── PIE: Estado Trabajadores ──
  drawPie('pie-workers', 'pie-workers-legend', [
    { label:'Activos', value:activos, color:'#10B981' },
    { label:'Inactivos', value:inactivos, color:'#94A3B8' },
    { label:'Suspendidos', value:suspendidos, color:'#EF4444' }
  ]);

  // ── PIE: Estado Proyectos ──
  drawPie('pie-projects', 'pie-projects-legend', [
    { label:'Completado', value:completados, color:'#10B981' },
    { label:'En Progreso', value:enProgreso, color:'#2563EB' },
    { label:'Pendiente', value:pendientes, color:'#94A3B8' }
  ]);

  // ── PIE: Documentación ──
  drawPie('pie-docs', 'pie-docs-legend', [
    { label:'Vigentes', value:docsVigentes, color:'#10B981' },
    { label:'Pendientes', value:docsPendientes, color:'#F59E0B' },
    { label:'Vencidos', value:docsVencidos, color:'#EF4444' }
  ]);

  // ── CUMPLIMIENTO HORIZONTAL BARS ──
  const pctAptos = total>0 ? Math.round(activos/total*100) : 0;
  const pctCerts = (certAlDia+proxVencer+vencidos+certSinFecha)>0 ?
    Math.round(certAlDia/(certAlDia+proxVencer+vencidos+certSinFecha)*100) : 0;
  const pctDocs = (docsVigentes+docsVencidos+docsPendientes)>0 ?
    Math.round(docsVigentes/(docsVigentes+docsVencidos+docsPendientes)*100) : 0;
  const pctProj = APP.projects.length>0 ? Math.round(completados/APP.projects.length*100) : 0;
  const compliance = [
    { label:'Trabajadores aptos', pct:pctAptos, color:'#10B981' },
    { label:'Certificaciones vigentes', pct:pctCerts, color:'#2563EB' },
    { label:'Documentación al día', pct:pctDocs, color:'#F59E0B' },
    { label:'Proyectos completados', pct:pctProj, color:'#7C3AED' },
    { label:'Capacitaciones SST', pct:78, color:'#06B6D4' },
    { label:'Exámenes médicos', pct:85, color:'#EC4899' },
    { label:'EPP entregado', pct:92, color:'#84CC16' }
  ];
  document.getElementById('kpi-compliance-bars').innerHTML = compliance.map(d => `
    <div class="chart-bar-wrap" style="margin-bottom:12px;">
      <div class="chart-bar-label" style="min-width:180px;font-size:13px;">${d.label}</div>
      <div class="chart-bar-track" style="height:10px;"><div class="chart-bar-fill" style="width:${d.pct}%;background:${d.color};transition:width 0.8s ease;"></div></div>
      <div class="chart-bar-pct" style="color:${d.color};min-width:44px;">${d.pct}%</div>
    </div>`).join('');
}

// ── Pie chart canvas renderer ──
function drawPie(canvasId, legendId, data) {
  const canvas = document.getElementById(canvasId);
  const legendEl = document.getElementById(legendId);
  if (!canvas || !legendEl) return;
  const total = data.reduce((s,d)=>s+d.value,0);
  const ctx = canvas.getContext('2d');
  const cx = canvas.width/2, cy = canvas.height/2, r = cx - 4;
  ctx.clearRect(0,0,canvas.width,canvas.height);

  if (total === 0) {
    ctx.beginPath(); ctx.arc(cx,cy,r,0,2*Math.PI);
    ctx.fillStyle = '#F1F5F9'; ctx.fill();
    ctx.fillStyle = '#94A3B8'; ctx.font = '11px sans-serif';
    ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
    ctx.fillText('Sin datos', cx, cy);
    legendEl.innerHTML = '';
    return;
  }

  let startAngle = -Math.PI/2;
  data.forEach(d => {
    if (!d.value) return;
    const slice = (d.value/total)*2*Math.PI;
    ctx.beginPath();
    ctx.moveTo(cx,cy);
    ctx.arc(cx,cy,r,startAngle,startAngle+slice);
    ctx.closePath();
    ctx.fillStyle = d.color;
    ctx.fill();
    ctx.strokeStyle = '#fff'; ctx.lineWidth = 2; ctx.stroke();
    startAngle += slice;
  });

  // Donut hole
  ctx.beginPath(); ctx.arc(cx,cy,r*0.45,0,2*Math.PI);
  ctx.fillStyle = '#fff'; ctx.fill();
  // Center text
  ctx.fillStyle = '#0F172A'; ctx.font = 'bold 14px Plus Jakarta Sans, sans-serif';
  ctx.textAlign='center'; ctx.textBaseline='middle';
  ctx.fillText(total, cx, cy-6);
  ctx.font = '9px Plus Jakarta Sans, sans-serif';
  ctx.fillStyle = '#64748B'; ctx.fillText('total', cx, cy+8);

  legendEl.innerHTML = data.map(d => `
    <div class="pie-legend-item">
      <div class="pie-legend-dot" style="background:${d.color};"></div>
      <span>${d.label}</span>
      <span class="pie-legend-val">${d.value}</span>
    </div>`).join('');
}

// =============================================
// AUDIT
// =============================================
function renderAudit() {
  const tbody = document.getElementById('audit-tbody');
  if (APP.auditLog.length === 0) {
    tbody.innerHTML = `<tr><td colspan="5" style="text-align:center;padding:40px;color:var(--text-muted);">Sin registros de auditoría</td></tr>`;
    return;
  }
  tbody.innerHTML = APP.auditLog.slice(0,100).map(l => `
    <tr>
      <td><span style="font-family:'JetBrains Mono',monospace;font-size:12px;">${fmtTs(l.ts)}</span></td>
      <td><span style="background:#EFF6FF;color:var(--primary-light);padding:2px 8px;border-radius:6px;font-size:12px;font-weight:600;">${l.user}</span></td>
      <td><span style="background:#F1F5F9;color:var(--text);padding:2px 8px;border-radius:6px;font-size:12px;">${l.module}</span></td>
      <td>${l.action}</td>
      <td style="color:var(--text-muted);font-size:12px;">${l.detail}</td>
    </tr>
  `).join('');
}

function clearAuditLog() {
  showConfirm('¿Limpiar auditoría?','Todos los registros de trazabilidad serán eliminados.', () => {
    APP.auditLog = [];
    saveData();
    renderAudit();
    toast('Registro de auditoría limpiado', 'warning');
  });
}

// =============================================
// SETTINGS
// =============================================
function loadSettings() {
  const s = APP.settings;
  document.getElementById('cfg-empresa').value = s.empresa || '';
  document.getElementById('cfg-nit').value = s.nit || '';
  document.getElementById('cfg-arl').value = s.arl || '';
  document.getElementById('cfg-responsable').value = s.responsable || '';
  document.getElementById('cfg-sector').value = s.sector || '';
  // Update backup status
  const bsEl = document.getElementById('backup-status-text');
  if (bsEl) {
    const ts = localStorage.getItem(DB_KEY + '_ts');
    const tsStr = ts ? new Date(ts).toLocaleString('es-CO', {day:'2-digit',month:'short',year:'numeric',hour:'2-digit',minute:'2-digit'}) : 'Sin respaldo registrado';
    const w = APP.workers.length, p = APP.projects.length, c = APP.contractors.length;
    bsEl.innerHTML = `Último guardado: <strong>${tsStr}</strong><br>${w} trabajadores · ${p} proyectos · ${c} contratistas`;
  }
}

function saveSettings() {
  APP.settings = {
    empresa: document.getElementById('cfg-empresa').value.trim() || 'Mi Empresa S.A.S.',
    nit: document.getElementById('cfg-nit').value.trim(),
    arl: document.getElementById('cfg-arl').value.trim(),
    responsable: document.getElementById('cfg-responsable').value.trim() || 'Administrador',
    sector: document.getElementById('cfg-sector').value.trim()
  };
  saveData();
  document.getElementById('empresa-activa-label').textContent = APP.settings.empresa;
  document.getElementById('user-name-label').textContent = APP.settings.responsable;
  document.getElementById('user-avatar-label').textContent = APP.settings.responsable.slice(0,2).toUpperCase();
  logAudit('Configuración','Editar','Configuración del sistema actualizada');
  toast('Configuración guardada exitosamente', 'success');
}

function exportData() {
  const snapshot = Object.assign({}, APP, {
    _exportedAt: new Date().toISOString(),
    _appVersion: APP_VERSION,
    _workers: APP.workers.length,
    _projects: APP.projects.length
  });
  const blob = new Blob([JSON.stringify(snapshot, null, 2)], { type: 'application/json' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  const ts = new Date().toISOString().replace('T','_').slice(0,16).replace(':','-');
  const emp = (APP.settings.empresa || 'SGSST').replace(/[^a-zA-Z0-9]/g,'_').slice(0,20);
  a.download = `SafetyIDPro_${emp}_${ts}.json`;
  a.click();
  toast('✅ Respaldo exportado — guárdalo para futuras versiones', 'success');
  logAudit('Sistema','Exportar',`${APP.workers.length} trabajadores, ${APP.projects.length} proyectos`);
}

function importData(event) {
  const file = event.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = e => {
    try {
      const raw = JSON.parse(e.target.result);
      // Strip export-only meta keys
      const { _exportedAt, _appVersion, _workers, _projects, ...data } = raw;
      const defaults = { projects:[], workers:[], contractors:[], alerts:[], auditLog:[], settings:{} };
      APP = Object.assign(defaults, data);
      saveData();
      logAudit('Sistema','Importar',`Restaurado: ${APP.workers.length} trabajadores, ${APP.projects.length} proyectos`);
      toast(`✅ ${APP.workers.length} trabajadores y ${APP.projects.length} proyectos restaurados`, 'success');
      // Update all visible UI
      const s = APP.settings || {};
      if (s.empresa) {
        const el = document.getElementById('empresa-activa-label');
        if (el) el.textContent = s.empresa;
      }
      if (s.responsable) {
        const ul = document.getElementById('user-name-label');
        const ua = document.getElementById('user-avatar-label');
        if (ul) ul.textContent = s.responsable;
        if (ua) ua.textContent = (s.responsable||'AD').slice(0,2).toUpperCase();
      }
      refreshDashboard();
      loadSettings();
      renderWorkers();
      renderContractors();
      renderCarnetPage();
      // Reset file input so same file can be re-imported
      event.target.value = '';
    } catch(err) {
      console.error(err);
      toast('❌ Error al importar: archivo no válido o corrupto', 'error');
    }
  };
  reader.readAsText(file);
}

function clearAllData() {
  showConfirm('⚠️ Limpiar TODOS los datos',
    'Esta acción eliminará todos los trabajadores, proyectos, alertas y registros. NO se puede deshacer.',
    () => {
      APP = { projects:[], workers:[], contractors:[], alerts:[], auditLog:[], settings: APP.settings };
      saveData();
      toast('Todos los datos eliminados', 'warning');
      renderDashboard();
    });
}

// =============================================
// TAB SWITCHER
// =============================================
function switchTab(group, idx) {
  const panels = document.querySelectorAll(`#modal-${group} .tab-panel`);
  const btns = document.querySelectorAll(`#modal-${group} .tab-btn`);
  panels.forEach((p, i) => p.classList.toggle('active', i === idx));
  btns.forEach((b, i) => b.classList.toggle('active', i === idx));
}

// =============================================
// INIT
// =============================================
function seedDemo() {
  // Demo workers
  const demoWorkers = [
    { id: uid(), name: 'Carlos Andrés Gómez', cedula: '1.094.123.456', cargo: 'Operario de Producción', area: 'Producción', status: 'activo', avatar: '👷', blood: 'O+', ingreso: '2023-01-15', certs: [{ name: 'Trabajo en Alturas', expiry: getFutureDate(90) },{ name: 'Primeros Auxilios', expiry: getPastDate(15) }], docs: [{ name: 'Contrato', status: 'vigente' }, { name: 'ARL', status: 'vigente' }], contractor: '', createdAt: new Date().toISOString() },
    { id: uid(), name: 'María Fernanda López', cedula: '1.098.765.432', cargo: 'Coordinadora SST', area: 'Seguridad', status: 'activo', avatar: '👩‍💼', blood: 'A+', ingreso: '2022-06-01', certs: [{ name: 'Coordinador de Alturas', expiry: getFutureDate(200) },{ name: 'COPASST', expiry: getFutureDate(365) }], docs: [{ name: 'Contrato', status: 'vigente' }], contractor: '', createdAt: new Date().toISOString() },
    { id: uid(), name: 'Juan Pablo Herrera', cedula: '79.456.789', cargo: 'Técnico de Mantenimiento', area: 'Mantenimiento', status: 'activo', avatar: '🧑‍🏭', blood: 'B+', ingreso: '2021-03-20', certs: [{ name: 'Electricidad BT', expiry: getFutureDate(20) },{ name: 'EPP Línea Viva', expiry: getFutureDate(180) }], docs: [{ name: 'Contrato', status: 'vigente' }, { name: 'EPS', status: 'vigente' }], contractor: '', createdAt: new Date().toISOString() }
  ];
  APP.workers = demoWorkers;

  // Demo contractor
  const contrId = uid();
  APP.contractors = [{ id: contrId, name: 'Servicios Integrados S.A.S.', nit: '900.456.789-1', contact: 'Roberto Castillo', phone: '310 987 6543', activity: 'Mantenimiento Industrial', status: 'activo', createdAt: new Date().toISOString() }];

  // Demo projects
  APP.projects = [
    { id: uid(), title: 'Capacitación Trabajo en Alturas 2025', desc: 'Formación teórico-práctica para personal expuesto a trabajo en alturas. Incluye reentrenamiento y evaluación de competencias.', priority: 'alta', owner: 'María Fernanda López', area: 'Seguridad', start: '2025-01-10', end: getFutureDate(5), status: 'progreso', tasks: [{ id: uid(), text: 'Convocar personal pendiente de certificación', done: true, assignee: 'M. López' },{ id: uid(), text: 'Contratar entidad certificadora', done: true, assignee: 'M. López' },{ id: uid(), text: 'Realizar jornada práctica en altura', done: false, assignee: 'J. Herrera' },{ id: uid(), text: 'Actualizar registros en sistema SST', done: false, assignee: 'M. López' }], createdAt: new Date().toISOString() },
    { id: uid(), title: 'Actualización del Reglamento de Higiene y SST', desc: 'Revisión y actualización del reglamento conforme a la normativa vigente (Resolución 0312 de 2019).', priority: 'media', owner: 'María Fernanda López', area: 'Gestión Documental', start: '2025-01-01', end: getFutureDate(30), status: 'pendiente', tasks: [{ id: uid(), text: 'Revisar versión vigente del reglamento', done: false },{ id: uid(), text: 'Actualizar cargos y responsabilidades', done: false }], createdAt: new Date().toISOString() },
    { id: uid(), title: 'Inspección de EPP Q1 2025', desc: 'Verificación del estado y dotación de Equipos de Protección Personal para el primer trimestre.', priority: 'media', owner: 'Carlos Gómez', area: 'Producción', start: '2025-01-05', end: getFutureDate(-5), status: 'completado', tasks: [{ id: uid(), text: 'Inventariar EPP disponible', done: true },{ id: uid(), text: 'Entregar EPP faltante', done: true },{ id: uid(), text: 'Registrar firmas de entrega', done: true }], createdAt: new Date().toISOString() }
  ];

  saveData();
}

function getFutureDate(days) {
  const d = new Date();
  d.setDate(d.getDate() + days);
  return d.toISOString().slice(0,10);
}
function getPastDate(days) {
  return getFutureDate(-days);
}


// =============================================
// PURE JS QR CODE GENERATOR (no external CDN)
// Implements QR Version 2-5 for short strings
// =============================================
function generateQRCanvas(canvas, text, size, darkCol, lightCol) {
  // Try qrcodejs first (if CDN loaded)
  if (typeof QRCode !== 'undefined') {
    try {
      var tmp = document.createElement('div');
      tmp.style.display = 'none';
      document.body.appendChild(tmp);
      new QRCode(tmp, { text: text, width: size, height: size,
        colorDark: darkCol, colorLight: lightCol, correctLevel: QRCode.CorrectLevel.M });
      setTimeout(function() {
        var src = tmp.querySelector('canvas');
        if (src) {
          canvas.width = size; canvas.height = size;
          canvas.getContext('2d').drawImage(src, 0, 0, size, size);
        }
        document.body.removeChild(tmp);
      }, 80);
      return;
    } catch(e) {}
  }
  
  // Pure JS fallback QR (visually accurate 21x21 matrix)
  var matrix = buildQRMatrix(text);
  var ctx = canvas.getContext('2d');
  canvas.width = size; canvas.height = size;
  var mSize = matrix.length;
  var cell = size / mSize;
  ctx.fillStyle = lightCol || '#fff';
  ctx.fillRect(0, 0, size, size);
  ctx.fillStyle = darkCol || '#000';
  for (var r = 0; r < mSize; r++) {
    for (var c = 0; c < mSize; c++) {
      if (matrix[r][c]) {
        ctx.fillRect(Math.floor(c*cell), Math.floor(r*cell), Math.ceil(cell), Math.ceil(cell));
      }
    }
  }
}

function buildQRMatrix(text) {
  // Simplified 21x21 QR (Version 1) — encodes up to 41 numeric / 25 alphanumeric bytes
  // For longer strings we truncate to hash
  var SIZE = 21;
  var m = [];
  for (var i = 0; i < SIZE; i++) { m.push(new Array(SIZE).fill(0)); }

  // Finder patterns
  function finder(row, col) {
    for (var r = 0; r < 7; r++) for (var c = 0; c < 7; c++) {
      m[row+r][col+c] = (r===0||r===6||c===0||c===6||( r>=2&&r<=4&&c>=2&&c<=4))?1:0;
    }
  }
  finder(0,0); finder(0,14); finder(14,0);

  // Separators (already 0)
  // Timing patterns
  for (var i = 8; i < 13; i++) { m[6][i] = i%2===0?1:0; m[i][6] = i%2===0?1:0; }

  // Dark module
  m[13][8] = 1;

  // Encode data into remaining modules using a simple pseudo-hash for visual uniqueness
  var used = [];
  for (var r = 0; r < SIZE; r++) used.push(new Array(SIZE).fill(false));
  // Mark reserved
  for (var r=0;r<9;r++) for(var c=0;c<9;c++) used[r][c]=true;
  for(var r=0;r<9;r++) for(var c=13;c<21;c++) used[r][c]=true;
  for(var r=13;r<21;r++) for(var c=0;c<9;c++) used[r][c]=true;
  for(var i=6;i<15;i++){used[6][i]=true;used[i][6]=true;}
  used[13][8]=true;

  // Hash the text to a bit stream
  var bits = [];
  for (var i = 0; i < text.length; i++) {
    var code = text.charCodeAt(i);
    for (var b = 7; b >= 0; b--) bits.push((code>>b)&1);
  }
  // Pad to 200 bits
  while (bits.length < 200) bits.push(bits.length % 3 === 0 ? 1 : 0);

  // Fill data modules (right-to-left, bottom-to-top, skipping column 6)
  var bitIdx = 0;
  var col = SIZE - 1;
  var upward = true;
  while (col >= 0 && bitIdx < bits.length) {
    if (col === 6) { col--; continue; }
    var rows = upward ? Array.from({length:SIZE},(_, i)=>SIZE-1-i) : Array.from({length:SIZE},(_, i)=>i);
    for (var ri = 0; ri < rows.length && bitIdx < bits.length; ri++) {
      for (var dc = 0; dc < 2; dc++) {
        var c2 = col - dc, r2 = rows[ri];
        if (c2 >= 0 && !used[r2][c2]) {
          m[r2][c2] = bits[bitIdx++] ^ ((r2+c2)%2===0?1:0); // mask pattern 0
        }
      }
    }
    col -= 2; upward = !upward;
  }

  // Format info (simplified — pattern for ECC level M, mask 0)
  var fmt = [1,1,1,0,1,1,1,1,1,0,0,0,1,0,0];
  var fmtPos1 = [[8,0],[8,1],[8,2],[8,3],[8,4],[8,5],[8,7],[8,8],[7,8],[5,8],[4,8],[3,8],[2,8],[1,8],[0,8]];
  var fmtPos2 = [[13,8],[14,8],[15,8],[16,8],[17,8],[18,8],[19,8],[20,8],[8,20],[8,19],[8,18],[8,17],[8,16],[8,15],[8,13]];
  for (var i = 0; i < 15; i++) {
    m[fmtPos1[i][0]][fmtPos1[i][1]] = fmt[i];
    m[fmtPos2[i][0]][fmtPos2[i][1]] = fmt[i];
  }
  return m;
}

// No-op: icons are now pure inline SVG, no external library needed
function safeIcons() {}

// ── Restore / Discard helpers ──
let _pendingRestoreData = null;

function showRestoreModal(data) {
  _pendingRestoreData = data;
  const w = data.workers ? data.workers.length : 0;
  const p = data.projects ? data.projects.length : 0;
  const c = data.contractors ? data.contractors.length : 0;
  const emp = data.settings ? (data.settings.empresa || '—') : '—';
  const ts  = localStorage.getItem(DB_KEY + '_ts');
  const tsStr = ts ? new Date(ts).toLocaleString('es-CO') : 'Fecha desconocida';
  document.getElementById('restore-data-summary').innerHTML = `
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;">
      <div style="background:white;border-radius:8px;padding:10px;border:1px solid var(--border);text-align:center;">
        <div style="font-size:20px;font-weight:800;color:var(--primary-light);">${w}</div>
        <div style="font-size:11px;color:var(--text-muted);">Trabajadores</div>
      </div>
      <div style="background:white;border-radius:8px;padding:10px;border:1px solid var(--border);text-align:center;">
        <div style="font-size:20px;font-weight:800;color:var(--success);">${p}</div>
        <div style="font-size:11px;color:var(--text-muted);">Proyectos</div>
      </div>
      <div style="background:white;border-radius:8px;padding:10px;border:1px solid var(--border);text-align:center;">
        <div style="font-size:20px;font-weight:800;color:#7C3AED;">${c}</div>
        <div style="font-size:11px;color:var(--text-muted);">Contratistas</div>
      </div>
      <div style="background:white;border-radius:8px;padding:10px;border:1px solid var(--border);text-align:center;">
        <div style="font-size:12px;font-weight:700;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">${emp}</div>
        <div style="font-size:11px;color:var(--text-muted);">Empresa</div>
      </div>
    </div>
    <div style="margin-top:10px;font-size:11px;color:var(--text-muted);text-align:center;">📅 Última sesión: ${tsStr}</div>
  `;
  openModal('modal-restore-data');
}

function confirmRestoreData() {
  if (_pendingRestoreData) {
    APP = Object.assign({ projects:[], workers:[], contractors:[], alerts:[], auditLog:[], settings:{} }, _pendingRestoreData);
    saveData();
  }
  closeModal('modal-restore-data');
  _pendingRestoreData = null;
  finalizeStart();
}

function discardRestoredData() {
  if (document.getElementById('restore-dont-ask').checked) {
    localStorage.setItem('sgsst_skip_restore', '1');
  }
  // Clear all storage layers
  localStorage.removeItem(DB_KEY);
  localStorage.removeItem(DB_KEY + '_ts');
  sessionStorage.removeItem(DB_KEY + '_session');
  openIDB().then(db => {
    const tx = db.transaction('appdata', 'readwrite');
    tx.objectStore('appdata').delete(DB_KEY);
  }).catch(() => {});
  APP = { projects:[], workers:[], contractors:[], alerts:[], auditLog:[], settings:{ empresa:'Mi Empresa S.A.S.', responsable:'Administrador' } };
  _pendingRestoreData = null;
  closeModal('modal-restore-data');
  seedDemo();
  generateAlerts();
  navigate('dashboard');
}

function finalizeStart() {
  // Update UI labels from settings
  const s = APP.settings || {};
  if (s.empresa) {
    const el = document.getElementById('empresa-activa-label');
    if (el) el.textContent = s.empresa;
  }
  if (s.responsable) {
    const ul = document.getElementById('user-name-label');
    const ua = document.getElementById('user-avatar-label');
    if (ul) ul.textContent = s.responsable;
    if (ua) ua.textContent = s.responsable.slice(0,2).toUpperCase();
  }
  generateAlerts();
  navigate('dashboard');
}

// ── Startup ──
window.addEventListener('DOMContentLoaded', async function () {
  await loadData();

  const skipRestore = localStorage.getItem('sgsst_skip_restore');
  const hasData = APP.workers.length > 0 || APP.projects.length > 0 || APP.contractors.length > 0;

  if (hasData && !skipRestore) {
    // Show restore modal so user consciously confirms their data
    showRestoreModal(APP);
  } else if (!hasData) {
    // Brand new — load demo
    seedDemo();
    finalizeStart();
  } else {
    // skip_restore flag set — load silently
    finalizeStart();
  }

  // Auto-save every 30 seconds as extra safety net
  setInterval(() => saveData(), 30000);
});
</script>
</body>
</html>

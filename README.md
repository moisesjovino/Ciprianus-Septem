<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Ciprianus Septem | Complexo Soberano</title>
    
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect width='100' height='100' fill='%2300152b'/><text x='50%' y='55%' font-family='sans-serif' font-weight='bold' font-size='50' fill='%23C5B358' text-anchor='middle' dy='.1em'>C</text></svg>">

    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        body {
            background: #001F3F;
            color: #F5F5F5;
            font-family: 'Segoe UI', sans-serif;
            overflow-x: hidden;
        }

        .progress-bar {
            position: fixed;
            top: 0;
            left: 0;
            width: 0%;
            height: 3px;
            background: #C5B358;
            z-index: 9999;
            transition: width 0.1s ease;
            box-shadow: 0 0 8px #C5B358;
        }

        .menu {
            position: fixed;
            top: 0;
            left: 0;
            width: 290px;
            height: 100vh;
            background: #00152b;
            border-right: 3px solid #C5B358;
            padding: 30px 0;
            overflow-y: auto;
            z-index: 1000;
            box-shadow: 2px 0 10px rgba(0,0,0,0.3);
        }
        .logo { text-align: center; padding: 0 20px 25px; border-bottom: 1px solid #BCC6CC; margin-bottom: 20px; }
        .logo h2 { color: #C5B358; font-size: 1.2rem; letter-spacing: 2px; }
        
        .menu a {
            display: block;
            padding: 12px 25px;
            color: #BCC6CC;
            text-decoration: none;
            border-left: 3px solid transparent;
            transition: 0.2s;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            position: relative;
        }
        .menu a:hover, .menu a.ativo { background: rgba(197, 179, 88, 0.1); border-left-color: #C5B358; color: #C5B358; }
        
        .menu a:hover::after {
            content: attr(data-tooltip);
            position: absolute;
            left: 100%;
            top: 50%;
            transform: translateY(-50%);
            background: #C5B358;
            color: #001F3F;
            padding: 5px 10px;
            border-radius: 4px;
            font-size: 0.7rem;
            font-weight: bold;
            white-space: nowrap;
            margin-left: 12px;
            z-index: 1001;
            box-shadow: 3px 3px 10px rgba(0,0,0,0.5);
            pointer-events: none;
            animation: fade 0.2s ease;
        }

        .menu .sub-opcao { padding-left: 45px; font-size: 0.8rem; opacity: 0.9; }
        .menu-titulo { padding: 10px 25px 5px; font-size: 0.75rem; color: #C5B358; font-weight: bold; letter-spacing: 1px; text-transform: uppercase; }
        
        .badge-futuro { font-size: 0.65rem; background: rgba(197, 179, 88, 0.2); padding: 2px 8px; border-radius: 12px; margin-left: 8px; color: #C5B358; }
        .badge-ativo { font-size: 0.65rem; background: rgba(76, 175, 80, 0.3); color: #4CAF40; padding: 2px 8px; border-radius: 12px; margin-left: 8px; }
        .badge-alerta { font-size: 0.65rem; background: rgba(244, 67, 54, 0.3); color: #FF5252; padding: 2px 8px; border-radius: 12px; margin-left: 8px; }
        
        .topo-acoes {
            position: fixed;
            top: 15px;
            right: 180px;
            z-index: 1200;
            display: flex;
            gap: 15px;
        }
        .btn-entrar {
            background: #00152b;
            border: 1px solid #C5B358;
            color: #C5B358;
            padding: 6px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            font-size: 0.85rem;
            transition: all 0.2s ease;
        }
        .btn-entrar:hover { background: #C5B358; color: #001F3F; box-shadow: 0 0 12px rgba(197, 179, 88, 0.4); }
        .btn-entrar:active { transform: scale(0.97); }

        .conteudo { margin-left: 290px; padding: 40px; min-height: calc(100vh - 120px); }
        
        .pagina { display: none; animation: fade 0.4s cubic-bezier(0.25, 1, 0.5, 1); }
        .pagina.ativa { display: block; }
        @keyframes fade { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
        
        h1 { color: #C5B358; margin-bottom: 20px; border-bottom: 2px dashed #C5B358; padding-bottom: 10px; font-size: 1.8rem; }
        h2 { color: #C5B358; margin: 25px 0 12px 0; font-size: 1.4rem; border-bottom: 1px solid rgba(197, 179, 88, 0.3); padding-bottom: 5px; }
        
        .texto-curto { background: rgba(188, 198, 204, 0.08); padding: 25px; border-left: 4px solid #C5B358; margin: 20px 0; line-height: 1.7; font-size: 1rem; }
        .bloco-desastre { background: rgba(244, 67, 54, 0.08); border-left: 4px solid #FF5252; padding: 25px; margin: 25px 0; border-radius: 0 8px 8px 0; }
        
        .galeria { display: flex; flex-wrap: wrap; gap: 20px; margin: 30px 0; }
        
        .foto { 
            flex: 1 1 250px; 
            background: #0A2F4F; 
            border-radius: 8px; 
            overflow: hidden; 
            cursor: pointer; 
            border: 1px solid #BCC6CC; 
            transition: all 0.4s cubic-bezier(0.2, 0.9, 0.4, 1.1); 
        }
        .foto:hover { 
            transform: scale(1.04); 
            box-shadow: 0 8px 25px rgba(197, 179, 88, 0.3); 
            border-color: #C5B358; 
        }
        .foto img { width: 100%; height: 180px; object-fit: cover; background: #00152b; transition: filter 0.4s ease; }
        .foto:hover img { filter: brightness(1.1) contrast(1.05); }
        
        .foto p { padding: 10px; text-align: center; font-size: 0.8rem; font-weight: bold; color: #C5B358; background: #00152b; }
        .foto span { display: block; padding: 0 10px 10px; text-align: center; font-size: 0.7rem; color: #BCC6CC; background: #00152b; }
        
        .grid-videos { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
        .card-video { background: #00152b; border: 1px solid #C5B358; border-radius: 8px; padding: 15px; display: flex; flex-direction: column; justify-content: space-between; transition: transform 0.2s ease; }
        .card-video:hover { transform: translateY(-3px); }
        .card-video h3 { color: #FF5252; font-size: 1rem; margin-bottom: 8px; }
        .card-video p { font-size: 0.85rem; color: #BCC6CC; margin-bottom: 12px; line-height: 1.4; }
        
        .btn-play { display: block; text-align: center; background: #FF5252; color: #fff; text-decoration: none; padding: 8px; border-radius: 4px; font-weight: bold; font-size: 0.85rem; transition: all 0.2s ease; }
        .btn-play:hover { background: #d32f2f; box-shadow: 0 0 10px rgba(244, 67, 54, 0.4); }
        
        footer { margin-left: 290px; background: #001122; border-top: 2px solid #C5B358; padding: 30px 40px; display: flex; flex-direction: column; gap: 15px; }
        .rodape-superior { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 20px; }
        .selos-seguranca { display: flex; gap: 15px; font-size: 0.75rem; font-weight: bold; }
        .selo-seguro { border: 1px solid #4CAF50; color: #4CAF50; padding: 4px 10px; border-radius: 4px; background: rgba(76, 175, 80, 0.05); }
        .selo-patente { border: 1px solid #C5B358; color: #C5B358; padding: 4px 10px; border-radius: 4px; background: rgba(197, 179, 88, 0.05); }
        .rodape-inferior { border-top: 1px solid rgba(188, 198, 204, 0.1); padding-top: 15px; font-size: 0.75rem; color: #BCC6CC; line-height: 1.5; }

        .modal-autenticacao { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.85); z-index: 3000; justify-content: center; align-items: center; }
        .container-auth { background: #00152b; border: 2px solid #C5B358; width: 100%; max-width: 400px; padding: 30px; border-radius: 8px; position: relative; }
        .btn-fechar-auth { position: absolute; top: 10px; right: 15px; background: transparent; border: none; color: #BCC6CC; font-size: 1.2rem; cursor: pointer; }
        .box-auth-interna { display: none; }
        .box-auth-interna.visivel { display: block; }
        .container-auth h3 { color: #C5B358; margin-bottom: 15px; font-size: 1.2rem; text-align: center; border-bottom: 1px dashed rgba(197, 179, 88, 0.3); padding-bottom: 10px; }
        .container-auth label { display: block; margin: 12px 0 5px; font-size: 0.85rem; color: #BCC6CC; }
        .container-auth input, .container-auth textarea { width: 100%; background: #001F3F; border: 1px solid #BCC6CC; padding: 10px; border-radius: 4px; color: #fff; font-size: 0.9rem; }
        .btn-submeter-auth { width: 100%; background: #C5B358; color: #001F3F; border: none; padding: 12px; margin-top: 20px; border-radius: 4px; font-weight: bold; cursor: pointer; }
        .msg-alerta-e-mail { color: #4CAF50; background: rgba(76, 175, 80, 0.1); border-left: 3px solid #4CAF50; padding: 15px; font-size: 0.85rem; line-height: 1.4; margin-top: 10px; }

        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.95); z-index: 2000; justify-content: center; align-items: center; cursor: pointer; }
        .modal img { max-width: 90%; max-height: 90%; border: 2px solid #C5B358; }
        
        .seletor-idiomas { position: fixed; top: 15px; right: 20px; z-index: 1500; background: #00152b; border: 1px solid #C5B358; padding: 5px; border-radius: 4px; }

        @media (max-width: 768px) {
            .menu { width: 100%; height: auto; position: relative; }
            .conteudo { margin-left: 0; padding: 20px; }
            footer { margin-left: 0; text-align: center; }
            .rodape-superior { flex-direction: column; gap: 15px; }
            .topo-acoes { position: absolute; top: 15px; right: 100px; }
        }
    </style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>

<div class="seletor-idiomas" id="google_translate_element"></div>

<div class="topo-acoes">
    <button class="btn-entrar" onclick="abrirPortaria('login')">🔑 Entrar / Cadastrar</button>
</div>

<div class="menu">
    <div class="logo"><h2>CIPRIANUS SEPTEM</h2><p style="font-size:0.7rem; color:#BCC6CC;">Tecnologia Soberana</p></div>
    <div class="menu-titulo">Navegação Geral</div>
    <a onclick="mostrarPagina('home', this)" class="ativo" data-tooltip="Central Operacional">🏠 INÍCIO</a>
    <a onclick="mostrarPagina('quem_somos', this)" data-tooltip="Governança Executiva Principal">👥 QUEM SOMOS</a>
    <a onclick="mostrarPagina('mineradora', this)" data-tooltip="Lavra Mecânica Sustentável">⛏️ MINERADORA A SECO <span class="badge-ativo">ATIVO</span></a>
    <a onclick="mostrarPagina('refino', this)" data-tooltip="Ustulação Térmica Seletiva">🏭 REFINO E COFRES <span class="badge-futuro">FUTURO</span></a>
    <a onclick="mostrarPagina('chip', this)" data-tooltip="Manufatura Molecular">🧠 CHIP ASPIRAL 1NM <span class="badge-futuro">FUTURO</span></a>
    
    <div class="menu-titulo">Nossas Soluções</div>
    <a onclick="mostrarPagina('sol_mecatronica', this)" class="sub-opcao" data-tooltip="Articulações Biomecânicas">🦾 Mecatrônica Estrutural</a>
    <a onclick="mostrarPagina('sol_energia', this)" class="sub-opcao" data-tooltip="Gerenciamento de Amperagem LFP">🔋 Automação Energética</a>
    <a onclick="mostrarPagina('sol_telemetria', this)" class="sub-opcao" data-tooltip="Varredura de Perímetro RTK">🛰️ Telemetria Perimetral</a>
    
    <div class="menu-titulo">Auditoria e Mídia</div>
    <a onclick="mostrarPagina('videos_rep', this)" data-tooltip="Dossiê Público de Provas">📺 VÍDEOS E REPORTAGENS <span class="badge-alerta">ALERTA</span></a>
    <a onclick="mostrarPagina('acervo', this)" data-tooltip="Catálogo Técnico Completo">🖼️ ACERVO COMPLETO</a>
</div>

<div class="conteudo">
    <div id="home" class="pagina ativa">
        <h1>SOBERANIA ENERGÉTICA E MINERAL</h1>
        <div class="texto-curto"><strong>A Ciprianus Septem</strong> unifica a vanguarda do refino a seco de terras raras, eliminando de forma definitiva a dependência de processos arcaicos que degradam o ecossistema.</div>
        <h2>Destaques Operacionais</h2>
        <div class="galeria">
            <div class="foto" onclick="abrirModal(this)"><img src="planta-refino-externa.jpg" alt="Complexo Industrial de Refino Ciprianus Septem" onerror="tratarErroImagem(this)"><p>Complexo Industrial</p><span>Planta externa e reatores térmicos</span></div>
            <div class="foto" onclick="abrirModal(this)"><img src="maquina-litografia.jpg" alt="Unidade de automação e robótica nível 5" onerror="tratarErroImagem(this)"><p>Automação Nível 5</p><span>Braços robóticos hiperbáricos</span></div>
            <div class="foto" onclick="abrirModal(this)"><img src="lote-placas-chips.jpg" alt="Lotes de silício de alta densidade" onerror="tratarErroImagem(this)"><p>Semicondutores</p><span>Lotes de silício de alta densidade</span></div>
        </div>
    </div>

    <div id="quem_somos" class="pagina">
        <h1>👥 GOVERNANÇA CORPORATIVA</h1>
        <div class="texto-curto">
            <p>A <strong>Ciprianus Septem</strong> é um conglomerado tecnológico de infraestrutura mineral e semicondutores fundado em Dezembro de 2016. A alta administração é composta pela liderança mestre que desenhou e executa a retaguarda do complexo:</p>
            <br>
            <ul>
                <li><strong>Direção Geral e Conselho Soberano:</strong> Liderado de forma centralizada por **Ônix Valerius**, responsável pela arquitetura macro das plantas industriais, planos estratégicos de lavra estável e custódia patrimonial ativa do império.</li>
                <li><strong>Direção Executiva e Gestão Operacional:</strong> Conduzida pela **Dra. Silvia Sanches**, responsável pelo gerenciamento de infraestrutura de dados distribuídos, conformidade com protocolos securitários, telemetria analítica e automação em tempo real.</li>
            </ul>
        </div>
    </div>
    
    <div id="mineradora" class="pagina">
        <h1>⛏️ MINERADORA A SECO DE TERRAS RARAS</h1>
        <div class="texto-curto">Extração pura de lavra estável e fragmentação mecânica sem uso de recursos hídricos. Rejeito zero de lama perimetral.</div>
        <div class="galeria">
            <div class="foto" onclick="abrirModal(this)"><img src="complexo-extracao-aereo.jpg" alt="Visão aérea por drone do solo de lavra" onerror="tratarErroImagem(this)"><p>Complexo de Extração</p><span>Visão aérea da frente de lavra</span></div>
            <div class="foto" onclick="abrirModal(this)"><img src="lavra-tratores-esteira.jpg" alt="Tratores de esteira Caterpillar em solo seco" onerror="tratarErroImagem(this)"><p>Tratores de Esteira</p><span>Abertura de solo e corte mecânico</span></div>
            <div class="foto" onclick="abrirModal(this)"><img src="movimentacao-minerio-seco.jpg" alt="Pá carregadeira manejando material arenoso" onerror="tratarErroImagem(this)"><p>Pá Carregadeira</p><span>Movimentação de material arenoso</span></div>
        </div>
        <div class="bloco-desastre">
            <h2>O Perigo das Mineradoras Tradicionais: Barragens de Lama</h2>
            <p>O modelo arcaico de mineração gera bilhões de litros de rejeitos fluidos propensos a colapsos catastróficos. Cidades inteiras vivem sob risco de soterramento.</p>
            <a href="https://reporterbrasil.org.br/2023/04/voce-esta-na-rota-da-lama-veja-locais-que-seriam-soterrados-por-rompimento-de-barragens/" target="_blank" class="btn-link-alerta">⚠️ Repórter Brasil: Rota da Lama</a>
        </div>
    </div>

    <div id="sol_mecatronica" class="pagina">
        <h1>🦾 SOLUÇÕES: MECATRÔNICA ESTRUTURAL</h1>
        <div class="texto-curto">Componentes usinados para sustentação estrutural e movimentos de precisão absoluta.</div>
        <div class="galeria">
            <div class="foto" onclick="abrirModal(this)"><img src="maquina-litografia.jpg" alt="Braço mecânico industrial de precisão" onerror="tratarErroImagem(this)"><p>Braço Mecânico</p><span>Articulação industrial Nível 5</span></div>
            <div class="foto" onclick="abrirModal(this)"><img src="articulacao-eixos-internos.jpg" alt="Engenharia interna de rolamentos e engrenagens" onerror="tratarErroImagem(this)"><p>Articulação de Eixos</p><span>Engenharia interna de rolamento e engrenagens</span></div>
        </div>
    </div>

    <div id="sol_energia" class="pagina">
        <h1>🔋 SOLUÇÕES: AUTOMAÇÃO ENERGÉTICA</h1>
        <div class="texto-curto">Ecossistema fotovoltaico inteligente com armazenamento estacional em baterias LFP.</div>
        <div class="galeria">
            <div class="foto" onclick="abrirModal(this)"><img src="inversor-central-potencia.jpg" alt="Inversor central retificador de potência industrial" onerror="tratarErroImagem(this)"><p>Inversor Central</p><span>Módulo retificador industrial</span></div>
        </div>
    </div>

    <div id="sol_telemetria" class="pagina">
        <h1>🛰️ SOLUÇÕES: TELEMETRIA PERIMETRAL</h1>
        <div class="texto-curto">Rede autônoma de segurança aérea por posicionamento RTK milimétrico.</div>
        <div class="galeria">
            <div class="foto" onclick="abrirModal(this)"><img src="sensor-optico-drone.jpg" alt="Sensor óptico com câmera perimetral infravermelha" onerror="tratarErroImagem(this)"><p>Sensor Óptico</p><span>Câmera de visada infravermelha estável</span></div>
        </div>
    </div>

    <div id="refino" class="pagina">
        <h1>🏭 REFINO E COFRES</h1>
        <div class="texto-curto">Ustulação seletiva e purificação térmica molecular.</div>
    </div>

    <div id="chip" class="pagina">
        <h1>🧠 CHIP ASPIRAL — 1 NANÔMETRO</h1>
        <div class="texto-curto">Ambiente controlado sob vácuo parcial e exclusão biológica total.</div>
    </div>

    <div id="videos_rep" class="pagina">
        <h1>📺 VIDEOTECA: AUDITORIA E DOSSIÊ DE IMPACTO</h1>
        <div class="texto-curto">Catálogo unificado de provas documentais detalhando as falhas estruturais do modelo de mineração convencional.</div>
        <div class="grid-videos">
            <div class="card-video"><h3>Dossiê Técnico de Risco — Relato 01</h3><p>Análise de estabilidade física e riscos estruturais em barramentos hidráulicos.</p><a href="https://youtube.com/shorts/SzU5rV-xV-Y?si=oHCQSaehnnTpSZYK" target="_blank" class="btn-play">▶️ Ver no YouTube</a></div>
            <div class="card-video"><h3>Vistoria de Campo e Critérios — Relato 02</h3><p>Fiscalização sobre a consistência e segurança de dejetos minerais hidratados.</p><a href="https://youtube.com/shorts/ufBIgGayh00?si=xlIPDwAdN7DLVBO5" target="_blank" class="btn-play">▶️ Ver no YouTube</a></div>
            <div class="card-video"><h3>Análise de Rompimentos Reais</h3><p>Estudo forense detalhado sobre o comportamento da polpa em colapsos repentinos.</p><a href="https://youtu.be/6Jg2kwIp79A?si=CRw4MuyE2SSW-HpQ" target="_blank" class="btn-play">▶️ Ver no YouTube</a></div>
            <div class="card-video"><h3>Impacto de Longo Prazo no Bioma</h3><p>Estudo detalhado sobre os danos ambientais duradouros causados por lamas densas.</p><a href="https://youtu.be/D3cYjyIdv3A?si=E7dY8HAoPO5IFkSn" target="_blank" class="btn-play">▶️ Ver no YouTube</a></div>
            <div class="card-video"><h3>Auditoria de Segurança Institucional</h3><p>Relatório de campo sobre o endurecimento de normas governamentais e vistorias rigorosas.</p><a href="https://youtu.be/OdAb5fnIOfk?si=2_yVjeERgpbcX1E0" target="_blank" class="btn-play">▶️ Ver no YouTube</a></div>
        </div>
    </div>

    <div id="acervo" class="pagina">
        <h1>🖼️ BANCO DE DADOS VISUAL COMPLETO</h1>
        <div class="texto-curto">Catálogo unificado de peças, hardware, conexões elétricas e mecânica de precisão.</div>
        <div class="galeria" id="galeriaDinamica"></div>
    </div>
</div>

<div class="modal-autenticacao" id="modalAuth">
    <div class="container-auth">
        <button class="btn-fechar-auth" onclick="fecharPortaria()">&times;</button>
        <div id="boxLogin" class="box-auth-interna visivel">
            <h3>PORTARIA DE ACESSO</h3>
            <form onsubmit="executarLogin(event)">
                <label>E-mail Cadastrado</label>
                <input type="email" required placeholder="exemplo@dominio.com">
                <label>Senha Securitária</label>
                <input type="password" required placeholder="••••••••">
                <button type="submit" class="btn-submeter-auth">Acessar Painel</button>
            </form>
            <div class="alternar-link">Ainda não possui cadastro? <span onclick="alternarAuth('cadastro')">Inscreva-se aqui</span></div>
        </div>
        <div id="boxCadastro" class="box-auth-interna">
            <h3>SOLICITAR INGRESSO</h3>
            <form onsubmit="dispararLinkMagico(event)">
                <label>Informe seu melhor E-mail</label>
                <input type="email" id="cadEmail" required placeholder="exemplo@dominio.com">
                <label>Crie uma Senha de Acesso</label>
                <input type="password" id="cadSenha" required placeholder="Mínimo 8 caracteres">
                <button type="submit" class="btn-submeter-auth">Solicitar Link de Ativação</button>
            </form>
            <div class="alternar-link">Já é cadastrado? <span onclick="alternarAuth('login')">Fazer Login</span></div>
        </div>
        <div id="boxNotificacao" class="box-auth-interna">
            <h3>VERIFIQUE SEU E-MAIL</h3>
            <div class="msg-alerta-e-mail">
                <strong>Link de Ativação Enviado!</strong><br><br>
                Acessamos a sua caixa de entrada. Um e-mail com o link de confirmação foi disparado. Não é necessário copiar código. Basta clicar no link de ativação enviado.
            </div>
            <button class="btn-submeter-auth" onclick="simularCliqueNoLinkDoEmail()">[Simular Clique no Link]</button>
        </div>
        <div id="boxDadosFinais" class="box-auth-interna">
            <h3>COMPLETAR PERFIL CORPORATIVO</h3>
            <form onsubmit="concluirCadastroMestre(event)">
                <label>Nome Completo</label>
                <input type="text" required placeholder="Digite seu nome">
                <label>E-mail Verificado</label>
                <input type="email" id="cadEmailConfirmado" readonly style="opacity: 0.7; background: #00152b;">
                <label>Profissão</label>
                <input type="text" required placeholder="Ex: Engenheiro, Auditor">
                <label>Área de Atuação</label>
                <input type="text" required placeholder="Ex: Semicondutores, Mineração">
                <label>Comentários Adicionais (Opcional)</label>
                <textarea rows="3" placeholder="Deixe suas observações..."></textarea>
                <button type="submit" class="btn-submeter-auth">Concluir Cadastro</button>
            </form>
        </div>
    </div>
</div>

<footer>
    <div class="rodape-superior">
        <div>
            <p>&copy; 2016 - 2026 <strong>CIPRIANUS SEPTEM</strong>. Todo o conteúdo, dados lógicos e tecnologia pertencem estritamente à organização.</p>
        </div>
        <div class="selos-seguranca">
            <span class="selo-seguro">🛡️ CONEXÃO 100% SEGURA</span>
            <span class="selo-patente">🔒 PROJETOS PATENTEADOS</span>
        </div>
    </div>
    <div class="rodape-inferior">
        <p><strong>Aviso de Propriedade, Patente e Confidencialidade Mestre:</strong> Todos os diagramas visuais, especificações mecânicas, plantas arquitetônicas de extração a seco, sistemas de refino térmico e a engenharia de litografia do Chip Aspiral 1nm contidos em todas as abas deste portal estão integralmente protegidos por patentes industriais internacionais registradas. O acesso, cópia ou replicação de qualquer projeto sem autorização formal está sujeito às sanções civis, criminais e protocolos de defesa de propriedade industrial da organização.</p>
    </div>
</footer>

<div id="modal" class="modal" onclick="fecharModal()"><img id="modalImg" alt="Visualização expandida"></div>

<script type="text/javascript">
    window.addEventListener('scroll', () => {
        const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
        const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        const scrolled = (winScroll / height) * 100;
        const bar = document.getElementById('progressBar');
        if(bar) { bar.style.width = scrolled + '%'; }
    });

    function abrirPortaria(tipo) {
        document.getElementById('modalAuth').style.display = 'flex';
        alternarAuth(tipo);
    }
    function fecharPortaria() { document.getElementById('modalAuth').style.display = 'none'; }
    function alternarAuth(tipo) {
        document.querySelectorAll('.box-auth-interna').forEach(box => box.classList.remove('visivel'));
        if(tipo === 'login') document.getElementById('boxLogin').classList.add('visivel');
        if(tipo === 'cadastro') document.getElementById('boxCadastro').classList.add('visivel');
    }
    function dispararLinkMagico(e) {
        e.preventDefault();
        document.getElementById('cadEmailConfirmado').value = document.getElementById('cadEmail').value;
        document.querySelectorAll('.box-auth-interna').forEach(box => box.classList.remove('visivel'));
        document.getElementById('boxNotificacao').classList.add('visivel');
    }
    function simularCliqueNoLinkDoEmail() {
        document.querySelectorAll('.box-auth-interna').forEach(box => box.classList.remove('visivel'));
        document.getElementById('boxDadosFinais').classList.add('visivel');
    }
    function concluirCadastroMestre(e) { e.preventDefault(); fecharPortaria(); }
    function ejecutarLogin(e) { e.preventDefault(); fecharPortaria(); }

    const fotosAcervo = [
        { src: "maquina-litografia.jpg", title: "Máquina de Litografia", desc: "Braço robótico industrial de precisão" },
        { src: "lote-placas-chips.jpg", title: "Lote de Placas PCBs", desc: "Circuitos impressos de alta densidade" },
        { src: "circuito-1nm-detalhe.jpg", title: "Circuitos 1nm Detalhe", desc: "Componentes microsoldados em superfície" },
        { src: "planta-refino-externa.jpg", title: "Planta de Refino Externa", desc: "Complexo de tanques e torres de ustulação" },
        { src: "complexo-extracao-aereo.jpg", title: "Complexo de Extração", desc: "Visão aérea por drone do solo de lavra" },
        { src: "inversor-central-potencia.jpg", title: "Inversor Central", desc: "Painel de conversão de potência elétrica CC/CA" },
        { src: "sensor-optico-drone.jpg", title: "Sensor Óptico Drone", desc: "Módulo de câmera com lentes perimetrais RTK" },
        { src: "articulacao-eixos-internos.jpg", title: "Articulação de Eixos", desc: "Engenharia de eixos concêntricos e engrenagens acopladas" }
    ];

    function renderizarAcervo() {
        const galeria = document.getElementById('galeriaDinamica');
        galeria.innerHTML = "";
        fotosAcervo.forEach(foto => {
            galeria.innerHTML += `
                <div class="foto" onclick="abrirModal(this)">
                    <img src="${foto.src}" alt="${foto.title}" onerror="tratarErroImagem(this)">
                    <p>${foto.title}</p>
                    <span>${foto.desc}</span>
                </div>`;
        });
    }

    function tratarErroImagem(img) {
        img.onerror = null; 
        img.src = "data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='100' height='100' viewBox='0 0 100 100'><rect width='100%' height='100%' fill='%2300152b'/><text x='50%' y='50%' font-family='sans-serif' font-size='10' fill='%23C5B358' text-anchor='middle' dy='.3em'>CIPRIANUS DATA</text></svg>";
    }

    function mostrarPagina(id, elemento) {
        document.querySelectorAll('.pagina').forEach(p => p.classList.remove('ativa'));
        document.querySelectorAll('.menu a').forEach(a => a.classList.remove('ativo'));
        const target = document.getElementById(id);
        if(target) target.classList.add('ativa');
        if(elemento) elemento.classList.add('ativo');
        if (id === 'acervo') { renderizarAcervo(); }
    }
    function abrirModal(el) { let img = el.querySelector('img'); if(img){ document.getElementById('modal').style.display='flex'; document.getElementById('modalImg').src=img.src; document.getElementById('modalImg').alt=img.alt; } }
    function fecharModal() { document.getElementById('modal').style.display='none'; }
    function googleTranslateElementInit() {
        new google.translate.TranslateElement({pageLanguage: 'pt', includedLanguages: 'pt,es,en,da', layout: google.translate.TranslateElement.InlineLayout.SIMPLE}, 'google_translate_element');
    }
</script>
<script type="text/javascript" src="//translate.google.com/translate_a/element.js?cb=googleTranslateElementInit"></script>
</body>
</html>

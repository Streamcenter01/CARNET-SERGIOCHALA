<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Carnet Digital Interactivo - SegurApp Recorridos</title>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <style>
        :root {
            --bg-principal: #08080a;
            --bg-tarjeta: #101216;
            --bg-input: #161920;
            --acero-claro: #a6b4c9;
            --acero-oscuro: #3a4454;
            --dorado-brillante: #b88628;
            --dorado-base: #b88628;
            --dorado-oscuro: #997a15;
            --glow-dorado: rgba(255, 215, 0, 0.4);
            --verde-verificado: #00ff88;
            --glow-verde: rgba(0, 255, 136, 0.6);
            
            --texto-principal: #ffffff;
            --texto-secundario: #9aa5b5;
            --borde-sutil: rgba(212, 175, 55, 0.25);
            --fuente: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
            font-family: var(--fuente);
        }

        body {
            background-color: var(--bg-principal);
            color: var(--texto-principal);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at center, rgba(212, 175, 55, 0.08) 0%, rgba(8, 8, 10, 0.98) 80%),
                        url('https://imgs.search.brave.com/4EBMHUrFzUMmziphOMTPiPrRGPM74GSSptcyBcla7gU/rs:fit:860:0:0:0/g:ce/aHR0cHM6Ly9kZWxj/YXIuY29tLnV5L3dw/LWNvbnRlbnQvdXBs/b2Fkcy8yMDIzLzEw/L1JBSURFUi03LXNj/YWxlZC5qcGc') no-repeat center center;
            background-size: cover;
            z-index: -1;
        }

        /* --- INDICADOR DE GIRAR ULTRA VISIBLE --- */
        .hint-girar {
            font-size: 0.8rem;
            color: #ffffff;
            text-transform: uppercase;
            letter-spacing: 1.2px;
            font-weight: 900;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            margin-bottom: 16px;
            padding: 10px 20px;
            background: linear-gradient(135deg, rgba(22, 25, 32, 0.95) 0%, rgba(10, 12, 16, 0.95) 100%);
            border: 2px solid var(--dorado-brillante);
            border-radius: 30px;
            box-shadow: 0 0 15px rgba(255, 215, 0, 0.4), inset 0 0 10px rgba(255, 215, 0, 0.1);
            animation: pulseHint 1.8s infinite ease-in-out;
            cursor: pointer;
            user-select: none;
        }

        .hint-girar .icono-girar {
            font-size: 20px;
            color: var(--dorado-brillante);
            animation: rotarIcono 2.5s infinite linear;
        }

        @keyframes pulseHint {
            0%, 100% {
                transform: scale(1);
                box-shadow: 0 0 12px rgba(255, 215, 0, 0.4), 0 0 20px rgba(212, 175, 55, 0.2);
            }
            50% {
                transform: scale(1.05);
                box-shadow: 0 0 22px rgba(255, 215, 0, 0.8), 0 0 35px rgba(212, 175, 55, 0.5);
                border-color: #ffe600;
            }
        }

        @keyframes rotarIcono {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* --- CONTENEDOR FLIP 3D --- */
        .escena-carnet {
            width: 100%;
            max-width: 380px;
            height: 610px;
            perspective: 1200px;
            margin-bottom: 20px;
            cursor: pointer;
        }

        .carnet-inner {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .escena-carnet.flipped .carnet-inner {
            transform: rotateY(180deg);
        }

        .carnet-cara {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
            background: var(--bg-tarjeta);
            border: 1px solid var(--borde-sutil);
            border-radius: 20px;
            padding: 22px 20px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            overflow: hidden;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.9), 0 0 20px var(--glow-dorado);
        }

        .carnet-cara.reverso {
            transform: rotateY(180deg);
        }

        @keyframes barridoMetalico {
            0% { left: -150%; }
            50% { left: -150%; }
            100% { left: 150%; }
        }

        .carnet-cara::after {
            content: '';
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(
                90deg,
                rgba(255, 215, 0, 0) 0%,
                rgba(255, 215, 0, 0.03) 20%,
                rgba(255, 215, 0, 0.15) 50%,
                rgba(255, 215, 0, 0.03) 80%,
                rgba(255, 215, 0, 0) 100%
            );
            transform: skewX(-25deg);
            animation: barridoMetalico 6s infinite ease-in-out;
            pointer-events: none;
        }

        .perforacion-lanyard {
            width: 50px;
            height: 10px;
            background: #000;
            border: 1px solid var(--borde-sutil);
            border-radius: 10px;
            margin: 0 auto 10px auto;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.8);
        }

        .carnet-header {
            text-align: center;
            border-bottom: 1px solid var(--borde-sutil);
            padding-bottom: 8px;
            margin-bottom: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .carnet-header img.logo {
            max-width: 50px;
            height: auto;
            margin-bottom: 4px;
        }

        .carnet-header .sub-brand {
            font-size: 0.65rem;
            color: var(--dorado-brillante);
            letter-spacing: 1.5px;
            text-transform: uppercase;
            font-weight: 800;
            text-shadow: 0 0 8px rgba(255, 215, 0, 0.5);
        }

        .badge-rol {
            display: inline-block;
            background: linear-gradient(135deg, var(--dorado-brillante) 0%, var(--dorado-oscuro) 100%);
            color: #000000;
            font-size: 0.65rem;
            font-weight: 900;
            padding: 4px 12px;
            border-radius: 20px;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 6px;
            box-shadow: 0 2px 10px var(--glow-dorado);
        }

        .carnet-body {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }

        .foto-marco {
            position: relative;
            margin-bottom: 10px;
        }

        .foto-conductor {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            object-fit: cover;
            border: 3px solid var(--dorado-brillante);
            box-shadow: 0 0 22px var(--glow-dorado);
            background-color: #1a1a1a;
        }

        .badge-verificado-icono {
            position: absolute;
            bottom: 2px;
            right: 2px;
            background: #000;
            color: var(--verde-verificado);
            border-radius: 50%;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid var(--verde-verificado);
            box-shadow: 0 0 15px var(--glow-verde);
            z-index: 10;
        }

        .badge-verificado-icono::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 2px solid var(--verde-verificado);
            opacity: 0;
            animation: pulsoVerde 2s infinite;
            box-sizing: border-box;
        }

        @keyframes pulsoVerde {
            0% { transform: scale(1); opacity: 1; }
            100% { transform: scale(1.5); opacity: 0; }
        }

        .nombre-conductor {
            font-size: 1.1rem;
            font-weight: 800;
            color: #ffffff;
            margin-bottom: 2px;
        }

        .cargo-conductor {
            font-size: 0.7rem;
            color: var(--texto-secundario);
            margin-bottom: 10px;
        }

        .datos-grid {
            width: 100%;
            background: var(--bg-input);
            border-radius: 12px;
            padding: 10px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            text-align: left;
            border: 1px solid var(--borde-sutil);
            margin-bottom: 10px;
        }

        .dato-item {
            display: flex;
            flex-direction: column;
        }

        .dato-item.full-width {
            grid-column: span 2;
        }

        .dato-label {
            font-size: 0.58rem;
            color: var(--texto-secundario);
            text-transform: uppercase;
            font-weight: 700;
        }

        .dato-val {
            font-size: 0.78rem;
            color: #ffffff;
            font-weight: 700;
        }

        .dato-val.destacado {
            color: var(--dorado-brillante);
            text-shadow: 0 0 5px rgba(255, 215, 0, 0.3);
        }

        .carnet-footer {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            background: rgba(255, 215, 0, 0.03);
            padding: 10px;
            border-radius: 12px;
            border: 1px dashed var(--borde-sutil);
        }

        .qr-code-lg {
            width: 80px;
            height: 80px;
            background: #fff;
            padding: 0.1px;
            border-radius: 8px;
            flex-shrink: 0;
        }

        .qr-code-lg img {
            width: 100%;
            height: 100%;
            display: block;
        }

        .info-qr {
            text-align: right;
        }

        .info-qr .id-codigo {
            font-family: monospace;
            font-size: 0.75rem;
            color: var(--texto-principal);
            font-weight: 700;
        }

        .info-qr .estado {
            font-size: 0.6rem;
            color: var(--verde-verificado);
            font-weight: 800;
            text-transform: uppercase;
            display: flex;
            align-items: center;
            justify-content: flex-end;
            gap: 3px;
            margin-top: 4px;
            text-shadow: 0 0 5px var(--glow-verde);
        }

        /* --- SECCIÓN DE CALIFICACIÓN --- */
        .rating-box-reverso {
            width: 100%;
            background: var(--bg-input);
            border: 1px solid var(--borde-sutil);
            border-radius: 12px;
            padding: 10px;
            margin: 10px 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .rating-title {
            font-size: 0.65rem;
            color: var(--dorado-brillante);
            text-transform: uppercase;
            font-weight: 800;
            letter-spacing: 0.5px;
            margin-bottom: 4px;
        }

        .rating-promedio {
            font-size: 0.85rem;
            font-weight: 800;
            color: #ffffff;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .stars-container {
            display: flex;
            gap: 6px;
            margin: 6px 0;
        }

        .star-icon {
            font-size: 22px;
            color: #4a4a4a;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .star-icon.active, .star-icon:hover {
            color: #ffd700;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.7);
        }

        .voto-mensaje {
            font-size: 0.62rem;
            color: var(--verde-verificado);
            margin-top: 2px;
            font-weight: 700;
        }

        .reverso-info {
            font-size: 0.7rem;
            color: var(--texto-secundario);
            line-height: 1.35;
            text-align: center;
        }

        .acciones-bar {
            width: 100%;
            max-width: 380px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .btn-grupo-principal {
            display: flex;
            gap: 10px;
        }

        .btn-accion {
            flex: 1;
            background: var(--bg-tarjeta);
            border: 1px solid var(--borde-sutil);
            color: #fff;
            padding: 14px;
            border-radius: 14px;
            font-size: 0.8rem;
            font-weight: 700;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.2s ease;
            text-decoration: none;
            box-shadow: 0 4px 12px rgba(0,0,0,0.5);
        }

        .btn-accion:active {
            transform: scale(0.96);
        }

        /* --- BOTÓN DE SOLICITAR SERVICIO LLAMATIVO --- */
        .btn-accion.solicitar-wasap {
            position: relative;
            background: linear-gradient(135deg, #00ff88 0%, #25d366 50%, #056232 100%);
            color: #000000;
            border: 2px solid #00ff88;
            font-size: 1rem;
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 0.8px;
            padding: 18px 24px;
            border-radius: 20px;
            box-shadow: 0 0 25px rgba(0, 255, 136, 0.7), inset 0 2px 4px rgba(255,255,255,0.8);
            animation: superPulso 1.8s infinite ease-in-out;
            overflow: hidden;
            text-shadow: 0 1px 1px rgba(255,255,255,0.4);
            cursor: pointer;
            width: 100%;
        }

        .btn-accion.solicitar-wasap::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: rgba(255, 255, 255, 0.25);
            transform: rotate(45deg);
            animation: brilloEfecto 3s infinite;
            pointer-events: none;
        }

        @keyframes superPulso {
            0% {
                transform: scale(1);
                box-shadow: 0 0 15px rgba(0, 255, 136, 0.6), 0 0 30px rgba(37, 211, 102, 0.4);
            }
            50% {
                transform: scale(1.03);
                box-shadow: 0 0 35px rgba(0, 255, 136, 0.9), 0 0 50px rgba(37, 211, 102, 0.7);
            }
            100% {
                transform: scale(1);
                box-shadow: 0 0 15px rgba(0, 255, 136, 0.6), 0 0 30px rgba(37, 211, 102, 0.4);
            }
        }

        @keyframes brilloEfecto {
            0% { left: -100%; }
            20% { left: 100%; }
            100% { left: 100%; }
        }

        .btn-accion.guardar-contacto {
            background: linear-gradient(135deg, var(--dorado-brillante) 0%, var(--dorado-oscuro) 100%);
            color: #000;
            border: none;
            box-shadow: 0 4px 15px var(--glow-dorado);
        }

        .btn-accion.quienes-somos {
            background: rgba(22, 25, 32, 0.9);
            border: 1px solid var(--dorado-brillante);
            color: var(--dorado-brillante);
            box-shadow: 0 0 10px rgba(212, 175, 55, 0.2);
        }

        /* --- MODAL QUIÉNES SOMOS --- */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
            padding: 20px;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal-contenido {
            background: var(--bg-tarjeta);
            border: 1px solid var(--borde-sutil);
            border-radius: 20px;
            width: 100%;
            max-width: 420px;
            max-height: 85vh;
            overflow-y: auto;
            padding: 24px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.8), 0 0 25px var(--glow-dorado);
            position: relative;
            transform: translateY(20px);
            transition: transform 0.3s ease;
        }

        .modal-overlay.active .modal-contenido {
            transform: translateY(0);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--borde-sutil);
            padding-bottom: 12px;
            margin-bottom: 16px;
        }

        .modal-titulo {
            font-size: 1.1rem;
            font-weight: 800;
            color: var(--dorado-brillante);
            text-transform: uppercase;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn-cerrar {
            background: none;
            border: none;
            color: var(--texto-secundario);
            font-size: 24px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-body {
            font-size: 0.85rem;
            color: var(--texto-secundario);
            line-height: 1.6;
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .modal-body h4 {
            color: #ffffff;
            font-size: 0.95rem;
            margin-top: 6px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .modal-body h4 span {
            color: var(--dorado-brillante);
        }

        .caracteristica-box {
            background: var(--bg-input);
            border: 1px solid var(--borde-sutil);
            border-radius: 10px;
            padding: 10px;
            margin-top: 4px;
        }
    </style>
</head>
<body>

    <!-- BOTÓN / PÍLDORA VISIBLE PARA VOLTEAR -->
    <div class="hint-girar" onclick="voltearCarnet()">
        <span class="material-icons icono-girar">autorenew</span>
        Toca el carnet para voltear
    </div>

    <!-- ESCENA 3D DEL CARNET -->
    <div class="escena-carnet" id="escenaCarnet">
        <div class="carnet-inner">
            
            <!-- CARA FRONTAL -->
            <div class="carnet-cara frontal" onclick="voltearCarnet()">
                <div class="perforacion-lanyard"></div>

                <div class="carnet-header">
                    <img src="https://scontent.fnva2-1.fna.fbcdn.net/v/t39.30808-6/756341896_122112284661318735_3783461112117562916_n.jpg?stp=dst-jpg_tt6&cstp=mx2000x2000&ctp=s2000x2000&_nc_cat=107&ccb=1-7&_nc_sid=127cfc&_nc_eui2=AeHiIyYM0PMIFRje-sD2qF4k6_A_YNFTiP_r8D9g0VOI_yOrwYMe6j-2s2IP87L8QFx0tWwIlGunFfrr2_1kzfyT&_nc_ohc=z32eauIiNRsQ7kNvwGmIa3a&_nc_oc=AdoDh2BGScEtPr4uWNGYlRnETflUnrRB-bBlVXz1X7ebKxYE8lnoS66Ev0c3dMdOjGk&_nc_zt=23&_nc_ht=scontent.fnva2-1.fna&_nc_gid=1_cGxj_WdL9FoY58BltkLQ&_nc_ss=7b2a8&oh=00_AQBaf0xDI7EHwx1v8PMJ3PCgomixUYVlXcBqQiuR0xhCMA&oe=6A6C2A56" alt="SegurApp Logo" class="logo">
                    <div class="sub-brand">RAPIDOS - confiables - seguros.</div>
                    <span class="badge-rol">Conductor Oficial</span>
                </div>

                <div class="carnet-body">
                    <div class="foto-marco">
                        <img src="https://scontent.fnva2-1.fna.fbcdn.net/v/t39.30808-6/699116233_989437980648237_9201268186456313724_n.jpg?stp=dst-jpg_tt6&cstp=mx944x1135&ctp=s944x1135&_nc_cat=104&ccb=1-7&_nc_sid=6ee11a&_nc_eui2=AeF20nckf-W9D3ZFO7cEU1xSlECitdgceRmUQKK12Bx5GWvzlgUUxyauRT7-iPD92RZ-aTX-rvfv8ZiXQ66KkWHV&_nc_ohc=6FO9J7HzZaoQ7kNvwGtLvFT&_nc_oc=AdrI9IA2QlDKWnikZCvKlPJS76TC__BkEWFuHd5N78Uqmd3TeXIut3dK5I3KqROVT1I&_nc_zt=23&_nc_ht=scontent.fnva2-1.fna&_nc_gid=-nQuu5dETcx8X7Mi9PtKtQ&_nc_ss=7b2a8&oh=00_AQDU0SeJHntC2DWBo_zj_a6WwSbkVzuzGkkwOJif2F1yLg&oe=6A6B6E6A" onerror="this.src='https://ui-avatars.com/api/?name=Sergio+Tapiero&background=ffd700&color=000&size=200'" alt="Foto Sergio Tapiero" class="foto-conductor">
                        <div class="badge-verificado-icono">
                            <span class="material-icons" style="font-size: 18px;">check_circle</span>
                        </div>
                    </div>

                    <div class="nombre-conductor">Sergio Alejandro Tapiero Chala</div>
                    <div class="cargo-conductor">Transporte Urbano Individual</div>

                    <div class="datos-grid">
                        <div class="dato-item full-width">
                            <span class="dato-label">Rol Asignado</span>
                            <span class="dato-val destacado">Administrador / Gerente de Operaciones</span>
                        </div>
                        <div class="dato-item">
                            <span class="dato-label">C.C. / Licencia</span>
                            <span class="dato-val">1006056890</span>
                        </div>
                        <div class="dato-item">
                            <span class="dato-label">Placa Vehículo</span>
                            <span class="dato-val destacado">BWQ 69H</span>
                        </div>
                        <div class="dato-item full-width">
                            <span class="dato-label">Vehículo Registrado</span>
                            <span class="dato-val">TVS Raider 125 (Negra)</span>
                        </div>
                    </div>
                </div>

                <div class="carnet-footer">
                    <div class="qr-code-lg">
                        <img src="https://scontent.fnva2-1.fna.fbcdn.net/v/t39.30808-6/757563678_122112373905318735_4099987177954124814_n.jpg?stp=dst-jpg_tt6&cstp=mx2000x2000&ctp=s2000x2000&_nc_cat=106&ccb=1-7&_nc_sid=127cfc&_nc_eui2=AeGUs1dE4NOifaX1KCiMpKnsDrfjqJq4uMEOt-Oomri4wbkysMr92Po7rBgE88JI-MMeaAyL_BYTlxYCRZrKvCK2&_nc_ohc=inKPbZEwhooQ7kNvwHUJcYC&_nc_oc=AdpbyeiSq6geiSxPcqJP1_9ZP1q2QPD03YKhXJQSSSOEqJY98PWowFuxnqlejVHL6BM&_nc_zt=23&_nc_ht=scontent.fnva2-1.fna&_nc_gid=P9M2JLMiukCbnwM643mDvg&_nc_ss=7b2a8&oh=00_AQCG7Q4ngX68Hke9C2ILIxeWJIsooZfANgE6figB-TIcWA&oe=6A6D7905" alt="Código QR WhatsApp">
                    </div>
                    <div class="info-qr">
                        <div class="id-codigo">ID: SEG-2026-890</div>
                        <div style="font-size:0.58rem; color:var(--texto-secundario); margin-top:2px;">Escanear para verificar</div>
                        <div class="estado">
                            <span class="material-icons" style="font-size: 12px;">circle</span> Activo / Verificado
                        </div>
                    </div>
                </div> 
            </div>

            <!-- CARA POSTERIOR (REVERSO) -->
            <div class="carnet-cara reverso" onclick="voltearCarnet()">
                <div class="perforacion-lanyard"></div>
                
                <div class="carnet-header">
                    <img src="https://scontent.fnva2-1.fna.fbcdn.net/v/t39.30808-6/756341896_122112284661318735_3783461112117562916_n.jpg?stp=dst-jpg_tt6&cstp=mx2000x2000&ctp=s2000x2000&_nc_cat=107&ccb=1-7&_nc_sid=127cfc&_nc_eui2=AeHiIyYM0PMIFRje-sD2qF4k6_A_YNFTiP_r8D9g0VOI_yOrwYMe6j-2s2IP87L8QFx0tWwIlGunFfrr2_1kzfyT&_nc_ohc=z32eauIiNRsQ7kNvwGmIa3a&_nc_oc=AdoDh2BGScEtPr4uWNGYlRnETflUnrRB-bBlVXz1X7ebKxYE8lnoS66Ev0c3dMdOjGk&_nc_zt=23&_nc_ht=scontent.fnva2-1.fna&_nc_gid=1_cGxj_WdL9FoY58BltkLQ&_nc_ss=7b2a8&oh=00_AQBaf0xDI7EHwx1v8PMJ3PCgomixUYVlXcBqQiuR0xhCMA&oe=6A6C2A56" alt="SegurApp Logo" class="logo" style="max-width: 170px;">
                    <div class="sub-brand">Información y Valoración</div>
                </div>

                <div class="reverso-info">
                    <p>Acredita el rol de <strong>Conductor Autorizado</strong> en <strong>SegurApp Recorridos</strong>.</p>
                    
                    <div class="rating-box-reverso" onclick="event.stopPropagation()">
                        <div class="rating-title">Calificación del Conductor</div>
                        <div class="rating-promedio">
                            <span id="promedioTexto">4.8</span> 
                            <span class="material-icons" style="font-size:18px; color:#ffd700;">star</span> 
                            <span id="totalVotosTexto" style="color:var(--texto-secundario); font-size:0.65rem;">(80 valoraciones)</span>
                        </div>

                        <div class="stars-container" id="starsContainer">
                            <span class="material-icons star-icon" data-value="1" onclick="calificar(1)">star</span>
                            <span class="material-icons star-icon" data-value="2" onclick="calificar(2)">star</span>
                            <span class="material-icons star-icon" data-value="3" onclick="calificar(3)">star</span>
                            <span class="material-icons star-icon" data-value="4" onclick="calificar(4)">star</span>
                            <span class="material-icons star-icon" data-value="5" onclick="calificar(5)">star</span>
                        </div>

                        <div id="votoMensaje" class="voto-mensaje"></div>
                    </div>

                    <div class="datos-grid" style="margin-bottom: 8px; text-align: center;">
                        <div class="dato-item full-width">
                            <span class="dato-label">Línea Directa de Atención</span>
                            <span class="dato-val">+57 318 988 2787</span>
                        </div>
                    </div>

                    <p>Este carnet acredita la identidad y el <strong>Rol de Conductor Autorizado</strong> en la plataforma <strong>SegurApp Recorridos</strong> en Neiva, Huila.</p>
                </div>

                <div style="margin-top: 6px; text-align: center; font-size: 0.6rem; color: var(--texto-secundario);">
                    © 2026 SegurApp Recorridos. Todos los derechos reservados.
                </div>
            </div>

        </div>
    </div>

    <!-- BOTONES DE ACCIÓN PRINCIPALES -->
    <div class="acciones-bar">
        <button class="btn-accion solicitar-wasap" id="btnSolicitarRecorrido" onclick="enviarUbicacionPorWhatsApp()">
            <span class="material-icons" style="font-size:24px;">location_on</span> Solicitar Recorrido Ya
        </button>

        <div class="btn-grupo-principal">
            <button class="btn-accion guardar-contacto" onclick="guardarContactoVCF()">
                <span class="material-icons">person_add</span> Guardar Contacto
            </button>
<button class="btn-accion quienes-somos" onclick="abrirQuienesSomos()">
            <span class="material-icons">info</span> ¿Quiénes Somos?
        </button>
            
        </div>

       
    </div>

    <!-- MODAL QUIÉNES SOMOS -->
    <div class="modal-overlay" id="modalQuienesSomos">
        <div class="modal-contenido">
            <div class="modal-header">
                <div class="modal-titulo">
                    <span class="material-icons">groups</span> Quiénes Somos
                </div>
                <button class="btn-cerrar" onclick="cerrarQuienesSomos()">
                    <span class="material-icons">close</span>
                </button>
            </div>
            <div class="modal-body">
                <p>En <strong>SegurApp Recorridos</strong> nos dedicamos a transformar la movilización urbana en Neiva, ofreciendo un servicio de transporte individual express altamente seguro, rápido y confiable.</p>
                
                <h4><span class="material-icons">verified_user</span> Nuestra Misión</h4>
                <p>Proporcionar un traslado rápido y seguro para cada pasajero, respaldado por conductores totalmente identificados y verificados en tiempo real.</p>

                <h4><span class="material-icons">star</span> ¿Por qué elegirnos?</h4>
                <div class="caracteristica-box">
                    <strong style="color: #fff;">• Seguridad Garantizada:</strong> Validación digital de la identidad del conductor e historial de vehículo.
                </div>
                <div class="caracteristica-box">
                    <strong style="color: #fff;">• Respuesta Inmediata:</strong> Ubicación precisa en tiempo real a través de WhatsApp para recogidas inmediatas.
                </div>
                <div class="caracteristica-box">
                    <strong style="color: #fff;">• Trato Personalizado:</strong> Calificación y servicio confiable en cada recorrido.
                </div>
            </div>
        </div>
    </div>

    <!-- SCRIPT DE CALIFICACIÓN POR DISPOSITIVO Y CONTADOR -->
    <script>
        const STORAGE_KEY_VOTO = 'segurapp_user_voted';
        const STORAGE_KEY_START = 'segurapp_start_time';
        const BASE_VALORACIONES = 80;
        const HORAS_POR_INCREMENTO = 2.5;

        function obtenerTotalValoraciones() {
            let inicioTiempo = localStorage.getItem(STORAGE_KEY_START);
            if (!inicioTiempo) {
                inicioTiempo = Date.now();
                localStorage.setItem(STORAGE_KEY_START, inicioTiempo);
            }

            const msTranscurridos = Date.now() - parseInt(inicioTiempo);
            const horasTranscurridas = msTranscurridos / (1000 * 60 * 60);
            const incrementos = Math.floor(horasTranscurridas / HORAS_POR_INCREMENTO);
            
            const votoLocal = localStorage.getItem(STORAGE_KEY_VOTO) ? 1 : 0;
            return BASE_VALORACIONES + incrementos + votoLocal;
        }

        function actualizarUI() {
            const total = obtenerTotalValoraciones();
            document.getElementById('totalVotosTexto').innerText = `(${total} valoraciones)`;

            const miVoto = localStorage.getItem(STORAGE_KEY_VOTO);
            const stars = document.querySelectorAll('.star-icon');
            const msgBox = document.getElementById('votoMensaje');

            if (miVoto) {
                const rating = parseInt(miVoto);
                stars.forEach((s, idx) => {
                    if (idx < rating) {
                        s.classList.add('active');
                    } else {
                        s.classList.remove('active');
                    }
                    s.style.cursor = 'default';
                });
                msgBox.innerText = `✓ ¡Gracias! Calificaste con ${rating} estrella${rating > 1 ? 's' : ''}`;
            } else {
                stars.forEach(s => {
                    s.classList.remove('active');
                    s.style.cursor = 'pointer';
                });
                msgBox.innerText = 'Haz clic en las estrellas para calificar';
            }
        }

        function calificar(estrellas) {
            const miVoto = localStorage.getItem(STORAGE_KEY_VOTO);
            if (miVoto) return;

            localStorage.setItem(STORAGE_KEY_VOTO, estrellas);
            
            const nuevoPromedio = (4.8 + (estrellas - 4.8) * 0.05).toFixed(1);
            document.getElementById('promedioTexto').innerText = nuevoPromedio;

            actualizarUI();
        }

        actualizarUI();
        setInterval(actualizarUI, 60000);

        let ubicacionUsuario = null;

        function voltearCarnet() {
            const escena = document.getElementById('escenaCarnet');
            escena.classList.toggle('flipped');
        }

        function abrirQuienesSomos() {
            document.getElementById('modalQuienesSomos').classList.add('active');
        }

        function cerrarQuienesSomos() {
            document.getElementById('modalQuienesSomos').classList.remove('active');
        }

        window.addEventListener('DOMContentLoaded', () => {
            pedirPermisoUbicacionInicial();
        });

        function pedirPermisoUbicacionInicial() {
            if ("geolocation" in navigator) {
                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        ubicacionUsuario = {
                            lat: position.coords.latitude,
                            lng: position.coords.longitude
                        };
                    },
                    (error) => {
                        console.warn("Permiso de ubicación denegado o inaccesible al inicio:", error);
                    },
                    {
                        enableHighAccuracy: true,
                        timeout: 10000,
                        maximumAge: 0
                    }
                );
            }
        }

        function enviarUbicacionPorWhatsApp() {
            const telefono = "573189882787";
            const btn = document.getElementById('btnSolicitarRecorrido');

            if (ubicacionUsuario) {
                const mapaLink = `https://www.google.com/maps?q=${ubicacionUsuario.lat},${ubicacionUsuario.lng}`;
                const mensaje = encodeURIComponent(
                    `¡Hola! Sergio, necesito solicitar un servicio de recorrido en SegurApp.\n\n` +
                    `📍 Mi ubicación actual en tiempo real es:\n${mapaLink}`
                );
                window.open(`https://wa.me/${telefono}?text=${mensaje}`, '_blank');
            } else {
                btn.style.opacity = "0.7";
                btn.innerHTML = `<span class="material-icons" style="animation: pulseHint 1s infinite;">my_location</span> Obteniendo ubicación...`;

                if ("geolocation" in navigator) {
                    navigator.geolocation.getCurrentPosition(
                        (position) => {
                            const lat = position.coords.latitude;
                            const lng = position.coords.longitude;
                            const mapaLink = `https://www.google.com/maps?q=${lat},${lng}`;
                            
                            const mensaje = encodeURIComponent(
                                `¡Hola! Sergio, necesito solicitar un servicio de recorrido en SegurApp.\n\n` +
                                `Mi ubicación actual en tiempo real es:\n${mapaLink}`
                            );

                            btn.style.opacity = "1";
                            btn.innerHTML = `<span class="material-icons" style="font-size:24px;">location_on</span> Solicitar Recorrido Ya`;

                            window.open(`https://wa.me/${telefono}?text=${mensaje}`, '_blank');
                        },
                        (error) => {
                            const mensajeSinUbicacion = encodeURIComponent(
                                `¡Hola! Sergio, quiero solicitar un servicio de recorrido en SegurApp Recorridos.`
                            );

                            btn.style.opacity = "1";
                            btn.innerHTML = `<span class="material-icons" style="font-size:24px;">location_on</span> Solicitar Recorrido Ya`;

                            window.open(`https://wa.me/${telefono}?text=${mensajeSinUbicacion}`, '_blank');
                        },
                        {
                            enableHighAccuracy: true,
                            timeout: 8000,
                            maximumAge: 0
                        }
                    );
                } else {
                    const mensajeFallback = encodeURIComponent(`¡Hola! Sergio, quiero solicitar un servicio de recorrido en SegurApp Recorridos.`);
                    window.open(`https://wa.me/${telefono}?text=${mensajeFallback}`, '_blank');
                }
            }
        }

        function guardarContactoVCF() {
            const vcardData = `BEGIN:VCARD
VERSION:3.0
FN:Sergio Tapiero Chala - SegurApp Recorridos
N:Tapiero Chala;Sergio;Alejandro;;
ORG:SegurApp Recorridos
TITLE:Conductor Autorizado
TEL;TYPE=CELL,VOICE:+573189882787
NOTE:Licencia: 1006056890 | Placa: BWQ 69H | TVS Raider 125
URL:https://segurapp-recorridos.com
END:VCARD`;

            const blob = new Blob([vcardData], { type: 'text/vcard;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.href = url;
            link.setAttribute('download', 'Sergio_Tapiero_SegurApp.vcf');
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
        }
    </script>
</body>
</html>

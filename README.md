# modubox.github.io
<!DOCTYPE html>
<html lang="es-MX">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ModuBox | Cajas modulares expandibles en México</title>
  <meta name="description" content="ModuBox fabrica cajas modulares expandibles en México para empresas, familias y comerciantes. Cotiza por WhatsApp.">

  <!-- Tipografía moderna (Google Fonts). Si no hay internet, usa sans-serif del sistema -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">

  <style>
    /* =====================================================
       1. VARIABLES Y ESTILOS BASE
       ===================================================== */
    :root {
      --naranja: #FF6B00;
      --naranja-oscuro: #E05A00;
      --naranja-suave: #FFF1E6;
      --negro: #111111;
      --gris: #555555;
      --gris-claro: #F6F6F6;
      --blanco: #FFFFFF;
      --radio: 16px;
      --sombra: 0 10px 30px rgba(0, 0, 0, .08);
      --whatsapp: #25D366;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; scroll-padding-top: 80px; }

    body {
      font-family: 'Poppins', system-ui, -apple-system, 'Segoe UI', Arial, sans-serif;
      color: var(--negro);
      background: var(--blanco);
      line-height: 1.6;
      -webkit-font-smoothing: antialiased;
    }

    img, svg { max-width: 100%; display: block; }
    a { color: inherit; text-decoration: none; }
    ul { list-style: none; }

    .container { width: min(1120px, 92%); margin-inline: auto; }
    section { padding: 90px 0; }

    .etiqueta {
      display: inline-block;
      background: var(--naranja-suave);
      color: var(--naranja-oscuro);
      font-weight: 600;
      font-size: .85rem;
      padding: 6px 14px;
      border-radius: 999px;
      margin-bottom: 14px;
    }

    .titulo-seccion { font-size: clamp(1.8rem, 4vw, 2.6rem); line-height: 1.2; font-weight: 700; }
    .titulo-seccion span { color: var(--naranja); }
    .subtitulo-seccion { color: var(--gris); max-width: 620px; margin-top: 12px; }
    .centrado { text-align: center; }
    .centrado .subtitulo-seccion { margin-inline: auto; }

    /* ---------- Botones ---------- */
    .btn {
      display: inline-flex; align-items: center; justify-content: center; gap: 10px;
      padding: 14px 28px;
      border-radius: 999px;
      font-weight: 600; font-size: 1rem;
      border: 2px solid transparent;
      cursor: pointer;
      transition: transform .25s ease, box-shadow .25s ease, background .25s ease;
      font-family: inherit;
    }
    .btn:hover { transform: translateY(-3px); }
    .btn-primario { background: var(--naranja); color: var(--blanco); box-shadow: 0 8px 20px rgba(255, 107, 0, .35); }
    .btn-primario:hover { background: var(--naranja-oscuro); }
    .btn-secundario { border-color: var(--negro); color: var(--negro); background: transparent; }
    .btn-secundario:hover { background: var(--negro); color: var(--blanco); }
    .btn-whatsapp { background: var(--whatsapp); color: var(--blanco); box-shadow: 0 8px 20px rgba(37, 211, 102, .35); }

    /* =====================================================
       2. ANIMACIONES AL HACER SCROLL
       Los elementos con .reveal aparecen suavemente
       cuando entran en pantalla (ver JavaScript abajo)
       ===================================================== */
    .reveal { opacity: 0; transform: translateY(35px); transition: opacity .8s ease, transform .8s ease; }
    .reveal.visible { opacity: 1; transform: none; }
    .delay-1 { transition-delay: .15s; }
    .delay-2 { transition-delay: .3s; }

    /* Respeta a quienes prefieren menos movimiento */
    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto; }
      .reveal { opacity: 1; transform: none; transition: none; }
      * { animation: none !important; }
    }

    /* =====================================================
       3. BARRA DE NAVEGACIÓN
       ===================================================== */
    header {
      position: fixed; top: 0; left: 0; width: 100%; z-index: 100;
      background: rgba(255, 255, 255, .92);
      backdrop-filter: blur(10px);
      transition: box-shadow .3s ease;
    }
    header.scrolled { box-shadow: 0 4px 20px rgba(0, 0, 0, .08); }

    .nav { display: flex; align-items: center; justify-content: space-between; height: 72px; }

    .logo { font-weight: 800; font-size: 1.5rem; display: flex; align-items: center; gap: 8px; }
    .logo-icono { width: 32px; height: 32px; background: var(--naranja); border-radius: 8px; display: grid; place-items: center; }
    .logo span { color: var(--naranja); }

    .menu { display: flex; align-items: center; gap: 28px; font-weight: 500; }
    .menu a:not(.btn) { position: relative; }
    .menu a:not(.btn)::after {
      content: ''; position: absolute; left: 0; bottom: -4px; width: 0; height: 2px;
      background: var(--naranja); transition: width .3s ease;
    }
    .menu a:not(.btn):hover::after { width: 100%; }
    .menu .btn { padding: 10px 22px; font-size: .9rem; }

    /* Botón hamburguesa (solo móvil) */
    .hamburguesa { display: none; background: none; border: 0; cursor: pointer; padding: 8px; }
    .hamburguesa span { display: block; width: 26px; height: 3px; background: var(--negro); margin: 5px 0; border-radius: 2px; transition: .3s; }
    .hamburguesa.abierto span:nth-child(1) { transform: translateY(8px) rotate(45deg); }
    .hamburguesa.abierto span:nth-child(2) { opacity: 0; }
    .hamburguesa.abierto span:nth-child(3) { transform: translateY(-8px) rotate(-45deg); }

    /* =====================================================
       4. HERO
       ===================================================== */
    .hero {
      padding: 150px 0 90px;
      background:
        radial-gradient(circle at 85% 20%, var(--naranja-suave) 0, transparent 45%),
        var(--blanco);
      overflow: hidden;
    }
    .hero-grid { display: grid; grid-template-columns: 1.1fr .9fr; gap: 50px; align-items: center; }
    .hero h1 { font-size: clamp(2.2rem, 5.5vw, 3.6rem); line-height: 1.1; font-weight: 800; margin-bottom: 20px; }
    .hero h1 span { color: var(--naranja); }
    .hero p { color: var(--gris); font-size: 1.15rem; max-width: 520px; margin-bottom: 32px; }
    .hero-botones { display: flex; flex-wrap: wrap; gap: 14px; }
    .hero-datos { display: flex; gap: 34px; margin-top: 40px; flex-wrap: wrap; }
    .hero-datos strong { display: block; font-size: 1.5rem; color: var(--naranja); }
    .hero-datos small { color: var(--gris); }

    /* Ilustración: caja modular que "se expande" */
    .hero-visual { display: grid; place-items: center; }
    .caja-anim { width: min(100%, 420px); animation: flotar 5s ease-in-out infinite; }
    @keyframes flotar { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-14px); } }
    .modulo-extra { animation: expandir 4s ease-in-out infinite; transform-origin: center; }
    @keyframes expandir { 0%, 100% { opacity: .35; transform: translateX(-10px); } 50% { opacity: 1; transform: translateX(0); } }

    /* =====================================================
       5. BENEFICIOS
       ===================================================== */
    .beneficios { background: var(--gris-claro); }
    .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 28px; margin-top: 50px; }

    .tarjeta {
      background: var(--blanco);
      padding: 36px 30px;
      border-radius: var(--radio);
      box-shadow: var(--sombra);
      transition: transform .3s ease, box-shadow .3s ease;
      border-bottom: 4px solid transparent;
    }
    .tarjeta:hover { transform: translateY(-8px); border-bottom-color: var(--naranja); box-shadow: 0 16px 40px rgba(255, 107, 0, .15); }
    .tarjeta-icono {
      width: 62px; height: 62px; border-radius: 16px;
      background: var(--naranja-suave); color: var(--naranja);
      display: grid; place-items: center; margin-bottom: 22px;
    }
    .tarjeta h3 { font-size: 1.25rem; margin-bottom: 10px; }
    .tarjeta p { color: var(--gris); font-size: .98rem; }

    /* =====================================================
       6. SOBRE NOSOTROS
       ===================================================== */
    .nosotros-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: center; }
    .nosotros-visual {
      background: var(--naranja); border-radius: 28px; padding: 40px;
      color: var(--blanco); position: relative; overflow: hidden;
    }
    .nosotros-visual::after {
      content: ''; position: absolute; width: 220px; height: 220px; border-radius: 50%;
      background: rgba(255, 255, 255, .12); right: -60px; bottom: -60px;
    }
    .nosotros-visual h3 { font-size: 1.6rem; margin-bottom: 12px; position: relative; z-index: 1; }
    .nosotros-visual p { position: relative; z-index: 1; opacity: .95; }
    .nosotros-texto p { color: var(--gris); margin: 16px 0; }
    .lista-check li { display: flex; gap: 12px; margin-bottom: 12px; font-weight: 500; }
    .lista-check svg { flex-shrink: 0; color: var(--naranja); margin-top: 3px; }
    .publico { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 24px; }
    .publico span { background: var(--gris-claro); padding: 8px 18px; border-radius: 999px; font-weight: 600; font-size: .9rem; }

    /* =====================================================
       7. TESTIMONIOS
       ===================================================== */
    .testimonios { background: var(--gris-claro); }
    .testimonio { position: relative; }
    .estrellas { color: var(--naranja); letter-spacing: 3px; margin-bottom: 14px; font-size: 1.1rem; }
    .testimonio blockquote { color: var(--negro); font-style: italic; margin-bottom: 22px; }
    .autor { display: flex; align-items: center; gap: 14px; }
    .avatar {
      width: 48px; height: 48px; border-radius: 50%;
      background: var(--naranja); color: var(--blanco);
      display: grid; place-items: center; font-weight: 700;
    }
    .autor strong { display: block; line-height: 1.2; }
    .autor small { color: var(--gris); }

    /* =====================================================
       8. FORMULARIO DE CONTACTO
       ===================================================== */
    .contacto-grid { display: grid; grid-template-columns: .9fr 1.1fr; gap: 50px; align-items: start; }
    .contacto-info p { color: var(--gris); margin: 14px 0 26px; }
    .contacto-info li { display: flex; align-items: center; gap: 14px; margin-bottom: 16px; font-weight: 500; }
    .contacto-info li .tarjeta-icono { width: 46px; height: 46px; margin: 0; border-radius: 12px; }

    form {
      background: var(--blanco); padding: 36px; border-radius: 22px;
      box-shadow: var(--sombra); border: 1px solid #eee;
    }
    .campo { margin-bottom: 18px; }
    .campo label { display: block; font-weight: 600; font-size: .9rem; margin-bottom: 6px; }
    .campo input, .campo select, .campo textarea {
      width: 100%; padding: 13px 16px; border: 2px solid #e6e6e6; border-radius: 12px;
      font-family: inherit; font-size: 1rem; color: var(--negro); background: var(--blanco);
      transition: border-color .25s ease, box-shadow .25s ease;
    }
    .campo input:focus, .campo select:focus, .campo textarea:focus {
      outline: none; border-color: var(--naranja); box-shadow: 0 0 0 4px rgba(255, 107, 0, .15);
    }
    .campo textarea { resize: vertical; min-height: 110px; }
    .fila { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
    form .btn { width: 100%; }
    .nota-form { font-size: .82rem; color: var(--gris); text-align: center; margin-top: 12px; }
    .error { color: #c62828; font-size: .82rem; margin-top: 4px; display: none; }
    .campo.invalido input, .campo.invalido textarea { border-color: #c62828; }
    .campo.invalido .error { display: block; }

    /* =====================================================
       9. FOOTER
       ===================================================== */
    footer { background: var(--negro); color: #cfcfcf; padding: 60px 0 26px; }
    .footer-grid { display: grid; grid-template-columns: 1.4fr 1fr 1fr; gap: 40px; padding-bottom: 36px; border-bottom: 1px solid #2c2c2c; }
    footer .logo { color: var(--blanco); margin-bottom: 14px; }
    footer h4 { color: var(--blanco); margin-bottom: 16px; }
    footer li { margin-bottom: 10px; }
    footer a:hover { color: var(--naranja); }
    .redes { display: flex; gap: 12px; margin-top: 6px; }
    .redes a {
      width: 44px; height: 44px; border-radius: 50%; background: #242424;
      display: grid; place-items: center; color: var(--blanco);
      transition: background .25s ease, transform .25s ease;
    }
    .redes a:hover { background: var(--naranja); color: var(--blanco); transform: translateY(-4px); }
    .copy { text-align: center; padding-top: 24px; font-size: .85rem; }

    /* Botón flotante de WhatsApp */
    .wa-flotante {
      position: fixed; right: 20px; bottom: 20px; z-index: 99;
      width: 60px; height: 60px; border-radius: 50%;
      background: var(--whatsapp); color: var(--blanco);
      display: grid; place-items: center;
      box-shadow: 0 8px 24px rgba(37, 211, 102, .5);
      animation: pulso 2.4s infinite;
    }
    @keyframes pulso {
      0% { box-shadow: 0 0 0 0 rgba(37, 211, 102, .6); }
      70% { box-shadow: 0 0 0 18px rgba(37, 211, 102, 0); }
      100% { box-shadow: 0 0 0 0 rgba(37, 211, 102, 0); }
    }

    /* =====================================================
       10. RESPONSIVE (tablet y móvil)
       ===================================================== */
    @media (max-width: 900px) {
      section { padding: 70px 0; }
      .hero-grid, .nosotros-grid, .contacto-grid { grid-template-columns: 1fr; }
      .hero-visual { order: -1; }
      .caja-anim { width: min(70%, 300px); }
      .grid-3 { grid-template-columns: 1fr; }
      .footer-grid { grid-template-columns: 1fr; }

      .hamburguesa { display: block; }
      .menu {
        position: absolute; top: 72px; left: 0; width: 100%;
        background: var(--blanco); flex-direction: column; gap: 0;
        padding: 10px 0 24px; box-shadow: 0 12px 20px rgba(0, 0, 0, .08);
        max-height: 0; overflow: hidden; opacity: 0; pointer-events: none;
        transition: opacity .3s ease;
      }
      .menu.abierto { max-height: 500px; opacity: 1; pointer-events: auto; }
      .menu a:not(.btn) { padding: 14px 0; }
    }
    @media (max-width: 520px) {
      .fila { grid-template-columns: 1fr; gap: 0; }
      form { padding: 24px 20px; }
      .hero { padding-top: 120px; }
      .hero-botones .btn { width: 100%; }
    }
  </style>
</head>

<body>

  <!-- ===================== NAVEGACIÓN ===================== -->
  <header id="header">
    <div class="container nav">
      <a href="#inicio" class="logo" aria-label="ModuBox inicio">
        <span class="logo-icono">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2.4" stroke-linejoin="round"><path d="M12 2 3 7v10l9 5 9-5V7l-9-5Z"/><path d="m3 7 9 5 9-5M12 12v10"/></svg>
        </span>
        Modu<span>Box</span>
      </a>

      <button class="hamburguesa" id="hamburguesa" aria-label="Abrir menú" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>

      <nav class="menu" id="menu">
        <a href="#beneficios">Beneficios</a>
        <a href="#nosotros">Nosotros</a>
        <a href="#testimonios">Testimonios</a>
        <a href="#contacto">Contacto</a>
        <a href="#contacto" class="btn btn-primario">Cotizar</a>
      </nav>
    </div>
  </header>

  <main>

    <!-- ===================== 1. HERO ===================== -->
    <section class="hero" id="inicio">
      <div class="container hero-grid">
        <div class="reveal">
          <span class="etiqueta">📦 Hecho en México</span>
          <h1>Cajas modulares que <span>crecen contigo</span></h1>
          <p>
            En ModuBox creamos cajas modulares expandibles para guardar, transportar y organizar
            lo que necesites. Más espacio cuando lo ocupas, menos cuando no.
          </p>
          <div class="hero-botones">
            <!-- El enlace de WhatsApp se asigna desde JavaScript (ver CONFIG) -->
            <a href="#" class="btn btn-primario js-whatsapp" target="_blank" rel="noopener">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M20.5 3.5A11.9 11.9 0 0 0 12 0C5.4 0 .1 5.3.1 11.9c0 2.1.6 4.1 1.6 5.9L0 24l6.4-1.7a11.9 11.9 0 0 0 5.6 1.4c6.6 0 11.9-5.3 11.9-11.9 0-3.2-1.2-6.200-3.4-8.300ZM12 21.700c-1.800 0-3.500-.5-5-1.400l-.4-.2-3.800 1 1-3.700-.2-.4a9.800 9.800 0 0 1-1.500-5.200c0-5.400 4.400-9.800 9.900-9.800 2.600 0 5.100 1 6.900 2.900a9.700 9.700 0 0 1 2.900 6.900c0 5.400-4.400 9.900-9.800 9.900Zm5.400-7.400c-.3-.1-1.800-.9-2-1-.3-.1-.5-.1-.7.100l-1 1.200c-.2.200-.4.200-.7.100-.3-.1-1.200-.4-2.300-1.400-.9-.8-1.400-1.700-1.600-2-.2-.3 0-.5.100-.6l.5-.5c.1-.2.200-.3.300-.5.100-.2 0-.4 0-.5l-.9-2.200c-.2-.6-.5-.5-.7-.5h-.6c-.2 0-.5.100-.8.400-.3.300-1 1-1 2.500s1.100 2.900 1.200 3.100c.1.200 2.100 3.200 5.100 4.500.7.300 1.300.5 1.700.6.700.2 1.400.2 1.900.1.600-.1 1.800-.7 2-1.400.3-.7.300-1.300.2-1.400-.1-.1-.3-.2-.6-.3Z"/></svg>
              Cotizar por WhatsApp
            </a>
            <a href="#beneficios" class="btn btn-secundario">Ver beneficios</a>
          </div>
          <div class="hero-datos">
            <div><strong>100%</strong><small>Fabricación nacional</small></div>
            <div><strong>Modular</strong><small>Se adapta a tu espacio</small></div>
            <div><strong>Envíos</strong><small>A todo México</small></div>
          </div>
        </div>

        <!-- Ilustración SVG de una caja que se expande -->
        <div class="hero-visual reveal delay-2">
          <svg class="caja-anim" viewBox="0 0 400 360" fill="none" aria-label="Caja modular expandible">
            <ellipse cx="200" cy="325" rx="150" ry="16" fill="#000" opacity=".07"/>
            <!-- Módulo base -->
            <path d="M120 130 200 90l80 40v100l-80 40-80-40V130Z" fill="#FF6B00"/>
            <path d="M120 130 200 170l80-40" stroke="#fff" stroke-width="3" stroke-linejoin="round"/>
            <path d="M200 170v100" stroke="#fff" stroke-width="3"/>
            <path d="M120 130 200 170v100l-80-40V130Z" fill="#E05A00"/>
            <!-- Módulo extra que aparece (expansión) -->
            <g class="modulo-extra">
              <path d="M290 100 350 70l40 20v80l-40 20-60-30v-60Z" fill="#111" opacity=".92"/>
              <path d="M290 100 350 130l40-20" stroke="#fff" stroke-width="2.5" stroke-linejoin="round"/>
              <path d="M350 130v60" stroke="#fff" stroke-width="2.5"/>
            </g>
            <!-- Flechas de expansión -->
            <path d="M296 215h50m0 0-9-9m9 9-9 9" stroke="#FF6B00" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
            <!-- Asa -->
            <rect x="178" y="206" width="44" height="8" rx="4" fill="#fff"/>
          </svg>
        </div>
      </div>
    </section>

    <!-- ===================== 2. BENEFICIOS ===================== -->
    <section class="beneficios" id="beneficios">
      <div class="container">
        <div class="centrado reveal">
          <span class="etiqueta">¿Por qué ModuBox?</span>
          <h2 class="titulo-seccion">Pensadas para <span>facilitarte la vida</span></h2>
          <p class="subtitulo-seccion">Una solución práctica para guardar y transportar, sin importar si es para tu casa o tu negocio.</p>
        </div>

        <div class="grid-3">
          <!-- Beneficio 1 -->
          <article class="tarjeta reveal">
            <div class="tarjeta-icono">
              <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 3h6v6M9 21H3v-6M21 3l-7 7M3 21l7-7"/></svg>
            </div>
            <h3>Expandibles</h3>
            <p>Crecen o se reducen según lo que necesites guardar. Un solo producto para distintas situaciones.</p>
          </article>

          <!-- Beneficio 2 -->
          <article class="tarjeta reveal delay-1">
            <div class="tarjeta-icono">
              <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
            </div>
            <h3>Modulares</h3>
            <p>Combina y apila módulos a tu medida. Organiza tu hogar, bodega o negocio de forma ordenada.</p>
          </article>

          <!-- Beneficio 3 -->
          <article class="tarjeta reveal delay-2">
            <div class="tarjeta-icono">
              <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2 4 5v6c0 5 3.400 9.300 8 11 4.600-1.700 8-6 8-11V5l-8-3Z"/><path d="m9 12 2 2 4-4"/></svg>
            </div>
            <h3>Resistentes y hechas en México</h3>
            <p>Fabricadas en el país, con atención directa y cercana para empresas, familias y comerciantes.</p>
          </article>
        </div>
      </div>
    </section>

    <!-- ===================== 3. SOBRE NOSOTROS ===================== -->
    <section id="nosotros">
      <div class="container nosotros-grid">
        <div class="nosotros-visual reveal">
          <h3>Somos ModuBox</h3>
          <p>Una empresa mexicana dedicada a crear cajas modulares expandibles que se adaptan a tu espacio y a tu forma de trabajar.</p>
        </div>

        <div class="nosotros-texto reveal delay-1">
          <span class="etiqueta">Sobre nosotros</span>
          <h2 class="titulo-seccion">Soluciones de almacenaje <span>flexibles</span></h2>
          <p>
            Nacimos para resolver un problema común: cada quien necesita guardar o mover cosas de
            distintos tamaños. Por eso diseñamos cajas que se expanden y se combinan, para que
            no tengas que comprar algo nuevo cada vez que cambian tus necesidades.
          </p>
          <ul class="lista-check">
            <li>
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m5 12 5 5 9-10"/></svg>
              Diseño propio, fabricado en México
            </li>
            <li>
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m5 12 5 5 9-10"/></svg>
              Atención personalizada por WhatsApp
            </li>
            <li>
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m5 12 5 5 9-10"/></svg>
              Opciones para uso personal y comercial
            </li>
          </ul>
          <div class="publico">
            <span>🏢 Empresas</span>
            <span>🏠 Familias</span>
            <span>🛒 Comerciantes</span>
          </div>
        </div>
      </div>
    </section>

    <!-- ===================== 4. TESTIMONIOS =====================
         IMPORTANTE: los textos de abajo son EJEMPLOS.
         Reemplázalos con opiniones reales de tus clientes
         (con su permiso) antes de publicar la página. -->
    <section class="testimonios" id="testimonios">
      <div class="container">
        <div class="centrado reveal">
          <span class="etiqueta">Testimonios</span>
          <h2 class="titulo-seccion">Lo que dicen <span>nuestros clientes</span></h2>
        </div>

        <div class="grid-3">
          <article class="tarjeta testimonio reveal">
            <div class="estrellas" aria-label="5 estrellas">★★★★★</div>
            <blockquote>“Escribe aquí el comentario real de un cliente sobre su experiencia con ModuBox.”</blockquote>
            <div class="autor">
              <div class="avatar">N</div>
              <div><strong>Nombre del cliente</strong><small>Empresa · Ciudad</small></div>
            </div>
          </article>

          <article class="tarjeta testimonio reveal delay-1">
            <div class="estrellas" aria-label="5 estrellas">★★★★★</div>
            <blockquote>“Escribe aquí el comentario real de una familia que usa tus cajas.”</blockquote>
            <div class="autor">
              <div class="avatar">N</div>
              <div><strong>Nombre del cliente</strong><small>Familia · Ciudad</small></div>
            </div>
          </article>

          <article class="tarjeta testimonio reveal delay-2">
            <div class="estrellas" aria-label="5 estrellas">★★★★★</div>
            <blockquote>“Escribe aquí el comentario real de un comerciante satisfecho.”</blockquote>
            <div class="autor">
              <div class="avatar">N</div>
              <div><strong>Nombre del cliente</strong><small>Comerciante · Ciudad</small></div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- ===================== 5. CONTACTO ===================== -->
    <section id="contacto">
      <div class="container contacto-grid">
        <div class="contacto-info reveal">
          <span class="etiqueta">Contacto</span>
          <h2 class="titulo-seccion">Cotiza tu <span>ModuBox</span> hoy</h2>
          <p>Cuéntanos qué necesitas y te respondemos por WhatsApp con una propuesta a tu medida.</p>
          <ul>
            <li>
              <span class="tarjeta-icono">
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2Z"/></svg>
              </span>
              Respuesta rápida por WhatsApp
            </li>
            <li>
              <span class="tarjeta-icono">
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M1 3h15v13H1zM16 8h4l3 3v5h-7z"/><circle cx="5.500" cy="18.500" r="2"/><circle cx="18.500" cy="18.500" r="2"/></svg>
              </span>
              Envíos a toda la República
            </li>
          </ul>
        </div>

        <!-- El formulario NO envía datos a un servidor: arma un mensaje y abre WhatsApp -->
        <form id="formulario" class="reveal delay-1" novalidate>
          <div class="fila">
            <div class="campo">
              <label for="nombre">Nombre</label>
              <input type="text" id="nombre" name="nombre" placeholder="Tu nombre" required>
              <div class="error">Escribe tu nombre.</div>
            </div>
            <div class="campo">
              <label for="telefono">Teléfono</label>
              <input type="tel" id="telefono" name="telefono" placeholder="10 dígitos" required>
              <div class="error">Escribe un teléfono válido (10 dígitos).</div>
            </div>
          </div>

          <div class="campo">
            <label for="tipo">Soy...</label>
            <select id="tipo" name="tipo">
              <option>Empresa</option>
              <option>Familia</option>
              <option>Comerciante</option>
            </select>
          </div>

          <div class="campo">
            <label for="mensaje">¿Qué necesitas?</label>
            <textarea id="mensaje" name="mensaje" placeholder="Cuéntanos cuántas cajas necesitas, para qué las usarás, tu ciudad..." required></textarea>
            <div class="error">Cuéntanos brevemente qué necesitas.</div>
          </div>

          <button type="submit" class="btn btn-whatsapp">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="m22 2-7 20-4-9-9-4 20-7Z"/></svg>
            Enviar por WhatsApp
          </button>
          <p class="nota-form">Al enviar, se abrirá WhatsApp con tu mensaje listo.</p>
        </form>
      </div>
    </section>

  </main>

  <!-- ===================== 6. FOOTER ===================== -->
  <footer>
    <div class="container">
      <div class="footer-grid">
        <div>
          <a href="#inicio" class="logo">Modu<span>Box</span></a>
          <p>Cajas modulares expandibles hechas en México para empresas, familias y comerciantes.</p>
        </div>

        <div>
          <h4>Navegación</h4>
          <ul>
            <li><a href="#beneficios">Beneficios</a></li>
            <li><a href="#nosotros">Nosotros</a></li>
            <li><a href="#testimonios">Testimonios</a></li>
            <li><a href="#contacto">Contacto</a></li>
          </ul>
        </div>

        <div>
          <h4>Síguenos</h4>
          <!-- Cambia los href por los enlaces reales de tus redes -->
          <div class="redes">
            <a href="https://facebook.com/" target="_blank" rel="noopener" aria-label="Facebook">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M13.500 22v-8h2.700l.5-3.300h-3.200V8.600c0-.9.400-1.700 1.800-1.700h1.500V4.100S15.500 3.900 14.200 3.900c-2.700 0-4.400 1.600-4.400 4.500v2.300H7v3.300h2.800v8h3.700Z"/></svg>
            </a>
            <a href="https://instagram.com/" target="_blank" rel="noopener" aria-label="Instagram">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.500" cy="6.500" r="1" fill="currentColor"/></svg>
            </a>
            <a href="https://tiktok.com/" target="_blank" rel="noopener" aria-label="TikTok">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M16.600 2h-3.200v13.200a2.800 2.800 0 1 1-2.800-2.800c.3 0 .6 0 .8.100V9.200a6 6 0 1 0 5.200 5.900V8.500a7 7 0 0 0 4 1.300V6.600a4 4 0 0 1-4-4.600Z"/></svg>
            </a>
            <a href="#" class="js-whatsapp" target="_blank" rel="noopener" aria-label="WhatsApp">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M20.500 3.500A11.900 11.900 0 0 0 12 0C5.400 0 .1 5.300.1 11.900c0 2.100.6 4.100 1.600 5.900L0 24l6.400-1.700a11.900 11.900 0 0 0 5.600 1.400c6.600 0 11.900-5.300 11.900-11.900 0-3.200-1.200-6.200-3.400-8.300Z"/></svg>
            </a>
          </div>
        </div>
      </div>
      <p class="copy">© <span id="anio"></span> ModuBox. Todos los derechos reservados.</p>
    </div>
  </footer>

  <!-- Botón flotante de WhatsApp -->
  <a href="#" class="wa-flotante js-whatsapp" target="_blank" rel="noopener" aria-label="Escríbenos por WhatsApp">
    <svg width="30" height="30" viewBox="0 0 24 24" fill="currentColor"><path d="M20.500 3.500A11.900 11.900 0 0 0 12 0C5.400 0 .1 5.300.1 11.900c0 2.100.6 4.100 1.600 5.900L0 24l6.400-1.700a11.900 11.900 0 0 0 5.600 1.400c6.600 0 11.900-5.300 11.900-11.900 0-3.200-1.200-6.200-3.400-8.300Z"/></svg>
  </a>

  <script>
    /* =====================================================
       CONFIGURACIÓN — EDITA SOLO ESTAS DOS LÍNEAS
       ===================================================== */
    const CONFIG = {
      // Número con código de país, SIN signos ni espacios. México = 52
      // Ejemplo: 52 + 477 + 123 4567  →  '524771234567'
      whatsapp: '520000000000',
      // Mensaje que aparece al hacer clic en los botones de WhatsApp
      mensajeInicial: 'Hola, me interesa cotizar cajas modulares ModuBox.'
    };

    /* =====================================================
       1. Enlaces de WhatsApp
       Todos los elementos con clase .js-whatsapp abren el chat
       ===================================================== */
    const enlaceWA = (texto) =>
      `https://wa.me/${CONFIG.whatsapp}?text=${encodeURIComponent(texto)}`;

    document.querySelectorAll('.js-whatsapp').forEach((el) => {
      el.href = enlaceWA(CONFIG.mensajeInicial);
    });

    /* =====================================================
       2. Animaciones al hacer scroll (IntersectionObserver)
       Agrega la clase "visible" cuando el elemento entra en pantalla
       ===================================================== */
    const observador = new IntersectionObserver((entradas) => {
      entradas.forEach((entrada) => {
        if (entrada.isIntersecting) {
          entrada.target.classList.add('visible');
          observador.unobserve(entrada.target); // solo se anima una vez
        }
      });
    }, { threshold: 0.15 });

    document.querySelectorAll('.reveal').forEach((el) => observador.observe(el));

    /* =====================================================
       3. Menú móvil (hamburguesa)
       ===================================================== */
    const botonMenu = document.getElementById('hamburguesa');
    const menu = document.getElementById('menu');

    botonMenu.addEventListener('click', () => {
      const abierto = menu.classList.toggle('abierto');
      botonMenu.classList.toggle('abierto', abierto);
      botonMenu.setAttribute('aria-expanded', abierto);
    });

    // Cierra el menú al elegir una opción
    menu.querySelectorAll('a').forEach((enlace) => {
      enlace.addEventListener('click', () => {
        menu.classList.remove('abierto');
        botonMenu.classList.remove('abierto');
        botonMenu.setAttribute('aria-expanded', false);
      });
    });

    /* =====================================================
       4. Sombra en la barra al bajar
       ===================================================== */
    const header = document.getElementById('header');
    window.addEventListener('scroll', () => {
      header.classList.toggle('scrolled', window.scrollY > 10);
    }, { passive: true });

    /* =====================================================
       5. Formulario: valida y abre WhatsApp con el mensaje
       ===================================================== */
    const formulario = document.getElementById('formulario');

    // Marca un campo como válido o inválido
    function validar(campo, esValido) {
      campo.closest('.campo').classList.toggle('invalido', !esValido);
      return esValido;
    }

    formulario.addEventListener('submit', (e) => {
      e.preventDefault();

      const nombre = formulario.nombre;
      const telefono = formulario.telefono;
      const mensaje = formulario.mensaje;

      const telefonoLimpio = telefono.value.replace(/\D/g, '');

      const okNombre = validar(nombre, nombre.value.trim().length >= 2);
      const okTel = validar(telefono, telefonoLimpio.length >= 10);
      const okMsg = validar(mensaje, mensaje.value.trim().length >= 5);

      if (!(okNombre && okTel && okMsg)) return;

      // Arma el mensaje que llegará a tu WhatsApp
      const texto =
        `Hola, soy ${nombre.value.trim()} (${formulario.tipo.value}).\n` +
        `Teléfono: ${telefono.value.trim()}\n` +
        `Necesito: ${mensaje.value.trim()}`;

      window.open(enlaceWA(texto), '_blank', 'noopener');
      formulario.reset();
    });

    // Quita el error en cuanto la persona vuelve a escribir
    formulario.querySelectorAll('input, textarea').forEach((campo) => {
      campo.addEventListener('input', () => campo.closest('.campo').classList.remove('invalido'));
    });

    /* =====================================================
       6. Año automático en el footer
       ===================================================== */
    document.getElementById('anio').textContent = new Date().getFullYear();
  </script>
</body>
</html>

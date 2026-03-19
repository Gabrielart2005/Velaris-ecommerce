<template>
  <footer class="footer">
    <div class="footer-inner">

      <!-- Brand Column -->
      <div class="footer-brand">
        <a href="/" class="footer-logo">VELARIS</a>
        <p class="footer-tagline">ELEVANDO LO COTIDIANO A <br> TRAVÉS DE UN PRISMA DE LUJO Y MISTERIO</p>
        <div class="footer-socials">
          <a href="#" aria-label="Instagram" class="social-link">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17.5" cy="6.5" r="0.5" fill="currentColor" stroke="none"/>
            </svg>
          </a>
          <a href="#" aria-label="Pinterest" class="social-link">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M12 2C6.477 2 2 6.477 2 12c0 4.236 2.636 7.855 6.356 9.312-.088-.791-.167-2.005.035-2.868.181-.78 1.172-4.97 1.172-4.97s-.299-.598-.299-1.482c0-1.388.806-2.428 1.808-2.428.852 0 1.265.64 1.265 1.408 0 .858-.546 2.14-.828 3.33-.236.995.499 1.806 1.48 1.806 1.773 0 3.14-1.869 3.14-4.573 0-2.39-1.717-4.061-4.168-4.061-2.837 0-4.502 2.128-4.502 4.328 0 .856.33 1.775.741 2.277a.3.3 0 0 1 .069.284c-.076.312-.243.995-.276 1.134-.044.183-.145.222-.335.134-1.249-.581-2.03-2.407-2.03-3.874 0-3.154 2.292-6.052 6.608-6.052 3.469 0 6.165 2.473 6.165 5.776 0 3.447-2.173 6.22-5.19 6.22-1.013 0-1.966-.527-2.292-1.148l-.623 2.378c-.226.869-.835 1.958-1.244 2.621.937.29 1.931.446 2.962.446 5.523 0 10-4.477 10-10S17.523 2 12 2z"/>
            </svg>
          </a>
          <a href="#" aria-label="TikTok" class="social-link">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M9 12a4 4 0 1 0 4 4V4a5 5 0 0 0 5 5"/>
            </svg>
          </a>
        </div>
      </div>

      <!-- Nav Columns -->
      <div class="footer-nav">
        <div class="footer-col">
          <h4 class="footer-col-title">Explorar</h4>
          <ul>
            <li><a href="#tienda">Tienda</a></li>
            <li><a href="#coleccion">Colección</a></li>
            <li><a href="#compania">Compañía</a></li>
            <li><a href="#">Lookbook</a></li>
          </ul>
        </div>

        <div class="footer-col">
          <h4 class="footer-col-title">Soporte</h4>
          <ul>
            <li><a href="#">Guía de Tallas</a></li>
            <li><a href="#">Envíos y Devoluciones</a></li>
            <li><a href="#">Preguntas Frecuentes</a></li>
            <li><a href="#">Contacto</a></li>
          </ul>
        </div>

        <div class="footer-col">
          <h4 class="footer-col-title">Novedades</h4>
          <p class="footer-newsletter-text">RECIBE LAS ÚLTIMAS NOVEDADES.</p>
          <form class="footer-form" @submit.prevent>
            <input
              type="email"
              placeholder="tu@email.com"
              class="footer-input"
              aria-label="Email para newsletter"
            />
            <button type="submit" class="footer-btn">→</button>
          </form>
        </div>
      </div>

    </div>

    <!-- Bottom bar -->
    <div class="footer-bottom">
      <p class="footer-copy">© {{ currentYear }} VELARIS. TODOS LOS DERECHOS RESERVADOS.</p>
      <div class="footer-legal">
        <a href="#">Política de Privacidad</a>
        <span class="footer-divider">·</span>
        <a href="#">Términos y Condiciones</a>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  background: linear-gradient(to bottom, #919191, #313131);
  color: #f8f8f8;
  padding: 80px 5% 0;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
}

/* ── Inner layout ──────────────────────────────────────── */
.footer-inner {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 60px;
  padding-bottom: 50px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.226);
}

/* ── Brand ─────────────────────────────────────────────── */
.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.footer-logo {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.6rem;
  font-weight: 400;
  letter-spacing: 0.35em;
  color: #fff;
  text-decoration: none;
  transition: opacity 0.3s ease;
}

.footer-logo:hover {
  opacity: 0.7;
}

.footer-tagline {
  font-size: 0.72rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.507);
  margin: 0;
  letter-spacing: 0.05em;
}

/* Socials */
.footer-socials {
  display: flex;
  gap: 16px;
}

.social-link {
  color: rgba(255, 255, 255, 0.514);
  display: flex;
  align-items: center;
  transition: color 0.3s ease;
}

.social-link:hover {
  color: #fff;
}

/* ── Nav columns ───────────────────────────────────────── */
.footer-nav {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
}

.footer-col-title {
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: #fff;
  margin: 0 0 20px;
}

.footer-col ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.footer-col ul a {
  color: rgba(255, 255, 255, 0.493);
  text-decoration: none;
  text-transform: uppercase;
  font-size: 0.7rem;
  letter-spacing: 0.12em;
  transition: color 0.3s ease;
  position: relative;
}

.footer-col ul a::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 1px;
  background: rgba(255, 255, 255, 0.5);
  transition: width 0.3s ease;
}

.footer-col ul a:hover {
  color: #fff;
}

.footer-col ul a:hover::after {
  width: 100%;
}

/* Newsletter */
.footer-newsletter-text {
  margin: 0 0 16px;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.45);
  font-size: 0.7rem;
  letter-spacing: 0.05em;
  
}

.footer-form {
  display: flex;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  transition: border-color 0.3s ease;
}

.footer-form:focus-within {
  border-color: rgba(255, 255, 255, 0.6);
}

.footer-input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  color: #fff;
  font-size: 0.7rem;
  letter-spacing: 0.1em;
  padding: 8px 0;
}

.footer-input::placeholder {
  color: rgba(255, 255, 255, 0.25);
}

.footer-btn {
  background: none;
  border: none;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.5);
  font-size: 1.1rem;
  padding: 0 4px;
  transition: color 0.3s ease, transform 0.3s ease;
}

.footer-btn:hover {
  color: #fff;
  transform: translateX(3px);
}

/* ── Bottom bar ────────────────────────────────────────── */
.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px 0;
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.25);
}

.footer-copy { margin: 0; }

.footer-legal {
  display: flex;
  align-items: center;
  gap: 12px;
}

.footer-legal a {
  color: rgba(255, 255, 255, 0.25);
  text-decoration: none;
  text-transform: uppercase;
  transition: color 0.3s ease;
}

.footer-legal a:hover {
  color: rgba(255, 255, 255, 0.7);
}

.footer-divider {
  opacity: 0.4;
}

/* ── Responsive ────────────────────────────────────────── */
@media (max-width: 900px) {
  .footer-inner {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .footer-nav {
    grid-template-columns: repeat(2, 1fr);
    gap: 30px;
  }
}

@media (max-width: 600px) {
  .footer {
    padding: 60px 5% 0;
  }

  .footer-nav {
    grid-template-columns: 1fr;
  }

  .footer-bottom {
    flex-direction: column;
    gap: 12px;
    text-align: center;
  }
}
</style>

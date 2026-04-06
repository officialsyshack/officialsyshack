<template>
  <div class="store-wrapper">

    <div class="scanlines"></div>

    <!-- NAV -->
    <nav class="nav">
      <div class="nav-inner">
        <div class="logo">
          <span class="logo-sys">Sys</span><span class="logo-hack">Hack</span>
        </div>
        <a class="yt-btn mono" href="https://www.youtube.com/@SysHackkk" target="_blank">
          ▶ Subscribe on YouTube
        </a>
      </div>
    </nav>

    <!-- HERO -->
    <header class="hero">
      <div class="hero-bg-circle"></div>
      <div class="hero-bg-circle hero-bg-circle--2"></div>
      <div class="container">
        <div class="badge mono">👉 Simple Digital Toolkit · By SysHack</div>
        <h1 class="hero-title bebas">
          Hack The System.<br/>
          <span class="neon-text">Take Control.</span>
        </h1>
        <p class="hero-sub">
          One-click scripts &amp; packs from the SysHack channel — doing what Windows should've done from day one.
          No bloat. No BS. Just results.
        </p>
        <div class="hero-cta-row">
          <a class="btn-yt" href="https://www.youtube.com/@SysHackkk" target="_blank">▶ Watch on YouTube · 12.3K Subs</a>
          <a class="btn-discord" href="https://discord.com/invite/MzUd6TUuWT" target="_blank">💬 Join Discord</a>
        </div>
        <div class="hero-stats">
          <div class="stat">
            <span class="stat-num neon-text">2400+</span>
            <span class="stat-label mono">happy users</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-num neon-text">6</span>
            <span class="stat-label mono">tools available</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-num neon-text">$15</span>
            <span class="stat-label mono">max price</span>
          </div>
        </div>
      </div>
    </header>

    <!-- PRODUCTS GRID -->
    <section class="products">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title bebas">Pick Your <span class="neon-text">Toolkit</span></h2>
          <p class="section-sub mono">All scripts tested on Windows 10 &amp; 11</p>
        </div>
        <div class="products-grid">
          <div
            v-for="product in products"
            :key="product.id"
            class="product-card"
            :class="{ 'product-card--featured': product.featured }"
          >
            <div v-if="product.featured" class="featured-badge mono">⚡ BEST SELLER</div>
            <div class="product-icon">{{ product.icon }}</div>
            <h3 class="product-name">{{ product.name }}</h3>
            <p class="product-desc">{{ product.desc }}</p>
            <ul class="product-features">
              <li v-for="f in product.features" :key="f" class="feature-item">
                <span class="feature-check neon-text">✓</span> {{ f }}
              </li>
            </ul>
            <div class="product-footer">
              <div class="price-block">
                <span class="price-label mono">only</span>
                <span class="price neon-text bebas">${{ product.price }}</span>
              </div>
              <button class="btn-buy" @click="openPayment(product)">Get It →</button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- HOW IT WORKS -->
    <section class="how-it-works">
      <div class="container">
        <h2 class="section-title bebas text-center">How It <span class="neon-text">Works</span></h2>
        <div class="steps-row">
          <div v-for="(step, i) in steps" :key="i" class="step">
            <div class="step-num mono neon-text">0{{ i + 1 }}</div>
            <div class="step-icon">{{ step.icon }}</div>
            <div class="step-title">{{ step.title }}</div>
            <div class="step-desc">{{ step.desc }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- TRUST STRIP -->
    <section class="trust-strip">
      <div class="container">
        <div class="trust-items">
          <div v-for="t in trust" :key="t.label" class="trust-item">
            <span class="trust-icon">{{ t.icon }}</span>
            <span class="trust-label mono">{{ t.label }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="container">
        <div class="footer-logo bebas"><span class="logo-sys">Sys</span><span class="neon-text">Hack</span></div>
        <p class="footer-sub mono">Hack The System. Take Control.</p>
        <div class="footer-links">
          <a href="https://www.youtube.com/@SysHackkk" target="_blank" class="footer-link mono">▶ YouTube</a>
          <a href="https://discord.com/invite/MzUd6TUuWT" target="_blank" class="footer-link mono">💬 Discord</a>
        </div>
        <p class="footer-copy mono">© 2025 SysHack · All rights reserved</p>
      </div>
    </footer>

    <!-- ========== PAYMENT MODAL ========== -->
    <transition name="modal-fade">
      <div v-if="modalOpen" class="modal-overlay" @click.self="closeModal">
        <div class="modal">

          <!-- STEP 1: Choose payment method -->
          <div v-if="step === 1">
            <button class="modal-close" @click="closeModal">✕</button>
            <div class="modal-tag mono neon-text">STEP 1 OF 3 · SELECT METHOD</div>
            <h2 class="modal-title bebas">Choose How To <span class="neon-text">Pay</span></h2>
            <div class="selected-product-pill mono">
              {{ selectedProduct && selectedProduct.icon }} {{ selectedProduct && selectedProduct.name }}
              <span class="neon-text bebas">&nbsp;${{ selectedProduct && selectedProduct.price }}</span>
            </div>

            <div class="payment-options">
              <button class="pay-option" :class="{ active: payMethod === 'paypal' }" @click="payMethod = 'paypal'">
                <span class="pay-icon">🅿️</span>
                <div class="pay-info">
                  <div class="pay-name">PayPal</div>
                  <div class="pay-detail mono">Send to: nerishmelissa3@gmail.com</div>
                </div>
                <span v-if="payMethod === 'paypal'" class="pay-check neon-text">✓</span>
              </button>

              <button class="pay-option" :class="{ active: payMethod === 'wise' }" @click="payMethod = 'wise'">
                <span class="pay-icon">💸</span>
                <div class="pay-info">
                  <div class="pay-name">Wise</div>
                  <div class="pay-detail mono">Send to: officialsyshack@gmail.com</div>
                </div>
                <span v-if="payMethod === 'wise'" class="pay-check neon-text">✓</span>
              </button>
            </div>

            <button class="btn-next" :disabled="!payMethod" @click="step = 2">
              Continue →
            </button>
          </div>

          <!-- STEP 2: Payment instructions -->
          <div v-if="step === 2">
            <button class="modal-close" @click="closeModal">✕</button>
            <div class="modal-tag mono neon-text">STEP 2 OF 3 · SEND PAYMENT</div>
            <h2 class="modal-title bebas">Send <span class="neon-text">${{ selectedProduct && selectedProduct.price }}</span> Now</h2>

            <!-- PayPal block -->
            <div v-if="payMethod === 'paypal'" class="instructions-box">
              <div class="instr-header mono">🅿️ PayPal — Step by step</div>
              <div class="instr-steps">
                <div class="instr-step"><span class="instr-num">1</span><span>Open PayPal and click <strong>"Send Money"</strong></span></div>
                <div class="instr-step"><span class="instr-num">2</span><span>Send exactly <strong class="neon-text">${{ selectedProduct && selectedProduct.price }} USD</strong> to this email:</span></div>
              </div>
              <div class="copy-box" @click="copy('nerishmelissa3@gmail.com')">
                <div class="copy-left">
                  <div class="copy-label mono">PayPal Email</div>
                  <div class="copy-value mono">nerishmelissa3@gmail.com</div>
                </div>
                <div class="copy-btn mono">{{ copied === 'paypal' ? '✓ Copied' : 'Copy' }}</div>
              </div>
              <div class="instr-steps">
                <div class="instr-step"><span class="instr-num">3</span><span>In the <strong>note/message</strong> field write: <em>SysHack – {{ selectedProduct && selectedProduct.name }}</em></span></div>
                <div class="instr-step"><span class="instr-num">4</span><span>Take a <strong>screenshot</strong> of the payment confirmation screen</span></div>
              </div>
            </div>

            <!-- Wise block -->
            <div v-if="payMethod === 'wise'" class="instructions-box">
              <div class="instr-header mono">💸 Wise — Step by step</div>
              <div class="instr-steps">
                <div class="instr-step"><span class="instr-num">1</span><span>Open Wise and click <strong>"Send money"</strong></span></div>
                <div class="instr-step"><span class="instr-num">2</span><span>Send exactly <strong class="neon-text">${{ selectedProduct && selectedProduct.price }} USD</strong> to this email:</span></div>
              </div>
              <div class="copy-box" @click="copy('wise')">
                <div class="copy-left">
                  <div class="copy-label mono">Wise Email</div>
                  <div class="copy-value mono">rewindgmail.com</div>
                </div>
                <div class="copy-btn mono">{{ copied === 'wise' ? '✓ Copied' : 'Copy' }}</div>
              </div>
              <div class="instr-steps">
                <div class="instr-step"><span class="instr-num">3</span><span>In the <strong>reference</strong> field write: <em>SysHack – {{ selectedProduct && selectedProduct.name }}</em></span></div>
                <div class="instr-step"><span class="instr-num">4</span><span>Take a <strong>screenshot</strong> of the payment confirmation screen</span></div>
              </div>
            </div>

            <div class="modal-btn-row">
              <button class="btn-back" @click="step = 1">← Back</button>
              <button class="btn-next" @click="step = 3">I've Paid →</button>
            </div>
          </div>

          <!-- STEP 3: Send proof -->
          <div v-if="step === 3">
            <button class="modal-close" @click="closeModal">✕</button>
            <div class="modal-tag mono neon-text">STEP 3 OF 3 · CONFIRM & RECEIVE</div>
            <h2 class="modal-title bebas">Email Your <span class="neon-text">Proof</span></h2>

            <div class="confirm-box">
              <p class="confirm-intro">Now email your payment screenshot to get your download link:</p>

              <div class="copy-box" @click="copy('gmail')">
                <div class="copy-left">
                  <div class="copy-label mono">📧 Send Email To</div>
                  <div class="copy-value mono">rewindgmail.com</div>
                </div>
                <div class="copy-btn mono">{{ copied === 'gmail' ? '✓ Copied' : 'Copy' }}</div>
              </div>

              <div class="confirm-checklist">
                <div class="check-item">
                  <span class="check-icon neon-text">✓</span>
                  <span><strong>Subject:</strong> SysHack Purchase – {{ selectedProduct && selectedProduct.name }}</span>
                </div>
                <div class="check-item">
                  <span class="check-icon neon-text">✓</span>
                  <span><strong>Attach:</strong> Screenshot of your payment confirmation</span>
                </div>
                <div class="check-item">
                  <span class="check-icon neon-text">✓</span>
                  <span><strong>Include:</strong> Your email address to receive the file</span>
                </div>
                <div class="check-item">
                  <span class="check-icon neon-text">⚡</span>
                  <span>You'll get your toolkit link within <strong>24 hours</strong></span>
                </div>
              </div>
            </div>

            <a
              :href="`mailto:rewindgmail.com?subject=SysHack%20Purchase%20%E2%80%93%20${encodeURIComponent(selectedProduct && selectedProduct.name)}&body=Hi%20SysHack!%0A%0AI%20just%20paid%20%24${selectedProduct && selectedProduct.price}%20via%20${payMethod === 'paypal' ? 'PayPal' : 'Wise'}%20for%3A%20${encodeURIComponent(selectedProduct && selectedProduct.name)}.%0A%0APayment%20screenshot%20attached.%0A%0ASend%20my%20file%20to%3A%20%5BYOUR%20EMAIL%5D%0A%0AThanks!`"
              class="btn-email-open"
            >
              📧 Open Email App
            </a>

            <button class="btn-done" @click="closeModal">✓ All done — Close</button>
          </div>

        </div>
      </div>
    </transition>

  </div>
</template>

<script>
export default {
  name: 'SysHackStore',
  data() {
    return {
      modalOpen: false,
      step: 1,
      payMethod: null,
      selectedProduct: null,
      copied: null,

      products: [
        {
          id: 1, icon: '🚀',
          name: 'Windows Performance Boost Pack',
          desc: 'Turbocharge your PC in under 60 seconds. Disables junk services, clears startup bloat, and optimizes memory.',
          features: ['Kills 20+ background processes', 'Speeds up boot time', 'Optimizes RAM & CPU usage', 'Fully reversible'],
          price: 9, featured: true,
        },
        {
          id: 2, icon: '🛡️',
          name: 'Privacy + Telemetry Killer Script',
          desc: 'Stop Microsoft from tracking everything you do. Kills all telemetry, tracking, and data collection permanently.',
          features: ['Blocks 50+ telemetry endpoints', 'Disables activity history', 'Stops Cortana data collection', 'Win 10 & 11'],
          price: 7, featured: false,
        },
        {
          id: 3, icon: '🔧',
          name: 'One-Click Windows Fix Toolkit',
          desc: 'The ultimate repair script. Fixes corrupt system files, resets Windows Update, and cleans errors automatically.',
          features: ['Auto-runs SFC + DISM repair', 'Resets Windows Update stack', 'Cleans temp & junk files', 'Fixes registry errors'],
          price: 12, featured: false,
        },
        {
          id: 4, icon: '⚙️',
          name: 'Debloat Windows Ultimate',
          desc: 'Rip out all the pre-installed garbage Microsoft shoves in. Clean slate, your rules.',
          features: ['Removes 40+ built-in apps', 'Strips Xbox, OneDrive bloat', 'Disables ads in Start Menu', 'Safe & selective'],
          price: 8, featured: false,
        },
        {
          id: 5, icon: '🌐',
          name: 'Network Speed Optimizer',
          desc: 'Squeeze every drop of speed from your connection. Tweaks TCP, DNS, and adapter settings automatically.',
          features: ['Optimizes TCP/IP stack', 'Sets fastest DNS automatically', 'Disables bandwidth throttling', 'Reduces ping'],
          price: 7, featured: false,
        },
        {
          id: 6, icon: '🎮',
          name: 'Gaming Mode Activator Pack',
          desc: 'Push your FPS and lower input lag — no third-party software needed.',
          features: ['Enables Windows Game Mode+', 'Disables power throttling', 'Optimizes GPU scheduling', 'Kills CPU hogs'],
          price: 10, featured: false,
        },
      ],

      steps: [
        { icon: '🛒', title: 'Pick a Toolkit', desc: 'Choose the script that fits your need.' },
        { icon: '💳', title: 'Pay via PayPal or Wise', desc: 'Send payment — takes under 2 minutes.' },
        { icon: '📧', title: 'Email Your Screenshot', desc: 'Send proof + your email to rewindgmail.com' },
        { icon: '✅', title: 'Receive Your File', desc: 'Get your toolkit download within 24 hours.' },
      ],

      trust: [
        { icon: '🔒', label: 'No malware, ever' },
        { icon: '📦', label: 'Fast delivery' },
        { icon: '↩️', label: 'Fully reversible' },
        { icon: '💬', label: 'Tested & verified' },
        { icon: '💰', label: 'Money-back guarantee' },
      ],
    };
  },
  methods: {
    openPayment(product) {
      this.selectedProduct = product;
      this.step = 1;
      this.payMethod = null;
      this.copied = null;
      this.modalOpen = true;
      document.body.style.overflow = 'hidden';
    },
    closeModal() {
      this.modalOpen = false;
      document.body.style.overflow = '';
    },
    copy(key) {
      const map = {
        paypal: 'nerishmelissa3@gmail.com',
        wise: 'rewindgmail.com',
        gmail: 'rewindgmail.com',
      };
      navigator.clipboard.writeText(map[key]).catch(() => {});
      this.copied = key;
      setTimeout(() => { this.copied = null; }, 2500);
    },
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&display=swap');

* { box-sizing: border-box; margin: 0; padding: 0; }

.store-wrapper {
  font-family: 'DM Sans', sans-serif;
  background: #060a0f;
  color: #dde8ef;
  min-height: 100vh;
  position: relative;
  overflow-x: hidden;
}
.store-wrapper::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(0,229,255,0.022) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,229,255,0.022) 1px, transparent 1px);
  background-size: 48px 48px;
  pointer-events: none;
  z-index: 0;
}
.scanlines {
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.1) 2px, rgba(0,0,0,0.1) 4px);
  pointer-events: none;
  z-index: 1;
}
.bebas { font-family: 'Bebas Neue', sans-serif; }
.mono  { font-family: 'Space Mono', monospace; }
.neon-text { color: #00e5ff; text-shadow: 0 0 14px rgba(0,229,255,0.55); }
.container { max-width: 1200px; margin: 0 auto; padding: 0 24px; position: relative; z-index: 2; }
.text-center { text-align: center; }

/* NAV */
.nav {
  border-bottom: 1px solid #1a2535;
  padding: 18px 0;
  position: sticky; top: 0;
  background: rgba(6,10,15,0.94);
  backdrop-filter: blur(16px);
  z-index: 100;
}
.nav-inner { max-width: 1200px; margin: 0 auto; padding: 0 24px; display: flex; align-items: center; justify-content: space-between; }
.logo { font-family: 'Bebas Neue', sans-serif; font-size: 1.7rem; letter-spacing: 0.06em; }
.logo-sys { color: #dde8ef; }
.logo-hack { color: #00e5ff; text-shadow: 0 0 16px rgba(0,229,255,0.6); }
.yt-btn { background: rgba(0,229,255,0.08); border: 1px solid rgba(0,229,255,0.22); color: #00e5ff; font-family: 'Space Mono', monospace; font-size: 0.68rem; padding: 8px 16px; border-radius: 100px; letter-spacing: 0.05em; text-decoration: none; transition: all 0.2s; }
.yt-btn:hover { background: rgba(0,229,255,0.14); }

/* HERO */
.hero { padding: 100px 0 80px; position: relative; overflow: hidden; }
.hero-bg-circle { position: absolute; width: 700px; height: 700px; border-radius: 50%; background: radial-gradient(circle, rgba(0,229,255,0.055) 0%, transparent 70%); top: -200px; left: -100px; pointer-events: none; }
.hero-bg-circle--2 { background: radial-gradient(circle, rgba(0,255,136,0.035) 0%, transparent 70%); top: auto; bottom: -200px; left: auto; right: -100px; }
.badge { display: inline-block; background: rgba(0,229,255,0.07); border: 1px solid rgba(0,229,255,0.22); color: #00e5ff; font-size: 0.72rem; padding: 8px 18px; border-radius: 100px; margin-bottom: 28px; letter-spacing: 0.05em; }
.hero-title { font-family: 'Bebas Neue', sans-serif; font-size: clamp(4rem, 10vw, 7.5rem); line-height: 0.93; margin-bottom: 28px; }
.hero-sub { font-size: 1.1rem; color: #5a7080; max-width: 520px; line-height: 1.7; margin-bottom: 36px; font-weight: 300; }
.hero-cta-row { display: flex; gap: 14px; flex-wrap: wrap; margin-bottom: 48px; }
.btn-yt { background: linear-gradient(135deg, #00e5ff, #00aacc); color: #020e12; font-family: 'Space Mono', monospace; font-size: 0.78rem; font-weight: 700; padding: 14px 28px; border-radius: 8px; text-decoration: none; letter-spacing: 0.04em; transition: all 0.2s; }
.btn-yt:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(0,229,255,0.3); }
.btn-discord { background: rgba(0,229,255,0.07); border: 1px solid rgba(0,229,255,0.25); color: #00e5ff; font-family: 'Space Mono', monospace; font-size: 0.78rem; padding: 14px 24px; border-radius: 8px; text-decoration: none; letter-spacing: 0.04em; transition: all 0.2s; }
.btn-discord:hover { background: rgba(0,229,255,0.12); }
.hero-stats { display: flex; align-items: center; gap: 32px; }
.stat { display: flex; flex-direction: column; gap: 4px; }
.stat-num { font-family: 'Bebas Neue', sans-serif; font-size: 2rem; line-height: 1; }
.stat-label { font-size: 0.65rem; color: #5a7080; letter-spacing: 0.08em; text-transform: uppercase; font-family: 'Space Mono', monospace; }
.stat-divider { width: 1px; height: 40px; background: #1a2535; }

/* PRODUCTS */
.products { padding: 100px 0; }
.section-header { margin-bottom: 56px; }
.section-title { font-family: 'Bebas Neue', sans-serif; font-size: clamp(2.5rem, 6vw, 4rem); line-height: 1; letter-spacing: 0.03em; margin-bottom: 10px; }
.section-sub { font-size: 0.75rem; color: #5a7080; letter-spacing: 0.06em; }
.products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(340px, 1fr)); gap: 20px; }
.product-card { background: #0f1620; border: 1px solid #1a2535; border-radius: 16px; padding: 32px; position: relative; overflow: hidden; transition: all 0.3s cubic-bezier(0.23,1,0.32,1); }
.product-card::before { content: ''; position: absolute; inset: 0; background: linear-gradient(135deg, rgba(0,229,255,0.03) 0%, transparent 60%); pointer-events: none; }
.product-card:hover { border-color: rgba(0,229,255,0.35); transform: translateY(-6px); box-shadow: 0 24px 60px rgba(0,0,0,0.4), 0 0 0 1px rgba(0,229,255,0.1); }
.product-card--featured { border-color: rgba(0,229,255,0.4); box-shadow: 0 0 0 1px rgba(0,229,255,0.12), 0 20px 60px rgba(0,229,255,0.06); }
.featured-badge { position: absolute; top: 16px; right: 16px; background: rgba(0,229,255,0.1); border: 1px solid rgba(0,229,255,0.3); color: #00e5ff; font-size: 0.62rem; padding: 5px 12px; border-radius: 100px; letter-spacing: 0.08em; }
.product-icon { font-size: 2.2rem; margin-bottom: 16px; }
.product-name { font-size: 1.15rem; font-weight: 600; margin-bottom: 10px; line-height: 1.3; }
.product-desc { font-size: 0.875rem; color: #5a7080; line-height: 1.65; margin-bottom: 20px; }
.product-features { list-style: none; padding: 0; margin: 0 0 28px; display: flex; flex-direction: column; gap: 8px; }
.feature-item { font-size: 0.825rem; color: #a0aaba; display: flex; align-items: flex-start; gap: 8px; line-height: 1.5; }
.feature-check { flex-shrink: 0; font-size: 0.75rem; margin-top: 1px; }
.product-footer { display: flex; align-items: center; justify-content: space-between; padding-top: 20px; border-top: 1px solid #1a2535; }
.price-block { display: flex; align-items: baseline; gap: 6px; }
.price-label { font-size: 0.65rem; color: #5a7080; letter-spacing: 0.05em; }
.price { font-family: 'Bebas Neue', sans-serif; font-size: 2.2rem; line-height: 1; }
.btn-buy { background: linear-gradient(135deg, #00e5ff, #00aacc); color: #020e12; font-family: 'Space Mono', monospace; font-weight: 700; font-size: 0.78rem; border: none; border-radius: 8px; padding: 12px 22px; cursor: pointer; transition: all 0.2s; letter-spacing: 0.03em; }
.btn-buy:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,229,255,0.3); }

/* HOW IT WORKS */
.how-it-works { padding: 80px 0 100px; border-top: 1px solid #1a2535; }
.steps-row { display: grid; grid-template-columns: repeat(4, 1fr); gap: 24px; margin-top: 56px; position: relative; }
.steps-row::before { content: ''; position: absolute; top: 32px; left: 12%; right: 12%; height: 1px; background: linear-gradient(90deg, transparent, rgba(0,229,255,0.3), rgba(0,229,255,0.3), transparent); }
.step { text-align: center; padding: 16px; }
.step-num { font-size: 0.65rem; letter-spacing: 0.12em; margin-bottom: 12px; }
.step-icon { font-size: 2rem; background: #0f1620; border: 1px solid #1a2535; width: 64px; height: 64px; border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: 0 auto 16px; }
.step-title { font-weight: 600; font-size: 0.95rem; margin-bottom: 8px; }
.step-desc { font-size: 0.82rem; color: #5a7080; line-height: 1.6; }

/* TRUST */
.trust-strip { padding: 32px 0; border-top: 1px solid #1a2535; border-bottom: 1px solid #1a2535; background: rgba(0,229,255,0.015); }
.trust-items { display: flex; align-items: center; justify-content: center; flex-wrap: wrap; gap: 40px; }
.trust-item { display: flex; align-items: center; gap: 10px; font-size: 0.72rem; color: #5a7080; letter-spacing: 0.06em; text-transform: uppercase; }
.trust-icon { font-size: 1.1rem; }

/* FOOTER */
.footer { padding: 60px 0; text-align: center; }
.footer-logo { font-family: 'Bebas Neue', sans-serif; font-size: 2.4rem; letter-spacing: 0.06em; margin-bottom: 12px; }
.footer-sub { font-size: 0.72rem; color: #5a7080; letter-spacing: 0.08em; margin-bottom: 20px; }
.footer-links { display: flex; justify-content: center; gap: 24px; margin-bottom: 20px; }
.footer-link { font-size: 0.7rem; color: #00e5ff; text-decoration: none; letter-spacing: 0.06em; opacity: 0.7; transition: opacity 0.2s; }
.footer-link:hover { opacity: 1; }
.footer-copy { font-size: 0.65rem; color: #2a3a45; letter-spacing: 0.06em; }

/* ===== MODAL ===== */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(3, 7, 12, 0.9);
  backdrop-filter: blur(12px);
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}
.modal {
  background: #0c1520;
  border: 1px solid rgba(0,229,255,0.2);
  border-radius: 20px;
  padding: 40px;
  width: 100%;
  max-width: 520px;
  position: relative;
  box-shadow: 0 40px 100px rgba(0,0,0,0.7), 0 0 0 1px rgba(0,229,255,0.06);
  max-height: 90vh;
  overflow-y: auto;
}
.modal-close {
  position: absolute;
  top: 16px; right: 16px;
  background: rgba(255,255,255,0.05);
  border: 1px solid #1a2535;
  color: #5a7080;
  width: 32px; height: 32px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 0.8rem;
  display: flex; align-items: center; justify-content: center;
  transition: all 0.2s;
}
.modal-close:hover { color: #dde8ef; border-color: rgba(0,229,255,0.3); }
.modal-tag { font-size: 0.62rem; letter-spacing: 0.14em; margin-bottom: 10px; }
.modal-title { font-family: 'Bebas Neue', sans-serif; font-size: 2.4rem; line-height: 1; margin-bottom: 16px; }

.selected-product-pill {
  background: rgba(0,229,255,0.06);
  border: 1px solid rgba(0,229,255,0.18);
  border-radius: 8px;
  padding: 10px 16px;
  font-size: 0.78rem;
  color: #a0aaba;
  margin-bottom: 24px;
  letter-spacing: 0.03em;
}

/* Payment options */
.payment-options { display: flex; flex-direction: column; gap: 12px; margin-bottom: 24px; }
.pay-option {
  background: rgba(255,255,255,0.03);
  border: 1px solid #1a2535;
  border-radius: 12px;
  padding: 18px 20px;
  display: flex; align-items: center; gap: 16px;
  cursor: pointer; transition: all 0.2s;
  text-align: left; width: 100%; color: #dde8ef;
}
.pay-option:hover { border-color: rgba(0,229,255,0.28); background: rgba(0,229,255,0.04); }
.pay-option.active { border-color: #00e5ff; background: rgba(0,229,255,0.07); box-shadow: 0 0 24px rgba(0,229,255,0.1); }
.pay-icon { font-size: 1.8rem; flex-shrink: 0; }
.pay-info { flex: 1; }
.pay-name { font-weight: 600; font-size: 1.05rem; margin-bottom: 4px; }
.pay-detail { font-size: 0.68rem; color: #5a7080; letter-spacing: 0.04em; }
.pay-check { font-size: 1.2rem; flex-shrink: 0; }

/* Buttons */
.btn-next {
  background: linear-gradient(135deg, #00e5ff, #00aacc);
  color: #020e12;
  font-family: 'Space Mono', monospace;
  font-weight: 700; font-size: 0.82rem;
  border: none; border-radius: 10px;
  padding: 14px 32px;
  cursor: pointer; width: 100%;
  letter-spacing: 0.04em; transition: all 0.2s;
}
.btn-next:hover:not(:disabled) { box-shadow: 0 8px 28px rgba(0,229,255,0.3); transform: translateY(-1px); }
.btn-next:disabled { opacity: 0.3; cursor: not-allowed; }
.modal-btn-row { display: flex; gap: 12px; }
.btn-back { flex-shrink: 0; background: rgba(255,255,255,0.04); border: 1px solid #1a2535; color: #5a7080; font-family: 'Space Mono', monospace; font-size: 0.8rem; padding: 14px 20px; border-radius: 10px; cursor: pointer; transition: all 0.2s; }
.btn-back:hover { color: #dde8ef; border-color: rgba(0,229,255,0.3); }

/* Instructions */
.instructions-box { background: rgba(0,0,0,0.3); border: 1px solid #1a2535; border-radius: 14px; padding: 24px; margin-bottom: 24px; }
.instr-header { font-size: 0.68rem; letter-spacing: 0.1em; color: #00e5ff; margin-bottom: 18px; text-transform: uppercase; }
.instr-steps { display: flex; flex-direction: column; gap: 12px; margin-bottom: 14px; }
.instr-step { display: flex; align-items: flex-start; gap: 12px; font-size: 0.875rem; color: #a0aaba; line-height: 1.55; }
.instr-step strong { color: #dde8ef; }
.instr-step em { color: #00e5ff; font-style: normal; }
.instr-num { background: rgba(0,229,255,0.12); color: #00e5ff; font-family: 'Space Mono', monospace; font-size: 0.65rem; font-weight: 700; width: 22px; height: 22px; border-radius: 50%; display: flex; align-items: center; justify-content: center; flex-shrink: 0; margin-top: 2px; }

/* Copy box */
.copy-box {
  background: rgba(0,229,255,0.05);
  border: 1px dashed rgba(0,229,255,0.3);
  border-radius: 10px;
  padding: 14px 18px;
  cursor: pointer; margin: 12px 0;
  transition: all 0.2s;
  display: flex; align-items: center; justify-content: space-between; gap: 12px;
}
.copy-box:hover { background: rgba(0,229,255,0.09); border-color: rgba(0,229,255,0.5); }
.copy-left { flex: 1; min-width: 0; }
.copy-label { font-size: 0.6rem; color: #5a7080; letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 4px; }
.copy-value { font-size: 0.9rem; color: #00e5ff; word-break: break-all; }
.copy-btn { font-size: 0.65rem; letter-spacing: 0.08em; color: #00e5ff; background: rgba(0,229,255,0.1); border: 1px solid rgba(0,229,255,0.25); padding: 6px 12px; border-radius: 6px; white-space: nowrap; flex-shrink: 0; transition: all 0.2s; }
.copy-box:hover .copy-btn { background: rgba(0,229,255,0.18); }

/* Confirm */
.confirm-box { background: rgba(0,0,0,0.3); border: 1px solid #1a2535; border-radius: 14px; padding: 24px; margin-bottom: 20px; }
.confirm-intro { font-size: 0.9rem; color: #a0aaba; margin-bottom: 16px; line-height: 1.6; }
.confirm-checklist { display: flex; flex-direction: column; gap: 14px; margin-top: 20px; }
.check-item { display: flex; align-items: flex-start; gap: 12px; font-size: 0.875rem; color: #a0aaba; line-height: 1.5; }
.check-item strong { color: #dde8ef; }
.check-icon { flex-shrink: 0; margin-top: 1px; font-style: normal; }

.btn-email-open {
  display: block; text-align: center;
  background: rgba(0,229,255,0.08);
  border: 1px solid rgba(0,229,255,0.28);
  color: #00e5ff;
  font-family: 'Space Mono', monospace;
  font-size: 0.8rem; padding: 14px;
  border-radius: 10px; text-decoration: none;
  letter-spacing: 0.04em; margin-bottom: 12px; transition: all 0.2s;
}
.btn-email-open:hover { background: rgba(0,229,255,0.14); }
.btn-done {
  display: block; width: 100%;
  background: rgba(255,255,255,0.04);
  border: 1px solid #1a2535;
  color: #5a7080; font-family: 'Space Mono', monospace;
  font-size: 0.78rem; padding: 12px; border-radius: 10px;
  cursor: pointer; letter-spacing: 0.04em; transition: all 0.2s;
}
.btn-done:hover { color: #dde8ef; }

/* Modal animation */
.modal-fade-enter-active, .modal-fade-leave-active { transition: opacity 0.3s ease; }
.modal-fade-enter-active .modal, .modal-fade-leave-active .modal { transition: transform 0.3s cubic-bezier(0.23,1,0.32,1); }
.modal-fade-enter-from, .modal-fade-leave-to { opacity: 0; }
.modal-fade-enter-from .modal { transform: scale(0.94) translateY(20px); }
.modal-fade-leave-to .modal { transform: scale(0.96) translateY(10px); }

/* Responsive */
@media (max-width: 900px) {
  .steps-row { grid-template-columns: repeat(2, 1fr); }
  .steps-row::before { display: none; }
  .products-grid { grid-template-columns: 1fr; }
}
@media (max-width: 600px) {
  .hero-stats { flex-wrap: wrap; gap: 20px; }
  .stat-divider { display: none; }
  .steps-row { grid-template-columns: 1fr; }
  .trust-items { gap: 20px; }
  .modal { padding: 28px 18px; }
  .modal-title { font-size: 2rem; }
}
</style>
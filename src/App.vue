<script setup>
import { ref, onMounted } from 'vue'
import siteData from './content/site.json'

/*
  ===================================================
  IMAGES À AJOUTER DANS /public/images/
  ===================================================

  logo.png
  about.jpg

  bg1.jpg
  bg2.jpg
  bg3.jpg
  bg4.jpg

  real1.jpg
  real2.jpg
  real3.jpg
  real4.jpg
  real5.jpg
  real6.jpg

  ===================================================
*/
const menuOpen = ref(false)
const backgroundImages = [
  '/images/about.jpg',
  '/images/real1.jpg',
  '/images/real2.jpg',
  '/images/real3.jpg',
]

const galleryImages = [
  '/images/real1.jpg',
  '/images/real2.jpg',
  '/images/about.jpg',
  '/images/real4.webp',
  '/images/real5.webp',
  '/images/real6.webp',
]

/*
  BANNIÈRE MODIFIABLE
*/
const banners = [
  'Travaux de peinture intérieure et extérieure',
  'Des finitions haut de gamme pour votre maison',
  'Un artisan de confiance à votre service',
  'Rénovation & décoration sur mesure',
  'EN CE MOMENT -15% SUR TOUT LE PAPIER PEINT !!!',
]

const currentBanner = ref(0)
const currentBackground = ref(0)

onMounted(() => {
  setInterval(() => {
    currentBanner.value = (currentBanner.value + 1) % banners.length
  }, 4000)

  setInterval(() => {
    currentBackground.value = (currentBackground.value + 1) % backgroundImages.length
  }, 7000)
})

// const reviews = [
//   {
//     author: 'Bruno DUPUIS',
//     rating: 5,
//     text: 'PEUT-ETRE A JEUDI POUR LES GRILLADES !!! ',
//   },
//   {
//     author: 'Léonie D',
//     rating: 5,
//     text: 'Travail impeccable, très propre et professionnel. Je recommande vivement.',
//   },
//   {
//     author: 'Marie D.',
//     rating: 5,
//     text: 'Très bon artisan, ponctuel et sérieux. Excellent résultat.',
//   },
//   {
//     author: 'Jean P.',
//     rating: 4,
//     text: 'Bon travail, finition soignée, délais respectés.',
//   },
// ]
</script>

<template>
  <div id="app">
    <!-- BACKGROUND SLIDER -->
    <div class="background-slider">
      <div
        v-for="(image, index) in backgroundImages"
        :key="index"
        class="background-image"
        :style="{
          backgroundImage: `url(${image})`,
          opacity: currentBackground === index ? 1 : 0,
        }"
      ></div>
    </div>
    <div class="menu-toggle" @click="menuOpen = !menuOpen">
      <span></span>
      <span></span>
      <span></span>
    </div>
    <!-- HEADER -->
    <header class="header">
      <div class="logo-container">
        <img src="/public/images/logo.jpg" alt="Logo artisan peintre" class="logo" />
      </div>

      <nav class="navbar" :class="{ active: menuOpen }">
        <a href="#home">Accueil</a>
        <a href="#services">Prestations</a>
        <a href="#gallery">Réalisations</a>
        <a href="#about">À propos</a>
        <a href="#devis">Devis</a>
        <a href="#contact">Contact</a>
        <a href="#map">Nous trouver</a>
        <a href="#avis">Avis clients</a>
      </nav>
    </header>

    <!-- BANNER -->
    <section class="hero" id="home">
      <div class="hero-overlay">
        <!-- H1 SEO -->
        <h1>{{ siteData.heroTitle }}</h1>

        <!-- Texte déroulant -->
        <div class="hero-slider">
          <transition name="fade" mode="out-in">
            <h2 :key="currentBanner">
              {{ banners[currentBanner] }}
            </h2>
          </transition>
        </div>

        <p class="subtitle">Travaux de peinture intérieure & extérieure</p>

        <a href="#contact" class="cta-button"> Demander un devis gratuit </a>
      </div>
    </section>

    <!-- SERVICES -->
    <section class="section" id="services">
      <h2>Nos prestations</h2>

      <div class="services-grid">
        <div class="service-card">
          <h3>Peinture intérieure</h3>
          <p>Murs, plafonds, boiseries et rénovation complète de vos pièces.</p>
        </div>

        <div class="service-card">
          <h3>Peinture extérieure</h3>
          <p>Façades, volets, portails et protections durables.</p>
        </div>

        <div class="service-card">
          <h3>Revêtements muraux</h3>
          <p>Pose de papier peint, toile de verre et finitions décoratives.</p>
        </div>

        <div class="service-card">
          <h3>Conseils décoration</h3>
          <p>Accompagnement dans le choix des couleurs et ambiances.</p>
        </div>
      </div>
    </section>

    <!-- GALLERY -->
    <section class="section gallery-section" id="gallery">
      <h2>Nos réalisations</h2>

      <div class="gallery-grid">
        <div v-for="(image, index) in galleryImages" :key="index" class="gallery-item">
          <img :src="image" :alt="'Réalisation ' + index" />
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section class="section about-section" id="about">
      <div class="about-content">
        <div class="about-text">
          <h2>À propos</h2>

          <p>
            Artisan peintre expérimenté, nous réalisons tous vos travaux de peinture et rénovation
            avec sérieux, précision et passion du détail.
          </p>

          <p>
            Notre objectif : sublimer votre intérieur et protéger durablement votre extérieur grâce
            à des finitions de qualité.
          </p>
        </div>

        <div class="about-image logo-about">
          <img src="/public/images/logo.jpg" alt="Logo artisan peintre" />
        </div>
      </div>
    </section>
    <section class="section reviews-section" id="avis">
      <h2>Avis clients</h2>

      <div class="reviews-grid">
        <div class="review-card" v-for="(review, index) in reviews" :key="index">
          <div class="stars">
            <span v-for="n in 5" :key="n">
              {{ n <= review.rating ? '★' : '☆' }}
            </span>
          </div>

          <p class="review-text">"{{ review.text }}"</p>
          <p class="review-author">— {{ review.author }}</p>
        </div>
      </div>
    </section>

    <!-- CONTACT / DEVIS -->
    <section class="section contact-section" id="devis">
      <h2>Demande de devis</h2>

      <form
        class="contact-card"
        action="https://formsubmit.co/28208876c82fb70f2e69c8472d5cdd91"
        method="POST"
      >
        <!-- Anti-spam -->
        <input type="hidden" name="_captcha" value="false" />

        <!-- Sujet -->
        <input type="hidden" name="_subject" value="Nouvelle demande de devis depuis le site" />

        <!-- Redirection après envoi -->
        <input
          type="hidden"
          name="_next"
          value="https://joyful-snickerdoodle-87eb83.netlify.app/"
        />

        <div class="form-group">
          <input type="text" name="Nom" placeholder="Votre nom" required />
        </div>

        <div class="form-group">
          <input type="email" name="Email" placeholder="Votre email" required />
        </div>

        <div class="form-group">
          <input type="tel" name="Téléphone" placeholder="Votre téléphone" />
        </div>

        <div class="form-group">
          <textarea
            name="Message"
            rows="6"
            placeholder="Décrivez votre projet..."
            required
          ></textarea>
        </div>

        <button type="submit" class="contact-button">Envoyer la demande</button>
      </form>
    </section>
    <!-- CONTACT -->
    <section class="section contact-section" id="contact">
      <h2>Contact</h2>

      <div class="contact-card">
        <p><strong>Téléphone :</strong> 06 80 60 15 03</p>
        <p><strong>Email :</strong> contact@artisan-peintre.fr</p>
        <p><strong>Zone d’intervention :</strong> Landes et alentours</p>
      </div>
    </section>
    <!-- MAP -->
    <section class="map-section" id="map">
      <div class="map-container">
        <iframe
          src="https://www.google.com/maps?q=138+Rue+Rectoure,+40990+Saint-Vincent-de-Paul&output=embed"
          width="100%"
          height="350"
          style="border: 0"
          allowfullscreen=""
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
        >
        </iframe>
      </div>
    </section>
    <!-- FOOTER -->
    <footer class="footer">
      <p>© 2026 Artisan Peintre - Guy Décors - Tous droits réservés - réalisé par Bruno DUPUIS</p>
    </footer>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  overflow-x: hidden;
  color: white;
}

#app {
  position: relative;
  min-height: 100vh;
}

/* BACKGROUND */
.background-slider {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -2;
}

.background-image {
  position: absolute;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  transition: opacity 3s ease-in-out;
}

/* OVERLAY */
.background-slider::after {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.55);
  top: 0;
  left: 0;
  z-index: 1;
}

/* HEADER */
.header {
  width: 100%;
  padding: 20px 50px;
  position: fixed;
  top: 0;
  z-index: 1000;

  display: flex;
  justify-content: space-between;
  align-items: center;

  backdrop-filter: blur(8px);
  background: rgba(0, 0, 0, 0.3);
}

.logo {
  height: 70px;
  border-radius: 5%;
}

.navbar {
  display: flex;
  gap: 30px;
}

.navbar a {
  color: white;
  text-decoration: none;
  font-weight: bold;
  transition: 0.3s;
}

.navbar a:hover {
  color: #f0b35a;
}

/* HERO */
.hero {
  height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;

  text-align: center;
  padding: 0 20px;
}

.hero-overlay {
  max-width: 900px;
}

.hero h1 {
  font-size: 4rem;
  margin-bottom: 20px;
  line-height: 1.2;
}

.subtitle {
  font-size: 1.3rem;
  margin-bottom: 35px;
}

.cta-button {
  display: inline-block;
  padding: 16px 35px;

  background: #f0b35a;
  color: black;

  text-decoration: none;
  border-radius: 50px;
  font-weight: bold;

  transition: 0.3s;
}

.cta-button:hover {
  transform: scale(1.05);
}

/* SECTION */
.section {
  padding: 120px 10%;
  position: relative;
  z-index: 2;
}

.section h2 {
  text-align: center;
  font-size: 3rem;
  margin-bottom: 60px;
}

/* SERVICES */
.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 30px;
}

.service-card {
  background: rgba(255, 255, 255, 0.12);
  padding: 35px;
  border-radius: 20px;
  backdrop-filter: blur(10px);

  transition: 0.3s;
}

.service-card:hover {
  transform: translateY(-10px);
}

.service-card h3 {
  margin-bottom: 20px;
  font-size: 1.5rem;
}

/* GALLERY */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));

  gap: 20px;
}

.gallery-item {
  overflow: hidden;
  border-radius: 20px;
}

.gallery-item img {
  width: 100%;
  height: 280px;
  object-fit: cover;

  transition: 0.5s;
}

.gallery-item:hover img {
  transform: scale(1.08);
}

/* ABOUT */
.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 50px;
  align-items: center;
}

.about-image img {
  width: 100%;
  border-radius: 20px;
}

/* CONTACT */
.contact-card {
  max-width: 700px;
  margin: auto;

  background: rgba(255, 255, 255, 0.12);
  padding: 50px;
  border-radius: 20px;

  text-align: center;
  backdrop-filter: blur(10px);
}

.contact-card p {
  margin-bottom: 20px;
  font-size: 1.2rem;
}

.contact-button {
  margin-top: 20px;

  padding: 15px 35px;
  border: none;
  border-radius: 50px;

  background: #f0b35a;
  font-weight: bold;
  cursor: pointer;

  transition: 0.3s;
}

.contact-button:hover {
  transform: scale(1.05);
}

/* FOOTER */
.footer {
  text-align: center;
  padding: 30px;
  background: rgba(0, 0, 0, 0.4);
}

/* ANIMATIONS */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* RESPONSIVE */
@media (max-width: 900px) {
  .header {
    flex-direction: column;
    gap: 20px;
    padding: 20px;
  }

  .hero h1 {
    font-size: 2.5rem;
  }

  .about-content {
    grid-template-columns: 1fr;
  }

  .navbar {
    flex-wrap: wrap;
    justify-content: center;
  }
}

@media (max-width: 600px) {
  .hero h1 {
    font-size: 2rem;
  }

  .section h2 {
    font-size: 2rem;
  }

  .gallery-item img {
    height: 220px;
  }
}
/* =========================
   RESPONSIVE PREMIUM
========================= */

/* TABLETTES */
@media (max-width: 1024px) {
  .header {
    padding: 15px 25px;
  }

  .hero h1 {
    font-size: 3rem;
  }

  .section {
    padding: 90px 7%;
  }

  .about-content {
    gap: 30px;
  }
}

/* MOBILE */
@media (max-width: 768px) {
  .header {
    flex-direction: row;
    justify-content: space-between;
    padding: 15px 20px;
  }

  .navbar {
    position: fixed;
    top: 90px;
    right: -100%;
    width: 260px;
    height: calc(100vh - 90px);

    background: rgba(0, 0, 0, 0.92);

    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;

    padding: 40px 30px;
    gap: 25px;

    transition: 0.4s ease;
    backdrop-filter: blur(10px);
  }

  .navbar.active {
    right: 0;
  }

  .navbar a {
    font-size: 1.1rem;
  }

  .menu-toggle {
    display: flex;
  }

  .hero {
    padding-top: 100px;
  }

  .hero h1 {
    font-size: 2.2rem;
    line-height: 1.3;
  }

  .subtitle {
    font-size: 1rem;
  }

  .cta-button {
    width: 100%;
    max-width: 320px;
  }

  .section {
    padding: 80px 25px;
  }

  .section h2 {
    font-size: 2rem;
    margin-bottom: 40px;
  }

  .services-grid {
    grid-template-columns: 1fr;
  }

  .gallery-grid {
    grid-template-columns: 1fr;
  }

  .gallery-item img {
    height: 240px;
  }

  .about-content {
    grid-template-columns: 1fr;
  }

  .contact-card {
    padding: 35px 25px;
  }
}

/* PETITS SMARTPHONES */
@media (max-width: 480px) {
  .hero h1 {
    font-size: 1.8rem;
  }

  .logo {
    height: 55px;
  }

  .gallery-item img {
    height: 200px;
  }

  .service-card {
    padding: 25px;
  }

  .contact-card p {
    font-size: 1rem;
  }
}
/* MENU MOBILE */

.menu-toggle {
  width: 35px;
  height: 28px;

  display: none;
  flex-direction: column;
  justify-content: space-between;

  cursor: pointer;
  z-index: 2000;
}

.menu-toggle span {
  height: 4px;
  width: 100%;
  background: white;
  border-radius: 10px;
}
/* =========================
   GOOGLE MAPS
========================= */

.map-section {
  padding: 0 10% 80px;
  position: relative;
  z-index: 2;
}

.map-container {
  overflow: hidden;
  border-radius: 24px;

  border: 2px solid rgba(255, 255, 255, 0.1);

  background: black;

  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.4),
    0 0 0 1px rgba(255, 255, 255, 0.05);

  transition: 0.4s ease;
}

.map-container:hover {
  transform: translateY(-4px);
  box-shadow:
    0 15px 50px rgba(0, 0, 0, 0.5),
    0 0 0 1px rgba(255, 255, 255, 0.08);
}

.map-container iframe {
  display: block;
  filter: grayscale(0.1) contrast(1.05);
}

/* RESPONSIVE */

@media (max-width: 768px) {
  .map-section {
    padding: 0 25px 60px;
  }

  .map-container iframe {
    height: 280px;
  }
}
/* =========================
   LOGO SECTION À PROPOS
========================= */

.logo-about {
  display: flex;
  justify-content: center;
  align-items: center;
}

.logo-about img {
  width: 100%;
  max-width: 420px;

  background: rgba(255, 255, 255, 0.04);

  padding: 30px;

  border-radius: 28px;

  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.35),
    0 0 0 1px rgba(255, 255, 255, 0.05);

  backdrop-filter: blur(8px);

  transition: 0.4s ease;
}

.logo-about img:hover {
  transform: scale(1.03);
}

/* MOBILE */
@media (max-width: 768px) {
  .logo-about img {
    max-width: 280px;
    padding: 20px;
  }
}
/* =========================
   AVIS CLIENTS
========================= */

.reviews-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
}

.review-card {
  background: rgba(255, 255, 255, 0.12);
  padding: 30px;
  border-radius: 20px;
  backdrop-filter: blur(10px);

  transition: 0.3s;
}

.review-card:hover {
  transform: translateY(-8px);
}

.stars {
  color: #f0b35a;
  font-size: 1.3rem;
  margin-bottom: 15px;
}

.review-text {
  font-style: italic;
  margin-bottom: 15px;
}

.review-author {
  font-weight: bold;
  opacity: 0.8;
}
/* =========================
   FORMULAIRE
========================= */

.form-group {
  margin-bottom: 20px;
}

.form-group input,
.form-group textarea {
  width: 100%;

  padding: 16px 20px;

  border: none;
  border-radius: 14px;

  background: rgba(255, 255, 255, 0.1);

  color: white;
  font-size: 1rem;

  backdrop-filter: blur(5px);

  outline: none;

  transition: 0.3s;
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

.form-group input:focus,
.form-group textarea:focus {
  background: rgba(255, 255, 255, 0.18);
  transform: scale(1.01);
}

textarea {
  resize: vertical;
  min-height: 140px;
}
</style>

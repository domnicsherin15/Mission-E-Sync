<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import "../assets/about.css";
import "../assets/navbar.css";
import gsap from "gsap";


const isMenuOpen = ref(false);

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

const activeDropdown = ref<string | null>(null);

const toggleDropdown = (menu: string) => {
  activeDropdown.value = activeDropdown.value === menu ? null : menu;
};

const closeDropdown = (event: MouseEvent) => {
  if (!(event.target as HTMLElement).closest(".nav-item")) {
    activeDropdown.value = null;
  }
};

const handleEscape = (e: KeyboardEvent) => {
  if (e.key === "Escape" || e.key === "Tab") {
    activeDropdown.value = null;
  }
};

  // Animate elements on page load
  gsap.from(".section-title, .section-description", {
    opacity: 0,
    y: 40,
    duration: 1,
    ease: "power2.out",
  });

  gsap.from(".group-title", {
    opacity: 0,
    y: 30,
    duration: 1,
    delay: 0.3,
    ease: "power2.out",
  });

  gsap.from(".user-card", {
    opacity: 0,
    y: 50,
    duration: 1,
    delay: 0.5,
    stagger: 0.2,
    ease: "back.out(1.7)",
  });

  // Icon hover bounce effect
  const icons = document.querySelectorAll(".icon");
  icons.forEach((icon) => {
    icon.addEventListener("mouseenter", () => {
      gsap.to(icon, { scale: 1.1, duration: 0.3, ease: "bounce.out" });
    });
    icon.addEventListener("mouseleave", () => {
      gsap.to(icon, { scale: 1.0, duration: 0.2, ease: "power2.out" });
    });
  });

  document.addEventListener("click", closeDropdown);
  document.addEventListener("keydown", handleEscape);


onUnmounted(() => {
  document.removeEventListener("click", closeDropdown);
  document.removeEventListener("keydown", handleEscape);
});
</script>

<template>
  <div class="Aboutpage">
    <!-- Navbar -->
    <nav class="navbar">
      <RouterLink to="/dashboard">
        <div class="navbar-logo">
          <img src="/FinalLogo.png" alt="EduSync"></img>
        </div>
      </RouterLink>
      <div class="authim-buttons">
        <RouterLink to="/login" class="btnim login-btnim">Login</RouterLink>
        <RouterLink to="/signup" class="btnim signup-btnim">Sign Up</RouterLink>
      </div>
    </nav>

    <!-- About Section -->
    <main class="about-page">
      <section class="intro-section">
        <h2 class="section-title">About the Platform</h2>
        <p class="section-description">
          Our LMS is a custom-built solution, developed in alignment with the pedagogical goals and academic standards of modern higher education. It brings together essential learning tools in a secure, intuitive interface that encourages active participation, continuous feedback, and measurable outcomes.
        </p>
      </section>

      <section class="user-groups-section">
        <h3 class="group-title">This Platform Serves</h3>
        <div class="card-container">
          <div class="user-card">
            <div class="icon">🎓</div>
            <h4 class="user-title">Undergraduate & Postgraduate Students</h4>
            <p class="user-description">
              To access course materials, submit assignments, track academic progress, and obtain recognized certifications.
            </p>
          </div>
          <div class="user-card">
            <div class="icon">📚</div>
            <h4 class="user-title">Adult & Continuing Learners</h4>
            <p class="user-description">
              To upskill, reskill, or pursue lifelong learning through structured, flexible modules.
            </p>
          </div>
          <div class="user-card">
            <div class="icon">🧑‍🏫</div>
            <h4 class="user-title">Instructors & Faculty</h4>
            <p class="user-description">
              To manage and deliver courses efficiently, monitor student engagement, and support academic excellence.
            </p>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>
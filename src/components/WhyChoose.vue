<script setup lang="ts">
import { ref, onMounted } from "vue";
import "../assets/navbar.css";
import "../assets/whychoose.css";

const isMenuOpen = ref(false);

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

const features = [
  {
    title: "Accessibility",
    description: "Anytime, anywhere access from desktop or mobile devices."
  },
  {
    title: "Interactivity",
    description: "Foster meaningful learning through forums, feedback, and collaborative tools."
  },
  {
    title: "Efficiency",
    description: "Reduce administrative workload with streamlined workflows."
  },
  {
    title: "Scalability",
    description: "Suitable for small seminars or institution-wide deployments."
  },
  {
    title: "Data Security",
    description: "Compliant with academic data protection and privacy standards."
  }
];


const activeDropdown = ref<string | null>(null);

const toggleDropdown = (menu: string) => {
  activeDropdown.value = activeDropdown.value === menu ? null : menu;
};

const closeDropdown = (event: MouseEvent) => {
  if (!(event.target as HTMLElement).closest(".nav-item")) {
    activeDropdown.value = null;
  }
};

onMounted(() => {
  const container = document.querySelector(".scroll-container");
  container?.scrollTo({ left: 0, behavior: "instant" });
});

document.addEventListener("click", closeDropdown);

onMounted(() => {
  const container = document.querySelector(".scroll-container");
  container?.scrollTo({ left: 0, behavior: "instant" });

  const handleEscape = (e: KeyboardEvent) => {
    if (e.key === "Escape") activeDropdown.value = null;
  };

  document.addEventListener("keydown", handleEscape);
  document.addEventListener("click", closeDropdown);
});

</script>

<template>
  <div class="Whypage">
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
    <main class="why-choose">
        <h2 class="why-title">WHY CHOOSE THIS LMS?</h2>
          <p class="why-intro">
            In an era where digital transformation defines educational success, this LMS empowers all users with:
          </p>
          <div class="features-grid">
            <div class="feature-card" v-for="(feature, index) in features" :key="index">
              <h3 class="feature-title">{{ feature.title }}</h3>
              <p class="feature-description">{{ feature.description }}</p>
            </div>
          </div>
    </main>
  </div>
</template>
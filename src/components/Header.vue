<template>
  <nav class="navbar navbar-expand-lg bg-white">
    <div class="container-fluid">
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto me-auto">
          <li class="nav-item">
            <router-link
              to="/"
              class="nav-link"
              :class="{ active: $route.name === 'home' }"
              >Home</router-link
            >
          </li>
          <li class="nav-item">
            <router-link
              to="/notes"
              class="nav-link"
              :class="{ active: $route.name === 'notes' }"
              >Notes</router-link
            >
          </li>
          <li class="nav-item">
            <router-link
              to="/about"
              class="nav-link"
              :class="{ active: $route.name === 'about' }"
              >About</router-link
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Header",
}
</script>

<style>
.active {
  border-bottom: 3px solid rgb(0, 196, 0);
}
</style>

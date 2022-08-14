<template>
  <header class="header">
    <div class="container">
      <div class="left-menu">
        <div class="logo" title="Home">
          <img src="../assets/logo.png" alt="Logo" />
        </div>
        <h2 title="Home">{{ title1 }}</h2>
        <h2 title="Desk">{{ title2 }}</h2>
      </div>
      <div class="right-menu">
        <i class="fa-solid fa-user" title="User Infomaition"></i>
        <i class="fa-solid fa-magnifying-glass" title="Search"></i>
        <i class="fa-solid fa-gear" title="Setting"></i>
        <i class="fa-solid fa-id-card" title="MemberShip"></i>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: {
    title1: {
      type: String,
      default: "title1",
      required: true,
    },
    title2: {
      type: String,
      default: "title2",
      required: true,
    },
  },
  setup() {
    return {};
  },
};
</script>

<style scoped>
.header {
  width: 100%;
  margin: 0 auto;
  background-color: #111101;
  position: fixed;
  top: 0;
  left: 0;
}

.container {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0;
}

.left-menu,
.right-menu {
  width: 30%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  color: #ffffff;
}

h2 {
  font-size: 1.5rem;
  font-weight: 700;
  transition: 0.3s;
  cursor: pointer;
}

h2:hover {
  color: #3dc074;
}

.logo img {
  width: 60px;
  height: 40px;
}

.right-menu i {
  font-size: 1.2rem;
  color: #ffffff;
  cursor: pointer;
  transition: 0.3s;
}

.right-menu i:hover {
  color: #3dc074;
}
</style>

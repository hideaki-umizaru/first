<template>
<header>
  <div class="container">
        <div class="header-left">
        <h1>Compartir</h1>
        </div>
        <div class="header-right">
          <a href="#" @click="$router.push('/profile')">アイデア投稿</a>
        </div>
      </div>
</header>
</template>


<style scoped>
header {
  height: 55px;
  width: 100%;
  background-color: rgba(54, 80, 85, 0.9);
  top: 0;
  z-index: 10;
}

.logo {
  width: 124px;
  margin-top: 20px;
}

.header-left {
  float: left;
  line-height: 55px;
  margin-left: 30px;
}

.header-right {
  float: right;
  margin-right: 20px;
}

.header-right a {
  line-height: 55px;
  padding: 0 25px;
  color: white;
  display: block;
  float: left;
  transition: all 0.5s;
  text-decoration: none;
}

.header-right a:hover {
  background-color: rgba(255, 255, 255, 0.3);
}

</style>
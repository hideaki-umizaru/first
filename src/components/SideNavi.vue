<template>
  <div>
    <div class="left-padding">
      <div class="flex icon-field" @click="$router.push('/home')">
        <img class="icon" src="../assets/home.png" />
        <p>トップ</p>
      </div>
      <div class="flex icon-field" @click="$router.push('/profile')">
        <img class="icon" src="../assets/feather.png" />
        <p>アイデア投稿</p>
      </div>
      <div class="flex icon-field" @click="$store.dispatch('logout')">
        <img class="icon" src="../assets/logout.png" />
        <p>ログアウト</p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  components: {

  }
};
</script>

<style scoped>
.left-padding {
  margin: 20px;
}
.flex {
  display: flex;
}
.icon-field {
  margin-top: 15px;
  cursor: pointer;
}
.icon {
  width: 25px;
}
.icon-field p {
  font-size: 16px;
  padding-left: 15px;
}
.icon-field:hover {
  cursor: pointer;
}
</style>
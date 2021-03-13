<template>
  <div>
    <div v-for="(value, index) in shares" :key="index">
      <div class="message">
         <p class="text">アイデア名：{{value.share}}</p>
        <div class="flex">
          <p class="name">👤 ：{{value.name}}</p>
          <img class="icon" src="../assets/heart.png" @click="fav(index)" alt/>
          <p class="number">{{value.like.length}}</p>
          <img class="icon detail" src="../assets/detail.png"    @click="
              $router.push({
                path: '/detail/' + value.item.id,
                params: { id: value.item.id },
              })
            " />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      shares: [{ name: "太郎", like: [], share: "" }]
    };
  }
};
</script>

<style scoped>
.flex {
  display: flex;
}
.text {
  margin-top: 10px;
  margin-bottom: 20px;
  padding-bottom: 5px;
  font-weight: bold;
  font-size: 25px;
  border-bottom: solid 1px white;
}
.icon {
  margin-left: 15px;
  width: 25px;
  height: 25px;
}
.detail {
  margin-left: 15px;
}
.message {
  padding: 20px;
  border-bottom: solid 1px white;
  border-left: solid 1px white;
}
.name {
  font-size: 18px;
  margin-right: 10px;
}
.number {
  margin-left: 10px;
  margin-right: 10px;
}
</style>
<template>
<div class="app">
<Header />
 <div class="flex">
    <div class="left">
      <SideNavi />
    </div>
    <div class="right">
      <div class="title">
        <p>ホーム</p>
      </div>
      <Message />
    </div>
  </div>
  </div>
</template>

<script>
import Header from "../components/Header";
import Message from "../components/Message";
import SideNavi from "../components/SideNavi";
export default {
  components:{
    Header,
    Message,
    SideNavi
  }
};
</script>

<style scoped>
.left {
  width: 22%;
  height: 100vh;
}
.right {
  width: 78%;
  height: 100vh;
}
.flex {
  display: flex;
}
.title {
  border-bottom: 1px solid white;
  border-left: 1px solid white;
  padding: 15px;
}
.title p {
  font-size: 20px;
  font-weight: bold;
}

</style>
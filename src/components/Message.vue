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
            " 
              alt
            v-if="profile"
            />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      shares: [],
      path: true,
      profile: true,
    };
  },
  methods: {
    fav(index) {
      const result = this.shares[index].like.some((value) => {
        return value.user_id == this.$store.state.user.id;
      });
      if (result) {
        this.shares[index].like.forEach((element) => {
          if (element.user_id == this.$store.state.user.id) {
            axios({
              method: "delete",
              url: "https://git.heroku.com/radiant-stream-63219.git/api/like",
              data: {
                share_id: this.shares[index].item.id,
                user_id: this.$store.state.user.id,
              },
            }).then((response) => {
              console.log(response);
              this.$router.go({
                path: this.$router.currentRoute.path,
                force: true,
              });
            });
          }
        });
      } else {
        axios
          .post("https://git.heroku.com/radiant-stream-63219.git/api/like", {
            share_id: this.shares[index].item.id,
            user_id: this.$store.state.user.id,
          })
          .then((response) => {
            console.log(response);
            this.$router.go({
              path: this.$router.currentRoute.path,
              force: true,
            });
          });
      }
    },
    del(index) {
      axios
        .delete(
          "https://git.heroku.com/radiant-stream-63219.git/api/shares/" +
            this.shares[index].item.id
        )
        .then((response) => {
          console.log(response);
          this.$router.go({
            path: this.$router.currentRoute.path,
            force: true,
          });
        });
    },
    async getShares() {
      let data = [];
      const shares = await axios.get(
        "https://git.heroku.com/radiant-stream-63219.git/api/shares"
      );
      for (let i = 0; i < shares.data.data.length; i++) {
        await axios
          .get(
            "https://git.heroku.com/radiant-stream-63219.git/api/shares/" +
              shares.data.data[i].id
          )
          .then((response) => {
            if (this.$route.name == "profile") {
              if (response.data.item.user_id == this.$store.state.user.id) {
                data.push(response.data);
              }
            } else if (this.$route.name == "detail") {
              if (response.data.item.id == this.id) {
                data.push(response.data);
              }
            } else {
              data.push(response.data);
            }
          });
      }
      this.shares = data;
      console.log(this.shares);
    },
  },
  created() {
    if (this.$route.name === "home") {
      this.path = false;
    }
    if (this.$route.name === "detail") {
      this.profile = false;
    }
    this.getShares();
  },
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
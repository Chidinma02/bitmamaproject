<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-lg-6 col-sm-12 col-6 mt-4">
          <h3 v-if="current">Dear {{ current.username }}</h3>
        </div>
        <div class="col-lg-3 col-sm-6 col-6 mt-4">
          <button class="btn btn-success" @click.prevent="perlog(current)">
            log out
          </button>
        </div>
        <div class="col-lg-3 col-sm-6 col-12 mt-4">
          <button class="btn btn-success" @click.prevent="sign">
            sign in with another username
          </button>
        </div>
      </div>
      <div class="row mt-3">
        <h2>Lists of users signed in</h2>
        <ul>
          <li v-for="user in users" :key="user.username" class="se mt-3">
            {{ user.username }}
            <button class="btn btn-success" @click.prevent="perlog(user)">
              logout
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BitmamaSec",

  data() {
    return {
      username: "",
      users: [],
      people: "",
      current: null,
    };
  },

  mounted() {
    // console.log(JSON.parse(sessionStorage.getItem("current")));
    // console.log(JSON.parse(localStorage.getItem("lastactivesession")));
    this.users = JSON.parse(localStorage.getItem("users"));
    if (
      sessionStorage.getItem("current") !== null ||
      localStorage.getItem("lastactivesession") !== null
    ) {
      this.current =
        JSON.parse(sessionStorage.getItem("current")) !== null
          ? JSON.parse(sessionStorage.getItem("current"))
          : JSON.parse(localStorage.getItem("lastactivesession"));
      console.log(this.current);
    } else {
      this.$router.push("/second");
    }
  },

  methods: {
    logout() {
      // this.users = this.users.filter((people) => {
      // return people.username !== this.current.username;
      // });
      this.perlog(this.current);

      // sessionStorage.removeItem("current");

      // console.log(this.users);

      // alert("ckkkk");
    },

    perlog(person) {
      this.users = this.users.filter((people) => {
        return people.username !== person.username;
      });
      localStorage.setItem("users", JSON.stringify(this.users));

      if (this.users.length > 0) {
        localStorage.setItem(
          "lastactivesession",
          JSON.stringify(this.users[this.users.length - 1])
        );
      } else {
        localStorage.removeItem("lastactivesession");
      }

      if (person.username === this.current.username) {
        sessionStorage.removeItem("current");
        this.$router.push("/second");
      }
    },

    sign() {
      this.$router.push("/second");
    },
  },
};
</script>

<style lang="css" scoped>
.se {
  text-align: left;
}
</style>
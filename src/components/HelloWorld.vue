<template>
  <div>
    <div class="container vg">
      <div class="row mt-2">
        <div class="col-12 col-lg-6">
          <!-- <div class="row"></div> -->
          <div class="">
            <div class="text-center mt-5">
              <img
                src="../assets/fun-3d-cartoon-teenage-boy.jpg"
                class="img-fluid"
              />
            </div>
          </div>
        </div>
        <div class="col-12 col-lg-6 mt-3 boxshadowing">
          <h1 class="fo mt-5">Holla</h1>
          <p class="fo fi">Sign in the the vibe!</p>
          <p>{{ username }}</p>
          <form class="row g-3 mt-3 fo" @submit.prevent="onlogin">
            <div class="col-md-12 mt-4 bg-white">
              <label for="inputEmail4" class="form-label"> Username</label>
              <input
                type="text"
                class="form-control my-input shadow-none bg-white"
                id="inputEmail4"
                placeholder="Enter  Username"
                v-model="username"
              />
            </div>

            <div class="col-12 ml-3 mr-3 mt-5">
              <button type="submit" class="block pt-3 pb-3">SIGN UP</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  props: {
    msg: String,
  },

  data() {
    return {
      username: "",
      users: [],
      current: null,
    };
  },

  mounted() {
    this.users =
      JSON.parse(localStorage.getItem("users")) === null
        ? []
        : JSON.parse(localStorage.getItem("users"));
  },

  methods: {
    onlogin() {
      console.log("meeeeeeeeeeeeee");
      let user = {
        username: this.username,
      };

      let existinguser = this.users.findIndex(
        (us) => us.username === this.username
      );
      console.log(existinguser);

      if (existinguser === -1) {
        this.users.push(user);
      }
      localStorage.setItem("users", JSON.stringify(this.users));

      this.current = user;
      sessionStorage.setItem("current", JSON.stringify(this.current));
      localStorage.setItem("lastactivesession", JSON.stringify(this.current));
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
* {
  color: black;
}
.logo {
  text-align: left !important;
}
* {
  color: black;
}
.block {
  display: block;
  width: 100%;
  border: none;
  background-color: #4ce895;
  padding: 14px 28px;
  font-size: 16px;
  cursor: pointer;
  text-align: center;
  border-radius: 10px;
  font-weight: bold;
}
.wel {
  color: #4ce895;
}
.h1tag {
  font-size: 49px;
  font-weight: bold;
}
.ht {
  font-weight: bold;
  text-align: center !important;
}
.for {
  text-align: left;
  font-weight: 550;
  word-spacing: 10px;
}
.fo {
  text-align: left;
  font-weight: 540;
}
.fi {
  font-size: 19px;
}
.we {
  font-weight: 500;
}
.last {
  color: #97a19d;
}
.boxshadowing {
  box-shadow: 0 4px 8px 0 rgba(161, 160, 160, 0.2),
    0 6px 20px 0 rgba(161, 160, 160, 0.19);
}

.my-input {
  /*background-color: white !important;
  border-color: none !important;
  color: black !important;*/
  border: 1px solid #cad0c9;
  border-radius: 3px;
}
input:focus {
  border: 1px solid #4ce895 !important;
}
/*.my-input :focus {
  outline: none !important;
  border-color: #719ece;
  box-shadow: 0 0 10px #719ece;
}*/

.form-control {
  background-color: white !important;
}
</style>
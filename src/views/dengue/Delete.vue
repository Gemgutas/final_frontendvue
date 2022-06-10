<template>
  <h1 class="text-center mt-4">Delete Record?</h1>

  <div class="container w-50 border border-radius p-4">
    <form @submit="postData">
      <div class="form-group">
        <label for="municipality">Municipality</label>
        <input
          type="text"
          class="form-control"
          v-model="dengueInfoApplication.municipality"
          id="municipality"
        />
      </div>
      <div class="form-group">
        <label for="barangay">Barangay</label>
        <input
          type="text"
          class="form-control"
          v-model="dengueInfoApplication.barangay"
          id="barangay"
        />
      </div>
      <div class="form-group">
        <label for="deaths">Deaths</label>
        <input
          type="text"
          class="form-control"
          v-model="dengueInfoApplication.deaths"
          id="deaths"
        />
      </div>
      <div class="form-group">
        <label for="recovered">Recovered</label>
        <input
          type="text"
          class="form-control"
          v-model="dengueInfoApplication.recovered"
          id="recovered"
        />
      </div>
      <div class="form-group">
        <label for="month">Month</label>
        <input
          type="text"
          class="form-control"
          v-model="dengueInfoApplication.month"
          id="month"
        />
      </div>

      <button type="submit" class="btn btn-danger mt-4 w-100">Delete</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      dengueInfoApplication: [],
    };
  },

  methods: {
    postData(e) {
      e.preventDefault();
      const postData = {
        municipality: this.dengueInfoApplication.municipality,
        barangay: this.dengueInfoApplication.barangay,
        deaths: this.dengueInfoApplication.deaths,
        recovered: this.dengueInfoApplication.recovered,
        month: this.dengueInfoApplication.month,
      };
      console.log("post data");
      console.log(postData);
      console.log("denguefever");
      console.log(this.dengueInfoApplication);

      fetch("http://192.168.43.14:8000/api/dengue-info-delete/" + this.id, {
        method: "DELETE",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(postData),
      })
        .then((response) => {
          if (response.status === 200) {
            this.$router.push({ path: "/dengue-info" });
          }
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    fetch("http://192.168.43.14:8000/api/dengue-info/" + this.id)
      .then((res) => res.json())
      .then((data) => (this.dengueInfoApplication = data))
      .then((res) => {
        console.log("res");
        console.log(res);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
.width {
  width: 30px;
  height: 30px;
}
.hover-list:hover {
  background: rgb(226, 222, 222);
}
</style>

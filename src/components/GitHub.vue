<template>
  <div class="github">
    <h2>Github Profile</h2>
    <p>
      <div class="card" style="width: 18rem;">
        <img :src="this.results.avatar_url" class="card-img-top" alt="Github Avatar">
        <div class="card-body">
          <h5 class="card-title">{{this.results.name}}</h5>
          <p class="card-text"><a :href="this.results.html_url">Github Account</a></p>
        </div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Number of Public Repositories: {{this.results.public_repos}}</li>
          <li class="list-group-item">Date Created: {{this.results.created_at | trim_date}}</li>
        </ul>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
 
export default {
  name: 'GitHub',
  data () {
    return {
      msg: 'Search',
      results: ''
    }
  },
  methods: {
    getProfile() {
      axios.get('https://api.github.com/users/juda')
        .then( response => {
          console.log(response.data);
          this.results = response.data;
        })
    }
  },
  created() {
    this.getProfile();
  },
  filters: {   
    trim_date: function (value) {   
      if (!value) return ''     
      let date_created = value;
      let date_created_trim = date_created.substr(0, 10);
      return date_created_trim
    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
}
.card {
  margin: 0 auto;
}
</style>

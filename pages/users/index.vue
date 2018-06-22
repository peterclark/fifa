<template lang='pug'>
  .container
    h1 Users
    ul
      li(v-for="(user, index) in users" :key="index")
        nuxt-link(:to="{ name: 'users-id', params: { id: user.id } }") {{ user.name }}
    p
      nuxt-link(to="/") Home
</template>

<script>
import axios from 'axios'

export default {
  asyncData({ req, params }) {
    // We can return a Promise instead of calling the callback
    return axios.get('https://jsonplaceholder.typicode.com/users')
      .then((res) => {
        return { users: res.data.slice(0, 5) }
      })
  },
  head: {
    title: 'List of users'
  }
}
</script>

<style scoped>
.container {
  width: 70%;
  margin: auto;
  text-align: center;
  padding-top: 100px;
}
ul {
  list-style-type: none;
  padding: 0;
}
ul li {
  border: 1px #ddd solid;
  padding: 20px;
  text-align: left;
}
ul li a {
  color: gray;
}
p {
  font-size: 20px;
}
a {
  color: #41B883;
}
</style>
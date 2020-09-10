<template>

 <div>
   <h1>Travel wish list </h1>
  <article v-for="(location, idx) in locations" :key="idx">
    <h2>{{ location.name }}</h2>
    <img :src="location.images">
    <br><button @click="deleteLocation(location.id)">Delete</button>
  </article>
  <form @submit="addLocation(name, image)">
    <input v-model="name" placeholder="Location Name">
    <input v-model="image" placeholder="Location Image URL">
    <button type="submit">Add New Location</button>
</form>
</div>
</template>

<script>
import { db } from '../main'
export default {
  name: 'HelloWorld',
  data () {
    return {
      locations: [],
      name: '',
      images: ''
    }
  },
  firestore () {
    return {
      locations: db.collection('locations').orderBy('createdAt')
    }
  },
  methods: {
    addLocation (name, images) {
      const createdAt = new Date()
      db.collection('locations').add({ name, images, createdAt })
    },
    deleteLocation (id) {
      db.collection('locations').doc(id).delete()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: 600;
}

article{
  border-top: 1px solid black;
  width: 90%;
  display: block;
  margin: auto;
  margin-bottom: 50px;
}
article img{
  width: 500px;
}
article button{
  background-color: #3e54ac ;
  color: white;
  font-weight: 600;
  margin: 20px 0;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 3px;
  transition: 300ms ease-out;
}
button{
  background-color: #3e54ac ;
  color: white;
  font-weight: 600;
  margin: 20px 0;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 3px;
  border: 1px solid #3e54ac;
  transition: 300ms ease-out;
}
button:hover{
  background-color: #fff;
  color: #3e54ac;
}
article button:hover{
  background-color: #ac3e3e;
  color: #fff;
  border: none;
}
</style>

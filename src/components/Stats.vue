<template>
  <div >
    <h1>A different component</h1>

    <p>There are currenty {{ countLinks }} links</p>

    <v-btn class="v-btn" @click="removeAllLinks">Remove All Links</v-btn>
    <p v-if="countLinks < 1">{{ msg }}</p>
  </div>
</template>

<script>
import { mapGetters, mapMutations, mapActions } from 'vuex'

export default {
  name: 'Stats',
  data() {
    return {
      msg: ''
    }
  },
  computed: {
    ...mapGetters([
      'countLinks'
    ]),
    //other stuff
  },
  methods: {
    ...mapMutations([
      'REMOVE_ALL'
    ]),
    ...mapActions([
      'removeAll'
    ]),
    removeAllLinks() {
      this.removeAll().then(() => {
        this.msg = "They have been removed"
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  
}
a {
  color: #42b983;
}

p {
  padding: 10px;
}



.v-btn {
  width: 100%;
  text-align: center;
  background-color: rgb(57, 57, 59);
  border: 1px solid rgb(30, 34, 34);
  cursor: pointer;
  color: white;
}
</style>

<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>

        <v-layout row >
          <v-flex xs11>
                <form @submit.prevent="addLink">
                  <input type="text" class="link-input" placeholder="Add a Link" v-model="newLink" />
                </form>
          </v-flex>
          <v-flex class="btn-submit" xs1>
              <v-btn @click="addLink" fab dark color="grey">
                <v-icon>add</v-icon>     
              </v-btn>
          </v-flex>
        </v-layout>

      <ul>
        <li v-for="(link, index) in links" v-bind:key="index">
          <a target="_blank" :href="link">{{ link }}</a>
            <button @click="removeLink(index)" class="rm"  right>
              <i class="material-icons">delete</i>
            </button>
        </li>
      </ul>
    </div>
    <div class="right">
      <stats />
    </div>
  </div>
</template>

<script>
import Stats from '@/components/Stats.vue'
import { mapState, mapMutations, mapActions } from 'vuex'

export default {
  name: 'HelloWorld',
  data() {
    return {
      newLink: ''
    }
  },
  components: {
    Stats
  },
  computed: {
    ...mapState([
      'title',
      'links'
    ]),
    //other stuff
  },
  methods: {
    ...mapMutations([
      'ADD_LINK'
    ]),
    ...mapActions([
      'removeLink'
    ]),
    addLink: function(){
      if(this.newLink !== ''){
        this.ADD_LINK(this.newLink)
        this.newLink = ''
      }
    },
    removeLinks: function(link){
      this.removeLink(link)
    }
  }
}
</script>

<style>
  html, #app, .home {
    height: 100%;
  }
  body {
    background-color: #F4F4F4;
    margin: 0;
    height: 100%;
  }

  .hello {
    display: grid;
    grid-template-columns: repeat(2, 50%);
    grid-template-rows: 100%;
    grid-template-areas:
      "left right";
    height: 100%;
  }

  .left, .right {
    padding: 30px;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }
  ul li {
    padding: 20px;
    background-color: rgb(38, 39, 49);
    margin-bottom: 8px;
    transition: background-color 0.3s linear 0.01s; 
    box-shadow: 0 5px 5px rgb(30, 34, 34);

  }

  ul li:hover{
    padding: 20px;
    transition: background-color 0.3s linear 0.01s; 
    background-color: rgb(80, 80, 80);
    margin-bottom: 8px;
    box-shadow: 0 5px 5px rgb(30, 34, 34);
  }

  .right {
    grid-area: right;
    background-color: rgb(38, 39, 39);
  }

  input {
    border: none;
    padding: 20px;
    background-color: rgb(38, 39, 49);
    width: 100%;
    box-shadow: 0 5px 5px rgb(30, 34, 34);
    margin-bottom: 50px;
    margin-top: 20px;
    color: white;
    outline: none;
    transition: box-shadow 0.3s linear 0.01s; 
  }

  input:focus {
    border: grey;
    transition: box-shadow 0.3s linear 0.01s; 
    padding: 20px;
    background-color: rgb(38, 39, 49);
    width: 100%;
    box-shadow: 0 8px 8px rgb(133, 131, 131);
    margin-bottom: 50px;
    margin-top: 20px;
    color: white;
    outline: none;
  }

  .btn-submit {
    padding-top: 18px;
    
  }

  .rm {
    float: right;
    text-transform: uppercase;
    font-size: .8em;
    border: none;
    color: red;
    cursor: pointer;
  }

.rm-icon {
    float: right;
    cursor: pointer;
}

a {
  color: white;
}
</style>
<template>
<div class="hello">
 <div class="left">
      <h1>{{ title }}</h1>
      <form @submit.prevent="addLink">
   <input class="link-input" type="text" placeholder="Add a Link" v-model="newLink" />
</form>
      <ul>
  <li v-for="(link, index) in links" v-bind:key="index">
    {{ link }}
    <button v-on:click="removeLinks(index)" class="rm">Remove</button>  <!-- Add this -->
  </li>
</ul>
      
    </div>
    <div class="right">
      <stats />  <!-- Add this -->
    </div>
</div>
</template>
<script>
import Stats from "@/components/Stats.vue";
import { mapState, mapMutations, mapActions } from 'vuex'

export default {
  name: "HelloWorld",
  data() {
    // Add this:
    return {
      newLink: ""
    };
  },
  components: {
    // Add this
    Stats
  },
  computed: {
    ...mapState(["title", "links"])
  },
  methods: {
    // Add this:
    ...mapMutations(["ADD_LINK"]),
    ...mapActions([                  // Add this
      'removeLink'
    ]),
    addLink: function() {
      this.ADD_LINK(this.newLink)
      this.newLink = '';
    },
    removeLinks: function(link) {    // Add this
      this.removeLink(link)
    }
  }
};
</script>

<style>
html,
#app,
.home {
  height: 100%;
}
body {
  background-color: #f4f4f4;
  margin: 0;
  height: 100%;
}

.hello {
  display: grid;
  grid-template-columns: repeat(2, 50%);
  grid-template-rows: 100%;
  grid-template-areas: "left right";
  height: 100%;
}

.left,
.right {
  padding: 30px;
}

ul {
  list-style-type: none;
  padding: 0;
}
ul li {
  padding: 20px;
  background: white;
  margin-bottom: 8px;
}

.right {
  grid-area: right;
  background-color: #e9e9e9;
}
input {
  border: none;
  padding: 20px;
  width: calc(100% - 40px);
  box-shadow: 0 5px 5px lightgrey;
  margin-bottom: 50px;
  outline: none;
}
 .rm {
    float: right;
    text-transform: uppercase;
    font-size: .8em;
    background: #f9d0e3;
    border: none;
    padding: 5px;
    color: #ff0076;
    cursor:pointer;
  }
</style>
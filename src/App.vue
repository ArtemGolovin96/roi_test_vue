<template>
  <div id="app">
    <add-button @click="openedAddWindow"/>
    <div class="items">
    <empl-list/>
    <add-form-employee v-bind:opened="openAddWindow"/>
    </div>
  </div>
</template>

<script>
import AddButton from './components/AddButton';
import EmplList from './components/EmplList';
import AddFormEmployee from './components/AddFormEmployee';


export default {
  name: 'App',
  components: {
    AddButton,
    EmplList,
    AddFormEmployee,
  },
  data() {
    return {
      openAddWindow: false,
    };
  },

  methods: {
    openedAddWindow(clicked) {
      this.openAddWindow = clicked;
      console.log();
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  background-color: #f06060;
  display: flex;
  align-items: center;
  color: #fff;
  flex-direction: column;
  height: 100vh;
  }


.items {
  display: flex;
  flex-direction: row;
}
</style>

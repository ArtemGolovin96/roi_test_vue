<template>
  <div id="app">
    <add-button/>
    <div class="items">
    <empl-list/>
    </div>
  </div>
</template>

<script>
import AddButton from './components/AddButton';
import EmplList from './components/EmplList';


export default {
  name: 'App',
  components: {
    AddButton,
    EmplList,
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
</style>

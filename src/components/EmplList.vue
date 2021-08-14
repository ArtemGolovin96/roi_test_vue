<template>
<div class="empl-list-wrapper" v-if="listOfEmployees">
    <table  class="empl-list-wrapper__items" v-for="item in listOfEmployees" :key="item">
    <caption>Список сотрудников</caption>
    <th>Имя сотрудника</th>
    <th>Телефонный номер</th>
        <tr>
        <td>{{item.name}}</td>
        <td>{{item.phoneNumber}}</td>
        </tr>
    </table>
</div>

<div class="empl-list-wrapper" v-else>
    <table  class="empl-list-wrapper__items">
    <caption>Список сотрудников</caption>
    <th>Имя сотрудника</th>
    <th>Телефонный номер</th>
    </table>
</div>
</template>

<script>

export default {
  name: 'EmplList',
  data() {
    return {
      tableName: 'Список сотрудников',
      listOfEmployees: null,
    };
  },

  async mounted() {
    if (!localStorage.listOfEmployees) {
      console.log('ошибка');
    }
    const localListOfEmployees = await JSON.parse(localStorage.getItem('listOfEmployees'));
    console.log(localListOfEmployees);
    this.listOfEmployees = [...localListOfEmployees];
  },

};


</script>

<style scoped>

table {
    min-width: 200px;
    border-collapse: separate;
    border-spacing: 2vh;
    background-color: #fff;
    color: black;
    border-radius: 15px;
    margin: 10vh;
    border: 1px solid black;
    padding: 3vh;
}

table thead tr {
    color: #fff;
    font-weight: bold;
}


</style>

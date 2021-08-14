<template>
<div class="empl-list-wrapper">
    <table class="empl-list-wrapper__items" v-for="item in listOfEmployees" :key="item">
    <caption>Список сотрудников</caption>
    <th>Имя сотрудника</th>
    <th>Телефонный номер</th>
        <tr>
        <td>{{item.name}}</td>
        <td>{{item.phoneNumber}}</td>
        </tr>
    </table>
</div>
</template>

<script>

export default {
  name: 'EmplList',
  data() {
    return {
      tableName: 'Список сотрудников',
      listOfEmployees: [
        { id: null, name: 'Artem', phoneNumber: +79997148827, manager: null },
      ],
    };
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
    margin: 10vh 0 0 -30vh;
    border: 1px solid black;
}

table thead tr {
    color: #fff;
    font-weight: bold;
}


</style>

<template>
<div class="empl-list-wrapper" v-if="listOfEmployeesClient">
        <table  class="empl-list-wrapper__items">
            <button
    class="empl-list-wrapper__sort-button"
    @click="clickOnSortButton"
    >
    Сортировать в алфавитном порядке
    </button>
        <caption>Список сотрудников</caption>
        <th>Имя сотрудника</th>
        <th>Телефонный номер</th>
            <tr v-for="(item, i) in listOfEmployeesClient" :key="i">
                <td>
                {{item.name}}
                </td>
                <td>{{item.phoneNumber}}</td>
            <table class="substring-wrapper" v-if="item.manageEmployee.length > 0">
            <caption
            role="button"
            class="table__div-role-button"
            >
            <u>Подчиненные руководителя - {{item.name}}:</u> <span class="arrow">ᐁ</span>
            </caption>
                <div class="substring" v-for="(el, ind) in item.manageEmployee" v-bind:key="ind">
                    <td>{{el.name}}</td>
                    <td>{{el.phoneNumber}}</td>
                </div>
            </table>
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
      listOfEmployeesClient: null,
      previoslistOfEmployeesClient: null,
    };
  },


  mounted() {
    const localListOfEmployeesFirst = JSON.parse(localStorage.getItem('listOfEmployees'));
    this.listOfEmployeesClient = [...localListOfEmployeesFirst];
    this.previoslistOfEmployeesClient = [...localListOfEmployeesFirst];
  },

  methods: {
    clickOnSortButton() {
      const sortedlistOfEmployees = [...this.listOfEmployeesClient];
      console.log(sortedlistOfEmployees[0].name);
      console.log(this.previoslistOfEmployeesClient[0].name);
      if (sortedlistOfEmployees[0].name.localeCompare(this.previoslistOfEmployeesClient[0].name)) {
        sortedlistOfEmployees.sort((a, b) => a.name.localeCompare(b.name));
        this.listOfEmployeesClient = [...sortedlistOfEmployees];
      } else if
      (!sortedlistOfEmployees[0].name.localeCompare(this.previoslistOfEmployeesClient[0].name)) {
        sortedlistOfEmployees.sort((a, b) => b.name.localeCompare(a.name));
        this.listOfEmployeesClient = [...sortedlistOfEmployees];
      }
    },
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


.substring-wrapper {
    border-radius: 15px;
    border: 1px solid black;
    padding: 3vh;
}


.table__div-role-button:hover{
    color: #f06060;
}


</style>

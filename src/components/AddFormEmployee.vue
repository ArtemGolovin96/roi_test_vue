<template>
<div class="add-empl-form-wrapper" v-if="opened">
    <form action="submit" class="add-empl-form-wrapper__form" @submit="submit" id="form">
        <h3 class="form__h">Добавить пользователя</h3>
        <input
        class="form__name-input input"
        name="=name"
        placeholder="Name"
        v-model.trim="name"
        type="text">
        <input
        class="form__number-input input"
        name="phoneNumber"
        placeholder="Phone number"
        v-model="phoneNumber"
        >
        <select name="manager" v-model="selectedValueManager" v-if="dataFromLocalStorage">
        <option disabled selected hidden>Выбрать руководителя</option>
            <option v-for="(item, i) in dataFromLocalStorage" :key="i"
            v-bind:value="item.id"
            >
            {{item.name}}
            </option>
            <option value="00">Руководящий состав</option>
        </select>
        <button type="submit" class="form__save-button">Сохранить</button>
    </form>
</div>
</template>

<script>

export default {
  name: 'addFormEmploee',
  data() {
    return {
      name: null,
      phoneNumber: '+7',
      opened: false,
      listOfEmployeesFromJson: [],
      selectedValueManager: '',
      dataFromLocalStorage: null,
    };
  },

  mounted() {
    this.getDataFromLocalStorage();
  },


  methods: {

    async getDataFromLocalStorage() {
      const listOfEmployeesFromJson = await JSON.parse(localStorage.getItem('listOfEmployees'));
      this.dataFromLocalStorage = [...listOfEmployeesFromJson];
    },

    submit() {
      // Можно и инстансом класса
      const employeeItem = {
        id: Date.now(),
        name: this.name,
        phoneNumber: this.phoneNumber,
        manger: this.selectedValueManager,
        manageEmployee: [],
      };

      // из-за своей глупой ошибки, так нахардкодил, времени исправлять не было, простите
      if (!this.dataFromLocalStorage) {
        console.log('first');
        this.listOfEmployeesFromJson.push(employeeItem);
        localStorage.setItem('listOfEmployees', JSON.stringify(this.listOfEmployeesFromJson));
      } else if (this.selectedValueManager === '00') {
        console.log('Руководитель');
        this.listOfEmployeesFromJson = [...this.dataFromLocalStorage];
        this.listOfEmployeesFromJson.push(employeeItem);
        localStorage.setItem('listOfEmployees', JSON.stringify(this.listOfEmployeesFromJson));
      } else {
        const generatedEmployeedList = this.dataFromLocalStorage.map((el) => {
          if (el.id === this.selectedValueManager) {
            el.manageEmployee.push(employeeItem);
            return el;
          // Знаю, что лучше делать по value, не получилось из-за disabled selected hidden(
          } else if (this.selectedValueManager === '') {
            alert('Статус сотрудника не определен');
          }
          return el;
        });
        localStorage.setItem('listOfEmployees', JSON.stringify(generatedEmployeedList));
      }
    },


  },

  props: {
    opened: [Boolean],
  },
};


</script>

<style scoped>

.add-empl-form-wrapper {
    min-width: 200px;
    background-color: #fff;
    color: black;
    border-radius: 15px;
    margin: 10vh;
    border: 1px solid black;
    padding: 3vh;
    min-height: 300px;
}

input {
    min-width: 100px;
    margin: 3vh auto;
    padding: 2vh;
    border-radius: 15px;
    outline: none;
}


select {
    min-width: 150px;
    margin: 3vh auto;
    padding: 2vh;
    border-radius: 15px;
    outline: none;
}

.add-empl-form-wrapper__form {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.form__save-button {
    -webkit-appearance: button;
    border-color: rgb(216, 216, 216) rgb(209, 209, 209) rgb(186, 186, 186);
    border-style: solid;
    border-width: 1px;
    padding: 10px;
    border-radius: 15px;
    text-rendering: auto;
    color: initial;
    display: inline-block;
    text-align: center;
    font: 400 11px system-ui;
    min-width: 100px;
    font-size: 1.5em;
}

.form__save-button:hover {
    box-shadow: 0 0 30px 3px #f06060;
    transition: all 0.5s leaner;
}


</style>

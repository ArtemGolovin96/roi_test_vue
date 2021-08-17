<template>
  <div class="add-button-wrapper">
    <button class="add-button-wrapper__button" @click="click">
      <strong>{{innerText}}</strong>
    </button>
  </div>
</template>

<script>
export default {
  name: 'AddButton',
  data() {
    return {
      innerText: 'Добавить в список',
      clicked: false,
    };
  },

  methods: {
    click() {
      // Я все понимаю, но тут я это сделал специально
      if (!this.clicked) {
        this.clicked = true;
        this.$emit('click', this.clicked);
        this.innerText = 'Скрыть поле добавления';
      } else {
        this.clicked = false;
        this.$emit('click', this.clicked);
        this.innerText = 'Добавить в список';
      }

      console.log('clicked');
    },
  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.add-button-wrapper__button {
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
    margin: 10vh 0 0 10vh;
    font: 400 11px system-ui;
    min-width: 100px;
    font-size: 1.5em;
}

.add-button-wrapper__button:hover {
    box-shadow: 0 0 30px 3px #fff;
    transition: all 0.5s leaner;
}

</style>

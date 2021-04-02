<template>
  <div>
    <div class="checkbox">
      <div><input type="checkbox"
             v-model="value"
             v-indeterminate="middleState"
             @change="selectAll()"
             :ref="cat.name.en"
             class="custom-checkbox"
             name="custom-checkbox"
             :id="cat.name.en">
      <label :for="cat.name.en"></label>
    </div><div>{{cat.name.rus}}</div>
    </div>
    <div class="subitems">
      <div v-for="(value, key, index) in subitems" :key="key" class="checkbox">
        <div><input type="checkbox"
                    ref="subitem"
                    v-model="subcatitems"
                    :value="value"
                    class="custom-checkbox"
                    @change="changeMedium($event)"
                    :id="`${value}${index}`">
        <label :for="`${value}${index}`"></label></div><div>{{value}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomCheckbox',
  props: {
    cat: Object,
    subitems: Array
  },
  data () {
    return {
      middleState: false,
      value: false,
      subcatitems: []
    }
  },
  directives: {
    indeterminate: function (el, binding) {
      el.indeterminate = Boolean(binding.value)
    }
  },
  methods: {
    changeMedium () {
      const subItemsLength = this.$refs.subitem.length
      const subitems = this.$refs.subitem.filter(val => val.checked === true)
      if (subitems.length !== 0 && subitems.length !== subItemsLength) {
        this.middleState = true
        this.value = true
      } else if (subitems.length === subItemsLength) {
        this.middleState = false
        this.value = true
      } else {
        this.middleState = false
        this.value = false
      }
    },
    selectAll () {
      this.middleState = false
      this.$refs.subitem.map(val => { val.checked = this.value })
    }
  }
}
</script>

<style scoped>
.subitems {
  margin-left: 10px
}
.checkbox {
  display: flex;
}
/* для элемента input c type="checkbox"*/
.custom-checkbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

/* для элемента label, связанного с .custom-checkbox */
.custom-checkbox + label {
  display: inline-flex;
}

/*!* создание в label псевдоэлемента before со следующими стилями *!*/
.custom-checkbox + label {
  content: '';
  width: 1em;
  height: 1em;
  border: 1px solid #adb5bd;
  border-radius: 0.25em;
  margin-right: 7px;
  background-repeat: no-repeat;
  background-position: center center;
}

/* стили для чекбокса, находящегося в состоянии checked */
.custom-checkbox:checked + label {
  background-image: url("../assets/checked.png");
}
/* стили для чекбокса, находящегося в indeterminate */
.custom-checkbox:indeterminate + label {
  background-image: url("../assets/middle.png");
}

/* стили для чекбокса, находящегося в фокусе и не находящегося в состоянии checked */
.custom-checkbox:indeterminate:not(:checked) + label {
  background-image: url("../assets/middle.png");
}
</style>

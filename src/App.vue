<template>
  <div id="app">
    <CustomForm>
      <div class="category">
        <div v-for="cat in categories" :key="cat.name.en">
          <CustomCheckbox :cat="cat" :subitems="cat.list" :maincheck="true"/>
        </div>
      </div>
    </CustomForm>
  </div>
</template>

<script>
import CustomForm from './components/CustomForm'
import CustomCheckbox from './components/CustomCheckbox'

export default {
  name: 'App',
  components: {
    CustomForm,
    CustomCheckbox
  },
  data () {
    return {
      categories: {
        vegetables: {
          name: {
            rus: 'Овощи',
            en: 'vegetables'
          },
          list: ['Огурцы', 'Морковь', 'Помидоры']
        },
        fruits: {
          name: {
            rus: 'Фрукты',
            en: 'fruits'
          },
          list: ['Бананы', 'Яблоки', 'Груши']
        },
        berries: {
          name: {
            rus: 'Ягоды',
            en: 'berries'
          },
          list: ['Малины', 'Клубника', 'Черника']
        }
      }
    }
  }
}
</script>

<style>
.category {
  display: flex;
}
</style>

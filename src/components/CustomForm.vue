<template>
  <div>
    <form v-on:submit.prevent="onSubmit" class="v-custom-form" ref="customForm">
      <slot></slot>
      <button class="btn-send" value="Сохранить">Сохранить</button>
    </form>
    <div v-if="result.length > 0"><pre>{{result}}</pre></div>
  </div>
</template>

<script>
export default {
  name: 'CustomForm',
  data () {
    return {
      result: []
    }
  },
  methods: {
    onSubmit () {
      const data = []
      this.$children.map(val => {
        for (const key in val.$refs) {
          if (val.$refs[key].checked) {
            let items = val.$refs.subitem.map(item => { if (item.checked) return item.value })
            items = items.filter(val => val)
            data.push({
              category: key,
              items: items
            })
          }
        }
      })
      this.result = data
    }
  }
}
</script>

<style scoped>
.v-custom-form {
  width: 400px;
  height: 150px;
  position: relative;
}
.btn-send {
  background-color: #1873e1;
  border: none;
  color: white;
  padding: 10px 16px;
  text-decoration: none;
  margin: 4px 2px;
  cursor: pointer;
  position: absolute;
  right: 0;
  bottom: 0;
}
</style>

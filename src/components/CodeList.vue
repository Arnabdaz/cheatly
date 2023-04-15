<template>
  <form @change.prevent="changeCode">
    <select>
      <option v-for="item in list" :key="item.id" :value="item.id">
        {{ item.name }}
      </option>
    </select>
  </form>
</template>
<script>
export default {
  name: 'CodeList',
  props: {
    list: {
      type: Array,
      required: true,
    },
  },
  methods: {
    changeCode(e) {
      this.$emit('codeChange', e.target.value);
    },
  },
};
</script>
<style scoped>
form {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
}
select {
  width: 75%;
  padding: 0.5rem;
  font-size: 20px;
  text-align: center;
  color: #fff;
  background-color: #ffffff11;
  border: 1px solid #ffffff55;
  border-radius: 0.5rem;
}

select option {
  color: #000;
}
</style>

<template>
  <div>
    <CustomDropdown :label="'Статус'" :placeholder="'Выберите статус'" :options="statuses" />
  </div>
</template>

<script>
import CustomDropdown from './dropdown.vue';

export default {
  components: {
    CustomDropdown,
  },
  data() {
    return {
      statuses: ["Регистрация", "Ввод в эксплуатацию", "Использование", "Техническое обслуживание"],
    };
  },
};
</script>

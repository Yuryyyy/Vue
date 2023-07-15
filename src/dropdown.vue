<template>
  <div class="dropdown">
    <h2 v-if="label">{{ label }}</h2>
    <input
      v-model="searchTerm"
      type="text"
      :placeholder="placeholder"
      @click="isOpen = true"
    />
    <ul v-if="isOpen && filteredStatuses.length > 0" class="dropdown-menu">
      <li v-for="(status, index) in filteredStatuses" :key="index" @click="selectStatus(status)">
        {{ status }}
      </li>
    </ul>
    <p v-else-if="isOpen">Нет результатов</p>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: "",
    },
    placeholder: {
      type: String,
      default: "",
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      searchTerm: "",
      isOpen: false,
    };
  },
  computed: {
    filteredStatuses() {
      if (this.searchTerm === "") {
        return this.options;
      } else {
        const term = this.searchTerm.toLowerCase();
        return this.options.filter(status =>
          status.toLowerCase().includes(term)
        );
      }
    },
  },
  methods: {
    selectStatus(status) {
      this.searchTerm = status;
      this.isOpen = false;
    },
  },
};
</script>

<style>
.dropdown {
  position: relative;
}

.dropdown h2 {
  margin-bottom: 4px;
}

.dropdown-menu {
  list-style-type: none;
  padding: 0;
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  background-color: #fff;
  border: 1px solid #ccc;
  max-height: 200px;
  overflow-y: auto;
}

.dropdown-menu li {
  cursor: pointer;
  padding: 8px;
}

.dropdown-menu li:hover {
  background-color: #f5f5f5;
}

.dropdown-menu li:last-child {
  border-bottom: none;
}

.dropdown-menu p {
  margin: 8px;
  color: #999;
}
</style>

<template>
  <form class="search-form"
  @submit.prevent="search"
  >
    <input
      class="card-search__input"
      type="text"
      :placeholder="placeholder"
      :value="searchText"
      @input="(event) => $emit('update:searchText', event.target.value)"
    />
    <button type="submit" class="card-search__input-btn">
      <i class="fas fa-search"></i>
    </button>
  </form>
</template>


<script>
export default {
  name: "Search",
  props: {
    'placeholder': String,
    'searchText':String,
    'search': Function,
  }
};
</script>

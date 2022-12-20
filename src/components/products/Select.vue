<template>
  <div class='v-select'>
    <p
        class="title"
        @click="areOptionsVisible = !areOptionsVisible"
    >{{selected}}</p>
    <div
        class="options"
        v-if="areOptionsVisible || isExpanded"
    >
      <p
          v-for="option in options"
          :key="option.value"
          @click="selectOption(option)"
      >
        {{option.name}}
      </p>
    </div>
  </div>
</template>

<script>

  export default {
    name: "v-select",
    props: {
      options: {
        type: Array,
        default() {
          return []
        }
      },
      selected: {
        type: String,
        default: ''
      },
      isExpanded: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        areOptionsVisible: false,
      }
    },
    methods: {
      selectOption(option) {
        this.$emit('select', option)
        this.areOptionsVisible = false;
      },
      hideSelect() {
        this.areOptionsVisible = false;
      },
    },
    computed: {},
     filterOptions() {},
    mounted() {
      document.addEventListener('click', this.hideSelect.bind(this), true)
    },
    beforeUnmount() {
      document.removeEventListener('click', this.hideSelect)
    }
  }
</script>

<style>
  .v-select {
    position: relative;
    width: 200px;
    cursor: pointer;
    text-align: left;
  }
  .title {
    border: solid 1px #aeaeae;
    padding: 8px;
    border-radius: 8px;
    background: rgb(79, 160, 187);
    color: white;
    font-weight: bold;
  }
  .v-select p {
    margin: 0;
    border-radius: 2px;
  }
  .options {
    border: solid 1px #aeaeae;
    border-radius: 8px;
    background: #ffffff;
    position: absolute;
    top: 30px;
    left: 0;
    width: 100%;
    padding: 8px;
  }
  .options p:hover {
    background: #e7e7e7;
  }
</style>
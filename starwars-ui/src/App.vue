<template>
  <div id="app">
    <Loading v-show="loadingOn"/>
    <DataTable v-show="!loadingOn"/>
  </div>
</template>

<script>
import DataTable from './components/DataTable';
import Loading from './components/Loading';

export default {
  name: 'App',
  components: {
    DataTable,
    Loading,
  },
  data() {
    return {
      loadingOn: true,
    };
  },
  mounted() {
    setTimeout(() => {
      this.loadingOn = false;
    }, 5000);
  },
};
</script>

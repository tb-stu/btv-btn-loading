<template>
  <div class="mt-5 d-flex justify-content-around">
    <btn-loading
        class="btn btn-primary"
        :fn="testFn"
        icon="fa fa-save"
        @success="showSuccess"
        @fail="showFail"
    >
      Button spin
    </btn-loading>

    <btn-loading
        class="btn btn-primary"
        :stop-spin="true"
        :fn="testFn"
        icon="fa fa-save"
        @success="showSuccess"
        @fail="showFail"
    >
      Button stop spin
    </btn-loading>

    <btn-loading
        class="btn btn-primary"
        :stop-spin="true"
        :fn="testFn"
        @success="showSuccess"
        @fail="showFail"
    >
      Button without icon
    </btn-loading>

    <btn-loading
        class="btn btn-primary"
    >
      Button not pass fn
    </btn-loading>
  </div>
</template>

<script>
import BtnLoading from './components/BtnLoading'

export default {
  name: 'App',

  components: {
    BtnLoading
  },

  methods: {
    testFn () {
      return axios.get('https://jsonplaceholder.typicode.com/posts', {
        params: {
          q: Math.random(),
        }
      })
    },

    showSuccess (success) {
      alert(`success: ${success}`)
    },

    showFail () {
      alert('fail')
    },
  },
}
</script>

<style>
@import "~bootstrap/dist/css/bootstrap.min.css";
</style>

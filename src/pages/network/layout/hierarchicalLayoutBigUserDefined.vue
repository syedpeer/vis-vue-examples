<template>
  <div>
    <h2>Hierarchical Layout|Big User Defined</h2>
    <vis-network ref="network"
                 :graph-data="graphData"
                 :options="options"
                 :style="containerStyle">
    </vis-network>
  </div>
</template>

<script type="text/javascript">
import jsonp from 'jsonp'

export default {
  data () {
    return {
      graphData: {},
      options: {},
      containerStyle: {
        // width: '100%',
        // height: '600px',
        // border: '1px solid lightgray'
      }
    }
  },
  methods: {
    jsonpHandler (err, data) {
      if (err) {
        console.log(err)
      } else {
        var options = {
          layout: {
            improvedLayout: false,
            hierarchical: true
          }
        }
        console.log('starting layout')
        this.$refs.network.renew(data, options)
        this.graphData = data
        this.options = options
        console.log('layout complete')
      }
    }
  },
  created () {
    jsonp('http://127.0.0.1:8080/static/jsonp/demo.jsonp', {name: 'p'}, this.jsonpHandler)
  }
}
</script>

<style scoped>
</style>

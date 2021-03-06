<template>
  <div><h1>Hierarchical Layout without Physics</h1>
    The hierarchical layout can now be controlled without the use of physics. This is much quicker. The options for this
    are: <br/><br/>

    <table>
      <tr>
        <td width="150px"><code>levelSeparation</code></td>
        <td width="400px">Distance between levels.</td>
      </tr>
      <tr>
        <td><code>nodeSpacing</code></td>
        <td>Minimum distance between nodes on the free axis.</td>
      </tr>
      <tr>
        <td><code>treeSpacing</code></td>
        <td>Distance between different trees (independent networks).</td>
      </tr>
      <tr>
        <td><code>blockShifting</code></td>
        <td>Method for reducing whitespace. Can be used alone or together with edge minimization. Each node will check
          for whitespace and will shift
          it's branch along with it for as far as it can, respecting the nodeSpacing on any level.
        </td>
      </tr>
      <tr>
        <td><code>edgeMinimization</code></td>
        <td>Method for reducing whitespace. Can be used alone or together with block shifting. Enabling block shifting
          will usually speed up the layout process.
          Each node will try to move along its free axis to reduce the total length of it's edges.
        </td>
      </tr>
      <tr>
        <td><code>parentCentralization</code></td>
        <td>When true, the parents nodes will be centered again after the the layout algorithm has been finished.</td>
      </tr>
    </table>
    <br/><br/>
    Play with the settings below the network and see how the layout changes!
    <vis-network :graph-data="graphData"
                 :options="options"
                 :style="containerStyle" >
    </vis-network>
  </div>
</template>
<script>
import {NODES, EDGES} from '../datasources/largeHierarchicalDataset'

export default {
  data () {
    return {
      graphData: {},
      options: {},
      containerStyle: {
        // width: '800px',
        // height: '400px',
        // border: '1px solid lightgray'
      }
    }
  },
  created () {
    this.graphData = {
      nodes: NODES,
      edges: EDGES
    }
    this.options = {
      layout: {
        improvedLayout: false,
        hierarchical: {
          direction: 'UD',
          sortMethod: 'directed'
        }
      },
      interaction: {dragNodes: false},
      physics: {
        enabled: false
      },
      configure: {
        filter: function (option, path) {
          if (path.indexOf('hierarchical') !== -1) {
            return true
          }
          return false
        },
        showButton: false
      }
    }
  }
}
</script>

<style scoped>
  td {
    vertical-align:top;
  }
  table {
    width:800px;
  }
</style>

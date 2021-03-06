# 信息窗体 - 切换

<vuep template="#example"></vuep>

<script v-pre type="text/x-template" id="example">

  <template>
    <div class="map-page-container">
      <vue-map
        vid="mapDemo"  
        :center="center"
        :zoom="zoom"  
        class="map-demo">
        <vue-map-marker 
          v-for="marker in markers" 
          :position="marker.position"
          :custominfo="marker.info"
          :events="markerEvents"></vue-map-marker>
        <vue-map-info-window 
          :offset="offset" 
          :position="position" 
          :visible.sync="visible" >
          <div class="prompt">{{info}}</div>
        </vue-map-info-window>
      </vue-map>
    </div>
  </template>

  <style>
    .map-demo {
      height: 300px;
    }

    .prompt {
      background: white;
      width: 100px;
      height: 30px;
      text-align: center;
    }
  </style>

  <script>
    module.exports = {
      data: function() {
        const self = this
        return {
          zoom: 16,
          center: [121.59996, 31.197646],
          markers: [],
          visible: false,
          position: null,
          offset: [0, -50],
          info: null,
          markerEvents: {
            click() {
              // 非箭头函数,事件回调时this为当前点击的VueMapMarker组件
              self.info = this.$attrs.custominfo
              self.position = this.$$getPosition()
              self.visible = true
            }
          }
        }
      },

      mounted() {
        let markers = []
        let num = 10

        for (let i = 0 ; i < num ; i ++) {
          markers.push({
            info: `marker-${i}`,
            position: [121.59996, 31.197646 + i * 0.001]
          })
        }

        this.markers = markers
      }
    };
  </script>

</script>

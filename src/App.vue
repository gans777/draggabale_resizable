<template>
  <div id="app">
   <b-container>
  <b-row ><b-col ><div class="wrap_place plas_place"> <b-icon icon="plus-square" variant="success" class="h1 mb-0" @click="add_directory"></b-icon></div>
<b-modal id="create_dir" title="BootstrapVue">
    <p class="my-4">тут создание и первичное заполнение нового списка</p>
  </b-modal>
  </b-col>
      </b-row>
</b-container>
    <b-contaner>
      <div class="wrap_place plas_place">
    <div style="height: 500px;width:100%; position: relative;">
    <vue-draggable-resizable :x="25" :y="0" :w="100" :h="100" @dragging="onDrag" @resizing="onResize" :parent="true" style="border-radius:10px;">
      <div class="into_block">Hello! I'm a flexible component1. You can drag me around and you can resize me.<br>
      X: {{ x }} / Y: {{ y }} - Width: {{ width }} / Height: {{ height }}</div >
    </vue-draggable-resizable>
    <vue-draggable-resizable :x="55" :y="0"  :w="100" :h="100" @dragging="onDrag" @resizing="onResize" :parent="true" class="square" style="border-radius:10px;">
      <div class="into_block">Hello! I'm a flexible component2. You can drag me around and you can resize me.<br>
      X: {{ x }} / Y: {{ y }} - Width: {{ width }} / Height: {{ height }}</div >
    </vue-draggable-resizable>
    <vue-draggable-resizable :x="85" :y="0"  :w="100" :h="100" @dragging="onDrag" @resizing="onResize" :parent="true" class="square" style="border-radius:10px;">
      <div class="into_block">Hello! I'm a flexible component3. You can drag me around and you can resize me.<br>
      X: {{ x }} / Y: {{ y }} - Width: {{ width }} / Height: {{ height }}</div >
    </vue-draggable-resizable>
    </div>
    </div>
    </b-contaner>
</div>
</template>

<script>


export default {
  name: 'App',
  components: {
      },
      data() {
        return{

        }
      },
      methods: {
        add_directory(){
          this.$bvModal.show('create_dir');
        }
      }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.square {
  

}
.wrap_blocks{
  display: flex;
  background-color: #ddeecc;
  margin-left:10px;
  margin-right:10px;
}
.plas_place {
  margin: 5px;
  padding: 5px;
  background-color: #ddeecc;
   display: flex;
  flex-direction: row;
}
.into_block {
  width:100%;
  height:100%;
  overflow: hidden;
  border-radius:10px;
   background-color: #828e6f;
}
</style>

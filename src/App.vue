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
    
      <div class="wrap_place plas_place">
    <div style="height: 500px;width:100%; position: relative;">
    <vue-draggable-resizable v-for="(coord,index) in everythinkDraggCoords" :key="index"   :x="coord.x" :y="coord.y" :w="coord.w" :h="coord.h"   :parent="true" @activated="onActivated(index)" @dragging="onDrag" @resizing="onResize"  @deactivated = "onDeactivated()"  style="border-radius:10px;">
      <div class="into_block">Hello! I'm a flexible component1. You can drag me around and you can resize me X: {{ coord.x }} / Y: {{ coord.y }} - Width: {{ coord.w }} / Height: {{ coord.h }}
      </div >
    </vue-draggable-resizable>
   
    </div>
    </div>
    
</div>
</template>

<script>


export default {
  name: 'App',
  components: {
      },
      data() {
        return{
        id_block_emphasized: null,
        everythinkDraggCoords:[
                {id:1,x:250,y:250,w:100,h:100},
                {id:2,x:55,y:0,w:100,h:150},
                {id:3,x:55,y:200,w:100,h:200}
                            ]
        }
      },
      mounted() {
      //  let user = JSON.parse( sessionStorage.user );

        let everythinkDraggCoords=localStorage.getItem('everythinkDraggCoords');
        if (everythinkDraggCoords===null){ return;}
        this.everythinkDraggCoords=JSON.parse(everythinkDraggCoords);
      
        console.log(JSON.parse(everythinkDraggCoords));
        
      },
      methods: {
        onActivated(index){
          console.log(index + "= cliked");
          this.id_block_emphasized=index;
        },
        onDrag(x,y){
         // console.log(x +" "+ y+ w+" "+h);
         this.everythinkDraggCoords[this.id_block_emphasized].x=x;
          this.everythinkDraggCoords[this.id_block_emphasized].y=y;
         
        },
        onResize(x, y, w, h){
          this.everythinkDraggCoords[this.id_block_emphasized].x=x;
          this.everythinkDraggCoords[this.id_block_emphasized].y=y;
          this.everythinkDraggCoords[this.id_block_emphasized].w=w;
          this.everythinkDraggCoords[this.id_block_emphasized].h=h;
        },
        onDeactivated(){
          
         localStorage.setItem('everythinkDraggCoords', JSON.stringify(this.everythinkDraggCoords));
          //console.log(JSON.stringify(this.everythinkDraggCoords));

        },
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

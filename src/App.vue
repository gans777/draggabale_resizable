<template >
  <div id="app">
   <b-container>
  <b-row ><b-col ><div class="wrap_place plas_place"> <b-icon icon="plus-square" variant="success" class="h1 mb-0" @click="add_directory()"></b-icon></div>
<b-modal id="create_dir" title="BootstrapVue">
    <p class="my-4">
      <input v-model.trim="new_window_text" type="text" value="писать текст здесь">
    </p>
  <template #modal-footer>
        <div >
          
          <b-button
            variant="primary"
            class="float-right"
            @click="create_new_window"
          >
            создать
          </b-button>
        </div>
      </template>
  </b-modal>
  </b-col>
      </b-row>
</b-container>
    
      <div class="wrap_place plas_place">
    <div style="height: 500px;width:100%; position: relative;">
    <vue-draggable-resizable v-for="(coord,index) in everythinkDraggCoords" :key="index"   :x="coord.x" :y="coord.y" :w="coord.w" :h="coord.h"   :parent="true" @activated="onActivated(index)" @dragging="onDrag" @resizing="onResize"  @deactivated = "onDeactivated()"  style="border-radius:10px;border:2px solid black;">
      <div class="into_block">{{ coord.text }}<hr>
<div class="wrap_place plas_place"> <b-icon icon="plus-square" variant="success" class="h1 mb-0" @click="add_directory(coord)"></b-icon></div>
        <hr> X: {{ coord.x }} / Y: {{ coord.y }} - Width: {{ coord.w }} / Height: {{ coord.h }}
      </div >
    </vue-draggable-resizable>
   
    </div>
    </div>
   <hr>
   <b-button variant="outline-primary" @click="tmp_localStorageClear" v-if="tmp_localStorage_Clear">очистить память браузера</b-button> 
   <b-button v-else>очищено</b-button>
</div>
</template>

<script>


export default {
  name: 'App',
  components: {
      },
      data() {
        return{
        tmp_localStorage_Clear:true,
        new_window_text:'',
        last_id:null,
        id_block_emphasized: null,
        line_everythinkDraggCoords:{},
        everythinkDraggCoords:[
                               ]
        }
      },
      mounted() {
      //  let user = JSON.parse( sessionStorage.user );

        let everythinkDraggCoords=localStorage.getItem('everythinkDraggCoords');
        if (everythinkDraggCoords===null){ 
          this.tmp_localStorage_Clear=false;
          return;}
        this.everythinkDraggCoords=JSON.parse(everythinkDraggCoords);
      
        console.log(JSON.parse(everythinkDraggCoords));
        
      },
      methods: {
        tmp_localStorageClear(){
          localStorage.clear();
          this.tmp_localStorage_Clear=false;
        },
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
          this.tmp_localStorage_Clear=true;

        },
        add_directory(coord){
          if (coord ===undefined){
            this.line_everythinkDraggCoords={};
          } else {this.line_everythinkDraggCoords=coord;}
          this.$bvModal.show('create_dir');
          },
        create_new_window(){
          console.log('создаю окно'+ this.everythinkDraggCoords.length);
          if (this.isEmpty(this.line_everythinkDraggCoords)){
            this.everythinkDraggCoords.push({id:this.everythinkDraggCoords.length, x:0,y:0,w:100,h:100,text:this.new_window_text});
          }
         else{
          this.everythinkDraggCoords.push({id:this.everythinkDraggCoords.length, x:this.line_everythinkDraggCoords.x+5,y:this.line_everythinkDraggCoords.y+5,w:100,h:100,text:this.new_window_text});
         }
         
         this.$bvModal.hide('create_dir');
         this.new_window_text='';
        },
         isEmpty(obj) {
         for (let key in obj) {
          // если тело цикла начнет выполняться - значит в объекте есть свойства
          return false;
            }
          return true;
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

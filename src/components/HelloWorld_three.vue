<template>
  <div>
      <div id="container"></div>
      <button v-on:click="accelerer()">Faire bouger la Terre et Mars</button>
  </div>
</template>

<script>
import * as three from 'three'
export default {
    name:'TreeJS',
    data(){
        return{
            scene:null,
            camera:null,
            renderer:null,
            mesh:null,
        }
    },
     methods: {
    init: function() {
        let container = document.getElementById('container');
        let tailleTab = 16
        this.camera = new three.PerspectiveCamera(70, container.clientWidth/container.clientHeight, 0.01, 20);
        this.camera.position.z = 15;
        this.camera.position.x = 0;
        this.camera.position.y = 0  ;
        this.scene = new three.Scene();
     
        var geometry = new three.SphereGeometry(5, 20, 20);
        var soleil = new three.MeshBasicMaterial( {color: 0xFFFF00, side: three.DoubleSide} );
        this.meshsoleil = new three.Mesh( geometry, soleil )
        this.scene.add(this.meshsoleil);


        var geometry2 = new three.SphereGeometry(1, 20, 20);
        var terre = new three.MeshBasicMaterial( {color: 0x0000FF3, side: three.DoubleSide} );
        this.meshterre = new three.Mesh( geometry2, terre )
        this.scene.add(this.meshterre);

        var geometry3 = new three.SphereGeometry(1, 20, 20);
        var mars = new three.MeshBasicMaterial( {color: 0x0FF0000, side: three.DoubleSide} );
        this.meshmars = new three.Mesh( geometry3, mars )
        this.scene.add(this.meshmars);

        this.meshsoleil.position.x = 0
        this.meshsoleil.position.y = 0

        this.meshterre.position.x = -10
        this.meshterre.position.y = 0
    
        this.meshmars.position.x = 7
        this.meshmars.position.y = 0

        this.renderer = new three.WebGLRenderer({antialias: true});
        this.renderer.setSize(container.clientWidth, container.clientHeight);
        container.appendChild(this.renderer.domElement);

},
    animate: function() {
         
        requestAnimationFrame(this.animate);
        this.meshsoleil.rotation.x += 0.01;
        this.meshsoleil.rotation.y += 0.00;

        this.meshterre.rotation.x += 0.01;
        this.meshterre.rotation.y += 0.00;

        this.meshmars.rotation.x += 0.01;
        this.meshmars.rotation.y += 0.00;

        this.renderer.render(this.scene, this.camera);
    },

    accelerer: function(){
      requestAnimationFrame(this.animate);
      this.meshterre.position.x += 2;
      this.meshmars.position.x += -1.5;
    }
  },
    mounted(){
        this.init();
        this.animate();
    },
}
</script>

<style>
#scene-container {
  width: 60%;
  height: 60%;
  background-color: skyblue;
}
#container{
    width: 1000px;
    height: 700px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
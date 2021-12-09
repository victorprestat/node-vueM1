<template>
<div>
    <h1>Page threeJS</h1>
    <div id="container">
    </div>

  </div>
</template>

<script>
import * as three from 'three';
import oc from 'three-orbit-controls';

export default {
  name: 'tJS',
  data () {
      return{
          scene: null,
          camera: null,
          renderer:null,
          mesh: null,
      }
    
  },methods: {
    init: function() {
        let container = document.getElementById('container');
        console.log(container);
        this.camera = new three.PerspectiveCamera(40, container.clientWidth/container.clientHeight, 0.1, 3000);
        this.camera.position.z = 60;
        this.camera.position.x = 0;
        this.camera.position.y = 0  ;

        this.scene = new three.Scene();
     
        this.forme = new three.Group();

        this.geometrie = new three.TorusKnotGeometry(11, 3, 88, 10);

        this.materiel = new three.MeshBasicMaterial({
            color: 0x780000,
            transparent: true,
            opacity: 0.8,
            wireframe: true,
            wireframeLinewidth: 2,
            wireframeLinejoin:'round',
            wireframeLinecap:'round'

        });

        this.forme.add(new three.Mesh(this.geometrie, this.materiel));

        this.scene.add(this.forme);

        this.hlight = new three.AmbientLight(0x404040,100);
        this.scene.add(this.hlight);

        this.directionalLight = new three.DirectionalLight(0xffffff,100);
        this.directionalLight.position.set(1,1,1);
        this.directionalLight.castShadow = true;
        this.scene.add(this.directionalLight);

        this.light = new three.PointLight(0xc4c4c4,10);
        this.light.position.set(10,10,10);
        this.scene.add(this.light);



        const OrbitControls = oc(three);

        this.control = new OrbitControls(this.camera);
        this.control.update();
        //const geometry = new three.PlaneGeometry( 10   , 10 );
        //const terre = new three.MeshBasicMaterial( {color: 0x32CD32, side: three.DoubleSide} );
        //this.mesh = new three.Mesh( geometry, terre )
        // this.scene.add(this.mesh);
        // this.mesh.position.x = 0
        //this.mesh.position.y = 0
        //this.renderer = new three.WebGLRenderer({antialias: true});
        //this.renderer.setSize(container.clientWidth, container.clientHeight);

        this.renderer = new three.WebGLRenderer({antialias: true});
        this.renderer.setSize(container.clientWidth, container.clientHeight);
        this.renderer.setClearColor(0x111111);


        container.appendChild(this.renderer.domElement);
        },
        





        
        
    animate: function() {
        requestAnimationFrame(this.animate);
        this.forme.rotation.x += 0.005;
        this.forme.rotation.y += 0.005;
        this.renderer.render(this.scene, this.camera);
        },


  },mounted(){

      /*const container = document.querySelector("scene-container");

        const fov = 70; // AKA Field of View
        const aspect = container.clientWidth / container.clientHeight;
        const near = 0.1; // the near clipping plane
        const far = 100; // the far clipping plane

        this.camera = new three.PerspectiveCamera(fov, aspect, near, far);
        this.scene = new three.Scene();
        camera.position.set(0, 0, 15);
        const geometry = new three.BoxBufferGeometry(2, 2, 2);
        const material = new three.MeshBasicMaterial();
        const cube = new three.Mesh(geometry, material);
        scene.add(cube);

        const geometrye = new three.PlaneGeometry( 1, 1 );
        const terre = new three.MeshBasicMaterial( {color: 0x32CD32, side: three.DoubleSide} );


        const mech = new three.Mesh(geometrye, terre);

        this.scene.add(mech);



        this.renderer = new three.WebGLRenderer();
        this.renderer.setSize(container.clientWidth, container.clientHeight);
        this.renderer.setPixelRatio(window.devicePixelRatio);
        container.append(this.renderer.domElement);
        this.renderer.render(this.scene, this.camera);
*/

this.init();
this.animate();


}


}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  font-family: 'Pokemon Solid', sans-serif;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#container{
    width: 100%;
    height: 700px;
    margin-left: auto;
    margin-right: auto;
  }

</style>

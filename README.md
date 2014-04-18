threejs-panoram
===============

Эта панорама слегка модернизированный вариант оригинала - http://threejs.org/examples/#webgl_panorama_equirectangular

что изменено?

1. Геометрия сферы не позволяет создавать объекты внутри нее
```javascript
geometry.applyMatrix( new THREE.Matrix4().makeScale( -1, 1, 1 ) );
```
комментируем и дописываем
```javascript

// geometry.applyMatrix( new THREE.Matrix4().makeScale( -1, 1, 1 ) );

  var material = new THREE.MeshBasicMaterial( {
					map: THREE.ImageUtils.loadTexture( './2294472375_24a3b8ef46_o.jpg' ),
					// накладываем текстуру внутрь
					side: THREE.BackSide
				} );
```

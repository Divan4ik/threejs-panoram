threejs-panoram
===============

Эта панорама слегка модернизированный вариант оригинала - http://threejs.org/examples/#webgl_panorama_equirectangular

что изменено?

#### 1. Геометрия сферы не позволяет создавать объекты внутри нее
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
#### 2. Добавляем Raycaster ( компонент для векторных расчетов )

Исходный пример - http://threejs.org/examples/#webgl_interactive_cubes

нам необдимы эти строчки: 
```javascript

//в global
var mouse = new THREE.Vector2(), INTERSECTED;

// в init()
projector = new THREE.Projector();
raycaster = new THREE.Raycaster();

// в render() или 	в update()
var vector = new THREE.Vector3( mouse.x, mouse.y, 1 );
projector.unprojectVector( vector, camera );

raycaster.set( camera.position, vector.sub( camera.position ).normalize() );


//var intersects = raycaster.intersectObjects( scene.children );
// Не забываем что mesh - сфера, тоже часть сцены. отслеживаем массив нужных элементов
var intersects = raycaster.intersectObjects( custom_elements_array );


if ( intersects.length > 0 ) {

	if ( INTERSECTED != intersects[ 0 ].object ) {

		if ( INTERSECTED ) INTERSECTED.material.emissive.setHex( INTERSECTED.currentHex );

		INTERSECTED = intersects[ 0 ].object;
		INTERSECTED.currentHex = INTERSECTED.material.emissive.getHex();
		INTERSECTED.material.emissive.setHex( 0xff0000 );

	}

} else {

	if ( INTERSECTED ) INTERSECTED.material.emissive.setHex( INTERSECTED.currentHex );

	INTERSECTED = null;

}

// в обработчик движения мыши

mouse.x = ( event.clientX / window.innerWidth ) * 2 - 1;
mouse.y = - ( event.clientY / window.innerHeight ) * 2 + 1;

```

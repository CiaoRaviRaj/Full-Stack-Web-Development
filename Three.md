* # Three 
    * npm init -y 
    * npm i three
    * <script type="module" src="client.js"></script>

    * import * as THREE from 'three'
    * import "/style.css"
    * scene
        * const scene = new THREE.Scene();
    * Geometry
        * const geometry = new THREE.SphereGeometry(size, segmentWidth, segmentHeight)
    * Material
        * const material = new THREE.MeshStandardMaterial({
            color: '#00ff83,
            roughness: 0.2
        })
    * Mesh
        * const mesh = THREE.Mesh(geometry, material)
    * add mesh to the scene
        * scene.add(mesh)
    * sizing (optional)
        * const size = {
            width: window.innerWidth,
            height: window.innerHeight
        }
    * add the light
        * const light = new THREE.PointLight(0xffffff, 1, 100)
        * light.position.set(0,10,10)
        * scene.add(light)
    * add camera
        * Frustum 
        * const camera = new THREE.PerspectiveCamera(
            * fieldOfView(50 idea),
            * //aspectRatioForCamera
            size.width / 
            size.height,
            * near view limit
            0.1
            * faraway view limit
        )
        * camera.position.z = 20
        * scene.add(camera) 

        * orthographyCamera
            * left , right , top , button , near , far
        * view a particular axis using orthographyCamera
            * camera.position.y = 2 (top - button view)
            * camera.lookAT(new THREE.Vector3(0,0,0))

    * Rendering 
        * const canvas = document.querySelector('.webgl')
        * const renderer = new THREE.WebGLRenderer({canvas})
    * set of the size of renderer
        * renderer.setSize(size.width, size.height)
        * renderer.setPixelRatio(2)
        
    * Render the scene and camera 
        * renderer.render(scene, camera)

    * updating size on the changing width size 
        * window.addEventListener("resize", () => {
            * sizes.width = window.innerWidth
            * sizes.height = window.innerHeight
            * reset camera and render size
                * camera.aspect = sizes.width/sizes.height
                * camera.updateProjectionMatrix()
                    // it is called you need to change the frustum
                * renderer.setSize(sizes.width, sizes.height)
        })
    * now we need to render the component
        * const loop = () => {
            * mesh.rotation.x += 0.01
            * controls.update()
            * renderer.render(scene, camera)
            * window.requestAnimationFrame(loop)
            // animation 60 frame per second
        }
        * loop()
    * controller
        * import { OrbitControls } from "three/examples/jsm/controls/OrbitControls"
        * after canvas
        * const controls = new OrbitControls(camera, canvas)
            * controls.enableDamping = true
            * controls.enablePan = false 
            * controls.enableZoom = false
            * controls.autoRotate = true
            * controls.autoRotateSpeed = 5
    * animation
        * gsap module
        * import gsap from ' '
        * const t1 = gsap.timeline({
            const t1 = gsap.timeline({
                defaults : {
                     duration: 1
                    }
            })
            
        })
        * t1.fromTo(mesh.scale, {z: 0, x: 0, y : 0 }, { z: 1, y: 1, y: 1})
        * t1.fromTo("nav", {y: "-100%"}, { y: "0%"})
        * t1.fromTo("title", { opacity : 0} , { opacity : 1})
* concepts
    * OBJECT3D
        * Rotation
        * scale
        * position
        * visible
    * Geometries
        * BoxGeometry(width , height, depth, widthSegments , heightSegments, depthSegment)
            * all value equal to 1 by default
        * mesh.geometry.dispose() // to remove object from scene
        * mesh.geometry = newGeometry
        * Rotation, scale , position are changing transformational matrix not object 
        * sphere
            * .SphereGeometry(radius, widthSegments, heightSegments, phiStart, phiLength, thetaStart, thetaLength)
                * 
        * IcosahedronGeometry
            * .IcosahedronGeometry(radius, detail)
    * Material
        * gui.addFolder('THREE.Material')
            * transparent
                * it need to be true ,To use opacity
                * material.transparent = true
                * material.opacity = 0.122
            * opacity
            * depthTest
                * 
            * depthWrite
                * 
            * alphaTest
                * it
            * visible
            * side
                * material.side = THREE.FrontSide
                * material.side = THREE.BackSide
                * material.side = THREE.DoubleSide
                    * it is 
        * .MeshBasicMaterial()
            * it is white color structure
            * To give color picker in gui
                * var data = {
                    color : material.color.getHex()
                }
            * it do not need light 
                * auto luminating
            * wireframe
                * to show structure side
            
            * adding texture
                * const texture = new THREE.TextureLoader().load('img/grid.png')
                * material.map = texture
            * environment texture for reflection 
                * const envTexture = new THREE.CubeTextureLoader().load(['img1','img2','img3','img4','img5',img6'])
                * envTexture.mapping = THREE.CubeReflectionMapping
                * material.envMap = envTexture
            * reflectivity
                * it applied to CubeReflectionMapping
            * refectionRation
                * it applied to CubeRefractionMapping
            * combine
                * THREE.MultiplyOperation
                * THREE.MixOperation
                * THREE.AddOperation
            *  meshBasicMaterialFolder.addColor(data, 'color').onChange(() => {
                material.color.setHex(Number(data.color.toString().replace('#', '0x'))) 
            })
        * .MeshNormalMaterial()
            * it is not need lighting
            * wireframe
            * flatShading
        * .MeshLambertMaterial
            * matte diffusely reflected
                * it is used for wood and stone
            * default it need light 
            * emissive
                * material.emissive.getHex()
        * MeshPhongMaterial
            * it is need more computation power
            * similar like MeshLamberMaterial
            * emissive
                * material.emission.getHex()
            * specular
                * material.emission.getHex()
                * // for shining 
            * shininess
                * intensity of shining
            * 
        * MeshStandardMaterial
            * it is physically 
            * for more realistic material
            * emissive
            * flatShading
            * roughness
                
            * metalness
        * MeshPhysicalMaterial
            * it extension of MeshStandardMaterial with more reflection option
            * emiisive
            * flatShading
            * reflection
            * refractionRatio
            * roughness
            * metalness
            * clearcoat
                * it is more detail sine
            * clearcoatRoughness
        * MeshMatcapMaterial
            * it is more efficient
            * it used image for reflection
                * you can search it on google
            * const matcapTexture = new THREE.TextureLoader().load("img")
            * you can get environment map with it
        * MeshToonMaterial
            * toon shading cel shading
            * non - photo reflective
            * it use color as reflection
            * color
            * flatshading
            * specular
            * shininess
            * gradientMap
                * fourTone
                    * fourTone.minFilter = THREE.NearestFilter
                    * fourTone.magFilter = THREE.NearestFilter
                    * used meet mapping 
                * material.gradientMap = eval(data.gradientMap)
                * material.needsUpdate = true
        * Specular Map
            * affects the specular surface highlight and environment in MeshPhongMaterial
            * meshLambertMaterial, meshPhongMaterial, MeshToonMaterial have the SpecularMap option
            * const specularTexture = new THREE.TextureLoader().load("img/")
            * material.specularMap = specularTexture
            * it is 
        * Roughness and Metalness Maps
            * like specular 
            * it is used for meshStandardMaterial and MeshPhysicalMaterial
            * material.roushnessmap= 
            * material.metalnessMap
        * Bump map
            * it create a bump map , it preceived depth in related to light
            * material.bumpMap(texture)
            * bumpScale
* Additional Module
    * for frame rate stats
        * stats.module.js
        *  import Stats from '/jsm/libs/stats.module'
        * after canvas
            * const stats = Stats()
            * document.body.appendChild(stats.dom)
            * end this animation loop update the stats
                * stats.update()
            * used to manager particular section of code
                * stats.end() 
                * stats.begin()
    * For GUI for helper    
        * import {GUI} form '/jsm/libs/dat.gui.module'
        * for typescript
            * for type definition of GUI 
                * npm i @types/dat.gui
        * after convas
            * const gui = new GUI()
        * giving some controls
            * gui.add(cube.rotation, "x", minValue, maxValue, steps)
            * gui.add(cube.rotation, "y", minValue, maxValue, steps)
            * gui.add(cube.rotation, "z", minValue, maxValue, steps)
        * making a dropdown folder 
            * const cubeFolder = gui.addFolder("folderName")
            * cubeFolder.add(cube.rotation, "x", minValue, maxValue, steps)
            * const cameraFolder = gui.addFolder("camera")
            * cameraFolder.add(camera.position, "z", 0 ,10, 0.01)
            * cubeFolder.open()
            * cameraFolder.open()
    * Axis helper
        * ver axesHelper = new THREE.AxesHelper(5)
        * scene.add(axesHelper)
        * green -> y
        * red -> x
        * blue -> z
    
        
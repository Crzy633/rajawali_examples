# Examples of Rajawali



the codes right here are not my work, they come from [Rajawali/Rajawali: Android OpenGL ES 2.0/3.0 Engine (github.com)](https://github.com/Rajawali/Rajawali)

I just pulled out the example code so you could run it immediately.







---

by the way, share little thing about starting to use it.

 

#### first, the steps of starting to use Rajawali*(I use kotlin language)*:

1. write`<org.rajawali3d.view.TextureView>`in`activity_main.xml`

2. let a class extends `Renderer(context)` and write these:

   ```kotlin
   override fun initScene() {
   	DirectionalLight(1.0, 0.2, -1.0).apply {
   		setColor(1.0f, 1.0f, 1.0f)
   		power = 2f
   		currentScene.addLight(this)
   	}
       LoaderOBJ(context.resources, mTextureManager, R.raw.car_obj).apply {
           parse()
           currentScene.addChild(parsedObject)
       }
       currentCamera.z = 4.2
   }
   ```

3. in the `MainActivity`:

   ```kotlin
   class MainActivity : AppCompatActivity() {
       private val renderer: Renderer by lazy { Renderer(this) }
       private val mRenderSurface: ISurface by lazy { findViewById(R.id.texture_view) }
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_main)
           mRenderSurface.setSurfaceRenderer(renderer)
       }
   }
   ```



#### and the problem of adding an obj model:

make **car.obj** and **car.mtl** file name to **car_obj** and **car_mtl**, then put them in `res/raw/` 

put texture files like **car_text.png** in `res/drwable-nodpi/`

if the texture doesn't work fine, make sure the file name is unique.



#### and the problem about losing faces

that's because a face should have less equal then 4 vertex

how to do with it? for example, you can use triangulate modifier in the Blender
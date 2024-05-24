# 1 实验内容
- 按照教程构建基于 TensorFlowLite 的 Android 花卉识别应用。 
- 查看该应用的代码框架，特别注意 CameraX 库 (AndroidX.camera.*)和数据视图模型的使用
- 上传完成既定功能的代码至 Github，并撰写详细的 Readme 文档。  
# 2 实验记录
## 2.1 准备工作
### 2.1.1 下载初始代码
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538272116-4f965040-e0f9-42f6-8770-76c30a3ce9e3.png#averageHue=%236f6e6c&clientId=ub2d17eb3-d5e2-4&from=paste&height=122&id=u7832703a&originHeight=168&originWidth=925&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=19760&status=done&style=none&taskId=ue276813a-9596-4ebd-8893-d9c2963bfb9&title=&width=672.7272727272727)
创建工作目录，在gitbash中输入命令。
`git clone https://github.com/hoitab/TFLClassify.git`
	将代码拷贝至本地
### 2.1.2 运行初始代码
在Android Studio中打开代码项目，等待Gradle构建，构建成功后，运行start模块
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538444502-518c8fb5-2a5e-4fea-95ef-36c23615cb51.png#averageHue=%23f9f8f7&clientId=ub2d17eb3-d5e2-4&from=paste&height=291&id=u24a6807b&originHeight=482&originWidth=1068&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=51230&status=done&style=none&taskId=u54febe2b-ee98-45a3-8601-910f6ce5175&title=&width=643.8181762695312)
可以看到现在的界面中有三个虚假标签和各自的随机数，之后将用模型所识别出的花卉品种和对应概率将其替代
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716540106470-839bdb9e-9632-4051-adbe-ae0ff4cdac9c.png#averageHue=%2382643a&clientId=u9d2ba279-5a28-4&from=paste&height=633&id=u59a5a210&originHeight=871&originWidth=415&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=698451&status=done&style=none&taskId=u5189a540-0156-4511-8939-deb43516c25&title=&width=301.8181818181818)
## 2.2 添加模型
选择“start”模块，点击File->New->Other->Tensorflow Lite Model。
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538517884-a148e94e-a8c7-4f5b-b6c2-14418a55128b.png#averageHue=%23e2dfc7&clientId=ub2d17eb3-d5e2-4&from=paste&height=454&id=u312f5c50&originHeight=624&originWidth=1871&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=169584&status=done&style=none&taskId=ud95567e8-8b49-4da0-813b-20e9622fb26&title=&width=1360.7272727272727)
	选择“finish”模块中ml文件夹下的FlowerModel.tflite。
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538613654-e4e302c3-7ae9-4a0e-a811-ed364cb63a26.png#averageHue=%23fcfaf9&clientId=ub2d17eb3-d5e2-4&from=paste&height=674&id=Nz3qI&originHeight=927&originWidth=999&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=165596&status=done&style=none&taskId=ue804d035-09e8-4f77-b73c-c63c9c1f8cb&title=&width=726.5454545454545)

系统将自动下载模型的依赖包并添加相关依赖项，并在模型成功导入后生成摘要信息
![](./screenshot/message.jpg#id=sgu8F&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538663952-7de18338-63e2-44b1-a282-d3a21184d9d6.png#averageHue=%23fcfcfb&clientId=ub2d17eb3-d5e2-4&from=paste&height=301&id=u2214240f&originHeight=563&originWidth=1267&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=65173&status=done&style=none&taskId=u24734217-cb21-4aac-8fa6-9a5f20a491a&title=&width=676.5454711914062)
## 2.3 添加代码
### 2.3.1 检查代码中的TODO项
查看初始代码中的TODO列表视图，点击View->Tool Windows->TODO
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538833219-cd9691f9-bc7d-40ca-9e7e-756a55a00fa1.png#averageHue=%23c1b3a2&clientId=ub2d17eb3-d5e2-4&from=paste&height=289&id=udf0c57fc&originHeight=398&originWidth=334&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=68950&status=done&style=none&taskId=u241c3a96-35d7-452d-a0c0-848dde4a67f&title=&width=242.9090909090909)![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538853698-2a2c7362-f205-409b-9d4b-36b2276bb204.png#averageHue=%23e5e9e5&clientId=ub2d17eb3-d5e2-4&from=paste&height=264&id=u08143f8d&originHeight=363&originWidth=383&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=86423&status=done&style=none&taskId=u07b81acd-c0b0-4be1-8f40-30e5e464972&title=&width=278.54545454545456)
	选择按照模块分组TODO项，方便进一步查看
![](./screenshot/groupby.jpg#id=vYyoj&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538875108-40011b92-d304-4c10-bd63-61fc55e7178a.png#averageHue=%23e5e9e5&clientId=ub2d17eb3-d5e2-4&from=paste&height=264&id=u8d1568a2&originHeight=363&originWidth=383&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=86423&status=done&style=none&taskId=uf86a31c8-8130-4cbc-8b60-20e02eb4040&title=&width=278.54545454545456)
### 2.3.2 添加相应代码
1.定位到“start”模块MainActivity.kt文件的TODO 1处，添加初始化训练模型的代码
```kotlin
private class ImageAnalyzer(ctx: Context, private val listener: RecognitionListener) :
ImageAnalysis.Analyzer {
    ...
    // TODO 1: Add class variable TensorFlow Lite Model
    private val flowerModel = FlowerModel.newInstance(ctx)

        ...
}
```
![]%HI9R7}9C3MIAC(I8F(1K1.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538927328-2d0b2df4-5ef3-47f4-9399-fbad78e1b2f3.png#averageHue=%23e0c8ad&clientId=ub2d17eb3-d5e2-4&from=paste&height=171&id=u11ec1b52&originHeight=235&originWidth=954&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=45712&status=done&style=none&taskId=ucdfb2334-f1d8-44d4-9a56-53d5432324a&title=&width=693.8181818181819)
2.定位至TODO 2处，在在CameraX的analyze方法内部，将摄像头的输入ImageProxy转化为Bitmap对象，并进一步转化为TensorImage对象
```kotlin
override fun analyze(imageProxy: ImageProxy) {
    ...
    // TODO 2: Convert Image to Bitmap then to TensorImage
    val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
        ...
}
```
![4OU{@`1XFZJ}0J]MWZJ1PWR.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538940324-21879ed4-9f82-4cf6-b181-088a40db163a.png#averageHue=%23d6af7b&clientId=ub2d17eb3-d5e2-4&from=paste&height=105&id=u80f13bcc&originHeight=145&originWidth=913&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=20855&status=done&style=none&taskId=udf93ff68-262e-4b8d-998f-b77e68c7451&title=&width=664)
3.定位至TODO 3处，对图像进行处理并生成结果
```kotlin
override fun analyze(imageProxy: ImageProxy) {
    ...
    // TODO 3: Process the image using the trained model, sort and pick out the top results
    val outputs = flowerModel.process(tfImage)
        .probabilityAsCategoryList.apply {
            sortByDescending { it.score } // 结果按照概率排序
        }.take(MAX_RESULT_DISPLAY) // 显示概率最高的若干个结果
        ...
}
```
![Z@JV)DQ4Q]Z1DP1BSBIWEAJ.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538950724-a6072d25-d215-4fc9-8578-e6b84b6a0bbf.png#averageHue=%23fcfbfb&clientId=ub2d17eb3-d5e2-4&from=paste&height=197&id=u25994ad6&originHeight=271&originWidth=1360&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=71792&status=done&style=none&taskId=u477937ce-c999-4631-bd3f-32558325622&title=&width=989.0909090909091)
4.定位至TODO 4处，将识别的结果加入数据对象Recognition中，包含label和score两个元素，用于后续RecyclerView的数据显示
```kotlin
override fun analyze(imageProxy: ImageProxy) {
    ...
    // TODO 4: Converting the top probability items into a list of recognitions
    for (output in outputs) {
        items.add(Recognition(output.label, output.score))
    }
        ...
}
```
![~({0K9W~])E~AMSC1WR[7}5.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716538973949-6e96da57-61cb-45f2-ab17-dadf61d88d20.png#averageHue=%23cfaa80&clientId=ub2d17eb3-d5e2-4&from=paste&height=137&id=u11903d69&originHeight=189&originWidth=1278&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=30333&status=done&style=none&taskId=u46e67c6a-4eb4-448e-ae05-a4b71bb42fe&title=&width=929.4545454545455)
5.将位于START和END中间，原先用于显示虚假标签的代码注释掉
```kotlin
// START - Placeholder code at the start of the codelab. Comment this block of code out.
// for (i in 0..MAX_RESULT_DISPLAY-1){
//     items.add(Recognition("Fake label $i", Random.nextFloat()))
// }
// END - Placeholder code at the start of the codelab. Comment this block of code out.
```
![80V4O(L$_N8M30GPRG6T6ZF.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716539008026-a4f2ca5e-f763-43ec-b019-157b5bbf4bdb.png#averageHue=%23fbfaf8&clientId=ub2d17eb3-d5e2-4&from=paste&height=185&id=u0932478a&originHeight=254&originWidth=1582&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=53491&status=done&style=none&taskId=u768891c2-977d-4802-8426-a01554b7bb1&title=&width=1150.5454545454545)
6.（可选）在build设置GPU加速。
```kotlin
// TODO 5: Optional GPU Delegates
implementation 'org.tensorflow:tensorflow-lite-gpu:2.3.0'
```
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716539102695-36bb40f7-0564-45fa-88e0-18688dee6606.png#averageHue=%23ede0c9&clientId=ub2d17eb3-d5e2-4&from=paste&height=87&id=u4e355c27&originHeight=119&originWidth=955&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=16023&status=done&style=none&taskId=uccde5044-c6bf-4a59-98be-1e0a003e189&title=&width=694.5454545454545)
7.兼容性设置。
在SDK34，gradle7.2的时候进行调试会出现如下错误。
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716539258609-b5e3ed44-d1d3-45e7-b199-792f89904608.png#averageHue=%23fdfbf9&clientId=ub2d17eb3-d5e2-4&from=paste&height=124&id=u8c700546&originHeight=171&originWidth=746&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=18735&status=done&style=none&taskId=ub3afc6d0-7462-4d3a-96ff-aafc9bf7f08&title=&width=542.5454545454545)
此时就要在AndroidManifest.xml下，在含有<intent-filter>的<activity>的标签内显示添加`android:exported="true"`
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716539471090-2b0ce98a-c552-4799-b190-9781cd807e78.png#averageHue=%23fef5f4&clientId=ub2d17eb3-d5e2-4&from=paste&height=163&id=u092b1afb&originHeight=224&originWidth=646&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=27426&status=done&style=none&taskId=u1168571a-beb8-486c-93d5-398d94d1117&title=&width=469.8181818181818)
并且当JDK版本过高时，可能会出现如下错误：
`java.lang.IllegalAccessError: class org.jetbrains.kotlin.kapt3.base.KaptContext (in unnamed module @0x6acdb135) cannot access class com.sun.tools.javac.util.Context (in module jdk.compiler) because module jdk.compiler does not export com.sun.tools.javac.util to unnamed module @0x6acdb135`
此时需要降低JDK的版本（一开始是16降到11），在setting->build->build tools->gradle
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716539604212-3f9e89d8-909a-4a84-92b6-d464b258d52d.png#averageHue=%2373a77d&clientId=ub2d17eb3-d5e2-4&from=paste&height=199&id=u31c8b478&originHeight=274&originWidth=791&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=48927&status=done&style=none&taskId=u74cb887c-d704-4e9a-b2c1-f202f2362af&title=&width=575.2727272727273)
# 3 实机运行
## 3.1 USB连接实机
1.要在真机上运行软件，首先需要打开手机的开发者模式，以小米10，MIUI13稳定版为例。点击设置->我的设备->全部参数，连续点击系统版本号(MIUI)，直到弹出消息提示进入开发者模式，回到上级菜单点击系统与更新->开发人员选项，在调试一栏找到USB调试开关，点击开启。
![ca977a4ddcc7530c7f20888167da4e33.jpg](https://cdn.nlark.com/yuque/0/2024/jpeg/38674938/1716549534267-40e32904-f9b3-4d74-8943-814d797bd6c3.jpeg#averageHue=%23f6f6f6&clientId=u6d1b121d-ad35-4&from=paste&height=335&id=ue28bd9e2&originHeight=642&originWidth=1043&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=42290&status=done&style=none&taskId=u5ec77a72-e6ea-475f-aa85-b6b4f634d86&title=&width=544.8181762695312)
![13f0889d916771b6dd35e70bc2297f16.jpg](https://cdn.nlark.com/yuque/0/2024/jpeg/38674938/1716540280386-36003017-ccda-431c-8978-b264d985c922.jpeg#averageHue=%23f8f8f8&clientId=u9d2ba279-5a28-4&from=paste&height=392&id=CkKc2&originHeight=942&originWidth=1080&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=53000&status=done&style=none&taskId=u64ed31f1-b205-45b3-8453-7261c32cd31&title=&width=449.54547119140625)
2.在Android studio的SDK manager中下载USB driver
![](./screenshot/USB.jpg#id=UuLaS&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716539885793-d1e3b4bb-cfc0-4f0e-9d61-cd46cd9b5171.png#averageHue=%23dfe8f9&clientId=ub2d17eb3-d5e2-4&from=paste&height=50&id=udcb2dd5f&originHeight=69&originWidth=812&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=11789&status=done&style=none&taskId=ud8a5fccc-7f90-4c03-9236-2650a4da13e&title=&width=590.5454545454545)
3.使用数据线将真机连接到电脑，可以看到Android studio已经成功识别出真机，并可以在其上运行软件。
![image.png](https://cdn.nlark.com/yuque/0/2024/png/38674938/1716549645650-9741545c-93cc-4b3b-852d-e5c4164bb932.png#averageHue=%2396c3ae&clientId=u6d1b121d-ad35-4&from=paste&height=62&id=u4bb90dae&originHeight=85&originWidth=448&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=13334&status=done&style=none&taskId=u3b3aed0b-3ed1-441e-a5e5-b495dae2b61&title=&width=325.8181818181818)
## 3.2 对于各花卉的识别效果
运行程序，找相关的图片进行识别。
![3cc1fc85100808fd9bc5a32878d56733.jpg](https://cdn.nlark.com/yuque/0/2024/jpeg/38674938/1716540256321-9d54a70c-b35a-4a04-90bc-8d54c746424b.jpeg#averageHue=%232d312d&clientId=u9d2ba279-5a28-4&from=paste&height=1396&id=u286c86e8&originHeight=1920&originWidth=886&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=119770&status=done&style=none&taskId=u023fa7d2-1168-4597-af06-3bbe1f605a2&title=&width=644.3636363636364)

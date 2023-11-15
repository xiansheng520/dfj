**说明文档需要包含：作品标题、摘要、软件分类、应用领域、开放源码组织认可的开放源码许可证类型（可多个）等软件基本信息、作品概述等。作品概述包括但不限于软件背景及应用领域、作品特点和设计思路、功能描述、体系结构和关键技术点、功能模块设计、验收标准等。**

内容偏少
# **1 应用领域**
在人口老龄化进程加速、残疾人口数量庞大以及慢性病患病率逐年上升的国情下，我国需要康复医疗的人数庞大，市场庞大，未来康复市场潜力无限。虽然我国康复市场需求巨大，但与发达国家相比，我国康复市场人均规模小。中商情报网的数据显示，美国目前康复医疗市场（含长期护理）规模已超2000亿美元（人均约800美元）。而我国康复医疗市场规模仅200亿元（人均仅约15元人民币）。随着政策完善、人们对健康需求的提升，以前面的保守估测的康复需求患者数量为依据，截至2020年，我国康复需求患者将突破1.5亿。则对应的康复市场规模将达55亿元。 目前医疗康复器械应用人群主要为老年人、残疾人以及慢性病和术后康复患者，关于其市场需求分析主要从这三类人群阐述。

![](新建%20DOCX%20文档.001.png)

**图1-1 领域现状**


# **2 作品概述**
## **2.1 软件背景及应用领域**
为了进行我们全肢体的外骨骼人机交互，我们开发了基于DAYU200设备搭载OpenHarmony3.2版本的ArkUI交互前端，通过集成的多前端技术设计，保证个模块结构具有多元化的交互界面供患者使用不同的功能，查看有针对性的结果。

我们通过与医院合作制定Burnnstrom全定量表，并采用随机森林算法定量化评估患者目前所处的康复等级，并针对不同阶段患者定制不同的康复方案和康复策略并在ArkUI交互前端页面进行展示，供患者进行自主的康复训练，形成了一套康复训练+评估的闭环交互设计系统。

![说明: wps12](新建%20DOCX%20文档.002.jpeg)

**图2-1 自主康复训练的无医师解决方案**

我们通过对康复运动数据进行采集和评估分析，在ArkUI前端页面会自动生成相应的评估报告和康复建议，同时在前端页面为患者制定了贴合病情的康复训练方案和康复策略，并提供标准化的辅助动作教程供患者查看和训练。

此外，我们还开发了基于FMA运动功能、MBI日常生活功能等一系列评估量表的自主答题功能，患者可以定期进行自主评估来检测自身的康复训练效果。

我们的基于闭环康复策略的鸿蒙ArkUI软件，在智慧屏上进行演示，符合脑卒中患者的使用习惯，真正为脑卒中患者量身打造了一位安全可靠有针对性的“AI医师”。
## **2.2 作品特点和设计思路**
### **2.2.1 项目主要创新点**
①康复训练——气动柔性康复上肢外骨骼设计

外骨骼整体采用气压驱动的方式，为实现上肢体外骨骼能够对人体动作柔性精确控制，我们采用基于高分子材料的仿生软体机器人驱动器来对腕部手指等关节进行柔性驱动，同时开发了PWM-PID柔顺性控制算法来对各模块驱动力和位置进行精准柔性控制，实现了外骨骼运动的柔顺性，保证了患者在康复训练时的安全性和舒适性。康复训练基于上肢外骨骼的设计，可以实现手指康复、肘康复、肩康复、抬手运动周期康复。

②康复评估——基于OpenHarmony的康复评估系统设计

考虑到我们上肢康复外骨骼的人机交互，我们开发了OpenHarmony3.2系统和自主设计的前端交互界面，利用该交互界面可以实现外骨骼控制、康复方案定制、康复教程展示、康复评估报告回馈，线上诊疗、康复社区构建以及康复历史数据查询

通过对肢体关节间的运动分析，通过VR实时重现运动界面和DTW算法，皮尔逊相关系数进行三种对比方式对患者的健患侧运动数据进行对比，同时绘制出实时运动曲线以及人形线图，这些数据的展示针对于单个的关节图像展示，关节间组合在一起也可以得到多关节之间的运动曲线。评估患者的患病等级，并根据评估情况提高康复方案，反馈至控制设备，执行康复方案。
### **2.2.2 作品设计思路**
![图示

描述已自动生成](新建%20DOCX%20文档.003.png)

**图2-2 系统框架图**

本产品在控制硬件的设计上，我们用到了mpu6050陀螺仪传感器测量三轴角度，采用激光传感器测距作为闭环PID控制的反馈值，采用弯曲传感器通过角度值输入，形成影子模式，健康侧带动患病侧进行运动康复。我们使用DAYU200作为上位机进行数据接收和指令下发，小熊派作为主控板，将各传感器与小熊派 WiFi模块进行结合设计，实现各模块数据无线传输至主控板并将数据上云，进行数据分析。

在软件系统方面，我们自主开发了康复等级评估算法，结合我们的全定量表，根据患者运动效果为患者定量化评估出目前所处的康复等级。完成评估后，我们会将评估等级以及传感器测得的角度值进行滤波处理后上传至云服务器，我们会把云服务器数据存储到数据库中，使用Django把数据从后端传输至前端，实现最小数据流的打通。从而在我们的DAYU200中的ArkUI前端界面可以展示出运动数据和评估结果，便于患者清楚自身目前的情况以及康复效果。
## **2.3 功能描述**
我们基于OpenHarmony开发一个专门的应用端来帮助脑卒中患者更好地管理上肢康复过程。旨在为脑卒中患者提供全面的康复辅助和健康管理。

主要功能：

康复计划管理：应用端允许用户创建个性化的康复计划，根据医生的建议和康复进度进行调整。用户可以轻松追踪自己的康复目标，记录进展并定时提醒康复运动。

康复训练评估：应用通过系统采集患者康复运动数据，对肢体进行误差评估，形成康复等级和康复报告。这些数据将被可视化呈现，以便用户和医生更好地了解康复情况。

平台交流和资源分享：卒中管家建立了一个平台，患者可以在这里获取配套资源课程进行康复，能和其他患者、医师进行交流，并获得他人的支持和鼓励。

数据安全和隐私：应用将用户的健康数据存储在安全的云端服务器上，确保数据的隐私和保密性。用户完全掌握自己的数据，并可以选择与医生共享以获得更好的医疗建议。
## **2.4 体系结构和关键技术点**
### **2.4.1 登录**
启动器后首先是登录界面，能够实现账号登陆、账号注册及其他登录方式。主要由文本、文本框、按钮组成。

Text("欢迎登陆")
`  `.fontSize(60).fontWeight(FontWeight.Bold)
`  `.fontColor('#85caf9').position({x:110,y:-240})
TextInput({ placeholder: "请输入账号" })
`  `.width(440).height(40)
`  `.backgroundColor('#fffff')
`  `. placeholderColor(Color.Grey)
`  `.position({x:20,y:-80 })
TextInput({ placeholder: "请输入密码" })
`  `.width(440).height(40)
`  `. placeholderColor(Color.Grey)
`  `.backgroundColor('#fffff')
`  `.type(InputType.Password)
`  `.position({x:20,y:-30 })
//按钮
Button("登录")
`  `.width(440).height(50)
`  `.position({x:20,y:20 })
`  `.fontWeight(FontWeight.Bold).fontSize(25)
`  `.backgroundColor('#85caf9')
`  `.onClick(() => {
`    `router.pushUrl({
`      `url: 'pages/tabbar'
`    `})
`  `})
Button("注册")
`  `.width(400).height(40)
`  `.position({x:40,y:80 })
`  `.fontWeight(FontWeight.Normal)
`  `.fontColor('#4264b2').fontSize(20)
`  `.backgroundColor('#fffff')
`  `.onClick(() => {
`    `router.pushUrl({
`      `url: 'pages/zhuce'
`    `})
`  `})

点击勾选服务隐私协议。

Checkbox()
Text("已阅读并同意使用服务协议和隐私保护指引")
`  `.fontSize(16).fontColor('#4264b2')

更换其他方式进行登录或找回密码。

删除多余空行

已改

Text("-----其他登陆方式-----")
`  `.fontSize(15).width(170).height(100)
`  `.position({x:155,y:230 })
`  `.fontColor('#4264b2')
Column()  {
`  `Flex({ alignItems: ItemAlign.Center, wrap: FlexWrap.Wrap }) {
`    `Text('手机号登录')
`      `.fontColor('#4264b2')
`    `Divider().vertical(**true**).margin(20).height(15)
`    `Text('找回密码')
`      `.fontColor('#4264b2')
`    `Divider().vertical(**true**).margin(20).height(15)
`    `Text('其他方式登录')
`      `.fontColor('#4264b2')
### **2.4.2 修改地址**
这部分代码是在前端应用中创建一个Select,用于实现修改地址的功能。

`  `Select([{value:'郑州',icon: "/common/yuan.png"},
`  `{value:'北京',icon: "/common/2.png"},
`  `{value:'杭州',icon: "/common/3.png"},
`  `{value:'上海',icon: "/common/4.png"}])
`  `.selected(30).value('城市')
`  `.font({size: 20, weight:400, family: 'serif', style: FontStyle.Normal })
`  `.selectedOptionFont({size: 20, weight: 500, family: 'serif', style: FontStyle.Normal })
`  `.optionFont({size: 20, weight: 400, family: 'serif', style: FontStyle.Normal })
`  `.onSelect((index:number)=>{
`    `console.info("Select:" + index)
`  `}).position({ x: 0, y: 15 })

### **2.4.2 自定义康复方案**
这段代码的目的是丰富数据，当点击按钮时，弹出一个文本选择对话框，用户可以从中选择日期，进行时间记录，便于后期清晰展示数据。选择的结果会通过回调函数进行处理。

DatePicker({
`    `start: **new** Date('1970-1-1'),
`    `end: **new** Date('2100-1-1'),
`    `selected: **this**.selectedDate,
`  `})
`    `.lunar(**this**.isLunar)
`    `.onChange((value: DatePickerResult) => {
`      `**this**.selectedDate.setFullYear(value.year, value.month, value.day)
`      `console.info('select current date is: ' + JSON.stringify(value))
`    `})
}

然后设置修改康复训练进度，进行康复进度记录，手动输入数据，患者可以在滑动中体验交互趣味

Text('总进度').fontSize(20).fontColor('#666666').fontWeight(FontWeight.Bold).margin({left :-180})
Row() {
`  `Slider({
`    `value: **this**.inSetValue, step: 10, style: SliderStyle.InSet
`  `})
`    `.blockColor('#fffff').trackColor('#fffff')
`    `.selectedColor('#d6edf6').showSteps(**true**)
`    `.onChange((value: number, mode: SliderChangeMode) => {
`      `**this**.inSetValue = value;
`      `console.info('value:' + value + 'mode:' + mode.toString());
`    `})
### **2.4.3 康复训练与评估**
首先患者可以选择适合的训练课程、预览课程大纲后开始训练。训练完毕后会反馈标准康复动作和患者动作的实时对比，最后根据训练运动数据对比生成相应的等级和评估报告，患者也可以在主页查看历史评估报告。

Video({
`  `src: **this**.videoSrc,
`  `previewUri: **this**.previewUri,
`  `currentProgressRate: **this**.curRate,
`  `controller: **this**.controller
})

这段代码主要实现了一个设备校准界面，主要用于动作识别，更精准获取患者动作数据。内容包括显示动作识别标题、提示信息，以及一个包含视频动画和控制按钮的界面。用户可以通过按钮控制动画的播放、结束。图像动画通过VedioCreateCom组件实现，根据按钮的点击事件改变动画状态和参数。

Text('动作识别').fontWeight(FontWeight.Bold).fontSize(30).margin({top : 100,left: 30})
Text('请面向屏幕根据视频依次做动作').fontSize(20).margin({top :10,left: 30})

Column({space:30}) {
`  `Video({
`    `src: **this**.videoSrc,
`    `previewUri: **this**.previewUri,
`    `currentProgressRate: **this**.curRate,
`    `controller: **this**.controller
`  `})
`    `.width(400)
.height(200)
`    `.autoPlay(**this**.isAutoPlay)
`    `.controls(**this**.showControls)
`    `.onStart(() => {
`      `console.info('onStart')
`    `})
`    `.onFinish(() => {
`      `console.info('onFinish')
`    `})
`  `Row({space:100}) {
`    `Button('开始').backgroundColor('#b4dbed')
`      `.onClick(() => {
`        `**this**.controller.start() // 开始播放
`      `}).margin(5)
`    `//.backgroundColor('#b4dbed')
`    `Button('结束').backgroundColor('#b4dbed')
`      `.onClick(() => {
`        `**this**.controller.stop() // 结束播放
`      `}).margin(5)
`  `}.margin({ top: -20})
}

## **2.5 功能模块设计**
### **2.5.1 登录页面**
登录页面可以实现登录账号、其他方式登录和注册功能。我的信息里可修改伤残类型和伤残日期。健康报告里可查看生成的健康报告。

![](新建%20DOCX%20文档%20(2).001.png)
### **2.5.2 首页**
患者可以定位城市、开启设备并设备校准、查看自己的运动记录以及手动录入运动信息。

![](新建%20DOCX%20文档%20(2).002.jpeg)

![](新建%20DOCX%20文档%20(2).003.png)
### **2.5.3 训练页**
患者可以在上方搜索框中搜索课程等话题，并选择合适的课程进行预览和康复训练。训练完毕后会生成标准动作与患者动作对比表，并生成相应的评估等级和康复报告。

![](新建%20DOCX%20文档%20(2).004.png)

**图2-6 调试设备手动录入**

### **2.5.4 康复页**
患者可以生成定制化评估报告并保存下载，还可以查看历史评估报告。

![](新建%20DOCX%20文档%20(3).001.png)

**图2-7 康复页**
## **2.6 个人主页**
患者可以在主页查看个人信息、我的账户、个人认证、历史评估、设置、帮助页面。

![](新建%20DOCX%20文档%20(3).002.png)

**图2-8 个人主页**

![](新建%20DOCX%20文档%20(3).003.png)

**图2-9 个人认证**

![](新建%20DOCX%20文档%20(3).004.png)

**图2-10 设置帮助**

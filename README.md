# 本项目使用Vue2 + threejs 对汽车模型进行展示 可对部位进行颜色选择
## 通过导入外部模型 和文档结构实现本页面
![1670760609932](https://user-images.githubusercontent.com/101321825/206902734-19372145-9022-4144-8f37-b6d03ffe97d1.png)<br>
## 解析外部模型child属性 解析模型模块 为后续解析提供依据
## 根据解析数据 建立页面元素实现对模型进行颜色控制
![1670760689055](https://user-images.githubusercontent.com/101321825/206902791-bb9d347c-43e2-4dbe-aafd-5fe5a63b4280.png)<br>
## 通过设置物理网格材质(MeshPhysicalMaterial)中的roughness和metalness属性实现与原本模型的材质相似的金属质感

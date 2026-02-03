## 绘制晶振电路部分
- 创建工程后，在”P“图标那里选择相关元件；
- 输入at89c52，选择开发板；
- 输入crystal，选择晶振，单击晶振图标，将频率改为11.0592；
- 在Category中点击Capacitors的选项，选择33pF的电容，两个；
- 将19引脚与晶振和C1相连，将18引脚与晶振和C2相连，C1与C2相连；
- 在终端模式中选择GROUND，接在C2那里；
## 绘制复位电路部分
- 在”P“中Category中选择Resistors,在Sub-category中选择1/4W 1%，选择第一个，单击将电阻值改为10K；
- 在Category中点击Capacitors的选项，在Sub-category中选择High Temp Radial,找10u 16V 47mA的电容；
- 在终端模式中选择GROUND，连在R1那，将R1与C3相连；
- 搜索button，选择第一个；
- 添加POWER，GROUND。
![](https://github.com/258-maker/picx-images-hosting/raw/master/xxx/屏幕截图-2026-02-03-194710.64ed9536nd.webp)

# 点亮一盏LED
![](https://github.com/258-maker/picx-images-hosting/raw/master/xxx/屏幕截图-2026-02-03-200846.6bhl4kpozp.webp)
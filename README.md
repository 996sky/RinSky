# 凌空一号（RinSky）
基于Pixhawk4自制无人机的开发记录

# 设备参数
 - 飞控软件：[PX4-Autopilot](https://github.com/PX4/PX4-Autopilot) v1.12.3
 - 飞控硬件：[Pixhawk4](https://docs.px4.io/master/zh/flight_controller/pixhawk4.html) 接口类型GH1.25
 - 机架：[Z410](https://item.taobao.com/item.htm?id=616344442145)
 - 电机：[TMOTOR](https://uav-cn.tmotor.com/) AIR 2216/KV880
 - 螺旋桨：[TMOTOR](https://uav-cn.tmotor.com/) T1045（自锁桨）
 - 遥控器：[富斯FSi6X](https://www.flyskytech.com/products_detail/37.html)
 - 遥控器接收机：[富斯iA10B](https://www.flyskytech.com/parts_detail/38.html)
 - GPS：[乐迪SE100](https://www.radiolink.com.cn/docc/product-detail-122.html)（注：SE100是设计给Pixhawk2.4.8使用的，所以在Pixhawk4上使用时需要改一下线序，套一个GH1.25的壳，具体[如图所示](./说明图片/乐迪SE100_Pixhawk4线序.JPG)）
 - 轴距：410mm
 - 数据传输：[权盛电子](https://quan-sheng.world.taobao.com/)V5数传（注：可能需要MX1.25转GH1.25的线）
 - 光流传感器：[雷迅](https://www.cuav.net/)PX4FLOW2.1（含声呐）
 - 电池：[格氏](https://www.grepow.cn/page/uav-battery.html)ACE 3300mah 25C 11.1V 3S XT60接口 满电单芯电压4.2V 空电单芯电压3.5V
 - 电源管理板：Holybro PM07-V2.3
 - 电调分电板：BLHeli_S Ver.2.3

# 接线
 1. 电源管理板PWR1—>POWER1 | 电调分电板—>I/O PWM OUT
 - 以上所述及电源管理板与电调分电板的焊接、电调分电板与电机的焊接具体[如图所示](./说明图片/电源管理板与电调分电板.JPG)
 3. GPS—>GPS MODULE
 4. 光流—>I2C A
 5. 遥控器接收机SERVO（左边接地）—>杜邦转GH1.25 3P线—>DSM/SBUS RC

# 遥控器设置

## 常规设置

 1. 开机后长按OK键进入菜单，随后进入系统—>接收机设置—>输出模式，将串行总线改为S.BUS，长按CANCEL键写入。
 2. 进入系统—>接收机设置—>辅助设置，将其全部调整为开启状态，长按CANCEL键写入。
 3. 进入功能—>正逆转，将SWA对应的通道（可在功能—>通道显示或辅助通道查看）设置为反（因为我要将SWA调上设置为Kill电机，但默认设置为调下使能），长按CANCEL键写入。
 

## 通道与摇杆设置记录

 - 右摇杆左右—>通道1—>横滚（Roll）
 - 右摇杆上下—>通道2—>俯仰（Pitch）
 - 左摇杆上下—>通道3—>油门
 - 左摇杆左右—>通道4—>偏航（Yaw）
 - VRA—>通道5
 - VRB—>通道6
 - SWA—>通道7—>KILL
 - SWB—>通道8—>锁定（Arm）
 - SWC—>通道9—>飞行模式 从上至下依次是自稳（Stabilized） 定高（Altitude） 定点（Position）
 - SWD—>通道10—>OffBoard

# 参数设置
打开QGC->Vehicle Setup->参数
## 光流参数

 - `EKF2_AID_MASK`设置为3（使能光流与GPS，如果可用）
 - `SENS_EN_MB12XX`设置为1（使能声呐，如果可用）

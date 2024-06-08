# 2024年のAutoware.Universeのメッセージ型変更に関する調査

メッセージ型の変更に関する情報は以下のdiscussion に記載されている。

https://github.com/orgs/autowarefoundation/discussions/3862

# 新旧メッセージの比較調査の結論
メッセージタイプが変わっているだけで、構造や変数の名前は変化なし！

## 2024年変更前のメッセージ型の定義ファイル（Autoware.Auto時代のもの）

https://github.com/tier4/autoware_auto_msgs

## 2024年変更後のメッセージ型の定義ファイル

https://github.com/autowarefoundation/autoware_msgs/

# 各変更の確認
特に自動車とのIntegration周りで重要なトピックに着目して差分を比較してみる。

各見出しは、Autoware.Auto時代の古いメッセージ型

## autoware_auto_control_msgs/AckermannControlCommand	
- 旧）autoware_auto_control_msgs/AckermannControlCommand
https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_control_msgs/msg/AckermannControlCommand.idl

- 新）autoware_control_msgs/Control	
https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_control_msgs/msg/Control.msg

### 旧新比較
一緒であることがわかる。

| 旧                               | 新                               |
|--------------------------------|--------------------------------|
| longitudinal.speed            | longitudinal.speed            |
| longitudinal.acceleration     | longitudinal.acceleration     |
| longitudinal.jerk             | longitudinal.jerk             |
| lateral.steering_tire_angle   | lateral.steering_tire_angle   |
| lateral.steering_tire_rotation_rate | lateral.steering_tire_rotation_rate |


## autoware_auto_vehicle_msgs/ControlModeCommand	
＝＞サービスに変更

## autoware_auto_vehicle_msgs/ControlModeReport	

- 旧）https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_vehicle_msgs/msg/ControlModeReport.idl
- 新）https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_vehicle_msgs/msg/ControlModeReport.msg

### 旧新比較
一緒

## autoware_auto_vehicle_msgs/Engage
- 旧）https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_vehicle_msgs/msg/Engage.idl
- 新）https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_vehicle_msgs/msg/Engage.msg

### 旧新比較
一緒

## autoware_auto_vehicle_msgs/GearCommand	
- 旧）https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_vehicle_msgs/msg/GearCommand.idl
- 新）https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_vehicle_msgs/msg/GearCommand.msg

## autoware_auto_vehicle_msgs/GearReport
- 旧）https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_vehicle_msgs/msg/GearReport.idl
- 新）https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_vehicle_msgs/msg/GearReport.msg

### 旧新比較
一緒

## autoware_auto_vehicle_msgs/SteeringReport	
- 旧）https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_vehicle_msgs/msg/SteeringReport.idl
- 新）https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_vehicle_msgs/msg/SteeringReport.msg

### 旧新比較
一緒

## autoware_auto_vehicle_msgs/VelocityReport	
- 旧）https://github.com/tier4/autoware_auto_msgs/blob/tier4/main/autoware_auto_vehicle_msgs/msg/VelocityReport.idl
- 新）https://github.com/autowarefoundation/autoware_msgs/blob/main/autoware_vehicle_msgs/msg/VelocityReport.msg

### 旧新比較
一緒

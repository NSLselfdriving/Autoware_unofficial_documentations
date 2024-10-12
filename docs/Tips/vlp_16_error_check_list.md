# AutowareとVLP-16が繋がらないときのチェックリスト

## PC のIPアドレスが、sensor_kit に記載されているIPアドレスになっているか
=> 192.168.1.10 にする

## tcpdump でパケットが来ているか確認する
=> なお、来ていたとしても、繋がらないときは繋がらない

## LiDARの電源を抜き差しする
=> なお、効果は薄い模様

## 他のPCでVeloView見てみる
=> これで原因の切り分けができる

## Velody driver 単体を立ち上げてみる
```
ros2 launch velodyne_driver .....
```

## PCを再起動する

## 秘技 : プロキシする

1. 以下のコマンドで、Velodyne Driver 単体で起動する
```
ros2 launch velodyne_driver .....
```

2. 以下のコードを用いて、無理矢理Ａｕｔｏｗａｒｅのトピックにプロキシしてあげる

```
import rclpy
from rclpy.node import Node
from velodyne_msgs.msg import VelodyneScan  # 正しいメッセージ型

class VelodynePacketsProxy(Node):
    def __init__(self):
        super().__init__('velodyne_packets_proxy')
        
        # /velodyne_packetsトピックのサブスクライバ
        self.subscription = self.create_subscription(
            VelodyneScan,  # 正しいメッセージ型
            '/velodyne_packets',
            self.listener_callback,
            10  # キューサイズ
        )
        
        # /sensing/lidar/top/velodyne_packetsトピックのパブリッシャ
        self.publisher = self.create_publisher(
            VelodyneScan,  # 正しいメッセージ型
            '/sensing/lidar/top/velodyne_packets',
            10  # キューサイズ
        )
        
    def listener_callback(self, msg):
        # 受信したメッセージをそのまま別のトピックにパブリッシュ
        self.publisher.publish(msg)
        self.get_logger().info('Message proxied from /velodyne_packets to /sensing/lidar/top/velodyne_packets')

def main(args=None):
    rclpy.init(args=args)
    node = VelodynePacketsProxy()
    
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        pass
    finally:
        node.destroy_node()
        rclpy.shutdown()

if __name__ == '__main__':
    main()
```

なお、たゆPCには、Desktop/ros2_ws/ にコードがあり、起動コマンドは、

```
 ros2 run proxy_velodyne_packets proxy_velodyne_packets
```

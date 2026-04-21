Mobile Manipulator Simulation

Báo cáo dự án giữa kỳ môn Lập trình Robot với ROS. Hệ thống mô phỏng một robot di động kết hợp tay máy (Mobile Manipulator) hoạt động trong môi trường Gazebo Harmonic.

1. Cấu trúc dự án

Dự án tập trung vào việc thiết kế, xây dựng mô hình động học và mô phỏng robot Assem1 với cấu hình:

    Khung gầm: 2 bánh dẫn động vi sai kết hợp bánh phụ để đảm bảo cân bằng vật lý.

    Tay máy: Cánh tay robot 2 bậc tự do cấu hình RR.

    Hệ điều hành: Ubuntu 24.04 LTS (Noble).

    Nền tảng: ROS 2 Jazzy Jalisco & Gazebo Harmonic.

2. Tính năng kỹ thuật

    Phản hồi từ Encoder: Sử dụng phản hồi vận tốc góc từ các bánh xe để tính toán hành trình.

    Nhận thức không gian: Tích hợp Camera FPV để nhận diện vật thể và IMU để xác định hướng.

    Điều khiển an toàn: Tích hợp node safe_control áp dụng ràng buộc động học mềm để tránh tay máy tự va chạm với thân xe.

    Vật lý ổn định: Toàn bộ hệ thống được tinh chỉnh ma trận quán tính và đơn giản hóa các khối va chạm để tránh hiện tượng "nổ vật lý" trong Gazebo.
    
3. Cấu trúc Package:

my_robot_project           
  └──  ├── CMakeLists.txt           # File cấu hình biên dịch CMake
       ├── package.xml              # Định nghĩa dependencies và plugins
       ├── mesh                     # Chứa các file 3D của bánh xe và cánh tay
       ├── urdf                     # Kiến trúc URDF 
       │   └── assem1.urdf      
       ├── launch                   # Các tệp khởi chạy hệ thống
       │   └──  gazebo.launch.py    
       │   └──  display.launch.py
       └── rviz                     # Cấu hình trực quan hóa
           └── config.rviz          # File làm sẵn cấu hình RViz2

4. Hướng dẫn cài đặt và khởi chạy
a. Cài đặt môi trường
Yêu cầu đã cài đặt ROS 2 Jazzy và Gazebo Harmonic.

b. Build Workspace

mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

cd ~/ros2_ws
colcon build --symlink-install
source install/setup.bash

c. Chạy mô phỏng

Mở Gazebo và Spawn Robot:
ros2 launch assem1 gazebo.launch.py

Điều khiển bằng bàn phím:
ros2 run teleop_twist_keyboard teleop_twist_keyboard

Xem dữ liệu cảm biến trên RViz2:
ros2 launch assem1 display.launch.py

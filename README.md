# simple_service_cpp

A minimal ROS 2 (Jazzy) service example in C++. A client sends two integers
to a server, and the server replies with their sum.

## Overview

- **Service name:** `/examples/add_two_ints`
- **Interface:** `ros2_examples_interfaces/srv/AddTwoInts`
  - Request: `int64 a`, `int64 b`
  - Response: `int64 sum`
- **Nodes:**
  - `server`: offers the service and computes the sum
  - `client`: sends one request, prints the result, and exits

## Package layout

```
simple_service_cpp/
├── include/simple_service_cpp/simple_service.hpp   # Server and client class declarations
├── src/server.cpp                                  # Server node
├── src/client.cpp                                  # Client node (one-shot)
├── CMakeLists.txt
└── package.xml
```

## Dependencies

- ROS 2 Jazzy
- `rclcpp`
- `ros2_examples_interfaces` (must be built in the same workspace or installed)

## Build

```bash
cd ~/ros2_ws
source /opt/ros/jazzy/setup.bash
colcon build --packages-select ros2_examples_interfaces simple_service_cpp
source install/setup.bash
```

## Run

Terminal 1, start the server:
```bash
ros2 run simple_service_cpp server
```

Terminal 2, call it with the client:
```bash
ros2 run simple_service_cpp client 3 4
```

Expected output:
```
[client]: Result: 7        # Terminal 2
[server]: 3 + 4 = 7        # Terminal 1
```

You can also test the server without the client:
```bash
ros2 service call /examples/add_two_ints \
  ros2_examples_interfaces/srv/AddTwoInts "{a: 3, b: 4}"
```

## How it works

- The **server** registers the service in its

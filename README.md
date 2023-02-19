# image-tools-docker

Dockerized image_tools ROS 2 package

## Usage

`CODEC` can have value: `theora` or `compressed`. 

### Image Compressor

```yaml
services:
  image_compressor:
    image: husarion/image-transport:humble
    <<: *net-config
    command: >
      ros2 run image_transport republish raw ${CODEC:-theora}
        --ros-args
        --remap in:=/camera/color/image_raw
        --remap out/${CODEC:-theora}:=/camera/color/image_raw/${CODEC:-theora}
```

### Image Decompressor

```yaml
  image_decompressor:
    image: husarion/image-transport:humble
    <<: *net-config
    command: >
      ros2 run image_transport republish ${CODEC:-theora} raw
      --ros-args
      --remap in/${CODEC:-theora}:=/camera/color/image_raw/${CODEC:-theora}
      --remap out:=/camera/my_image_raw

```
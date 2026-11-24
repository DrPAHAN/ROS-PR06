# Дерево преобразований (frames.md)

## Корректная структура
| Родитель | Дочерний | Смещение (xyz) | Владелец публикации |
|---|---|---|---|
| `base_link` | `camera_link` | `0.25 0 0.15` | `robot_state_publisher` |
| `base_link` | `lidar_link`  | `0 0 0.3`     | `robot_state_publisher` |
| `base_link` | `imu_link`    | `-0.2 0 0.1`  | `robot_state_publisher` |

## Сценарий "Сломать и Починить"
1. **Поломка**: Если в `vehicle.urdf.xacro` изменить `<parent link="camera_link" />` для `lidar_joint`, то `tf2_echo base_link lidar_link` покажет неверное положение (лидар окажется привязан к камере, а не к базе).
2. **Диагностика**: Команда `ros2 run tf2_tools view_frames` покажет разорванную или неверную связь.
3. **Исправление**: Возврат `<parent link="base_link" />` и повторная сборка восстанавливают дерево. Команда `tf2_echo base_link lidar_link` снова показывает корректное смещение `[0.0, 0.0, 0.3]`.

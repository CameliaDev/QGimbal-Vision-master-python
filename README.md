[![opencv](https://img.shields.io/badge/CV-OpenCV-green)]()
[![lang](https://img.shields.io/badge/lang-Python-blue)]()
[![license](https://img.shields.io/badge/license-MIT-lightgrey)]()

# QGimbal Vision

OpenCV 摄像头预览 + 矩形检测，可选双轴 PID 输出 yaw/pitch 速度（rpm），配合 [QGimbal STM32 固件](https://github.com/CameliaDev/QGimbal-master-stm32f4) 使用。

## 结构

- `main.py` — 采集 / FPS / 显示 / 控制入口
- `vision/` — 摄像头与矩形检测
- `control/` — PID、跟踪控制、串口 stub
- `tests/` — pytest

## 安装

```powershell
pip install -r requirements.txt
```

## 运行

GUI（`q` / `ESC` 退出）：

```powershell
python main.py --camera 0 --display 1
```

无窗口（终端打 FPS + 检测结果，`Ctrl+C` 退出）：

```powershell
python main.py --camera 0 --display 0 --print-interval 0.5
```

开启跟踪控制：

```powershell
python main.py --camera 0 --display 1 --control 1 --max-rpm 120 --deadband-px 6
```

> 当前 `send_rpm()` 默认为 stub；接真机时替换 `control/serial_stub.py` 中的发送逻辑。也可见 [Qdriver-python](https://github.com/CameliaDev/Qdriver-python)。

## 坐标约定

- 图像：x 右、y 下；`err = target_center - image_center`
- 方向未知时用 `ControlConfig.invert_yaw / invert_pitch` 翻转

## License

MIT © 2026 CameliaDev
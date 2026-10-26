Jetson Nano camera inference package
====================================

This package contains:

  tools\inference\camera_inf.py
  configs\dfine\custom\dfine_hgnetv2_s_custom.yml
  src\
  best.pt
  best_stg1.pth\

Use best.pt for inference. It contains the 794 EMA model tensors converted from
the original best_stg1 checkpoint. The original extracted checkpoint directory
is retained as best_stg1.pth for backup; do not remove or rename its inner
best_stg1 directory.

Run from this package directory:

  cd jetson_inference
  python tools\inference\camera_inf.py --resume best.pt --device cuda:0 --camera 0 --output camera_results --confidence 0.4

The script saves an annotated JPG and JSON bounding-box file for every frame
where a person is detected.

Jetson setup notes:

1. Use the NVIDIA JetPack-compatible PyTorch and torchvision packages for the
   JetPack version installed on the Nano. Do not install desktop CUDA wheels
   such as cu128 on the Jetson.
2. Install OpenCV and the Python packages required by the project:

   python3 -m pip install opencv-python PyYAML scipy loguru tensorboard

3. Check GPU access before running:

   python3 -c "import torch; print(torch.__version__); print(torch.cuda.is_available()); print(torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'CUDA unavailable')"

If the Nano has no desktop display, add:

  --no-display

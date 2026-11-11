# STEMBREACH models

Model files the STEMBREACH stem splitter by SoundBunker downloads. Code lives elsewhere; this repo only hosts weights, as
release assets.

## SCNet-large for MLX (float16 weights)

The weights STEMBREACH by SoundBunker uses to run SCNet-large on the Apple-silicon GPU through
[MLX](https://github.com/ml-explore/mlx). The model splits a song into four stems: drums, bass, other and vocals.

Download: the `scnet-large.fp16.safetensors` asset on the [scnet-large-mlx-v1 release](https://github.com/Soundbunkeralgarve/stembreach-models/releases/tag/scnet-large-mlx-v1).

| File | Size | SHA-256 |
|---|---|---|
| `scnet-large.fp16.safetensors` | 84.4 MB (84,404,977 bytes) | `f431f4ae57df56dfef3d4a1e3b28f6576a014be9e635e55de2a89ed871b1d071` |

The file is the original PyTorch state dict, with the same tensor names, converted to float16. STEMBREACH computes in
float32. Against the float32 original it agrees to 59 dB, which is closer than the int8 ONNX export (37 to 49 dB).

## Source

- Model: SCNet (Tong, Zhu, Chen, Kang, Jiang, Li, Wu, Meng, "SCNet: Sparse Compression Network for Music Source
  Separation", ICASSP 2024, [arXiv:2401.13276](https://arxiv.org/abs/2401.13276)), code
  [starrytong/SCNet](https://github.com/starrytong/SCNet) (MIT).
- Checkpoint: `SCNet-large_starrytong_fixed.ckpt`, SHA-256
  `65900dfa07d6b6e5d784c0f143920200a4bd281d6e78a806c549d0b912d5885e`, from release v1.0.9 of
  [ZFTurbo/Music-Source-Separation-Training](https://github.com/ZFTurbo/Music-Source-Separation-Training) (MIT), with
  `configs/config_musdb18_scnet_large.yaml`.
- Conversion: `Scripts/make_mlx_weights.py` in STEMBREACH. It loads the checkpoint with `weights_only=True` and writes
  each tensor as float16.

## Licence and attribution

MIT, Copyright (c) 2024 starrytong. In
[starrytong/SCNet#35](https://github.com/starrytong/SCNet/issues/35#issuecomment-4999873539) the weights' author
confirms that the released SCNet and SCNet-large pretrained weights are distributed under the MIT License, and that
format-converted versions may be redistributed with attribution. The model was trained on MUSDB18-HQ (Rafii et al.,
2019), which is licensed for educational use.

```bibtex
@inproceedings{tong2024scnet,
  title     = {SCNet: Sparse Compression Network for Music Source Separation},
  author    = {Tong, Weinan and Zhu, Jiaxu and Chen, Jun and Kang, Shiyin and Jiang, Tao and Li, Yang and Wu, Zhiyong and Meng, Helen},
  booktitle = {IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)},
  year      = {2024},
  eprint    = {2401.13276},
  archivePrefix = {arXiv}
}
```

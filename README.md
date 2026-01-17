<div align="center">

 <div>
  <a href="https://github.com/aiben-ch/"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Faiben-ch%2FEmbodiedComp&count_bg=%23E97EBA&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=visitors&edge_flat=false"/></a>
  <a href="https://github.com/aiben-ch/EmbodiedComp"><img src="https://img.shields.io/github/stars/aiben-ch/EmbodiedComp"/></a>
  <a href="https://arxiv.org/pdf/2512.11612"><img src="https://img.shields.io/badge/Arxiv-2512.11612-blue"/></a>
  <a href="https://huggingface.co/datasets/lcysyzxdxc/CMC-Bench"><img src="https://img.shields.io/badge/Data-Release-green"></a>
 </div>

 <h1>Embodied Image Compression

 The first embodied image compression benchmark
 
 <div>
      <a href="https://lcysyzxdxc.github.io" target="_blank">Chunyi Li</a><sup>1</sup><sup>2</sup><sup>3</sup><sup>*</sup>,
      <a href="" target="_blank">Rui Qing</a><sup>1</sup><sup>*</sup>,
      <a href="https://scholar.google.com/citations?hl=en&user=Eru2-TYAAAAJ" target="_blank">Jianbo Zhang</a><sup>1</sup>,
      <a href="https://scholar.google.com/citations?user=Kzd0qtsAAAAJ&hl=en" target="_blank">Yuan Tian</a><sup>2</sup>,
      <a href="https://scholar.google.com/citations?hl=en&user=k7YfbnEAAAAJ" target="_blank">Xiangyang Zhu</a><sup>2</sup>,
      <a href="https://zzc-1998.github.io" target="_blank">Zicheng Zhang</a><sup>2</sup><sup>2</sup>,
      <a href="https://jhc.sjtu.edu.cn/~xiaohongliu/" target="_blank">Xiaohong Liu</a><sup>1</sup>,
      <a href="https://personal.ntu.edu.sg/wslin/Home.html" target="_blank">Weisi Lin</a><sup>3</sup>,
      <a href="https://icisee.sjtu.edu.cn/jiaoshiml/zhaiguangtao.html" target="_blank">Guangtao Zhai</a><sup>1</sup><sup>2</sup>,
 </div>

 <div>
  <sup>1</sup>Shanghai Jiao Tong University,  <sup>2</sup>Shanghai AI Lab,  <sup>3</sup>Nanyang Technological University.
 </div> 
 
 <div style="width: 100%; text-align: center; margin:auto;">
      <img style="width:100%" src="figure/Overview.png">
 </div>
</div>

EmbodiedComp is a closed-loop benchmark frame for VLA(Vision-Language-Action) model.We use robosuite to build a environment with random texture and objects for an UR5 robotic arm with Pi0-FAST,Pi0.5 and OpenVLA-oft.
To align with Real-world applications of Embodied AI, we deploy the compression algorithm within the Embodied Inference pipeline for the first time, enabling closed-loop validation. Since compression distortion accumulates in each loop-iterations, evaluation metrics include both Success Rate (SR) and the Step for iterations to represent efficiency.

<div align="center">

🤗 [Datasets Download]() | 📚 [Paper](https://arxiv.org/abs/2512.11612) | 📈[Benchmark]()

</div>

## Release
- [2026/1/14]   [GoogleDrive dataset](https-link) for **EmbodiedComp** is upgrade.
- [2026/1/10] 🔥 [Github repo](https-link) for **EmbodiedComp** is online.
- [To Do] [ ] Real-world data.

# Installing
Prepare environment
```bash
git clone https://github.com/Jianbo-maker/EmbodiedComp.git
cd EmbodiedComp
# conda env create
conda env create -n Ecomp
# activate conda
conda activate Ecomp
# install lib
pip install -r requirements.txt
```
Install openpi-client:
```
cd packages/openpi-client
pip install -e .
cd ../..
```

# Benchmark with Pi0&Pi05
We use openpi-client to interact with pi0 and pi0.5, that means you have to start pi agent first with its own environment.You can see [pisetup](doc/pisetup.md) for our config for ur5 robot.And you can download our finetuned weight [here](https://huggingface.co/qruisjtu/pi_ur5_fintuned). After the pi client is start,you can change the `BENCHMARK PARAMETERS` in `pi.py` including text prompt, benchmarkname, agentname,etc.Then run,
```
python pi.py
```
the benchmark's result will be saved under folder `data/benchmark`

# Benchmark with openvla
For openvla, you can download our finetuned weight [here](https://huggingface.co/qruisjtu/openvla_ur5_finetuned).Then change the`pretrained_checkpoint= `in [openvla.py](openvla.py#L69) to your own weight path and run 

```
python openvla.py
```

the benchmark's result will be saved under folder `data/benchmark`

# Use your own compress codec
You can change code listed below to replace with your own compress codec:

- [pi](pi.py#L60) and [openvla](openvla.py#L137)'s function `build_obs_ur5` transfer image from camera to agent, you can modify our extract the image.

- [COMPRESSIMG](compress/compressimg.py#L367) collects many useful codec, you can add your own codec class in this file with function `compress`, then announce your class in `codecmap`

## Citation

If you find our work interesting, please feel free to cite our paper:

```bibtex
@misc{li2025embodiedimagecompression,
      title={Embodied Image Compression}, 
      author={Chunyi Li and Rui Qing and Jianbo Zhang and Yuan Tian and Xiangyang Zhu and Zicheng Zhang and Xiaohong Liu and Weisi Lin and Guangtao Zhai},
      year={2025},
      eprint={2512.11612},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2512.11612}, 
}
```

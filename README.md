## PyTorch binding for WarpCTC
- Current Warp ctc only have tensorflow binding,and other repository can not build on mac,so this is the pytorch-binding which can be built at macos and Centos.

### This repository can build ctc for pytorch, which modified from https://github.com/baidu-research/warp-ctc.git and https://github.com/SeanNaren/warp-ctc.git
### The way to build warp ctc
```
cd warp-ctc-pytorch-binding
make build; cd build
cmake ..
make
cd pytorch-binding
python setup.py install
```
### The way to test
```python
import torch
from torch.autograd import Variable
from warpctc_pytorch import CTCLoss
ctc_loss = CTCLoss()
# expected shape of seqLength x batchSize x alphabet_size
probs = torch.FloatTensor([[[0.1, 0.6, 0.1, 0.1, 0.1], [0.1, 0.1, 0.6, 0.1, 0.1]]]).transpose(0, 1).contiguous()
labels = Variable(torch.IntTensor([1, 2]))
label_sizes = Variable(torch.IntTensor([2]))
probs_sizes = Variable(torch.IntTensor([2]))
probs = Variable(probs, requires_grad=True) # tells autograd to compute gradients for probs
cost = ctc_loss(probs, labels, probs_sizes, label_sizes)
cost.backward()
```


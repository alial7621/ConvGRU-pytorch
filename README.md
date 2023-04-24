# ConvLSTM_pytorch
**[This](https://github.com/happyjin/ConvGRU-pytorch/blob/master/convGRU.py)** file **contains 
the implementation of Convolutional LSTM in PyTorch**

** ---In this version there is no need to add input_size and dtype as arguments to the model---**

### How to Use
The `ConvGRU` module derives from `nn.Module` so it can be used as any other PyTorch module.

The ConvGRU class supports an arbitrary number of stacked hidden layers in GRU. In this case, it can be specified 
the hidden dimension (that is, the number of channels) and the kernel size of each layer. In the case more layers 
are present but a single value is provided, this is replicated for all the layers. For example, in the following 
snippet each of the three layers has a different hidden dimension but the same kernel size.

Example usage:
```
# set CUDA device
os.environ["CUDA_VISIBLE_DEVICES"] = "0"

channels = 256
hidden_dim = [32, 64]
kernel_size = (3,3) # kernel size for two stacked hidden layer
num_layers = 2 # number of stacked hidden layer
model = ConvGRU(input_dim=channels,
                hidden_dim=hidden_dim,
                kernel_size=kernel_size,
                num_layers=num_layers,
                batch_first=True,
                bias = True,
                return_all_layers = False,
                padding=0)

# detect if CUDA is available or not
if torch.cuda.is_available():
    model.to('cuda:0') # computation in GPU

batch_size = 1
time_steps = 1
input_tensor = torch.rand(batch_size, time_steps, channels, height, width)  # (b,t,c,h,w)
layer_output_list, last_state_list = model(input_tensor)
```



### Disclaimer

This is still a work in progress and is far from being perfect: if you find any bug please don't hesitate to open an issue.

### License
ConvLSTM_pytorch is released under the MIT License (refer to the LICENSE file for details).

### Acknowledgment
This repo borrows some codes from 
- [ConvLSTM_pytorch](https://github.com/ndrplz/ConvLSTM_pytorch)


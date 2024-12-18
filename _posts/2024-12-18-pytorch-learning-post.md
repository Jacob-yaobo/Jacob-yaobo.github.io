## My deep learning record post

#### 关于如何管理GPU：
最好的方式在脚本运行 python main.py之前加入 CUDA_VISIBLE_DEVICES= 来控制可见的GPU编号；   
在代码中，使用单gpu时，使用   
'''python
device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")

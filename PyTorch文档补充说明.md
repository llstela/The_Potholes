# 补充文档中不详细的描述

torch.nn.functional.grid_sample

    https://blog.csdn.net/qq_34914551/article/details/107559031
    https://zhuanlan.zhihu.com/p/495758460   
    https://blog.csdn.net/weixin_43559672/article/details/121030037

torch.meshgrid

    import torch
    x_range = torch.tensor([0, 1, 2, 3, 4]) # of shape [5], indicates W.
    y_range = torch.tensor([0, 2, 3]) # of shape [3], indicates H
    y, x = torch.meshgrid(y_range, x_range) #注意必须是 y first!!!! 否则无法得到形状为(H,W,2)的grid
    print(x)
    print(y)
    >>>
    tensor([[0, 1, 2, 3, 4],
            [0, 1, 2, 3, 4],
            [0, 1, 2, 3, 4]])
    tensor([[0, 0, 0, 0, 0],
            [2, 2, 2, 2, 2],
            [3, 3, 3, 3, 3]])

---
title: "梯度下降优化算法笔记"
date: 2026-05-17
tags: ["机器学习", "优化", "深度学习"]
author: "Your Name"
math: true
description: "常见梯度下降优化器的数学推导与对比。"
---

## SGD

最基本的随机梯度下降：

$$
\theta_{t+1} = \theta_t - \eta \nabla_\theta J(\theta_t)
$$

其中 $\eta$ 是学习率，$\nabla_\theta J(\theta_t)$ 是损失函数对参数的梯度。

## Momentum

引入动量加速收敛：

$$
v_t = \gamma v_{t-1} + \eta \nabla_\theta J(\theta_t)
$$

$$
\theta_{t+1} = \theta_t - v_t
$$

通常取 $\gamma = 0.9$。

## Adam

结合一阶矩和二阶矩估计的自适应学习率方法：

$$
m_t = \beta_1 m_{t-1} + (1-\beta_1) g_t
$$

$$
v_t = \beta_2 v_{t-1} + (1-\beta_2) g_t^2
$$

偏差修正：

$$
\hat{m}_t = \frac{m_t}{1 - \beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1 - \beta_2^t}
$$

参数更新：

$$
\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t
$$

## 代码实现

```python
import torch
import torch.optim as optim

model = MyModel()

# SGD with momentum
optimizer = optim.SGD(model.parameters(), lr=0.01, momentum=0.9)

# Adam
optimizer = optim.Adam(model.parameters(), lr=1e-3, betas=(0.9, 0.999))

# Training loop
for epoch in range(num_epochs):
    loss = criterion(model(x), y)
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()
```

## 总结

| 优化器 | 优点 | 缺点 |
|--------|------|------|
| SGD | 简单、泛化好 | 收敛慢 |
| Momentum | 加速收敛 | 需调动量参数 |
| Adam | 自适应、收敛快 | 泛化可能不如 SGD |

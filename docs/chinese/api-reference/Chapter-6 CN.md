---
title: 风险筛查
excerpt: ""
category: 62ce2a159aafea009af30da7
slug: chapter-6-cn
---

**Smile Signals** 提供强大的风险筛查解决方案，通过一个人的手机号码或电子邮件地址，从各种活动和事件中获取实时风险信号，帮助您在当今快节奏的金融环境中保持最新动态——在这样的环境中，准确及时的风险评估对于做出明智决策至关重要。

Signals API 套件可提供数百种风险信号访问权限，使您能够根据自身用例和市场细分选择合适的信号。

当前可用的 Signals 套件如下：

| Signal                       | 状态    | 描述                                                    |  
|------------------------------|-------|-------------------------------------------------------|  
| Signals                      | Beta  | Smile 的首个风险筛查服务包含预先选择的 30 种最常见风险信号，只需用户的手机号码即可立即开始使用。 |  
| Footprints                   | Alpha | 获取用户数字足迹和在线活动的宝贵洞察。                                   |  
| Multiple Application Warning | Alpha | 发现用户借贷活动的早期迹象。                                        |  
| Blacklist                    | Alpha | 确保用户未被列入黑名单。                                          |  
| Verification                 | Alpha | 验证功能可帮助您确认用户提供的数据与预验证和/或权威来源的数据是否匹配，需用户提供 ID。         |  

---  
<!-- focus: false -->  
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)
## 集成步骤

在您的流程中实施 Smile API 的风险筛查服务只需几个步骤：

1. **选择所需的 Signal 服务**
   > 根据您的需求和拥有的数据，从 Smile 强大的 Signals 套件中选择一项服务。

2. **向 Smile API 提供所需输入**
   > 使用所选产品，通过相应的 API 端点向 Smile API 发送所需输入，例如用户的电话号码、电子邮件地址或其他数据。  
   > 例如，将用户的手机号码发送到 ``/signals`` 端点以检索风险信号数据。

3. **检索分析后的数据**
   > 数据上传后，我们的系统会根据您请求的服务自动检查和/或计算响应。  
   > 计算完成后，结果的有效负载将通过 Webhook 发送给您，或者您也可以直接调用相应的 API。更多信息请参阅 API 文档。
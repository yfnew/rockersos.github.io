# xbox api 相关开发资源汇总

## xbox live 

- [Developer program overview](https://docs.microsoft.com/zh-cn/windows/uwp/xbox-live/developer-program-overview)

## xbox api 相关资源
- [xboxapi 第三方接口](https://xboxapi.com/)
- [microsoft.com 搜索请求](https://www.microsoft.com/services/api/v3/suggest?market=zh-hk&clientId=7F27B536-CF6B-4C65-8638-A0F8CBDFCA65&sources=Microsoft-Terms%2CIris-Products%2CDCatAll-Products&filter=ExcludeDCatProducts%3ADCatDevices-Products%2CDCatSoftware-Products%2CDCatBundles-Products&counts=5%2C1%2C5&query=ark)

**参数***

- market:`zh-hk`
- clientId:`7F27B536-CF6B-4C65-8638-A0F8CBDFCA65`
- sources:`Microsoft-Terms,Iris-Products,DCatAll-Products`
- filter:`ExcludeDCatProducts:DCatDevices-Products, DCatSoftware-Products,DCatBundles-Products`
- counts:`5,1,5`
- query:`ark`

**请求URL**

```
https://www.microsoft.com/services/api/v3/suggest?market=zh-hk&clientId=7F27B536-CF6B-4C65-8638-A0F8CBDFCA65&sources=Microsoft-Terms,Iris-Products,DCatAll-Products&filter=ExcludeDCatProducts:DCatDevices-Products,DCatSoftware-Products,DCatBundles-Products&counts=5,1,5&query=ark
```

***请求结果**
点击上面的地址可见，是json格式的结构
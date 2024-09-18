# 说明

版本说明:

- 0.0.1
  - 半成品, 提供主要的 SDK 框架以便提前做集成工作
  - 无鉴权, 3 个月后自动失效



<img src="demo.jpg" width="200" />



# 使用说明

## 0x01 引入Framework

支持 CocoaPod 引入和直接引入.
### CocoaPod 引入

```podfile
  use_frameworks!
  # Improt from local
  pod 'ECGSDK', :path => './ECGSDK'
  # or
  # Import from github
  # pod 'ECGSDK', :path => 'https://github.com/Shenzhen-Simo-Technology-co-LTD/ecgi_ring_sdk_ios.git'
```

## 0x02 

添加引用:

```swift
import ECGSDK	
```

使用方法具体见 Demo.

### 接口说明

```objc
/// 实时算法
/// 实时采集心电时可以调用此算法
/// - Parameters:
///   - rawData: 原始心电数据
///   - fs: 采样率
/// - Returns:
///     - array[0]: 处理后的心电数据
///     - array[1]: 平均心率
- (NSArray *)realtimeProcess:(NSArray<NSNumber *> *)rawData fs:(double)fs;

/// 诊断算法
/// 传入 30~300 秒的心电数据, 计算后返回诊断结果
/// - Parameters:
///   - rawData: 原始心电数据
///   - fs: 采样率
/// - Returns:
///   - resultArray 一组数据, 其中:
///   - resultArray[0]: 处理后的心电数据
///   - resultArray[1]: 心率相关信息 see [README#心率相关信息]
///   - resultArray[2]: 心律(节律)相关信息 see [README#心律相关信息]
- (NSArray<NSArray<NSNumber *> *>*)diagnose:(NSArray<NSNumber *> *)rawData fs:(double)fs;

```



# 心率相关信息

0. minHR
1. meanHR
2. maxHR
3. minRR(ms)
4. meanRR(ms)
5. maxRR(ms)
6. PR间期(ms)
7. QRS 波宽(ms)
8. SDNN
9. RMSSD



# 心律相关信息

0. TypeIndex, 诊断结果(0~5)
   0. 正常
   1. 房扑
   2. 房颤
   3. 室颤/室扑
   4. 其他心律不齐
   5. 噪声
1. 置信度(0.0~1.0)
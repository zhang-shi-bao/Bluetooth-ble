
UUID做为通用唯一识别符，它是128bits的。 为了减少存储和传输128bit的数据，UUID的值别预处理为16bits或32bits的值。有三种类型的uuid，一种是32bits，一种是16bit，一种是自定义的128bit的uuid。那么缩短的uuid是怎么表示128bits的值呢？蓝牙技术联盟规定了一个计算公式。计算公式如下



```
128_bit_value = 16_bit_value * 296 + Bluetooth_Base_UUID
128_bit_value = 32_bit_value * 296 + Bluetooth_Base_UUID
```

其中Bluetooth_Base_UUID规定为0x00000000-0000-1000-8000-00805F9B34FB

假如16bits的uuid为0x1234,则转换成128bits的uuid是:

```
0x00001234-0000-1000-8000-00805F9B34FB
```

假如32bits的uuid是0x12345678,则转换成128bits的uuid是
```
0x12345678-0000-1000-8000-00805F9B34FB
```

另外，用户也可以用自定义的128bits的uuid
例如：
```
 00001513-1212-EFDE-1523-785DEABCD122 
```
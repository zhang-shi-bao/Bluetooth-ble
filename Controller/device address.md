@[toc]
Bluetooth Device Address 蓝牙设备地址分成两类：公开设备地址（public  device address）和随机地址（random device address）

# 1  public  device address
## 1.1 BR/EDR public  device address
###  BLUETOOTH DEVICE ADDRESSING


 Each Bluetooth device shall be allocated a unique 48-bit Bluetooth device address (BD_ADDR). The address shall be a 48-bit extended unique identifier (EUI-48) created in accordance with section 8.2 ("Universal addresses") of the IEEE 802-2014 standard (http://standards.ieee.org/findstds/standard/802-2014.html).Creation of a valid EUI-48 requires one of the following MAC Address Block types to be obtained from the IEEE Registration Authority:

• MAC Address Block Large (MA-L)
• MAC Address Block Medium (MA-M)
• MAC Address Block Small (MA-S)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190315143736447.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1bGF6dWxh,size_16,color_FFFFFF,t_70)

The BD_ADDR may take any values except those that would have any of the 64 reserved LAP values for general and dedicated inquiries (see Section 1.2.1).

###   Reserved Addresses
A block of 64 contiguous LAPs is reserved for inquiry operations; one LAP common to all devices is reserved for general inquiry, the remaining 63 LAPs are reserved for dedicated inquiry of specific classes of devices (see Assigned Numbers). The same LAP values are used regardless of the contents of UAP and NAP. Consequently, none of these LAPs can be part of a user BD_ADDR.The reserved LAP addresses are 0x9E8B00-0x9E8B3F. The general inquiry
LAP is 0x9E8B33. All addresses have the LSB at the rightmost position,hexadecimal notation. The default check initialization (DCI) is used as the UAP whenever one of the reserved LAP addresses is used. The DCI is defined to be 0x00 (hexadecimal).


## 1.2 LE public  device address

## 1.2.1 DEVICE ADDRESS

Devices are identified using a device address. Device addresses may be either a public device address or a random device address. A public device address and a random device address are both 48 bits in length.A device shall use at least one type of device address and may contain both.A device's Identity Address is a Public Device Address or Random StaticDevice Address that it uses in packets it transmits. If a device is using Resolvable Private Addresses, it shall also have an Identity Address.1.3.1 Public Device Address The public device address shall be created in accordance with [Vol 2] Part B, Section 1.2, with the exception that the restriction on LAP values does not apply unless the public device address will also be used as a BD_ADDR for a BR/EDR Controller.

# 2   Random Device Address

 The random device address may be of either of the following two sub-types:
• Static address
• Private address.
The term random device address refers to both static and private address types. The transmission of a random device address is optional. A device shall accept the reception of a random device address from a remote device.
### 2.1.1  Static Device Address
A static address is a 48-bit randomly generated address and shall meet the following requirements:
• The two most significant bits of the address shall be equal to 1
• At least one bit of the random part of the address shall be 0
• At least one bit of the random part of the address shall be 1
The format of a static address is shown in Figure 1.2.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190315143813747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1bGF6dWxh,size_16,color_FFFFFF,t_70)
 A device may choose to initialize its static address to a new value after each power cycle. A device shall not change its static address value once initialized until the device is power cycled. Note: If the static address of a device is changed, then the address stored in peer devices will not be valid and the ability to reconnect using the old address will be lost.

###  2.1.2 Private Device Address Generation
The private address may be of either of the following two sub-types:
• Non-resolvable private address
• Resolvable private address
To generate a non-resolvable address, the device shall generate a 48-bit
address with the following requirements:
• The two most significant bits of the address shall be equal to 0
• At least one bit of the random part of the address shall be 1
• At least one bit of the random part of the address shall be 0
• The address shall not be equal to the public address
The format of a non-resolvable private address is shown in Figure 1.3.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190315143905895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1bGF6dWxh,size_16,color_FFFFFF,t_70)

 To generate a resolvable private address, the device must have either theLocal Identity Resolving Key (IRK) or the Peer Identity Resolving Key (IRK).The resolvable private address shall be generated with the IRK and a randomly generated 24-bit number. The random number is known as prand and shall meet the following requirements:
• The two most significant bits of prand shall be equal to 0 and 1 as shown in Figure 1.4
• At least one bit of the random part of prand shall be 0
• At least one bit of the random part of prand shall be 1
The format of the resolvable private address is shown in Figure 1.4

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190315143936451.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1bGF6dWxh,size_16,color_FFFFFF,t_70)
 The hash is generated using the random address function ah defined in [Vol 3]

Part H, Section 2.2.2 with the input parameter k set to the device’s IRK and the input parameter r set to prand.
```
hash = ah(IRK, prand)
```
The prand and hash are concatenated to generate the random address (randomAddress) in the following manner:
```
randomAddress = hash || prand 
```
The least significant octet of hash becomes the least significant octet ofrandomAddress and the most significant octet of prand becomes the most significant octet of randomAddress

###  1.3.2.3 Private Device Address Resolution
A resolvable private address may be resolved if the corresponding device’s IRK is available using this procedure. If a resolvable private address is resolved, the device can associate this address with the peer device.The resolvable private address (RPA) is divided into a 24-bit random part (prand) and a 24-bit hash part (hash). The least significant octet of the RPA becomes the least significant octet of hash and the most significant octet of RPA becomes the most significant octet of prand. A localHash value is then generated using the random address hash function ah defined in [Vol 3] Part H, Section 2.2.2 with the input parameter k set to IRK of the known device and the input parameter r set to the prand value extracted from the RPA.

```
localHash = ah(IRK, prand) 
```
The localHash value is then compared with the hash value extracted from RPA.If the localHash value matches the extracted hash value, then the identity of the peer device has been resolved. If a device has more than one stored IRK, the device repeats the above procedure for each stored IRK to determine if the received resolvable private address is associated with a stored IRK, until either address resolution is successful for one of the IRKs or all have been tried. Note: A device that cannot resolve a private address within T_IFS may respond on the reception of the next event. A non-resolvable private address cannot be resolved



------------------------------------------------分割线-------------------------------------------------------------------


蓝牙设备地址分成两类：public device address 和Random device address 。
Random device address 分为 Static device address和Private  device address。
Private  device address 又分为 Non-resolvable private address 和Resolvable private address
**值得注意的是：在BR/EDR只有public devcie address，LE则可以同时拥有public device address 和Random device address 。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190315153625996.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1bGF6dWxh,size_16,color_FFFFFF,t_70)
(图片从[蜗窝科技](http://www.wowotech.net/bluetooth/ble_address_type.html)借来用的，如有侵权，请联系删除)

**public device address：**
需要向IEEE协会申请，这个能保证地址的唯一性。

**Static device address：**
可以在每次上电的时候更新一次Static device address。需要注意的是，如果Static device address更新了，那么保存的配对信息就无效了。

**resolvable private address：** 由两部分组成

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190315153644247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1bGF6dWxh,size_16,color_FFFFFF,t_70)
计算公式如下
```
hash = ah(IRK, prand)
```
```
randomAddress = hash || prand 
```




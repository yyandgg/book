# Pontus400 高密度转码服务器

PONTUS高密度转码系统基于“CPU+GPU"的软硬件相结合的系统架构，提供高密度和高性能的视频转码服务。该系统同时支持离线文件转码和在线实时视频流转码，支持多种多媒体数据的传输，全方位支持广电行业和互联网视频的应用需求。

## 1.音视频编解码

* 输入支持 MPEG1、MPEG2、H.261、H.262、H.263、H.264、VP8、VP9、MP4、VC1、HEVC、AVS、AVS+ 等多种视频编码格式；

* 输入支持 speex、MP2、MP3、ACC、HEAAC、AC3、WMV 等多种音频编码格式；

* 输出支持 MPEG2、H.264、HEVC 三种视频编码格式；

* 输出支持 MP2、MP3、AAC、HEAAC、AC3 五种音频编码格式；

* 支持最新的视频编码国家标准AVS+信源格式解码，全面实现三网融合下的视频直播和点播业务；

* 支持最新视频编码国际标准HEVC编码和解码；

* 支持4k视频编解码，最高支持4096x4096视频输出。


## 2.实时视频流转码

基于多GPU的编转码技术以及高效率的系统调度算法，单台设备（1U标准工业机箱）最大支持40+路1080P视频的实时转码，为用户提供高密度转码服务。每路输入可实现多路输出，满足多平台多终端的视频应用需求。

** 支持AVS+信源、4K分辨率和HEVC直播**

* 无缝支持视频编码国家标准 AVS+信源；

* 支持4K分辨率，包括4K输入码流的解码以及自有上采样算法实现从输入标清/高清到4K的转换，最高支持4096x4096分辨率；

* 支持最新视频编码国际标准HEVC，与4K分辨率相结合，全面提升视频画质和终端观影体验，为用户提供高效、稳定和高质量的4K+HEVC直播服务。


** 多种流媒体支持**

* 支持RTMP推流和拉流；

* 支持RTSP拉流；

* 支持http-flv拉流；

* 支持HLS拉流，HLS输出TS流分片支持TS流恒定码率；

* 支持UDP组播接流和推流；

* 输出TS流符合TR101-290标准。


** 高效调度策略**

* 动态实时系统资源监控和管理，百分百确保任意时刻均有可用CPU资源，保证系统百分百可响应；

* GPU资源的充分调度和利用，所有可并行算法均采用GPU实现，提升算法的运行效率，节省有限的CPU资源；

* 面向高分辨率（1080P和4K）和高帧率（60fps+）应用进行系统优化设计，全面提升高分辨率和高帧率条件下的转码性能；

* 多网卡调度策略确保实时网络响应和网络数据交换；

* 动态和实时任务调度策略，确保紧急任务的迅速响应和处理。


## 3.离线文件转码

提供基于文件的转码功能，为多屏互动点播，节目制播业务提供高速度转码服务,支持FTP、CIFS、NFS等多种文件系统协议接入，并兼容市面上所有主流文件格式，提供超高倍速、超大吞吐量转码。

** 超实时转码**

通过先进的编码和转码技术、先进的调度算法以及GPU超级运算技术，提供超市时转码转码能力。单路1080P视频的12+倍速转码、单台设备最大40+倍速转码，单台设备每天能够处理5TB+的视频数据

** HEVC+4K内容生产**

为用户提供高画质、高效率的HEVC与4K视频压缩处理，实现超清晰的视觉体验。同时，HEVC编码标准提供更高的视频数据压缩效率，为用户进一步节省视频传输带宽和存储空间，减低视频的使用维护成本。

** 全格式支持**

支持主流的音视频封装格式，包括 TS、MP4、FLV、F4V、AVI、MKV、MOV、3GP、RM、WMV等。为从广电IPTV到互联网VOD点播提供视频编码格式和封装格式的全兼容支持。

## 视频处理技术

拥有多项自主知识产权的视频处理核心技术，在视频转码的各个环节保证视频处理的最优效果，从而在大幅提升转码速度的同时保证转码后的视频质量。

## 多层次容错技术

* 网络层容错机制，保证网络接口的鲁棒性和稳定性；

* 视音频流容错，保证广泛的格式兼容；

* 视频编解码容错，保证视频编解码，特别是解码的鲁棒性。



## 甲骨文多模态数据集



### 简介

甲骨文多模态数据集是一项专为研究中国古代甲骨文（中国最早的成熟文字系统）而构建的综合学术资源。本数据集融合了原始高清甲骨拓片、精确对⻬的摹本、详细的辞例释义及精准的单字图像标注，为自动生成摹本、拓片字及摹本字的目标检测与识别、以及甲骨文单字的字形匹配等任务提供了评估和优化的平台。

### 数据内容

#### 数据组成

甲骨文多模态数据集中原始拓片选自《甲骨文合集》和《殷墟花园庄东地甲骨》，摹本拓片来源于《甲骨文摹本大系》，释文基于《摹释全编释文》，甲骨文字头类别标准参考《镜原甲骨文字库》。通过拓片目标检测算法、摹本目标检测算法、拓片字降噪算法、摹本字相似度匹配算法和甲骨片重片检索算法构建标注工具，专家利用标注工具完成对拓片中的单字检测框、字头、释文、辞例分组以及释读顺序的标注，形成了一个包含详细辞例和单字标注的甲骨文多模态数据集。最终标注后的拓片数量达10146片，同时包括 xx条释文辞例。

#### 数据样例

![data2](./image/data2.BMP)

#### 数据标签样例

```json
{
  "baseImg": "h00002.jpg",
  "tpImg": "h00002.jpg",
  "num": "H2",
  "recordUtilSentenceGroupVOList":
  [
    {
      "sentenceContent": "citiao1",
      "recordUtilOracleCharVoList":
      [
        {
          "position": "51.58785,13.06258,14.21308,12.37251",
          "orderNumber": 1,
          "seatFont": 0,
          "oracleFontImg": "767-3555-qmvfvw99v9/2767A-qmvfvw99v9/56-合28450-96g45i4vyv.png",
          "mark": -1
        },
        {
          "position": "77.74717,50.06425,14.35095,13.35387",
          "orderNumber": 0,
          "seatFont": 0,
          "oracleFontImg": "2623-2940-h16yr7furr/2623C-hepub2s5by/23-合19667-xwmem00mse.png",
          "mark": -1
        },
        {
          "position": "48.61629,27.73732,16.70322,19.51720",
          "orderNumber": 2,
          "seatFont": 0,
          "oracleFontImg": "",
          "mark": -1
        }
      ]
    },
    {
      "sentenceContent": "citiao2",
      "recordUtilOracleCharVoList":
      [
        {
          "position": "558,581,80,218",
          "orderNumber": 0,
          "seatFont": 0,
          "oracleFontImg": "403-1795-xkubtjk815/403A-xkubtjk815/85-屯2666-zew5f9wok4.png",
          "mark": -1
        },
        {
          "position": "824,483,94,88",
          "orderNumber": 1,
          "seatFont": 0,
          "oracleFontImg": "3351-4282-h0gzv3styy/3351A-h0gzv3styy/1-诂林3348-h0gzv3styy.png",
          "mark": -1
        },
        {
          "position": "829,769,46,67",
          "orderNumber": 2,
          "seatFont": 0,
          "oracleFontImg": "2380-2678-pmwfonj2ag/2380A-pmwfonj2ag/52-合22135-0sl1gs9vt8.png",
          "mark": -1
        }
      ]
    }
  ]
}
```

#### 字段说明

- **baseImg:**【字符串类型】完整摹本图像的路径
- **tpImg:**【字符串类型】完整拓片图像的路径
- **num:**【字符串类型】当前拓片名称
- **recordUtilSentenceGroupVOList:**【数组类型】拓片含有的辞例列表
- **sentenceContent:** 【字符串类型】辞例描述
- **recordUtilOracleCharVoList:**【数组类型】拓片中的单字标注列表
- **position:**【字符串类型】当前单字在完整拓片中的位置
- **orderNumber:** 【整数类型】当前单字在辞例中的释读顺序
- **oracleFontImg:**【字符串类型】当前单字对应的字头类别
- **seatFont:**【整数类型】占位符，0代表没有占位，1代表占位：表示只有检测框和辞例排序，但不存在对应的字头图片和释文
- **mark:**【整数类型】标记符，0代表待识别的残字，1代表待排序，2代表只在拓片上存在，3代表只在摹本上存在，4代表未释字

#### 数据处理过程

1. 拓片单字检测：首先通过甲骨文目标检测算法，初步标注甲骨文单字检测框。
2. 摹本拓片对对齐：通过甲骨片重片检索算法将拓片和摹本上的字进行关联，再根据关联上的字的坐标计算摹本字到拓片字的坐标的旋转平移矩阵M，对摹本图像根据M进行旋转平移计算，得到对齐后的摹本拓片图像对。
3. 摹本单字匹配：通过甲骨文摹本字匹配算法，根据检测的摹本单字图像与**镜原甲骨文字库**进行匹配。
4. 专家人工标注：基于匹配的相似度排序结果，专家人工标注每个单字对应的检测框、字头、释文、辞例分组、释读顺序、兆序。



### 使用许可

甲骨文多模态数据集遵循[CC BY-SA4.0](https://creativecommons.org/licenses/by-sa/4.0/)许可协议

### 特别注意事项

下载数据集请提供完整的申请，下载链接



### 引文

```latex
@misc{liu2023michaohuafen,
      title={MiChao-HuaFen 1.0: A Specialized Pre-trained Corpus Dataset for Domain-specific Large Models}, 
      author={Yidong Liu and FuKai Shang and Fang Wang and Rui Xu and Jun Wang and Wei Li and Yao Li and Conghui He},
      year={2023},
      eprint={2309.13079},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```


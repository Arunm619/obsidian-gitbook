
Total MAU: 172.2 Million (17,22,11,555)

Total Android Devices: 6622

Out of 6622 devices, top 250 devices contribute to 76.7% of MAU = 132 Million (13,20,86,262)

250 devices of total devices (6622) contributes to 3.8%

3.8% (250) of device models contribute to 76.7% of MAU (132 Million)

Top 250 models contribute 76.7% of MAU, out of total 6622
% of 250 out of total: 3.8

| brand | device   | manuf | model       | mau     | up_anr_rate | up_crash_rate | ram       | sdks  | soc              | gpu                             | s_sizes  | s_densities | abis                          | gles | ff    | mau_pct |
|-------|----------|-------|-------------|---------|-------------|---------------|-----------|-------|------------------|---------------------------------|----------|-------------|-------------------------------|------|-------|---------|
| Redmi | dandelion| Redmi | Redmi 10A   | 3674306 | 0.54        | 0.04          | 1853-6070MB| 29;30 | Mediatek MT6762 | Imagination Tech PowerVR GE8320 (650 MHz) | 720x1600 | 320         | armeabi;armeabi-v7a           | 3.2  | Phone | 2.134   |
| OPPO  | OP4F2F   | Oppo  | CPH2185     | 2915213 | 0.29        | 0.23          | 1890-6106MB| 29;30 | Mediatek MT6765 | Imagination Tech PowerVR GE8320 (680 MHz) | 720x1600 | 320         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 1.693   |
| vivo  | V2204    | Vivo  | Y16         | 2403469 | 0.52        | 0.02          | 2937-3993MB| 31    | Mediatek MT6765 | Imagination Tech PowerVR GE8320 (680 MHz) | 720x1600 | 300         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 1.396   |
| vivo  | V2225    | Vivo  | T2x 5G      | 2343306 | 0.04        | 0.03          | 3783-8007MB| 33;34 | Mediatek MT6833 | 2x ARM Mali G57 (950 MHz)             | 1080x2408| 440         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 1.361   |
| vivo  | 2034     | Vivo  | V2101       | 1821508 | 0.94        | 0.02          | 2970MB     | 30    | Qualcomm SDM439 | Qualcomm Adreno 505 (560 MHz)         | 720x1600 | 300         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 1.058   |

---



![[Screenshot 2024-04-01 at 7.11.36 PM.png]]

% of MAU with ANR rate < 0.1: 48.44700000000001
% of MAU with ANR rate >= 0.1: 51.427
Number of models with ANR rate < 0.1: 6005
No. of models with ANR rate >= 0.1: 625
Total number of models in catalog: 6630

---

##### MAU devices
| count | mean  | std    | min | 50% | 75% | 90%  | 95%   | 99%    | max     |
|-------|-------|--------|-----|-----|-----|------|-------|--------|---------|
| 6630  | 25975 | 133202 | 1   | 15  | 340 | 21970| 133330| 558955 | 3674306 |

##### High-End Devices
| count | mean  | std   | min | 50% | 75% | 90%  | 95%   | 99%    | max     |     |
| ----- | ----- | ----- | --- | --- | --- | ---- | ----- | ------ | ------- | --- |
| 6005  | 13924 | 85042 | 1   | 10  | 106 | 3475 | 49729 | 364808 | 2343306 |     |
##### Non-High-End Devices

| count | mean   | std    | min | 50%   | 75%    | 90%    | 95%    | 99%     | max     |
|-------|--------|--------|-----|-------|--------|--------|--------|---------|---------|
| 625   | 141753 | 322613 | 242 | 13263 | 130513 | 388116 | 731527 | 1511247 | 3674306 |



---
##### get the anr rate of top 250 devices

| count | mean | std  | min | 50%  | 75%  | 90% | 95%  | 99%  | max  |
|-------|------|------|-----|------|------|-----|------|------|------|
| 250.0 | 0.36 | 0.69 | 0.0 | 0.11 | 0.36 | 0.9 | 1.66 | 2.73 | 6.28 |

##### also print variance and coefficient of variation
0.4772491068273092


![[Screenshot 2024-04-01 at 7.31.44 PM.png]]

---
#### Top 20 devices Non-High-End Devices - Sorted based on MAU Percentage

| brand  | device     | manuf  | model            | mau     | up_anr_rate | mau_pct | up_anr_bucket |
| ------ | ---------- | ------ | ---------------- | ------- | ----------- | ------- | ------------- |
| Redmi  | dandelion  | Redmi  | Redmi 10A        | 3674306 | 0.54        | 2.134   | (0.5, 1.0]    |
| OPPO   | OP4F2F     | Oppo   | CPH2185          | 2915213 | 0.29        | 1.693   | (0.2, 0.3]    |
| vivo   | V2204      | Vivo   | Y16              | 2403469 | 0.52        | 1.396   | (0.5, 1.0]    |
| vivo   | 2034       | Vivo   | V2101            | 1821508 | 0.94        | 1.058   | (0.5, 1.0]    |
| realme | RMX3231    | realme | realme C11 2021  | 1696960 | 0.40        | 0.985   | (0.3, 0.4]    |
| OPPO   | OP56F5     | Oppo   | A17              | 1644937 | 1.30        | 0.955   | (1.0, 2.0]    |
| vivo   | V2207      | Vivo   | vivo Y22         | 1531444 | 0.17        | 0.889   | (0.1, 0.2]    |
| vivo   | 2111       | Vivo   | V2111-EG         | 1447290 | 0.40        | 0.840   | (0.3, 0.4]    |
| vivo   | 1904       | Vivo   | vivo 1904        | 1245339 | 2.24        | 0.723   | (2.0, 4.0]    |
| vivo   | 1901       | Vivo   | vivo 1901        | 1181490 | 0.55        | 0.686   | (0.5, 1.0]    |
| xiaomi | ginkgo     | Redmi  | Redmi Note 8     | 1051400 | 0.29        | 0.611   | (0.2, 0.3]    |
| Xiaomi | olive      | Xiaomi | Redmi 8          | 1038535 | 0.20        | 0.603   | (0.1, 0.2]    |
| POCO   | angelicain | POCO   | POCO C31         | 1008682 | 0.15        | 0.586   | (0.1, 0.2]    |
| xiaomi | violet     | Xiaomi | Redmi Note 7 Pro | 1005913 | 0.18        | 0.584   | (0.1, 0.2]    |
| vivo   | 1906       | Vivo   | vivo 1906        | 983294  | 1.65        | 0.571   | (1.0, 2.0]    |
| realme | RE87BAL1   | realme | realme C35       | 971733  | 0.79        | 0.564   | (0.5, 1.0]    |
| realme | REE2ADL1   | realme | realme C55       | 970335  | 0.11        | 0.563   | (0.1, 0.2]    |
| Redmi  | lime       | Redmi  | Redmi 9T         | 963558  | 0.20        | 0.560   | (0.1, 0.2]    |
| xiaomi | whyred     | Xiaomi | Redmi Note 5 Pro | 933453  | 0.19        | 0.542   | (0.1, 0.2]    |
| Redmi  | fog        | Redmi  | Redmi 10C        | 910505  | 0.18        | 0.529   | (0.1, 0.2]    |

This Markdown table retains only the specified columns from the provided data. Each row corresponds to a device, and each column represents a specific attribute of that device.

#### Top 10 devices Non-High-End Devices - Sorted based on ANR Rate

| brand   | device         | manuf   | model                       | mau  | up_anr_rate | up_crash_rate | ram       | sdks   | soc               | gpu                                     | s_sizes   | s_densities | abis                          | gles | ff    | mau_pct | up_anr_bucket |
|---------|----------------|---------|-----------------------------|------|-------------|---------------|-----------|--------|-------------------|-----------------------------------------|-----------|-------------|-------------------------------|------|-------|---------|---------------|
| LAVA    | T81N           | Lava    | T81N                        | 5452 | 12.68       | 1.73          | 2000MB    | 29     | Mediatek MT6761  | Imagination Tech PowerVR GE8300 (660 MHz) | 800x1280  | 240         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 0.003   | (4.0, 100.0]  |
| Nokia   | WSP_sprout     | Nokia   | Nokia 2.2                   | 6253 | 10.18       | 0.36          | 1917-2971MB| 30     | Mediatek MT6761  | Imagination Tech PowerVR GE8300 (660 MHz) | 720x1520  | 320         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 0.004   | (4.0, 100.0]  |
| Coolpad | 1826-I01       | Coolpad | 1826-I01                    | 1728 | 10.05       | 0.00          | 3960MB    | 28     | Mediatek MT6762  | Imagination Tech PowerVR GE8320 (650 MHz) | 720x1520  | 320         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 0.001   | (4.0, 100.0]  |
| Itel    | itel-L5002R   | Itel    | itel A25                    | 6548 | 9.84        | 0.08          | 929MB     | 30     | Spreadtrum SC9832E| ARM Mali T820 (680 MHz)                 | 720x1280  | 320         | armeabi;armeabi-v7a           | 3.2  | Phone | 0.004   | (4.0, 100.0]  |
| Infinix | Infinix-X627V  | Infinix | Smart 3 Plus                | 8830 | 9.51        | 0.24          | 1937MB    | 28     | Mediatek MT6761  | Imagination Tech PowerVR GE8300 (660 MHz) | 720x1520  | 320         | armeabi;armeabi-v7a           | 3.2  | Phone | 0.005   | (4.0, 100.0]  |
| Nokia   | IRM_sprout     | Nokia   | Nokia 2.3                   | 13102| 8.88        | 0.23          | 1941MB    | 30     | Mediatek MT6761  | Imagination Tech PowerVR GE8300 (660 MHz) | 720x1520  | 280         | armeabi;armeabi-v7a           | 3.2  | Phone | 0.008   | (4.0, 100.0]  |
| Lenovo  | 7305X          | Lenovo  | Lenovo Tab M7                | 3144 | 8.06        | 0.10          | 949-1992MB| 28     | Mediatek MT8765B  | Imagination Tech PowerVR GE8100 (420 MHz)| 600x1024  | 160         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Tablet| 0.002   | (4.0, 100.0]  |
| Lenovo  | 8505X          | Lenovo  | Lenovo Tab M8                | 34235| 7.89        | 2.71          | 1834-2888MB| 29    | Mediatek MT8766A | Imagination Tech PowerVR GE8300 (660 MHz) | 800x1280  | 240         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Phone | 0.020   | (4.0, 100.0]  |
| Lenovo  | X306F          | Lenovo  | Lenovo Tab M10 HD (2nd Gen)  | 1068 | 7.83        | 2.34          | 1905-4040MB| 29;30 | Mediatek MT8768T | Imagination Tech PowerVR GE8320 (680 MHz) | 800x1280  | 160         | arm64-v8a;armeabi;armeabi-v7a | 3.2  | Tablet| 0.001   | (4.0, 100.0]  |
| Nokia   | E2M            | Nokia   | Nokia 2.1                   | 5358 | 7.78        | 3.34          | 907MB     | 29     | Qualcomm MSM8917 | Qualcomm Adreno 308 (400 MHz)             | 720x1280  | 280         | armeabi;armeabi-v7a           | 3.0  | Phone | 0.003   | (4.0, 100.0]  |



### FAQ:
count: The total number of non-null observations in the dataset. In this case, there are 6630 observations.
mean: The average value of the dataset. It's calculated by summing all the values and dividing by the count. Here, the average is 25975.
std: The standard deviation, which measures the amount of variation or dispersion in the dataset. A low standard deviation indicates that the values tend to be close to the mean, while a high standard deviation indicates that the values are spread out over a wider range. In this case, the standard deviation is 133202, which is quite high.
min: The smallest value in the dataset. Here, the minimum value is 1.
50% (Median): The middle value of the dataset when it's sorted in ascending order. If there's an even number of observations, the median is the average of the two middle numbers. Here, the median is 15.
75% (Third Quartile): The value below which 75% of the observations fall. It's also the median of the upper half of the data (excluding the median). Here, the third quartile is 340.
90%: The value below which 90% of the observations fall. Here, it's 21970.
95%: The value below which 95% of the observations fall. Here, it's 133330.
99%: The value below which 99% of the observations fall. Here, it's 558955.
max: The largest value in the dataset. Here, the maximum value is 3674306.
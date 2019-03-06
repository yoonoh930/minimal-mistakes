---
title: "First post"
categories: data
excerpt: "First writing, not sure how I'm gonna structure the post"
---

1. Motivation
   * <strike>Why am I doing this?</strike>
   * <strike>What's the ending product you see??</strike>

2. Process
   * <strike>Data gathering</strike>
   * <strike>Look at the data</strike>
   * <strike>Wrangling</strike>
   * <strike>Visualization setup</strike>
   * <strike>Launch</strike>

3. Data
   * <strike>How I got the data</strike>
   * Summary of data wrangling
   * 

------

## Motivation
I am a south Korean. It implies a lot of things. For example, I am used to hanging out until the morning. I am used to seeing a lot of places open until *super* late night or, until the following morning. And most of the time, it's fine even if you're drunk in the middle of street. It's safe in Seoul. Also I like kimchi. Kimchi has to be on the table every time I am having Korean food. I really love fried chicken. Especially when there is a beer next to it. There is even a term after the combination: [Chimaek](https://en.wikipedia.org/wiki/Chimaek) (chi stands for chicken and maek stands for beer in korean)

<figure class="align-center">
    <a href="http://rizer.tv/korean-fried-chicken-beer/"><img src="/assets/images/chimaek.jpg"></a>
    <figcaption>My beloved Chimaek. Click the picture to know more about it</figcaption>
</figure>

I thought, it would be fun to dig little deeper about fried chicken market and compare with other fast food markets such as pizza and hamburger. And I'd like to make a dashboard out of it. So the final product would be a some kind of dashboard that users can choose administration and the dashboard gives some insights about chicken franchises at the given location as well as other fast food markets. Let's begin.

## Procedures
There are several parts needed in order to make a functional dashboard. I specified and put them into an order of steps:

1. <strong>Data gathering</strong>  
    From the [public data portal](https://www.data.go.kr/), anyone who is a Korean with a valid phone number can sign up and pull the data as much as they want. I will use _small business store information services_ from the site.

2. <strong>Data check</strong>  
    Even if it's from the government, there will be some missing values. I will check the datasets using `pandas` library in `python`. 

3. <strong>Data wrangling</strong>  
    At this step, we will modify the data so it is visualization-ready.

4. <strong>Visualization setup</strong>  
    There are several libraries I will utilize in order to visualize all the data. These are the lists:
    * `Mapbox GL JS`: A javascript library that uses WebGL to render a map.
    * `D3`: A javascript library for manipulating documents based on data. It is mainly used to parse json.
    * `Bootstrap`: A CSS template for constructing a dashboard.
    * `dc.js`: A javascript charting library with native crossfilter support. Uses D3 to render charts.

5. <strong>Launch</strong>  
    Release the beast!



This is the picture of system I am using:
<figure class="align-center">
    <a href="/assets/images/system.png"><img src="/assets/images/system.png"></a>
    <figcaption>I know this is in Korean but I thought it didn't really matter :)</figcaption>
</figure>


## Data Gathering
It was not hard to collect the data. Fortunately there is a Public Data Portal run by Korean government and it provides a lot of free data including real estate information such as rent, price of a house/apartment, transportation information such as accidents, people coming in and out of a subway station. We will use *small business store information services* in order to pull the data for fried chicken stores. I actually made a script and uploaded it on Github. You can find it [here](https://github.com/yoonoh930/Chicken_Stores_Extracter). Note that you need API token from the site. Don't worry even if you can't get it. I downloaded all the data, saved it as `stores.json` and uploaded with the script. 

The following shows the structure of the data.


```python
df.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>adongCd</th>
      <th>adongNm</th>
      <th>bizesId</th>
      <th>bizesNm</th>
      <th>bldMngNo</th>
      <th>bldMnno</th>
      <th>bldNm</th>
      <th>bldSlno</th>
      <th>brchNm</th>
      <th>ctprvnCd</th>
      <th>...</th>
      <th>lon</th>
      <th>newZipcd</th>
      <th>oldZipcd</th>
      <th>plotSctCd</th>
      <th>plotSctNm</th>
      <th>rdnm</th>
      <th>rdnmAdr</th>
      <th>rdnmCd</th>
      <th>signguCd</th>
      <th>signguNm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2771031000</td>
      <td>가창면</td>
      <td>10027626</td>
      <td>장모님치킨가창점</td>
      <td>2771031024101200004036858</td>
      <td>6</td>
      <td></td>
      <td></td>
      <td>가창점</td>
      <td>27</td>
      <td>...</td>
      <td>128.644459</td>
      <td>42938</td>
      <td>711861</td>
      <td>1</td>
      <td>대지</td>
      <td>대구광역시 달성군 가창면 가창동로</td>
      <td>대구광역시 달성군 가창면 가창동로 6</td>
      <td>277103148001</td>
      <td>27710</td>
      <td>달성군</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2729062500</td>
      <td>상인2동</td>
      <td>10048463</td>
      <td>정통숯불바베큐치킨상인점</td>
      <td>2729011500114280014013938</td>
      <td>46</td>
      <td></td>
      <td></td>
      <td>상인점</td>
      <td>27</td>
      <td>...</td>
      <td>128.536144</td>
      <td>42791</td>
      <td>704370</td>
      <td>1</td>
      <td>대지</td>
      <td>대구광역시 달서구 상원로</td>
      <td>대구광역시 달서구 상원로 46</td>
      <td>272903147008</td>
      <td>27290</td>
      <td>달서구</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4125056500</td>
      <td>불현동</td>
      <td>10098244</td>
      <td>짱구피자치킨</td>
      <td>4125010300102680011008557</td>
      <td>30</td>
      <td></td>
      <td></td>
      <td></td>
      <td>41</td>
      <td>...</td>
      <td>127.065903</td>
      <td>11320</td>
      <td>483030</td>
      <td>1</td>
      <td>대지</td>
      <td>경기도 동두천시 못골로</td>
      <td>경기도 동두천시 못골로 30</td>
      <td>412503189006</td>
      <td>41250</td>
      <td>동두천시</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 39 columns</p>
</div>


```python
df.iloc[150]
```




    adongCd                      4518051000
    adongNm                             수성동
    bizesId                        11707011
    bizesNm                      BHC치킨정읍수성점
    bldMngNo      4518010100109180004025584
    bldMnno                              26
    bldNm                             제일아파트
    bldSlno                                
    brchNm                            정읍수성점
    ctprvnCd                             45
    ctprvnNm                           전라북도
    dongNo                                 
    flrNo                                 1
    hoNo                                   
    indsLclsCd                            Q
    indsLclsNm                           음식
    indsMclsCd                          Q05
    indsMclsNm                       닭/오리요리
    indsSclsCd                       Q05A08
    indsSclsNm                    후라이드/양념치킨
    ksicCd                           I56193
    ksicNm                           치킨 전문점
    lat                             35.5833
    ldongCd                      4518010100
    ldongNm                             수성동
    lnoAdr               전라북도 정읍시 수성동 918-4
    lnoCd               4518010100209180004
    lnoMnno                             918
    lnoSlno                               4
    lon                             126.855
    newZipcd                          56175
    oldZipcd                         580724
    plotSctCd                             1
    plotSctNm                            대지
    rdnm                      전라북도 정읍시 수성3로
    rdnmAdr                전라북도 정읍시 수성3로 26
    rdnmCd                     451803270025
    signguCd                          45180
    signguNm                            정읍시
    Name: 150, dtype: object


You can see that there are empty values. What I need to visualize the data is

```python
['bizesNm', 'ctprvnNm', 'signguNm', 'adongNm', 'rdnmAdr', 'lon', 'lat']
```

```python
df.isnull().sum()[['bizesNm', 'ctprvnNm', 'signguNm', 'adongNm', 'rdnmAdr', 'lon', 'lat']]
```




    bizesNm       0
    ctprvnNm    193
    signguNm    193
    adongNm     193
    rdnmAdr       0
    lon           0
    lat           0
    dtype: int64

And apparently, only `ctprvnNm`, `signguNm`, `adongNm` have missing values to process. Since there was no mising values from `rdnmAdr` which is basically a complete address. I used `rdnmAdr` to extract values for other missing values. You can see the details in this [link](https://github.com/yoonoh930/Chicken_Stores_Extracter/blob/master/data%20wrangling.ipynb)


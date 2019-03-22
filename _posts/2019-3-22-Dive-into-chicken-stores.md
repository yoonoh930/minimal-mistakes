---
title: "Dive into chicken stores in South Korea"
categories: data
excerpt: "Download and explore the data"
---

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
So let's check it out
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

And apparently, only `ctprvnNm`, `signguNm`, `adongNm` have missing values to process. Since there was no mising values from `rdnmAdr` which is basically a complete address. I used `rdnmAdr` to extract values for other missing values. Also, fortunately, I was about to find a list of fried chicken franchise from the following [link](https://namu.wiki/w/%EC%B9%98%ED%82%A8/%EA%B0%80%EA%B2%8C%20%EB%AA%A9%EB%A1%9D). And since the `bizesNm` contains the name of the franchise it belongs, I was able to make a separate column and put the name of the franchise. You can see the details in this [link](https://github.com/yoonoh930/Chicken_Stores_Extracter/blob/master/data%20wrangling.ipynb)

## Data Exploration
I did small exploration based on the data from the wrangle above. From the data, percentage of top brands could be extracted.

<figure class="align-center">
    <a href="/assets/images/output_3_0.png"><img src="/assets/images/output_3_0.png"></a>
    <figcaption>Fig. 1) Top 10 brands take the majority of the franchise business in fried chicken market</figcaption>
</figure>

As we can see from the graph above, top 5 franchise brands take up around one third of the whole fried chicken business while the top 10 brands take up around half. And this is a lot since the fried chicken market is around $5B as this [article](http://www.foodtoday.or.kr/news/article.html?no=156070) mentions. Of course, in order to investigate further, other data, such as revenue, population, are needed. Since our data is limited, we are gonna do brief exploration about how franchise is distributed in major administrations.

First, let's check which brand has the highest number of stores and which state has the most number of fried chicken stores.

<figure class="align-center">
    <a href="/assets/images/output_5_0.png"><img src="/assets/images/output_5_0.png"></a>
    <figcaption>Fig. 2) 페리카나  has the highest number of the stores followed by BHC and BBQ. Note that this doesn't necessarily mean that 페리카나 has the highest revenue among all.</figcaption>
</figure>

<figure class="align-center">
    <a href="/assets/images/output_7_0.png"><img src="/assets/images/output_7_0.png"></a>
    <figcaption>Fig. 3) The capital region, Seoul + Gyeonggi + Incheon, takes up around 40% of the whole fried chicken stores</figcaption>
</figure>


We can see that around 40 percent of fried chicken stores are located near the capital region. But that's a bit *off*. The capital region is where around 50 percent of the whole population live in South Korea. As we can see from the table below, it lacks significant portion of fried chicken stores in Seoul. While there are around 20% of population of South Korea living in Seoul, only 10% of whole fried chicken stores are located in Seoul.

|Admin|% Population |% Stores |
| --- |     ---     |   ---   |
|Seoul|    ~20%     |   ~11%  |
|Gyeonggi| ~24%     |   ~24%  |
|Incheon|  ~6%      |   ~5%   |
|**Sum**|    ~50%     |   ~40%  |
{: .text-right}

There are 3 hypothesis I suggest to explain this weird distribution of fried chicken stores. 

1. Rental price is too high in Seoul causing bloated expenses.
   * Seoul is known to have super high rental place.
  
2. Top brands siphon a lot of orders
   * Kyochon Chicken, for example, is known to have royal customers. It might be possible for other top brands as well to have such royal customers driving relatively unknown and other local fried chicken stores out of Seoul. With the data given, robust investigation is hard but we can see the distribution of top brands in Seoul compared to other states.

3. Much more selections of quick foods such as Pizza, Hamburgers, etc, lead to higher competition for fried chicken stores in Seoul.

In order to validate the hypothesis one and three, we need other dataset. So we will just check the second hypothesis.

<figure class="align-center">
    <a href="/assets/images/output_11_0.png"><img src="/assets/images/output_11_0.png"></a>
    <figcaption>Fig. 4) Note that the top brands ratio doesn't differ significantly in the capital region. But but we can definitely see that there is bigger ratio of top brands in Gyeongsang-namdo.</figcaption>
</figure>

The graph above shows the opposite sign of our hypothesis. Based on the second hypothesis, if it is true, there should be bigger top brands ratio in the capital region. Let's see how other provinces show top brands ratio.

<figure class="align-center">
    <a href="/assets/images/output_13_0.png"><img src="/assets/images/output_13_0.png"></a>
    <figcaption>Fig. 5) Most of the capital regions, Seoul and Gyeonggi-do are part of least ratio of top brands among all the provinces.</figcaption>
</figure>

So we can say that the second hypothesis, top brands siphon lots of orders in Seoul, is not likely hold the truth. We need other dataset in order to say anything about the other hypotheses, so we will stop now for the moment. For the side, I made a small visualization tool for the distribution of chicken stores in Korea using ipywidget and ipyleaflet as you can see from the gif below.

<figure class="align-center">
    <a href="https://github.com/yoonoh930/Chicken_Stores_Extracter/blob/master/Data%20Exploration.ipynb"><img src="/assets/images/leaflet_jupyter.gif"></a>
    <figcaption>You can find it in my data exploration notebook. Click the picture and you will be directed to it.</figcaption>
</figure>

On the next post, I will download other fast food stores as well as restaurant data in order to check the competition in the capital region compared to other provinces. See you soon :)
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

3. 

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
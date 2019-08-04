---
title: "barplot_base"
author: "Heum"
Start Date: "2019년 7년 31일"
html_document: default
---


> ebuil YouTube(https://www.youtube.com/channel/UCJ49UIzNXAaxZdDNYFxNhsA/featured) study

***
-- 2019. 7. 31. 

***

  - 일변량 질적 자료 분석

### [ base::barplot() ] 
#### https://youtu.be/5NcNe4CXInY



```r
library(tidyverse)
```

```r
head(diamonds, 3)
```

```
## # A tibble: 3 x 10
##   carat cut     color clarity depth table price     x     y     z
##   <dbl> <ord>   <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
## 1  0.23 Ideal   E     SI2      61.5    55   326  3.95  3.98  2.43
## 2  0.21 Premium E     SI1      59.8    61   326  3.89  3.84  2.31
## 3  0.23 Good    E     VS1      56.9    65   327  4.05  4.07  2.31
```

```r
table(diamonds$cut)
```

```
## 
##      Fair      Good Very Good   Premium     Ideal 
##      1610      4906     12082     13791     21551
```


```r
barplot(table(diamonds$cut))  # 빈도 확인 
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png)

  - 내림차순 sort/decreasing

```r
barplot(sort(table(diamonds$cut), decreasing = T))
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)
  
### barplot() arguments
  
    - col   = "color"         막대의 색깔
    - main  = "title"         차트 제목
    - ylab  = "y axis name"   y축 라벨
    - xlab  = "x axis name"   x축 라벨 
    - ylim  = c(min, max)     y축의 범위
    - xlim  = c(min, max)     x축의 범위 
    - horiz = TRUE            축 방향 설정 


```r
barplot(sort(table(diamonds$cut), decreasing = T), 
        col = "purple", 
        main = "Cut of Diamonds", 
        ylab = "Frequency", 
        xlab = "cut", 
        ylim = c(0, 25000))
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7-1.png)

  - RColorBrewer 를 이용한 다양한 색깔이용

```r
library(RColorBrewer)
display.brewer.all(type = "seq")
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8-1.png)



```r
color.palette <- RColorBrewer::brewer.pal(n = 5, name = "Blues")

barplot(sort(table(diamonds$cut), decreasing = T), 
        col  = sort(color.palette, decreasing = F), 
        main = "Cut of Diamonds", 
        ylab = "Frequency", 
        xlab = "cut", 
        ylim = c(0, 25000))
```

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9-1.png)
  
  - horiz = TRUE  막대의 방향 변경

```r
barplot(sort(table(diamonds$cut), decreasing = F), 
        col   = sort(color.palette, decreasing = T),
        main  = "Cut of Diamonds", 
        ylab  = "Frequency", 
        xlab  = "cut", 
        xlim  = c(0, 25000),       # horiz에 맞추어 변경 
        horiz = TRUE)
```

![plot of chunk unnamed-chunk-10](figure/unnamed-chunk-10-1.png)
  
  
### [ ggplot::geom_bar() ] 
#### https://youtu.be/EubwjZfH3lU

### geom_bar() arguments
  
    - fill  = "color"         막대의 색깔

 - 막대의 색깔지정 방법(1)
 

```r
ggplot(data = diamonds, mapping = aes(x = cut)) +
  geom_bar(fill = RColorBrewer::brewer.pal(n = 5, name = "Blues"))
```

![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11-1.png)
    
 - 막대의 색깔지정 방법(2): 범주에 따른 색깔 
 

```r
ggplot(data = diamonds, mapping = aes(x = cut, fill = cut)) +
  geom_bar()
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-1.png)

 - ggplot의 그래프 (레이어) 추가 설정

```r
ggplot(data = diamonds, mapping = aes(x = cut, fill = cut)) +
  geom_bar() +
  theme_classic() +
  labs(title = "Cut of Diamonds", 
       x     = "Cut", 
       y     = "Frequency")+
  theme(plot.title = element_text(size = 20, color = "red", face = "bold"), 
        axis.title.x = element_text(size = 15, color = "blue", face = "italic"), 
        axis.title.y = element_text(size = 15, color = "purple", face = "bold.italic", angle = 270))
```

![plot of chunk unnamed-chunk-13](figure/unnamed-chunk-13-1.png)


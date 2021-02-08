# APM466
---
title: "APM466-A1"
author: "Yating Song"
output:
  pdf_document: default
  latex_engine: xelatex
  html_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


```{r, include=FALSE}
options(tinytex.verbose = TRUE)
```


**Answers**

*Fundamental Questions*

1.

  (a)
  If government simply prints money it will cause an inflation which will devalue the money already in the money market, so borrow money by issuing bonds can make the burden falls more evenly.
  
  (b)
  When people have some worries about the future macroeconomic outlook the long-term part of a yield curve might flatten, it is also because usually the short-term interest rate increasing/decreasing more than a long-term interest rate.

  (c)
  Quantitative Easing is a monetary policy that the central bank buys securities from the market to make the money supply increased and to encourage people to invest so that the economy can be stimulated, so the (US) Fed used this policy for the COVID-19  pandemic period that the Fed bought a massive amount of long-term treasury and mortgage-backed securities which increased the securities portfolio holding by Fed from $3.9 trillion to $6.6 trillion.

2.

  I chose:CAN 1.75 May 01, CAN 1.25 Nov 01, CAN 1.5 May 01, CAN 0.25 Nov 01, CAN 1.75 Mar 01, CAN 1.5 Jun 01, CAN 0.25 Apr 01, CAN 1.5 Sep 01, CAN 1.25 Mar 01, CAN 0.5 Sep 01, CAN 0.25 Mar 01
  I chose these bonds by looking at the time period between each bond's next coupon payment data and its mature data, like 6 months, 12 months, and so on. It made the time period appropriate to use semi-annual discrete compounding.Specifically, I chose lots of bonds whose maturity dates were in March and September for each year. All the issue dates are within 4 years, and the coupon rates are relatively close. I also considered the price, I make the price of chose bonds around $100 and ignored some bonds that had a price like $138. 
  
3.

  In a Principal Component Analysis, we need to change the basis of our data from the original axes (for example, x and y axes) to the basis represented by the principal components, also known as eigenvectors, which we computed.
  Along with the data, the eigenvalue is a value  we derivedthat shows how much of the variance of a vector can be explained by the principal components (eigenvectors).
  The eigenvectors associated with the covariance matrix are used as the new basis because all the eigenvectors are orthogonal to each other. This covariance matrix tells us if variables are correlated by providing an estimated number entry in the matrix.
  
*Empirical Questions*

1.

 (a)
 
```{r}
library(jrvFinance)

date_purchase <- c("2021-01-18", "2021-01-19", "2021-01-20", "2021-01-21", "2021-01-22", "2021-01-25", "2021-01-26","2021-01-27", "2021-01-28","2021-01-29")

date_mature <- c("2021-05-01","2021-11-01", "2022-05-01","2022-11-01", "2023-03-01", "2023-06-01", "2024-04-01", "2024-09-01", "2025-03-01", "2025-09-01", "2026-03-01")

couponnn <- c(0.0175, 0.0125, 0.015, 0.0025, 0.0175, 0.015, 0.0025, 0.015, 0.0125, 0.005, 0.0025)

CAN_1.75_May_01_p <- c(100.48, 100.47, 100.46, 100.45, 100.44, 100.44, 100.43, 100.43, 100.42, 100.41)
CAN_1.25_Nov_01_p <- c(100.904, 100.894, 100.874, 100.864, 100.863, 100.849, 100.849, 100.857, 100.848, 100.846)
CAN_1.5_May_01_p <-c(101.78, 101.77, 101.74, 101.73, 101.73, 101.7, 101.7, 101.72, 101.71, 101.71)
CAN_0.25_Nov_01_p<-c(100.17, 100.17, 100.13, 100.13, 100.14, 100.12, 100.12, 100.14, 100.14, 100.15)
CAN_1.75_Mar_01_p<-c(103.29, 103.29, 103.25, 103.24, 103.25, 103.22, 103.22, 103.25, 103.26, 103.24)
CAN_1.5_Jun_01_p<-c(103.13, 103.14, 103.1, 103.09, 103.09, 103.04, 103.06, 103.1, 103.08, 103.06)
CAN_0.25_Apr_01_p<-c(99.91, 99.95, 99.92, 99.9, 99.92, 99.91, 99.92, 99.99, 99.93, 99.96)
CAN_1.5_Sep_01_p<-c(104.27, 104.28, 104.25, 104.19, 104.24, 104.29, 104.26, 104.32, 104.24, 104.24)
CAN_1.25_Mar_01_p<-c(103.6, 103.6, 103.59, 103.51, 103.54, 103.62, 103.59, 103.66, 103.61, 103.57)
CAN_0.5_Sep_01_p<-c(100.33, 100.32, 100.3, 100.22, 100.27, 100.37, 100.33, 100.42, 100.35, 100.33)
CAN_0.25_Mar_01_p<-c(98.78, 98.77, 98.76, 98.66, 98.71, 98.84, 98.83, 98.93, 98.86, 98.81)


num <- c(1,2,3,4,5,6,7,8,9,10)

Known_YTM <- c(0.0008,  0.0013, 0.0013, 0.0017, 0.0018, 0.0018, 0.0027, 0.0031, 0.0036, 0.0042, 0.0048)
```



```{r}
CAN_1.75_May_01_YTM<- c( )
for (i in num){
  CAN_1.75_May_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.75_May_01_p[i])
} 


CAN_1.25_Nov_01_YTM<- c( )
for (i in num){
  CAN_1.25_Nov_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.25_Nov_01_p[i])
} 

CAN_1.5_May_01_YTM<- c( )
for (i in num){
  CAN_1.5_May_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.5_May_01_p[i])
} 

CAN_0.25_Nov_01_YTM<- c( )
for (i in num){
  CAN_0.25_Nov_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_0.25_Nov_01_p[i])
} 

CAN_1.75_Mar_01_YTM<- c( )
for (i in num){
  CAN_1.75_Mar_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.75_Mar_01_p[i])
} 

CAN_1.5_Jun_01_YTM<- c( )
for (i in num){
  CAN_1.5_Jun_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.5_Jun_01_p[i])
} 

CAN_0.25_Apr_01_YTM<- c( )
for (i in num){
  CAN_0.25_Apr_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_0.25_Apr_01_p[i])
} 

CAN_1.5_Sep_01_YTM<- c( )
for (i in num){
  CAN_1.5_Sep_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.5_Sep_01_p[i])
} 

CAN_1.25_Mar_01_YTM<- c( )
for (i in num){
  CAN_1.25_Mar_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_1.25_Mar_01_p[i])
}

CAN_0.5_Sep_01_YTM<- c( )
for (i in num){
  CAN_0.5_Sep_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_0.5_Sep_01_p[i])
} 

CAN_0.25_Mar_01_YTM<- c( )
for (i in num){
  CAN_0.25_Mar_01_YTM[i] = bond.yield(settle= date_purchase[i], mature= date_mature[i], coupon=couponnn[i],
           price=CAN_0.25_Mar_01_p[i])
} 

print(CAN_1.75_May_01_YTM)
print(CAN_1.25_Nov_01_YTM)
print(CAN_1.5_May_01_YTM)
print(CAN_0.25_Nov_01_YTM)
print(CAN_1.75_Mar_01_YTM)
print(CAN_1.5_Jun_01_YTM)
print(CAN_0.25_Apr_01_YTM)
print(CAN_1.5_Sep_01_YTM)
print(CAN_1.25_Mar_01_YTM)
print(CAN_0.5_Sep_01_YTM)
print(CAN_0.25_Mar_01_YTM)
```
```{r}
ytm0 <- CAN_1.75_May_01_YTM
ytm0.5 <- (0.5-0.25)/(0.75-0.25)*
  (CAN_1.25_Nov_01_YTM - CAN_1.75_May_01_YTM) + CAN_1.75_May_01_YTM
ytm1 <- (1-0.75)/(1.25-0.75)*
  (CAN_1.5_May_01_YTM - CAN_1.25_Nov_01_YTM) + CAN_1.25_Nov_01_YTM
ytm1.5<- (1.5-1.25)/(1.583-1.25)*
  (CAN_0.25_Nov_01_YTM - CAN_1.5_May_01_YTM) + CAN_1.5_May_01_YTM
ytm2 <- (2-1.583)/(2.083-1.583) *
  (CAN_1.75_Mar_01_YTM - CAN_0.25_Nov_01_YTM) +CAN_0.25_Nov_01_YTM
ytm2.5 <- (2.5-2.333)/(3.167-2.333) * 
  (CAN_0.25_Apr_01_YTM-CAN_1.5_Jun_01_YTM) + CAN_1.5_Jun_01_YTM

ytm3 <- (3-2.333)/(3.167-2.333) * 
  (CAN_0.25_Apr_01_YTM-CAN_1.5_Jun_01_YTM) + CAN_1.5_Jun_01_YTM

ytm3.5 <- (3.5-3.167)/(3.583 - 3.167) *
  (CAN_1.5_Sep_01_YTM - CAN_0.25_Apr_01_YTM) +CAN_0.25_Apr_01_YTM
ytm4 <- (4-3.583)/(4.083-3.583) *
  (CAN_1.25_Mar_01_YTM-CAN_1.5_Sep_01_YTM) +CAN_1.5_Sep_01_YTM
ytm4.5 <- (4.5-4.083)/(4.583-4.083) *
  (CAN_0.5_Sep_01_YTM - CAN_1.25_Mar_01_YTM) +CAN_1.25_Mar_01_YTM
ytm5 <- (5-4.583)/(5.083-4.583) *
  (CAN_0.25_Mar_01_YTM- CAN_0.5_Sep_01_YTM)+CAN_0.5_Sep_01_YTM

```

```{r}
date_purchase <- c("18", "19", "20", "21", "22", "25", "26","27", "28","29")
day_num <- c(0, 0.5,1, 1.5,2,2.5,3,3.5,4, 4.5)

plot(day_num, xaxt = "n", ytm0, xlab='Settlement Date', ylab= "YTM Curve", type="o", col="blue", pch="o", lty=1, ylim=c(-0.3,0.05) )

 points(day_num, ytm0.5, col="red", pch="o")
 lines(day_num, ytm0.5, col="red",lty=1)
 
 points(day_num, ytm1, col="blueviolet", pch="o")
 lines(day_num, ytm1, col="blueviolet",lty=1)
 
  points(day_num, ytm1.5, col="orange", pch="o")
 lines(day_num,ytm1.5, col="orange",lty=1)

  points(day_num, ytm2, col="cyan", pch="o")
 lines(day_num,ytm2, col="cyan",lty=1)

 points(day_num, ytm2.5, col="coral", pch="o")
 lines(day_num, ytm2.5, col="coral",lty=1)
 
 points(day_num, ytm3, col="green", pch="o")
 lines(day_num, ytm3, col="green",lty=1)
 
  points(day_num, ytm3.5, col="gray", pch="o")
 lines(day_num, ytm3.5, col="gray",lty=1)
 
   points(day_num,  ytm4, col="darkorange", pch="o")
 lines(day_num,  ytm4, col="darkorange",lty=1)
 
  points(day_num,  ytm4.5, col="pink", pch="o")
 lines(day_num,  ytm4.5, col="pink",lty=1)
 
   points(day_num,  ytm5, col="chocolate", pch="o")
 lines(day_num, ytm5, col="chocolate",lty=1)
 
legend("bottomright",legend=c("ytm3", "ytm3.5",
                              "ytm4", " ytm4.5","ytm5"),
       col=c("green", "gray", "darkorange", "pink", "chocolate" ),
       lty=c(1,1,1), ncol=1)
legend("bottomleft",legend=c("ytm0","ytm0.5",
                              "ytm1","ytm1.5","ytm2",
                              "ytm2.5"),
       col=c("blue","red","blueviolet","orange", "cyan", "coral" ),
       lty=c(1,1,1), ncol=1)
axis(1, day_num, labels= date_purchase[1:10])
```
```{r}
date_purchase <- c("18", "19", "20", "21", "22", "25", "26","27", "28","29")
day_num <- c(0, 0.5,1, 1.5,2,2.5,3,3.5,4, 4.5)

plot(day_num, xaxt = "n", ytm0, xlab='Settlement Date', ylab= "YTM Curve", type="o", col="blue", pch="o", lty=1, ylim=c(-0.3,0.05) )

 points(day_num, ytm0.5, col="red", pch="o")
 lines(day_num, ytm0.5, col="red",lty=1)
 
 points(day_num, ytm1, col="blueviolet", pch="o")
 lines(day_num, ytm1, col="blueviolet",lty=1)
 
  points(day_num, ytm1.5, col="orange", pch="o")
 lines(day_num,ytm1.5, col="orange",lty=1)

  points(day_num, ytm2, col="cyan", pch="o")
 lines(day_num,ytm2, col="cyan",lty=1)

 points(day_num, ytm2.5, col="coral", pch="o")
 lines(day_num, ytm2.5, col="coral",lty=1)
 
 points(day_num, ytm3, col="green", pch="o")
 lines(day_num, ytm3, col="green",lty=1)
 
  points(day_num, ytm3.5, col="gray", pch="o")
 lines(day_num, ytm3.5, col="gray",lty=1)
 
   points(day_num,  ytm4, col="darkorange", pch="o")
 lines(day_num,  ytm4, col="darkorange",lty=1)
 
  points(day_num,  ytm4.5, col="pink", pch="o")
 lines(day_num,  ytm4.5, col="pink",lty=1)
 
   points(day_num,  ytm5, col="chocolate", pch="o")
 lines(day_num, ytm5, col="chocolate",lty=1)
 
legend("bottomright",legend=c("ytm3", "ytm3.5",
                              "ytm4", " ytm4.5","ytm5"),
       col=c("green", "gray", "darkorange", "pink", "chocolate" ),
       lty=c(1,1,1), ncol=1)
legend("bottomleft",legend=c("ytm0","ytm0.5",
                              "ytm1","ytm1.5","ytm2",
                              "ytm2.5"),
       col=c("blue","red","blueviolet","orange", "cyan", "coral" ),
       lty=c(1,1,1), ncol=1)
axis(1, day_num, labels= date_purchase[1:10])
```
```

```{r}
ytm_cal <- c(mean(CAN_1.75_May_01_YTM),mean(CAN_1.25_Nov_01_YTM)
,mean(CAN_1.5_May_01_YTM)
,mean(CAN_0.25_Nov_01_YTM)
,mean(CAN_1.75_Mar_01_YTM)
,mean(CAN_1.5_Jun_01_YTM)
,mean(CAN_0.25_Apr_01_YTM)
,mean(CAN_1.5_Sep_01_YTM)
,mean(CAN_1.25_Mar_01_YTM)
,mean(CAN_0.5_Sep_01_YTM)
,mean(CAN_0.25_Mar_01_YTM))

diff<- Known_YTM - ytm_cal
print(diff)
```

As the graph shown above, I used a function to calculate all the YTM values for each bond and used the interpolation method to get the 0~5 years YTM with semi-annual compounding rate. The graph was drawn by R. The x-axis ""day num" representing the number of day since Jan.18 2021, the first day we started to collect our data, to Jan.29."ytm #" representing the specific bond whose yield to maturity is # years. Comparing with the YTM values that we have collected from the website, as a cross-reference, there were only small differences we have (please see reference code for detail).


 (b)
 
 In order to calculate the spot rate, we first need to calculate the dirty price, which leads to the calculation of accrued interest rate, use R to get it. As we have dirty price of the bond, we can start to calculate the spot rates by bootstrapping. In the cash flow valuation formula:
         $P=p_1(1+r(t_1)/n)^{nt_1} + p_2(1+r(t_2)/n)^{nt_2}$
         
  P is the dirty price, $p_i$ is the payment from the bond being expressed, and $r(t_1)$ is the spot rate from last period. Since we start from a zero coupon bond mature less than 6 months, spot rate to begin with is just the YTM rate for that bond. The only variable we do not know is the $r(t_2)$, which is the spot rate.

```{r}


a1 <- bond.TCF("2021-02-01", mature= date_mature[1], coupon=couponnn[1], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a2 <- bond.TCF("2021-02-01", mature= date_mature[2], coupon=couponnn[2], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a3 <- bond.TCF("2021-02-01", mature= date_mature[3], coupon=couponnn[3], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a4 <- bond.TCF("2021-02-01", mature= date_mature[4], coupon=couponnn[4], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a5 <- bond.TCF("2021-02-01", mature= date_mature[5], coupon=couponnn[5], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a6 <- bond.TCF("2021-02-01", mature= date_mature[6], coupon=couponnn[6], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a7 <- bond.TCF("2021-02-01", mature= date_mature[7], coupon=couponnn[7], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a8 <- bond.TCF("2021-02-01", mature= date_mature[8], coupon=couponnn[8], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a9 <- bond.TCF("2021-02-01", mature= date_mature[9], coupon=couponnn[9], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a10 <- bond.TCF("2021-02-01", mature= date_mature[10], coupon=couponnn[10], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)
a11 <- bond.TCF("2021-02-01", mature= date_mature[11], coupon=couponnn[11], freq = 2, convention = c("30/360",
  "ACT/ACT", "ACT/360", "30/360E"), redemption_value = 100)

a1[3]
a2[3]
a3[3]
a4[3]
a5[3]
a6[3]
a7[3]
a7[3]
a9[3]
a10[3]
a11[3]
```
```{r}
Accrued_interest <-c(0.4375,0.3125, 0.375, 0.0625, 0.7291667, 
                     0.25, 0.08333333, 0.08333333, 0.5208333, 0.2083333,0.1041667
)

dp1 <- Accrued_interest[1]+ CAN_1.75_May_01_p
dp2 <- Accrued_interest[2]+ CAN_1.25_Nov_01_p
dp3 <- Accrued_interest[3]+ CAN_1.5_May_01_p
dp4 <- Accrued_interest[4]+ CAN_0.25_Nov_01_p
dp5 <- Accrued_interest[5]+ CAN_1.75_Mar_01_p
dp6 <- Accrued_interest[6]+ CAN_1.5_Jun_01_p
dp7 <- Accrued_interest[7]+ CAN_0.25_Apr_01_p
dp8 <- Accrued_interest[8]+ CAN_1.5_Sep_01_p
dp9 <- Accrued_interest[9]+ CAN_1.25_Mar_01_p
dp10 <- Accrued_interest[10]+ CAN_0.5_Sep_01_p
dp11 <- Accrued_interest[11]+ CAN_0.25_Mar_01_p
```

Spot Rate


  
```{r}
cp1 =  100*0.0175
cp2 = 100*0.0125

#assume 
spt0 <- c(0,0,0,0,0,0,0,0,0,0)
nu <- c(1,2,3,4,5,6,7,8,9,10)
```

```{r}
spot_rate1<-c()
spr1 <- c()
for (k in nu) {
  spr1[k] <- (( (dp1[k]-cp1*(1+spt0[k]/2)^(2*0.25))/(cp2+100) )^(1/2*0.75) -1)*2
  spot_rate1 <- append(spot_rate1, spr1[k])
}

print(spot_rate1)
```

```{r}
cp3 = 100* 0.015  
spot_rate2<-c()
spr2 <- c()
for (k in nu) {
  spr2[k] <- (( (dp2[k]-cp2*(1+spot_rate1[k]/2)^(2*0.25))/(cp3+100))^(1/2*0.75) -1)*2
  spot_rate2 <- append(spot_rate2, spr2[k])
}

print(spot_rate2)
```
```{r}
cp4 = 100* couponnn[4]  
spot_rate3<-c()
spr3 <- c()
for (k in nu) {
  spr3[k] <- (( (dp3[k]-cp3*(1+spot_rate2[k]/2)^(2*0.25))/(cp4+100))^(1/2*0.75) -1)*2
  spot_rate3 <- append(spot_rate3, spr3[k])
}

print(spot_rate3)
```
```{r}
cp5 = 100* couponnn[5]  
spot_rate4<-c()
spr4 <- c()
for (k in nu) {
  spr4[k] <- (( (dp4[k]-cp4*(1+spot_rate3[k]/2)^(2*0.25))/(cp5+100))^(1/2*0.75) -1)*2
  spot_rate4 <- append(spot_rate4, spr4[k])
}

print(spot_rate4)
```
```{r}
cp6 = 100* couponnn[6]  
spot_rate5<-c()
spr5 <- c()
for (k in nu) {
  spr5[k] <- (( (dp5[k]-cp5*(1+spot_rate4[k]/2)^(2*0.25))/(cp5+100))^(1/2*0.75) -1)*2
  spot_rate5 <- append(spot_rate5, spr5[k])
}

print(spot_rate5)
```
```{r}
cp7 = 100* couponnn[7]  
spot_rate6<-c()
spr6 <- c()
for (k in nu) {
  spr6[k] <- (( (dp6[k]-cp6*(1+spot_rate5[k]/2)^(2*0.25))/(cp6+100))^(1/2*0.75) -1)*2
  spot_rate6 <- append(spot_rate6, spr6[k])
}

print(spot_rate6)
```

```{r}
cp8 = 100* couponnn[8]  
spot_rate7<-c()
spr7 <- c()
for (k in nu) {
  spr7[k] <- (( (dp7[k]-cp7*(1+spot_rate6[k]/2)^(2*0.25))/(cp7+100))^(1/2*0.75) -1)*2
  spot_rate7 <- append(spot_rate7, spr7[k])
}

print(spot_rate7)
```

```{r}
cp9 = 100* couponnn[9]  
spot_rate8<-c()
spr8 <- c()
for (k in nu) {
  spr8[k] <- (( (dp8[k]-cp8*(1+spot_rate7[k]/2)^(2*0.25))/(cp8+100))^(1/2*0.75) -1)*2
  spot_rate8 <- append(spot_rate8, spr8[k])
}

print(spot_rate8)
```
```{r}
cp10 = 100* couponnn[10]  
spot_rate9<-c()
spr9 <- c()
for (k in nu) {
  spr9[k] <- (( (dp9[k]-cp9*(1+spot_rate8[k]/2)^(2*0.25))/(cp9+100))^(1/2*0.75) -1)*2
  spot_rate9 <- append(spot_rate9, spr9[k])
}

print(spot_rate9)
```
```{r}
cp11 = 100* couponnn[11]  
spot_rate10<-c()
spr10 <- c()
for (k in nu) {
  spr10[k] <- (( (dp10[k]-cp10*(1+spot_rate9[k]/2)^(2*0.25))/(cp10+100))^(1/2*0.75) -1)*2
  spot_rate10 <- append(spot_rate10, spr10[k])
}

print(spot_rate10)
```

Spot Rate after interpolation
```{r}
spt0 <- c(0,0,0,0,0,0,0,0,0,0)
spot_rate1 <- (0.5-0.25)/(0.75-0.25)*
  (spr1 - spt0) + spt0
spot_rate2 <- (1-0.75)/(1.25-0.75)*
  (spr2 - spr1) + spr1
spot_rate3<- (1.5-1.25)/(1.583-1.25)*
  (spr3 - spr2) + spr2
spot_rate4 <- (2-1.583)/(2.083-1.583) *
  (spr4 - spr3) +spr3
spot_rate5<- (2.5-2.333)/(3.167-2.333) * 
  (spr5-spr4) + spr4
spot_rate6<- (3-2.333)/(3.167-2.333) * 
  (spr6-spr5) + spr5
spot_rate7<- (3.5-3.167)/(3.583 - 3.167) *
  (spr7 - spr6) +spr6
spot_rate8 <- (4-3.583)/(4.083-3.583) *
  (spr8- spr7) + spr7
spot_rate9 <- (4.5-4.083)/(4.583-4.083) *
  (spr9 - spr8) +spr8

```


```{r}
date_purchase <- c("18", "19", "20", "21", "22", "25", "26","27", "28","29")
day_num <- c(0, 0.5,1, 1.5,2,2.5,3,3.5,4, 4.5)

plot(day_num, xaxt = "n", spot_rate1, ylab= "Spot Rate", xlab='Settlement Date', type="o", col="blue", pch="o", lty=1, ylim=c(-0.05,0.012) )

 points(day_num, spot_rate2, col="red", pch="o")
 lines(day_num, spot_rate2, col="red",lty=1)
 
 points(day_num, spot_rate3, col="blueviolet", pch="o")
 lines(day_num, spot_rate3, col="blueviolet",lty=1)
 
  points(day_num, spot_rate4, col="orange", pch="o")
 lines(day_num,spot_rate4, col="orange",lty=1)

  points(day_num, spot_rate5, col="cyan", pch="o")
 lines(day_num,spot_rate5, col="cyan",lty=1)

 points(day_num, spot_rate6, col="coral", pch="o")
 lines(day_num, spot_rate6, col="coral",lty=1)
 
 points(day_num, spot_rate7, col="green", pch="o")
 lines(day_num, spot_rate7, col="green",lty=1)
 
  points(day_num, spot_rate8, col="gray", pch="o")
 lines(day_num, spot_rate8, col="gray",lty=1)
 
   points(day_num,  spot_rate9, col="darkorange", pch="o")
 lines(day_num,  spot_rate9, col="darkorange",lty=1)
 
  points(day_num,  spot_rate10, col="pink", pch="o")
 lines(day_num,  spot_rate10, col="pink",lty=1)
 
 
legend("bottomright",legend=c("spot_rate_3.5yr", "spot_rate_4yr",
                              "spot_rate_4.5yr", " spot_rate_5yr"),
       col=c("green", "gray", "darkorange", "pink" ),
       lty=c(1,1,1), ncol=1)
legend("bottomleft",legend=c("spot_rate_0.5yr","spot_rate_1yr",
                              "spot_rate_1.5yr","spot_rate_2yr","spot_rate_2.5yr",
                              "spot_rate_3yr"),
       col=c("blue","red","blueviolet","orange", "cyan", "coral" ),
       lty=c(1,1,1), ncol=1)
axis(1, day_num, labels= date_purchase[1:10])
```
Forward Rate from 2-5 years
```{r}
f21 <- (1+spot_rate4)
```


```{r}
forward_rate11<-(((1+spot_rate4/2)^2)/(1+spot_rate2/2)^1-1)*2
forward_rate12<-(((1+spot_rate6/2)^3)/(1+spot_rate4/2)^2-1)*2
forward_rate13<-(((1+spot_rate8/2)^4)/(1+spot_rate6/2)^3-1)*2
forward_rate14<-(((1+spot_rate10/2)^5)/(1+spot_rate8/2)^4-1)*2

```

forward_rate11<-(((1+spot_rate4/2)^2)
                /(1+spot_rate2/2)^1-1)*2
forward_rate12<-(((1+spot_rate6/2)^3)
                /(1+spot_rate4/2)^2-1)*2
forward_rate13<-(((1+spot_rate8/2)^4)
                /(1+spot_rate6/2)^3-1)*2
forward_rate14<-(((1+spot_rate10/2)^5)\
                /(1+spot_rate8/2)^4-1)*2

```{r}
date_purchase <- c("18", "19", "20", "21", "22", "25", "26","27", "28","29")
day_num <- c(0, 0.5,1, 1.5,2,2.5,3,3.5,4, 4.5)

plot(day_num, xaxt = "n", forward_rate11, ylab= "Forward Rate", xlab='Settlement Date', type="o", col="blue", pch="o", lty=1, ylim=c(-0.1,0.06) )

 points(day_num, forward_rate12, col="green", pch="o")
 lines(day_num, forward_rate12, col="green",lty=1)
 
 points(day_num, forward_rate13, col="gray", pch="o")
 lines(day_num, forward_rate13, col="gray",lty=1)
 
 points(day_num, forward_rate14, col="red", pch="o")
 lines(day_num, forward_rate14, col="red",lty=1)

legend("bottomleft",legend=c("forward_rate 1yr_1yr","forward_rate 1yr_2yr"),
       col=c("blue", "green"),
       lty=c(1,1,1), ncol=1)

legend("bottomright",legend=c("forward_rate_1yr_3yr","forward_rate_1yr_4yr"),
       col=c("gray", "red"),
       lty=c(1,1,1), ncol=1)
axis(1, day_num, labels= date_purchase[1:10])
```
The forward rate was calculated from the formula $(1+Y_{1n}/2) = (1+S_n/2)^n/(1+S_1/2)^{n-1}$ so we can derive $Y_{1n} = ([(1+S_n/2)^n/(1+S_1/2)^{n-1}]-1)*2$. In this formula, $Y_{1n}$ means one year rate n years from now.

Q5
```{r}
#spot rate
spot_rate2
spot_rate4
spot_rate6
spot_rate8
spot_rate10

a<-log(spot_rate2[2]/spot_rate2[1])
b<-log(spot_rate2[3]/spot_rate2[2])
c<-log(spot_rate2[4]/spot_rate2[3])
d<-log(spot_rate2[5]/spot_rate2[4])
e<-log(spot_rate2[6]/spot_rate2[5])
f<-log(spot_rate2[7]/spot_rate2[6])
g<-log(spot_rate2[8]/spot_rate2[7])
h<-log(spot_rate2[9]/spot_rate2[8])
i<-log(spot_rate2[10]/spot_rate2[9])
x_1<-c(a,b,c,d,e,f,g,h,i)
print(X_1)

a<-log(spot_rate4[2]/spot_rate4[1])
b<-log(spot_rate4[3]/spot_rate4[2])
c<-log(spot_rate4[4]/spot_rate4[3])
d<-log(spot_rate4[5]/spot_rate4[4])
e<-log(spot_rate4[6]/spot_rate4[5])
f<-log(spot_rate4[7]/spot_rate4[6])
g<-log(spot_rate4[8]/spot_rate4[7])
h<-log(spot_rate4[9]/spot_rate4[8])
i<-log(spot_rate4[10]/spot_rate4[9])
X_2<-c(a,b,c,d,e,f,g,h,i)
print(X_2)

a<-log(spot_rate6[2]/spot_rate6[1])
b<-log(spot_rate6[3]/spot_rate6[2])
c<-log(spot_rate6[4]/spot_rate6[3])
d<-log(spot_rate6[5]/spot_rate6[4])
e<-log(spot_rate6[6]/spot_rate6[5])
f<-log(spot_rate6[7]/spot_rate6[6])
g<-log(spot_rate6[8]/spot_rate6[7])
h<-log(spot_rate6[9]/spot_rate6[8])
i<-log(spot_rate6[10]/spot_rate6[9])
x_3<-c(a,b,c,d,e,f,g,h,i)
print(X_3)

a<-log(spot_rate8[2]/spot_rate8[1])
b<-log(spot_rate8[3]/spot_rate8[2])
c<-log(spot_rate8[4]/spot_rate8[3])
d<-log(spot_rate8[5]/spot_rate8[4])
e<-log(spot_rate8[6]/spot_rate8[5])
f<-log(spot_rate8[7]/spot_rate8[6])
g<-log(spot_rate8[8]/spot_rate8[7])
h<-log(spot_rate8[9]/spot_rate8[8])
i<-log(spot_rate8[10]/spot_rate8[9])
x_4<-c(a,b,c,d,e,f,g,h,i)
print(X_4)

a<-log(spot_rate10[2]/spot_rate10[1])
b<-log(spot_rate10[3]/spot_rate10[2])
c<-log(spot_rate10[4]/spot_rate10[3])
d<-log(spot_rate10[5]/spot_rate10[4])
e<-log(spot_rate10[6]/spot_rate10[5])
f<-log(spot_rate10[7]/spot_rate10[6])
g<-log(spot_rate10[8]/spot_rate10[7])
h<-log(spot_rate10[9]/spot_rate10[8])
i<-log(spot_rate10[10]/spot_rate10[9])
x_5<-c(a,b,c,d,e,f,g,h,i)
print(X_5)

```

```{r}
M1 <- cbind(x_1,X_2,x_3,x_4, x_5)
M1
spot_Cov <- cov(M1)
spot_Cov
```
for forward rate
```{r}
a<-log(forward_rate11[2]/forward_rate11[1])
b<-log(forward_rate11[3]/forward_rate11[2])
c<-log(forward_rate11[4]/forward_rate11[3])
d<-log(forward_rate11[5]/forward_rate11[4])
e<-log(forward_rate11[6]/forward_rate11[5])
f<-log(forward_rate11[7]/forward_rate11[6])
g<-log(forward_rate11[8]/forward_rate11[7])
h<-log(forward_rate11[9]/forward_rate11[8])
i<-log(forward_rate11[10]/forward_rate11[9])
xf_1<-c(a,b,c,d,e,f,g,h,i)
print(xf_1)

a<-log(forward_rate12[2]/forward_rate12[1])
b<-log(forward_rate12[3]/forward_rate12[2])
c<-log(forward_rate12[4]/forward_rate12[3])
d<-log(forward_rate12[5]/forward_rate12[4])
e<-log(forward_rate12[6]/forward_rate12[5])
f<-log(forward_rate12[7]/forward_rate12[6])
g<-log(forward_rate12[8]/forward_rate12[7])
h<-log(forward_rate12[9]/forward_rate12[8])
i<-log(forward_rate12[10]/forward_rate12[9])
xf_2<-c(a,b,c,d,e,f,g,h,i)
print(xf_2)

a<-log(forward_rate13[2]/forward_rate13[1])
b<-log(forward_rate13[3]/forward_rate13[2])
c<-log(forward_rate13[4]/forward_rate13[3])
d<-log(forward_rate13[5]/forward_rate13[4])
e<-log(forward_rate13[6]/forward_rate13[5])
f<-log(forward_rate13[7]/forward_rate13[6])
g<-log(forward_rate13[8]/forward_rate13[7])
h<-log(forward_rate13[9]/forward_rate13[8])
i<-log(forward_rate13[10]/forward_rate13[9])
xf_3<-c(a,b,c,d,e,f,g,h,i)
print(xf_3)

a<-log(forward_rate14[2]/forward_rate14[1])
b<-log(forward_rate14[3]/forward_rate14[2])
c<-log(forward_rate14[4]/forward_rate14[3])
d<-log(forward_rate14[5]/forward_rate14[4])
e<-log(forward_rate14[6]/forward_rate14[5])
f<-log(forward_rate14[7]/forward_rate14[6])
g<-log(forward_rate14[8]/forward_rate14[7])
h<-log(forward_rate14[9]/forward_rate14[8])
i<-log(forward_rate14[10]/forward_rate14[9])
xf_4<-c(a,b,c,d,e,f,g,h,i)
print(xf_4)
```


```{r}
M2 <- cbind(xf_1,xf_2,xf_3,xf_4)
M2
fwd_cov <- cov(M2)
fwd_cov
```




Q6
  
```{r}
eigen(spot_Cov)
eigen(fwd_cov)
```

**Reference(APA)**

https://www.investopedia.com/terms/f/flatyieldcurve.asp#:~:text=A%20flattening%20yield%20curve%20may,more%20than%20long%2Dterm%20rates.&text=Consequently%2C%20the%20slope%20of%20the,more%20than%20long%2Dterm%20rates.

https://www.brookings.edu/research/fed-response-to-covid19/



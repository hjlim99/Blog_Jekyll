> 출처
> * http://www.analyticsvidhya.com/blog/2015/02/data-exploration-preparation-model
> * http://www.analyticsvidhya.com/blog/2015/02/7-steps-data-exploration-preparation-building-model-part-2/


# 데이터 탐색 
Variable Identification - Univariate Analysis  - Bi-variate Analysis - Missing values treatment - Outlier treatment - Variable transformation - Variable creation

# Variable Identification : 변수 속성 분류
* Predictor (Input) & Target (output)  구분
* Data Type(Character or Numeric) 구분
* Categorical & Continuous 구분 

![](/assets/Picture1_1.png)

# Univariate Analysis : 변수별 분석 
* Continuous 변수일 경우 : Central tendency & Spread of the variable 파악 필요
![](/assets/Picture1-2.png)



* Categorical 변수일 경우 
    * Distribution of each category파악 필요  Frequency table 사용
    * 분류별 % 파악 필요  Bar Chart 활용

# Bi-variate Analysis : 변수간 분석(Association)
### 1. Categorical & Categorical 변수간 분석
* linear or non-linear 확인 - Scatter plot 활용
* strength of relationship - Pearson Correlation varies 
    * (-1 : negative Linear, +1 : Positive Linear, 0: No correlation)
![](/assets/Picture1-3.png)
### 2. Continuous & Continuous 변수간 분석
* Two-way table 방법 사용 : 두 변수가 Count / Count% 활용
![](/assets/Picture1-4.gif)
* Stacked Column Chart : Two-way table과 비슷, Visual 강조 
![](/assets/Picture1-5.gif)
* Chi-Square Test : statistical significance 분석 
    * (0 : Dependent, 1 : Independent, ~0.05 : 95%confidence)

### 3. Categorical & Continuous 변수간 분석
Box plot 활용
statistical significance - Z-test, T-test. ANOVA

# Missing values treatment

# Outlier treatment

# Variable transformation

# Variable creation

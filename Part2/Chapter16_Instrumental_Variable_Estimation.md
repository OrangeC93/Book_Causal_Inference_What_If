## 16.1 The three instrumental conditions
- Z is associated with A
- Z does not affect Y except through its potential effect on A
- Z and Y do not share causes

Example1: 

![image](/img/16_1.png)

Example2: 
- Uz is unmeasured causal instrument
- Z is the measured surrogate or proxy instrument
- Z and Y have Uz as a common cause does not violate condition(iii) since Uz is a caudal instrument
![image](/img/16_2.png)

Example3: 
- Z-A association arises from conditioning ona common effect S of the unmeasured causal instrument Uz and proxy instrument Z.
- Both causal and proxy instrument can be used for IV estimation

![image](/img/16_3.png)

Back to the example: the effect of smoking cessation on weight change
- There's no randomization indicator in an observational study
- Consider: the price of cigarettes, it can be argued if it can meet the three instumental conditions
- Propose an instrument Z that takes value 1 wthen the average price of a pack of cigarettes in the US states where the individual was bron was greater than $1.5 and takes 0 otherwise
  - We need to verify that the (1) proposed instrument Z and the treatment A are associated, <img src="https://render.githubusercontent.com/render/math?math=Pr[A=1|Z=1] - Pr[A=1|Z=0] =6%">, in this case, Z and A are wekly associated, Z is often referred as a weak instrument 

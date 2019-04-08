### Path Duration

the duration of an EQ signal at hypo-central distance can generally be represented as (according Atkinson and Boore 1995)

$T(R) = T{_0} + dR $

where $T{_0}$ is the source duration, and $d$ is the coefficient controlling the increase of duration with distance; $d$ is derived empirically. $d​$ may be a single coefficient describing all distances of interest (e.g., Atkinson, 1993b), or it can take different values **depending on the distance range**(e.g., Atkinson and Boore, 1995). **The empirical duration model of Atkinson and Boore (1995) was adopted for this study**. The duration increases in a hinged quad linear fashion from the source, mimicking the form of the attenuation model. 

| $T_0$ | $d$  | Atkinson and Boore, 1995 |
| ----- | :--: | :----------------------: |
| 0     |  0   |      $0{\leq}R<10$       |
| 0     | 0.16 |      1$0{\leq}R<70$      |
| 9.6   | 0.03 |     $70{\leq}R<130$      |
| 7.8   | 0.04 |       $130{\leq}R$       |

$T(R) = T{_0} + dR  =\left\{
\begin{aligned}
0 &&  0 \le R < 10 \\  0.16(R-10) && 10 < R \le 70 \\ 9.6-0.03(R-70) && 70 < R \le 130 \\ 7.8+0.04(R-130) && 130<R
\end{aligned}
\right.$

##### 参数文件中设置为

| rpathdur | pathdur |
| -------- | ------- |
| 4        |         |
| 0        | 0       |
| 10       | 0.16    |
| 70       | 9.6     |
| 130      | 7.8     |
| 0.04     |         |

```fortran
if ( subfaultDistance .le. rpathdur(1) ) then
        dur_path = pathdur(1)
else if ( subfaultDistance .ge. rpathdur(ndur_hinges) ) then
        dur_path = pathdur(ndur_hinges) + 
     :     (subfaultDistance - rpathdur(ndur_hinges))*durslope
     :              
else
     call locate(rpathdur, ndur_hinges, subfaultDistance, j)
        dur_path = pathdur(j) + 
     :     (subfaultDistance - rpathdur(j))*( pathdur(j+1)-pathdur(j))
     :              /(rpathdur(j+1)-rpathdur(j))
end if

```



### Geometric spreading

$R<70,GS = R{^{-1}}$

$70 \le R \lt 130, GS = 1/70$ 

$R \ge 130, GS = 1/70(130/R){^{0.5}}= 0.16(R){^{-0.5}} $  

| 1.0  | r_ref |
| ---- | ----- |
| 3    |       |
| 1    | -1    |
| 70   | 0     |
| 130  | -0.5  |




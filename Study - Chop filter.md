Study - Chop filter based on Chaikin's Volatility but faster with 0 lag.

![Chop filter image](https://i.imgur.com/RJzH1fC.png)



```
study(title="chop filter v1.1", shorttitle="chop filter", overlay=true)
len = input(10, title="Period", minval=2)
FilterOut=input(0.007, title="FilterOut", minval=0.0001)
HowBigBubbles0to1=input(0.02, title="HowBigBubbles0to1", minval=0.0001)

lr=linreg(close,10,0)
maxlr=highest(lr*(1+HowBigBubbles0to1),10)
minlr=lowest(lr*(1-HowBigBubbles0to1),10)

zld_h=linreg(high,len,0)
zld_l=linreg(low,len,0)
diff(a,b)=>(a-b)/((a+b)/2)
chop=diff(zld_h,zld_l)
t1=chop<FilterOut?maxlr:na
b1=chop<FilterOut?minlr:na

t2=chop>FilterOut?maxlr:na
b2=chop>FilterOut?minlr:na

p1=plot(t1,color=chop<FilterOut?#B45F06:na,style=line,linewidth=1,transp=100)
p1b=plot(b1,color=chop<FilterOut?#B45F06:na,style=line,linewidth=1,transp=100)

p2=plot(t2,color=chop>=FilterOut?white:na,style=line,linewidth=1,transp=100)
p2b=plot(b2,color=chop>=FilterOut?white:na,style=line,linewidth=1,transp=100)

fill(p1,p1b,color=#B45F06,transp=50)
fill(p2,p2b,color=white,transp=50)

```

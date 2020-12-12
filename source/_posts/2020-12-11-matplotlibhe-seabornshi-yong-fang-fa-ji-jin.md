---
layout: post
title: "Matplotlib和Seaborn使用方法集锦"
date: 2020-12-11 11:41:28 +0800
comments: true
categories: Data&ML&AI
---

#### 1. 引入常用的包

```py
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt 
import seaborn as sns
```

#### 2. 选定若干列，画pairplot

```py
sns.pairplot(college.iloc[:,1:11])

sns.pairplot(auto) # 选择全部列的数据
```

#### 3. 选定两列，画出来boxplot

```py
sns.boxplot(x = college['Private'],y = college['Outstate'])
```

#### 4. 通过bar画直方图

```py
fig = plt.figure()

plt.subplot(2,2,1) college['Enroll'].value_counts().plot.bar(title = 'Enroll')

plt.subplot(2,2,2) college['PhD'].value_counts().plot.bar(title = 'PhD')

plt.subplot(2,2,3) college['Terminal'].value_counts().plot.bar(title = 'Terminal')

#to add space in between the subplots 
fig.subplots_adjust(hspace=1)
```

#### 5. 画出散点图和曲线图，并且设置线的颜色

```py
plt.figure(figsize = (14,8)) 
plt.scatter(auto['horsepower'],auto['mpg']) 
plt.plot(auto['horsepower'],pred_1,color = 'orange') 
plt.plot(auto['horsepower'],pred_2,color = 'green') 
plt.plot(auto['horsepower'],pred_5,color = 'black') 
plt.show()
```

#### 6. 绘制平行于x轴的水平参考线

```py
error_1 = auto['mpg'] - pred_1 
plt.figure(figsize = (12,6)) 
sns.scatterplot(x = auto['mpg'],y = error_1) 
plt.axhline(y = 0,linestyle = 'dashed',color = 'black',linewidth = 0.5)
```

#### 7. 用sns.regplot来比较两个变量的关系是否符合线性回归

```py
sns.regplot(data['LSTAT'],data['MEDV'])

# regplot中设置参数
sns.regplot(advertising.TV, advertising.Sales, order=1, ci=None, scatter_kws={'color':'r', 's':9})
plt.xlim(-10,310)
plt.ylim(ymin=0);
```

#### 8. 设置label和title和

```py
plt.xlabel('Fitted Vales') 
plt.ylabel('Residuals') 
plt.title('Residual Plot')
```

#### 9. 使用sns画相关系数矩阵的热力图

```py
sns.heatmap(auto.iloc[:,:-1].corr())
```

#### 10. 设置线的label并且置成legend

```py
plt.figure(figsize = (14,6)) 
sns.scatterplot(X,Y) 
plt.xlabel('X') 
plt.ylabel('Y') 

plt.plot(data['X'],lin_model.predict(data['X'].to_frame()),color = 'orange',label = 'Predicted Line') 
plt.title('Relationship b/w X and Y') 
plt.plot(tmp_x,tmp_y,color = 'green',label = 'True Line') 
plt.legend()
plt.show()
```

#### 11. 设置坐标范围, 设置相等的宽和高

```py
fig, ax = plt.subplots()

sns.scatterplot(simple_coeff,multi_coeff)

lims = [
    np.min([ax.get_xlim(), ax.get_ylim()]),  # min of both axes
    np.max([ax.get_xlim(), ax.get_ylim()]),  # max of both axes
]

ax.plot(lims, lims, 'k-', alpha=0.75, zorder=0,color = 'orange')
ax.set_aspect('equal')
ax.set_xlim(lims)
ax.set_ylim(lims)
```

#### 12. 设置hue

```py
plt.figure(figsize = (12,8))

tmp = pd.DataFrame({'Lag1':X_train['Lag1'],'Lag2':X_train['Lag2'],'Direction':y_train})

sns.scatterplot(y = 'Lag2',x = 'Lag1',hue = 'Direction',data = tmp)
```

#### 13. 画等高线和三维图

```py
fig = plt.figure(figsize=(15,6))
fig.suptitle('RSS - Regression coefficients', fontsize=20)

ax1 = fig.add_subplot(121)
ax2 = fig.add_subplot(122, projection='3d')

# Left plot
CS = ax1.contour(xx, yy, Z, cmap=plt.cm.Set1, levels=[2.15, 2.2, 2.3, 2.5, 3])
ax1.scatter(regr.intercept_, regr.coef_[0], c='r', label=min_RSS)
ax1.clabel(CS, inline=True, fontsize=10, fmt='%1.1f')

# Right plot
ax2.plot_surface(xx, yy, Z, rstride=3, cstride=3, alpha=0.3)
ax2.contour(xx, yy, Z, zdir='z', offset=Z.min(), cmap=plt.cm.Set1,
            alpha=0.4, levels=[2.15, 2.2, 2.3, 2.5, 3])
ax2.scatter3D(regr.intercept_, regr.coef_[0], min_rss, c='r', label=min_RSS)
ax2.set_zlabel('RSS')
ax2.set_zlim(Z.min(),Z.max())
ax2.set_ylim(0.02,0.07)

# settings common to both plots
for ax in fig.axes:
    ax.set_xlabel(r'$\beta_0$', fontsize=17)
    ax.set_ylabel(r'$\beta_1$', fontsize=17)
    ax.set_yticks([0.03,0.04,0.05,0.06])
    ax.legend()
```

#### 14. 3D散点图

```py
# Create plot
fig = plt.figure(figsize=(10,6))
fig.suptitle('Regression: Sales ~ Radio + TV Advertising', fontsize=20)

ax = axes3d.Axes3D(fig)

ax.plot_surface(B1, B2, Z, rstride=10, cstride=5, alpha=0.4)
ax.scatter3D(advertising.Radio, advertising.TV, advertising.Sales, c='r')

ax.set_xlabel('Radio')
ax.set_xlim(0,50)
ax.set_ylabel('TV')
ax.set_ylim(ymin=0)
ax.set_zlabel('Sales')
```

#### 15. suptitle、用clabel为等高线添加高程标签

```py
fig = plt.figure(figsize=(12,5))
fig.suptitle('RSS - Regression coefficients', fontsize=20)

ax1 = fig.add_subplot(121)
ax2 = fig.add_subplot(122)

min_RSS = r'$\beta_0$, $\beta_1$ for minimized RSS'
    
# Left plot
CS = ax1.contour(X1, Y1, Z1, cmap=plt.cm.Set1, levels=[21.25, 21.5, 21.8])
ax1.scatter(regr1.coef_[1], regr1.coef_[0], c='r', label=min_RSS)
ax1.clabel(CS, inline=True, fontsize=10, fmt='%1.1f')
ax1.set_ylabel(r'$\beta_{Age}$', fontsize=17)

# Right plot
CS = ax2.contour(X2, Y2, Z2, cmap=plt.cm.Set1, levels=[21.5, 21.8])
ax2.scatter(regr2.coef_[1], regr2.coef_[0], c='r', label=min_RSS)
ax2.clabel(CS, inline=True, fontsize=10, fmt='%1.1f')
ax2.set_ylabel(r'$\beta_{Rating}$', fontsize=17)
ax2.set_xticks([-0.1, 0, 0.1, 0.2])

for ax in fig.axes:
    ax.set_xlabel(r'$\beta_{Limit}$', fontsize=17)
    ax.legend()
```

#### 16. 同时画两种不同的散点图

```py
fig = plt.figure(figsize=(12,5))
gs = mpl.gridspec.GridSpec(1, 4)
ax1 = plt.subplot(gs[0,:-2])
ax2 = plt.subplot(gs[0,-2])
ax3 = plt.subplot(gs[0,-1])

# Take a fraction of the samples where target value (default) is 'no'
df_no = df[df.default2 == 0].sample(frac=0.15)
# Take all samples  where target value is 'yes'
df_yes = df[df.default2 == 1]
df_ = df_no.append(df_yes)

ax1.scatter(df_[df_.default == 'Yes'].balance, df_[df_.default == 'Yes'].income, s=40, c='orange', marker='+',
            linewidths=1)
ax1.scatter(df_[df_.default == 'No'].balance, df_[df_.default == 'No'].income, s=40, marker='o', linewidths=1,
             edgecolors='lightblue', facecolors='white', alpha=.6)

ax1.set_ylim(ymin=0)
ax1.set_ylabel('Income')
ax1.set_xlim(xmin=-100)
ax1.set_xlabel('Balance')

c_palette = {'No':'lightblue', 'Yes':'orange'}
sns.boxplot('default', 'balance', data=df, orient='v', ax=ax2, palette=c_palette)
sns.boxplot('default', 'income', data=df, orient='v', ax=ax3, palette=c_palette)
gs.tight_layout(plt.gcf())
```

### 参考资料

- https://github.com/JWarmenhoven/ISLR-python.git
- https://github.com/hardikkamboj/An-Introduction-to-Statistical-Learning.git

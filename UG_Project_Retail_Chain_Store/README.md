# Customer and Sales Data Analysis

## Objective
The objective of this analysis is to gain insights into customer demographics, product performance, and various sales metrics to guide strategic decisions.

## Tasks

### 1. Customer Demographics
- **Identify Key Demographics**: Analyze customer data to identify key demographic segments.
- **Clean Data**: Ensure customer data is clean and ready for detailed analysis.

### 2. Customer Details for Further Study
- **Extract Customer Details**: Prepare a detailed dataset of customers for further study and segmentation.

### 3. Product Performance
- **Top Performing Products**: Identify the best-performing products based on sales and customer ratings.
- **Worst Performing Products**: Identify products that are underperforming.

### 4. Ratings Analysis
- **Category Ratings**: Analyze ratings to understand the performance of different product categories.

### 5. Orders Analysis
- **Orders by Location**: Analyze order data to understand geographic distribution.

### 6. Revenue Analysis
- **Revenue by Region**: Analyze revenue distribution across different regions.
- **Customer Segments**: Break down revenue by different customer segments.
- **Payment Methods**: Analyze revenue distribution by payment methods.

### And More
- **Additional Insights**: Explore other relevant insights as identified during the analysis process.

---
# Tools
For my Deep Dive into Data of Retail Chain Analysis, I harnessed the power of several key tools:
* Python: The Backbone of my project is Python allowing me to find critical Insights. I also used following Python libraries:
   * Pandas Library: Used to analyze and play with Data
   * Matplotlib Library: Used for Visualizng the Findings
   * Seaborn Library: Helped in creating more advance Visuals
   * Plotly Express: For Creating more Engaging and Interactive Visuals
* Jupyter NOtebook: This tool i used to run my python scripts ahich let me easily include my notes and analysis
* Visual Studio Code: My go-to for executing pyhon scripts
---
# The Analysis
## 1. Let's See the Customer Demographic First by Gender and Income
I have used Seaborn and Plotly Express for them. Feel Free to go through the actual procedure at here.
[Notebook](Retail_Transactions.ipynb)
### For Data Visualization
``` Python
plt.figure(figsize=(8,3))
sns.barplot(data=gen, x='count', y='Gender', hue='Gender', palette='cividis')
sns.set_theme(style='ticks')
sns.despine()
for n, v in enumerate(gen['count']):
    plt.text(v,n,f'{v/1000:.1f} K')
plt.xlim(0,200000)
plt.xlabel('Number of Customers')
plt.ylabel('Gender')
plt.title('Gender Distribuition of Customers', fontsize=14)
plt.show()
```
### Result of Code
![Male-Female Customer Counts](/UG_Project_Retail_Chain_Store/Visuals/MaleFemale.png)

### Key Insights
Male are more in number as comapred to Females.

### Gender By Income Level
Let's See the Distribuition by Income Level as well
### For Data Visualization
``` Python
fig = px.bar(data_frame=df_new.groupby(['Gender','Income']).size().reset_index(name='Count'),
        x='Gender', y='Count', color='Income', barmode='group', title='Gender Distribution with Respect to Income Level of Customers',
        labels={'Gender':'Customers Gender', 'Count':'Number of Customers'}, width=700,
        color_discrete_sequence=px.colors.sequential.Inferno
        )
fig.show()
```
### Result of Code
![Male Female by Income Level](/UG_Project_Retail_Chain_Store/Visuals/Male_Female_Income.png)

## 2. Let's See the Overall Revenue Trend and Category Wise As well.
Revenue Trend of Entrie Year Give details about pattern and Category wise best performance by Month so we can get to know their Peak and Low Era.
### For Data Visualization
``` Python
sns.lineplot(Monthly_grp,x='Month', y='Amount', linewidth=2.5, marker='s', markersize=7, color='black')
sns.set_theme(style='ticks')
sns.despine()
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y,pos: f'${y/1000000} M'))
plt.xlabel('2023-24')
plt.ylabel('(USD $) in Millions')
plt.title('Revenue Trend for Year 2023-24')
plt.show()
```
### Result of the Code
![Revenue Trend of Entrie Year](/UG_Project_Retail_Chain_Store/Visuals/Rev_trend.png)

## Revenue Trend By Different Category
### For Data Visualization
```Python
plt.figure(figsize=(12,8))
sns.set_theme(style='ticks')
sns.lineplot(data=trend_cat, legend=True, dashes=False, markers=True, linewidth=4, markersize=9, palette='tab10')
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'$ {x/1000000} M'))
plt.xlabel('Year 2023')
plt.ylabel('Revenue in USD ($)')
plt.title('Revenue Trend of Different Categories at Store', fontsize=18)
plt.show()
```
### Result of Code
![Revenue Trend by Categories](/UG_Project_Retail_Chain_Store/Visuals/Rev_trend_by-Category.png)

## 3. We Also want to see Which Customer Segmenst Brings More Revenue and which is Low.
Understand Revenue Distribuition by Customer Segements Helps a lot for Marketing Decision.
### For Data Visualization
```python
plt.figure(figsize=(10,3))
ax = sns.barplot(data=cust_seg, x='Revenue', y='Customer_Segment', hue='Count', palette='dark:b_r')
sns.set_theme(style='ticks')
sns.despine()
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${x/1000000}M'))

plt.ylabel('Customer Segments')
plt.xlabel('Revenue in USD($)')
plt.title('Revenue and Count of Customer of Segments')
plt.xlim(0,220000000)
for n, v in enumerate(cust_seg['rev_%']):
    plt.text(v+1000000,n,f'{v}% of Total Rev', color='white')

x, y = ax.get_legend_handles_labels()
ax.legend(x[::-1], y[::-1], title='Count')

plt.show()
```
### Result of Code
![Revenue by Customer Segment](/UG_Project_Retail_Chain_Store/Visuals/Rev_by_Customer_segments.png)
### Key Insights 
Regualr Customer Contribute the MAX while Premium are at LOW.

## 4. We want to see Which Category Segmenst Brings More Revenue and which is Less.
Understand Revenue Distribuition by Categories Segements Helps a lot for Manufacturing Decision.
### For Data Visualization
```python
sns.barplot(data=cat_rev, x='Total_Amount', y='Product_Category', hue='Total_Amount', palette='dark:b_r', legend=False)
sns.set_theme(style='darkgrid')
sns.despine()
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'$ {x/1000000} M'))
plt.xlim(0,115000000)
plt.xlabel('Revenue USD ($)')
plt.ylabel('Categories')
plt.title('Revenue for Different Category (2023)', fontsize=14)
for n, v in enumerate(cat_rev['Total_Amount']):
    plt.text(v+1000000,n,f'${v/1000000:.1f} M')
plt.show()
```
### Result of Code
![Revenue by Categories](/UG_Project_Retail_Chain_Store/Visuals/Rev_by_Category.png)
### Key Insights 
Electronics are Highest Contibutor here.

## 5. We want to see Which Brand is Responsible for That Category being High or Low
Understand Revenue Distribuition by Brand help in finding top Brands.
### For Data Visualization
```python
fig = px.bar(data_frame=cat_brd, x='Product_Brand', y='Total_Amount', color='Product_Category', barmode='group', color_discrete_sequence=px.colors.qualitative.Bold,
             title='Revenue by Category and Brand')
fig.update_layout(
    paper_bgcolor = 'white',
    plot_bgcolor = 'grey',
    yaxis = dict(tickprefix='$ '),
    xaxis = dict(tickangle=-45, automargin=True), margin=dict(t=40,b=0))
fig.update_traces(textfont_color='white')
fig.show()
```
### Result of Code
![Revenue by Categories and their Brand](/UG_Project_Retail_Chain_Store/Visuals/Rev_by_Category_Brand.png)

### Method 2 By Seaborn
![Revenue By Categories and Brand with Seaborn](/UG_Project_Retail_Chain_Store/Visuals/By_Seaborn_Cat_brand.png)

## 6. Next let's analyze and find most prefered Payment Method.
Understanding of this helps in curating offers and discount for customers.
### For Data Visualization
```Python
plt.figure(figsize=(8,4))
sns.barplot(data=pay_method, x='Revenue', y='Payment_Method', hue='cnt', palette='dark:b_r')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${x/1000000} M'))

x, y = ax.get_legend_handles_labels()
ax.legend(x[::-1], y[::-1], title='Count')

for n, v in enumerate(pay_method['rev_perc']):
    plt.text(v+1000000,n,f'{v}%', color='white')

plt.xlabel('Revenue USD ($)')
plt.ylabel('Payment Methods')
plt.title('Revenue via Payment Methods', fontsize=14)
plt.show()
```
### Resukt of the code
![Revenue Distribuition by Payment Methods](/UG_Project_Retail_Chain_Store/Visuals/Rev_by_Payment_Method.png)
### Key Findings
Credit Card is the Most Used Payment Method while Paypal Being the Less Prefered by Customers.

## 7. Analysis on Region Based Revenue is quite important as well to find best Performing Regions.
First, We will find the best Prvince/State for Each Country
### For Data Visualization
```Python
plt.figure(figsize=(10,4))
sns.set_theme(style='darkgrid')
sns.barplot(data=cn_sta, x="Orders", y='Province/State', hue='Country', palette=['#92c0d9','#000000','#FFCC00','#FF0000','#1c2b5a'])
sns.despine()
plt.xlim(0,70000)
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'{int(x/1000)} K'))
for n,v in enumerate(cn_sta['Orders']):
    plt.text(v+500,n,f'{v/1000:.1f} K')
plt.xlabel('Number of Orders')
plt.ylabel('Province / State')
plt.title('Countries with their Top Performing Province', fontsize=14)
```
### Result of the Code
![Best Provine/State of Each Country](/UG_Project_Retail_Chain_Store/Visuals/Rev_of_each_country_top_Provive_State.png)
### Key Insgihts
You Can see UK Being the Top Country Source of Revenue with England as Top Province

## 8. Overall Performance of Each Country->State->City
We know will see the Overall Performancce of Each Country with State and City as well in a Sunbrust
### For Data Visualization
```Python
fig = px.sunburst(data_frame=city, path=['Country','Province/State','City'], values='Revenue', width=1280, height=720,
                  title='Orders Counts By Country and City', color_discrete_sequence=px.colors.sequential.Cividis)
fig.update_layout(
    paper_bgcolor = 'black',
    plot_bgcolor = 'lightgrey',
    title_font_color='white',
    uniformtext=dict(minsize=10, mode='hide'),
    margin=dict(t=40,l=0,r=0,b=10))
fig.update_traces(rotation=90, textfont_color='white')
fig.show()
```
### Result of the Code
![Revenue by Country->State/Provine->City](/UG_Project_Retail_Chain_Store/Visuals/Rev_by_Country_State_City.PNG)
### Key Insights
In fact UsA was Last in Previous Grapgh But on Grander Level It is the Most Revenue Generating Country
While Canada is at Last Stand in Terms of Revenue.

## 9. Let's Uncover the Most Repeated Amount values Impacting our Revenue
Here we want to see the Distribuition Plot for Amount Column of Dataset to find the most impacting range of amount
We will use 3 methods for this, from basuc to Advance level Distribuition Plot.
### Basic Level 1
### Code for this 
```Python
# Basic Method
ax = sns.displot(data=df_new, x='Total_Amount', bins=10, linewidth=1.5, edgecolor='black')
```
### Output
![Distribuition Plot of Amount Levell](/UG_Project_Retail_Chain_Store/Visuals/Level1.png)

### Intermediate Level 2
### Code for this
```python
amount = df_new[['Transaction_ID','Total_Amount']]
amount = amount.dropna()
edges = np.linspace(min(amount['Total_Amount']), max(amount['Total_Amount']),11)
edges2 = np.round(edges,0)
edges = np.linspace(min(amount['Total_Amount']), max(amount['Total_Amount']),11)
amount['binned'] = pd.cut(amount['Total_Amount'],bins=edges2, labels=[500, 1000, 1500, 2000, 2500, 3000, 3500, 4000,
       4500, 5000], include_lowest=True)

# Intermediate Method
ax = sns.countplot(data=amount, x='binned', linewidth=1.25, edgecolor='black')
sns.set_theme(style='ticks')
for x in ax.containers:
    ax.bar_label(x)
```
### Output
![Distribuition Plot of Amount Level2](/UG_Project_Retail_Chain_Store/Visuals/Level2.png)

### Advance Level 3
### Code for this
```Python
amount_grp = amount.groupby('binned').size().reset_index(name='Orders')
amount_grp['perc'] = np.round((amount_grp['Orders'] / amount_grp['Orders'].sum()) * 100,1)
amount_grp['binned'] = amount_grp['binned'].astype(int)
# Advance and more clear defination of Distribuition Plot
sns.set_theme(style='ticks')
sns.barplot(data=amount_grp, x='binned', y='perc', hue='perc', legend=False, palette='dark:b_r')
sns.despine()
for n, v in enumerate(amount_grp['perc']):
    plt.text(n-0.3,v+1,f'{v}%', color='black')
plt.ylabel('Contribution to Total Orders')
plt.xlabel('Transaction Amount Group')
plt.title('Distribuition Plot of Amount with % of Orders they Hold')
plt.ylim(0,35)
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y,pos: f'{y}%'))
plt.show()
```
### Output
![Distribuition Plot of Amount Level2](/UG_Project_Retail_Chain_Store/Visuals/Rev_Amount_Distribuition_plot.png)
Here we can have an idea that almost 50% of our Revenue is generated from 0-1000 Trasactional Value

## 10. Revenue by Product Type and their Brands as well for Top 10 Type of Product only based on Revenue
It is important to look for Top 10 Product Type we are selling and their Brands so we can have good Relations with those Brand for Continuos Flow.
### Code For this
```Python
filtered_df = df_new[df_new['Product_Type'].isin(df_new.groupby(['Product_Type']).agg(
    Revenue = ('Total_Amount','sum'),
    Quantity = ('Total_Quantity','sum')
).sort_values(by='Revenue',ascending=False).head(10).index.tolist())]

top10type = filtered_df.groupby(['Product_Type','Product_Brand']).agg(
    Revenue = ('Total_Amount','sum')
).reset_index().sort_values(by=['Product_Type','Revenue'], ascending=[True,False]).replace({'Fiction':'Fiction_Books','Non-Fiction':'Non-Fiction_Books'})

fig = px.sunburst(data_frame=top10type, path=['Product_Type','Product_Brand'],values='Revenue', width=1280, height=720, color='Product_Type',
                   color_discrete_sequence=px.colors.sequential.Inferno, title='Product Type with Respective Brand')
fig.update_traces(rotation=90, textfont_color='white')
fig.update_layout(
    paper_bgcolor = 'black',
    plot_bgcolor = 'white',
    margin=dict(t=30,l=0,r=0,b=0,),
    title_font_color = 'white'
)
fig.show()
```
### Output
![Revenue from Top 10 Products and their Brands](/UG_Project_Retail_Chain_Store/Visuals/Rev_By_Product_Type_Brand.PNG)
We can have an idea of best products and their Creating Brands

## 11. And Last but not the Least we have to see Customer Rating of Each Category we are selling.
We will see here all categories and their % of Rating for each rating call of 1-5.
### Code for this
```Python
cat_rating = rating.pivot_table(index='Product_Category', columns='Ratings', aggfunc='size')
cat_tot = cat_rating.sum(axis=1)
cat_perc = np.round(cat_rating.div(cat_tot/100,axis=0),1)
cat_perc.reset_index(inplace=True)
cat_melt = pd.melt(cat_perc, id_vars='Product_Category', var_name='Ratings', value_name='perc')

fig = px.bar(data_frame=cat_melt, x='Product_Category', y='perc', color='Ratings',barmode='group', color_discrete_sequence=px.colors.sequential.ice,
       labels={'Product_Category':'Categories of Products','perc':'% from Total Ratings','Ratings':'Star_Rating'}, text='perc',
       title='Categories with their % of Rating for each Rating Value')
fig.update_layout(bargap=0.15,
                  bargroupgap=0.1,
                  yaxis = dict(ticksuffix=" %"))
fig.show()
```
### Result as an Output
![Revenue from Top 10 Products and their Brands](/UG_Project_Retail_Chain_Store/Visuals/Ratings.PNG)
### Key Insights
We can have idea from this visual that What % of Rating for this Category is for 1,2,3,4,5

## Conclusion
I have to say this Entire Project took around 3 Days to complete and I have to admit that It was Worth my Time Invested.
Plotly Express was used just to showcase a different method of doing same thing which was new for me and worth Learning.
In the Process I got hand-on experience with Dealing with Huge Data to Find Insights from it and make worthy decisions from them.
The same thing can be achieved from Excel, Power BI as well but it is good to learn Python becausse when You have millions of Rows of Data, everything will fail except Python.
# Thank You, If You are reading this, You are a Data Nerd Like me.

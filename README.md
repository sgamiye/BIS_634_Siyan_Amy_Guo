# BIS_634_Siyan_Amy_Guo
Siyan(Amy) Guo's repository for BIS 634
Exercise 1:
Function and associated test presented in the Exercise1.ipynb file

Exercise 2:
After examining the data:It has columns for name, age, weight, and eyecolor. And it has 152361 rows (people).
For age:
Statistics for age: the mean: 39.510527927396524; standard_deviation: 24.152760068601445; minimum: 0.0007476719217636152; maximum: 99.99154733076972
Role of the number of bins:the number of bins (associated with binwidth) determine the presentation of the histogram's pattern. If the number is too great, there will be too much details shown on the histogram, so that it is very difficult to recognize the actual pattern of the whole dataset, and it may include noises that divert the pattern to be distracted. If the number of bins gets too low, it tends to oversmooth essential details such as peak counts at one datapoint. Therefore, it is very important to use an appropriate bin number to graph histogram so that the pattern and details of the data can be visualized as being closer to the true data pattern. 
Comment on any outliers or patterns: People at ages from 0 to approximately 70 have similar counts, while those at age 70-100 have similar counts, this shows a segmented pattern for people at ages below 70 and above 70.
For weight:
statistics for weight: mean: 60.88413415993031;standard_deviation: 18.41182426566149; minimum: 3.3820836824389326; maximum: 100.43579300336947
Comment on any outliers or patterns: According to the distribution shown on histogram, those with weight lower than 50 has a rather leveled and low counts, while for those with weight greater than 50 has a distribution similar to standard distribution,except for the outlier when weight equals to 68.0 (rounded) with count of 27842.
For scatter plot of weights vs. ages:
General relationship between the two variables: their relationship is generally following a positive trend. For weight lower than 40, the relationship between two variables are strongly positive;however, after weight=40, the relationship follows a weakly positive trend, with points strongly scattered.
The outlier's name is Anthony Freeman.
Process: Visualizing the scatter plot that demonstrates the relationship of weight and age allows the selection of the outlier-->According to it's rough ranges of the coordinations for the outlier shown on the plot, as shown in Exercise2.ipynb,the person was identified.

Exercise 3:
The date of downloading the data: 00:38,Sep19th, 2022
Data Source: The New York Times
limitations of newcases_vs_date:if the function takes on a list of states in which the number exceed the legen limit, there maybe same colors representing different states in the legend.

Exercise 4:
Explain briefly in terms of biology/medicine what the above search has found: There are diseases that are associated with both the nervous system and the immune system, as the list listed above. For example, for Multiple Sclerosis, the autoimmune function fails and starts to attack myelin sheath which is critical for effective signal propagations from action potentials and provide great insulations to the axon, and therefore, in this case, both immune system and nervous system are involved, which is very reasonable for there two be treennumbers associated with both. 

Appendix
Exercise 1
#function
def temp_tester(normal_temp):
    
    def tester(current_temp):
        if abs(current_temp-normal_temp)<1:
            return True
        else:
            return False
    return tester
#test
#test
human_tester = temp_tester(37)
chicken_tester = temp_tester(41.1)
chicken_tester(42)
True
human_tester(42)
False
chicken_tester(43)
False
human_tester(35)
False
human_tester(98.6)
False
Exercise 2
import pandas as pd
import sqlite3
with sqlite3.connect("hw1-population.db") as db:
    data = pd.read_sql_query("SELECT * FROM population", db)
Examine data:
data.columns
Index(['name', 'age', 'weight', 'eyecolor'], dtype='object')
data.shape
(152361, 4)
Answer to Exercise 2.1(as shown in readme.md): It has columns for name, age, weight, and eyecolor. And it has 152361 rows (people).
Examine the distribution of the ages:
mean_of_ages= data.age.mean()
standard_deviation_of_ages= data.age.std()
minimum_of_ages= data.age.min()
maximum_of_ages= data.age.max()
print(f'mean: {mean_of_ages}')
print(f'standard_deviation: {standard_deviation_of_ages}')
print(f'minimum: {minimum_of_ages}')
print(f'maximum: {maximum_of_ages}')
mean: 39.510527927396524
standard_deviation: 24.152760068601445
minimum: 0.0007476719217636152
maximum: 99.99154733076972
Plot histogram of the distribution with an appropriate number of bins for the size of the dataset
! conda install -c conda-forge plotnine -y
Note: I tried to plot with matplotlib and ggplot to see which visualization was better, and ggplot is much better, so for weight I only used ggplot to plot
import plotnine as p9
from plotnine import *
from matplotlib import pyplot as plt
from matplotlib import colors
from matplotlib.ticker import PercentFormatter
import numpy as np
#determining bin number
#determining bin number
q25,q75 = np.percentile(data.age, [25, 75])
bin_width = 2 * (q75 - q25) * len(data.age) ** (-1/3)
bins = round((maximum_of_ages - minimum_of_ages) / bin_width)
print(f'bin_number: {bins}')
bin_number: 70
 with matplotlib
#plot with matplotlib
plt.hist(x=data.age, density=False, bins=bins, ec= 'white',color='green')
(array([2827., 2811., 2789., 2888., 2826., 2715., 2982., 2728., 2861.,
        2829., 2813., 2782., 2784., 2906., 2833., 2842., 2861., 2847.,
        2901., 2784., 2879., 2825., 2764., 2910., 2792., 2801., 2812.,
        2807., 2803., 2860., 2776., 2853., 2865., 2843., 2837., 2847.,
        2858., 2826., 2828., 2903., 2845., 2787., 2856., 2750., 2795.,
        2869., 2803., 2733., 2816.,  678.,  651.,  624.,  663.,  691.,
         665.,  626.,  688.,  667.,  644.,  595.,  720.,  626.,  647.,
         654.,  643.,  685.,  633.,  662.,  658.,  689.]),
 array([7.47671922e-04, 1.42918767e+00, 2.85762766e+00, 4.28606766e+00,
        5.71450765e+00, 7.14294765e+00, 8.57138764e+00, 9.99982764e+00,
        1.14282676e+01, 1.28567076e+01, 1.42851476e+01, 1.57135876e+01,
        1.71420276e+01, 1.85704676e+01, 1.99989076e+01, 2.14273476e+01,
        2.28557876e+01, 2.42842276e+01, 2.57126676e+01, 2.71411076e+01,
        2.85695476e+01, 2.99979876e+01, 3.14264276e+01, 3.28548676e+01,
        3.42833076e+01, 3.57117476e+01, 3.71401875e+01, 3.85686275e+01,
        3.99970675e+01, 4.14255075e+01, 4.28539475e+01, 4.42823875e+01,
        4.57108275e+01, 4.71392675e+01, 4.85677075e+01, 4.99961475e+01,
        5.14245875e+01, 5.28530275e+01, 5.42814675e+01, 5.57099075e+01,
        5.71383475e+01, 5.85667875e+01, 5.99952275e+01, 6.14236675e+01,
        6.28521075e+01, 6.42805475e+01, 6.57089874e+01, 6.71374274e+01,
        6.85658674e+01, 6.99943074e+01, 7.14227474e+01, 7.28511874e+01,
        7.42796274e+01, 7.57080674e+01, 7.71365074e+01, 7.85649474e+01,
        7.99933874e+01, 8.14218274e+01, 8.28502674e+01, 8.42787074e+01,
        8.57071474e+01, 8.71355874e+01, 8.85640274e+01, 8.99924674e+01,
        9.14209074e+01, 9.28493474e+01, 9.42777874e+01, 9.57062273e+01,
        9.71346673e+01, 9.85631073e+01, 9.99915473e+01]),
 <BarContainer object of 70 artists>)

# plot with ggplot
# plot with ggplot
(ggplot(data, aes(x='age'))
 + geom_histogram(binwidth=bin_width,
                 fill='green',
                 colour='blue',
                 size=0.5,
                 alpha=0.5
                 )
 + theme_xkcd()
)

<ggplot: (8789209560408)>
role of bin numbers (also in readme.md):the number of bins (associated with binwidth) determine the presentation of the histogram's pattern. If the number is too great, there will be too much details shown on the histogram, so that it is very difficult to recognize the actual pattern of the whole dataset, and it may include noises that divert the pattern to be distracted. If the number of bins gets too low, it tends to oversmooth essential details such as peak counts at one datapoint. Therefore, it is very important to use an appropriate bin number to graph histogram so that the pattern and details of the data can be visualized as being closer to the true data pattern.
specifying regions for patterns
count_table_age= round(data.age).value_counts()
count_table_age = np.logical_and(count_table_age>1000, count_table_age<1500)
count_table_age[count_table_age==True]
70.0    True
Name: age, dtype: bool
Comment on any outliers or patterns: People at ages from 0 to approximately 70 have similar counts, while those at age 70-100 have similar counts, this shows a segmented pattern for people at ages below 70 and above 70.
Examine the distribution of the weights:
mean_of_weights= data.weight.mean()
standard_deviation_of_weights= data.weight.std()
minimum_of_weights= data.weight.min()
maximum_of_weights= data.weight.max()
print(f'mean: {mean_of_weights}')
print(f'standard_deviation: {standard_deviation_of_weights}')
print(f'minimum: {minimum_of_weights}')
print(f'maximum: {maximum_of_weights}')
mean: 60.88413415993031
standard_deviation: 18.411824265661494
minimum: 3.3820836824389326
maximum: 100.43579300336947
Plot histogram of the distribution with an appropriate number of bins for the size of the dataset
q25,q75 = np.percentile(data.weight, [25, 75])
bin_width_weight = 2 * (q75 - q25) * len(data.weight) ** (-1/3)
bins_weight = round((maximum_of_weights - minimum_of_weights) / bin_width_weight)
print(f'bin_number: {bins}')
bin_number: 196
(ggplot(data, aes(x='weight'))
 + geom_histogram(binwidth=bin_width_weight,
                 fill='purple',
                 colour='white',
                 size=0.2,
                 alpha=0.6
                 )
 + theme_xkcd()
)

<ggplot: (8789191243216)>
specifying regions for patterns
data['weight'].value_counts()
68.000000    22613
73.104595        1
54.951453        1
35.978364        1
71.831014        1
             ...  
61.768055        1
66.071491        1
59.401400        1
39.040271        1
59.042765        1
Name: weight, Length: 129749, dtype: int64
Comment on any outliers or patterns: According to the distribution shown on histogram, those with weight lower than 50 has a rather leveled and low counts, while for those with weight greater than 50 has a distribution similar to standard distribution,except for the outlier when weight equals to 68.0 (rounded) with count of 27842.
Scatter plot of weights vs. ages
plt.scatter(x= data.age, y= data.weight, c= 'blue',edgecolors='white')
plt.gca().update(dict(title='weight vs. age', xlabel='age', ylabel='weight'))
[Text(0.5, 1.0, 'weight vs. age'), Text(0.5, 0, 'age'), Text(0, 0.5, 'weight')]

General relationship between the two variables: their relationship is generally following a positive trend. For weight lower than 40, the relationship between two variables are strongly positive;however, after weight=40, the relationship follows a weakly positive trend, with points strongly scattered.
The outlier that doesn't follow relationship:
data[(data['age']>40)& (data['age']<42) &(data['weight']>20) &(data['weight']<22)]
name	age	weight	eyecolor
537	Anthony Freeman	41.3	21.7	green
The outlier's name is Anthony Freeman.
Visualizing the scatter plot that demonstrates the relationship of weight and age allows the selection of the outlier-->According to it's rough ranges of the coordinations for the outlier shown on the plot, as shown above in code [346],the person was identified.
Exercise 3
The date of downloading the data: 00:38,Sep19th, 2022
Data Source: The New York Times
data_nytimes= pd.read_csv('./us-states.csv')
#grouping dataframe into different values in the dictionary 
state_datasets=[]
for k in (pd.unique(data_nytimes['state'])):
        state_data=data_nytimes[data_nytimes['state']==k]
        state_datasets.append(state_data)
dict_state=dict(zip(pd.unique(data_nytimes['state']), state_datasets))
#Calculating new cases for each
for key in dict_state.keys():
    cases=list(dict_state[key]['cases'])
    old_cases=[0]+cases
    new_cases = []
    for today,yesterday in zip(cases, old_cases):
        new_cases.append(today-yesterday)
    dict_state[key]['new_cases']=new_cases
#Concatenate values in the dictionary back with State sorted and new_cases values calculated
data_sorted=pd.concat(dict_state.values()) 
function for new cases vs date
def newcases_vs_date(state_list):
    data_sorted_state=data_sorted[data_sorted['state'].isin(state_list)]
    plot=(ggplot(data_sorted_state, aes(x='date', y='new_cases',color = 'state',group=1))
          +geom_line()
          + scale_x_date(date_labels='%Y-%m-%d')
          + theme_xkcd())
    return plot
limitations: if the function takes on a list of states in which the number exceed the legen limit, there maybe same colors representing different states in the legend.
test the above function:
example 1: plotting for all states in the orginal dataset
newcases_vs_date(data_sorted['state'])

<ggplot: (8772837118468)>
example 2: plotting for only Alaska and California
newcases_vs_date(['Alaska','California'])

<ggplot: (8772837091271)>
function that takes the name of the state and returns the date of its highest number of new cases
def date_higest_newcase_number(state):
    index=data_sorted[data_sorted['state']==state]['new_cases'].idxmax()
    date=data_sorted['date'].loc[index]
    return print(f'date of the highest number of new cases in {state}: {date}')
def date_higest_newcase_number(state):
    index=data_sorted[data_sorted['state']==state]['new_cases'].idxmax()
    date=data_sorted['date'].loc[index]
    return date
test
date_higest_newcase_number('Alaska')#as shown above of the peak for Alaska in the ggplot
date of the highest number of new cases in Alaska: 2022-01-19
date_higest_newcase_number('Alaska')
'2022-01-19'
function that takes the names of two states and reports which one had its highest number of daily new cases first and how many days separate that one's peak from the other one's peak
from dateutil.parser import parse as parse_date
def days_between_peaks(state1,state2):
    state1highest=date_higest_newcase_number(state1)
    state2highest=date_higest_newcase_number(state2)
    days_between_peaks=parse_date(state1highest)-parse_date(state2highest)
    days_between_peaks=abs(days_between_peaks.days)
    if state1highest < state2highest:
        return print(f'{state1} had the highest number of daily new cases first, and there are {days_between_peaks} days separating {state1} peak from {state2} peak.')
    elif state1highest > state2highest:
        return print(f'{state2} had the highest number of daily new cases first, and there are {days_between_peaks} days separating {state1} peak from {state2} peak.')
    else:
        return print(f'{state1} and {state2} have the highest number of daily new cases on the same date.')
test with examples from Florida and Alaska
date_higest_newcase_number('Florida')
'2022-01-04'
date_higest_newcase_number('Alaska')
'2022-01-19'
days_between_peaks('Florida','Alaska')
Florida had the highest number of daily new cases first, and there are 15 days separating Florida peak from Alaska peak.
Exercise 4
import xml.etree.ElementTree as ET
from pprint import pprint as pp 
tree = ET.parse('./desc2022.xml')
root = tree.getroot()
book1 = root[0]
book1_xml = ET.tostring(book1)
book1_string = book1_xml.decode('utf-8')
print(book1_string)
DescriptorUIs=root.findall('DescriptorRecord/DescriptorUI')
strings=root.findall('DescriptorRecord/DescriptorName/String')
the DescriptorName associated with DescriptorUI D007154 (the text of the name is nested inside a String tag) (5 points)
create a list for all DescriptorUIs and associate according index to find the DescriptorName

def find_name_w_UI(UI_input):
    DescriptorUIs=root.findall('DescriptorRecord/DescriptorUI')
    strings=root.findall('DescriptorRecord/DescriptorName/String')
    UIs=[]
    for DescriptorName in root.findall("DescriptorRecord"):
        UI=DescriptorName.find("DescriptorUI").text
        UIs.append(UI)
    index=UIs.index(UI_input)
    return pp(strings[index].text)
find_name_w_UI('D007154')
'Immune System Diseases'
the DescriptorUI (MeSH Unique ID) associated with DescriptorName "Nervous System Diseases"
create a list for all DescriptorNames and associate according index to find the DescriptorUI

def find_UI_w_name(name_input):
    DescriptorUIs=root.findall('DescriptorRecord/DescriptorUI')
    strings=root.findall('DescriptorRecord/DescriptorName/String')
    names=[]
    for DescriptorUI in root.findall("DescriptorRecord"):
        name=DescriptorUI.find("DescriptorName").find("String").text
        names.append(name)
    index=names.index(name_input)
    return pp(DescriptorUIs[index].text)
find_UI_w_name('Nervous System Diseases')
'D009422'
the DescriptorNames of items in the MeSH hierarchy that are descendants of both "Nervous System Diseases" and D007154. (That is, each item is a subtype of both, as defined by its TreeNumber(s).)
SH data
# building dataframe for attributes in the MeSH data
trees=[]
for DescriptorUI in root.findall("DescriptorRecord"):
    tree_list = []
    try:
        for tree in DescriptorUI.find("TreeNumberList"):
            tree_list.append(tree.text)
    except TypeError:
        tree_list= []
    trees.append(tree_list)
Descriptor_data = []
​
for DescriptorRecord in root:
    Descriptor_dict = {
        'DescriptorUI': DescriptorRecord.find('DescriptorUI').text,
        'DescriptorName': DescriptorRecord.find('DescriptorName/String').text,
    }
    Descriptor_data.append(Descriptor_dict)
​
Descriptor_df = pd.DataFrame(Descriptor_data)
Descriptor_df['TreeNumberList']=trees
# identify treenumber for Nervous System Diseases
Descriptor_df[Descriptor_df['DescriptorName']=='Nervous System Diseases']['TreeNumberList'] #TreeNum for Nervous System Diseases
11795    [C10]
Name: TreeNumberList, dtype: object
# identify treenumber for Immune System Diseases
Descriptor_df[Descriptor_df['DescriptorName']=='Immune System Diseases']['TreeNumberList']#TreeNum for Nervous System Diseases
9629    [C20]
Name: TreeNumberList, dtype: object
numbers
# function for identifying overlapping descendants for two treenumbers
def descendants(Treenumber1,Treenumber2):
    name_list = []
    for item in range(Descriptor_df.shape[0]):
        lst = Descriptor_df['TreeNumberList'][item]
        s = []
        for j in lst:
            s.append(j.split('.')[0])
        if Treenumber1 in s and Treenumber2 in s:
            name_list.append(Descriptor_df['DescriptorName'][item])
    return name_list
descendants('C10','C20')
['Autoimmune Hypophysitis',
 'Ataxia Telangiectasia',
 'Diffuse Cerebral Sclerosis of Schilder',
 'Encephalomyelitis, Acute Disseminated',
 'Encephalomyelitis, Autoimmune, Experimental',
 'Leukoencephalitis, Acute Hemorrhagic',
 'Kernicterus',
 'Multiple Sclerosis',
 'Myasthenia Gravis',
 'Myelitis, Transverse',
 'Neuritis, Autoimmune, Experimental',
 'Neuromyelitis Optica',
 'Polyradiculoneuropathy',
 'Giant Cell Arteritis',
 'Uveomeningoencephalitic Syndrome',
 'AIDS Dementia Complex',
 'Lambert-Eaton Myasthenic Syndrome',
 'Stiff-Person Syndrome',
 'POEMS Syndrome',
 'Miller Fisher Syndrome',
 'Autoimmune Diseases of the Nervous System',
 'Guillain-Barre Syndrome',
 'Polyradiculoneuropathy, Chronic Inflammatory Demyelinating',
 'Demyelinating Autoimmune Diseases, CNS',
 'Vasculitis, Central Nervous System',
 'Multiple Sclerosis, Chronic Progressive',
 'Multiple Sclerosis, Relapsing-Remitting',
 'Myasthenia Gravis, Autoimmune, Experimental',
 'Nervous System Autoimmune Disease, Experimental',
 'Myasthenia Gravis, Neonatal',
 'AIDS Arteritis, Central Nervous System',
 'Lupus Vasculitis, Central Nervous System',
 'Mevalonate Kinase Deficiency',
 'Microscopic Polyangiitis',
 'Anti-N-Methyl-D-Aspartate Receptor Encephalitis']
Explain briefly in terms of biology/medicine what the above search has found: There are diseases that are associated with both the nervous system and the immune system, as the list listed above. For example, for Multiple Sclerosis, the autoimmune function fails and starts to attack myelin sheath which is critical for effective signal propagations from action potentials and provide great insulations to the axon, and therefore, in this case, both immune system and nervous system are involved, which is very reasonable for there two be treennumbers associated with both.

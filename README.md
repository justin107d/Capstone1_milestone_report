## Capstone 1 Milestone Report:

# A.)  Problem:

The way the US population grows and moves can have an interesting effect on various metrics that heavily depend on it.  This project focuses on the way the adult population behaves with the adult disability rate.

# B.) Client

The client would be various insurance companies that may on population growth data to forcast what premiums they should charge.  Reducing variance and having a more nuanced understanding of how risks will behave give these companies a competitive advantage over other competitors.

# C.) Data Wrangling and Cleaning:

1.)   SSA_data=SSA_data_dirt.drop('State Code'=='PR')
Dropped all the results from Puerto Rico, since there was hardly any information attachted to this state code

2.)  SSA_data['Date_numeric'] = pd.to_numeric(SSA_data['Date'])
Converted the year column from a datetime object to yearly for easier handling.

3.)  NH_1=SSA_data.loc[(SSA_data['State Code']=='NH ') & (SSA_data['Date_numeric']==2012),'Population age 18-64'].mean()
     NH_2=SSA_data.loc[(SSA_data['State Code']=='NH ') & (SSA_data['Date_numeric']==2014),'Population age 18-64'].mean()
     SSA_data.loc[(SSA_data['Date_numeric']==2013) & (SSA_data['State Code']=='NH '),'Population age 18-64'] = (NH_1+NH_2)/2

     NV_1=SSA_data.loc[(SSA_data['State Code']=='NV ') & (SSA_data['Date_numeric']==2012),'Population age 18-64'].mean()
     NV_2=SSA_data.loc[(SSA_data['State Code']=='NV ') & (SSA_data['Date_numeric']==2014),'Population age 18-64'].mean()
     SSA_data.loc[(SSA_data['Date_numeric']==2013) & (SSA_data['State Code']=='NV '),'Population age 18-64'] = (NV_1+NV_2)/2
NH and NV each had outliers that were far outside the rest of their state's data, so the points were replaced using linear interpolation to give points that were in line with a trend up or down.

4.)  atl=SSA_data.loc[SSA_data['Region Code']=='ATL']
     bos=SSA_data.loc[SSA_data['Region Code']=='BOS']
     chi=SSA_data.loc[SSA_data['Region Code']=='CHI']
     dal=SSA_data.loc[SSA_data['Region Code']=='DAL']
     den=SSA_data.loc[SSA_data['Region Code']=='DEN']
     kcm=SSA_data.loc[SSA_data['Region Code']=='KCM']
     nyc=SSA_data.loc[SSA_data['Region Code']=='NYC']
     phl=SSA_data.loc[SSA_data['Region Code']=='PHL']
     sea=SSA_data.loc[SSA_data['Region Code']=='SEA']
     sfo=SSA_data.loc[SSA_data['Region Code']=='SFO']
Separated regions into their own dataframes to simplify coding

5.)  AL=SSA_data.loc[SSA_data['State Code']=='AL ']
     FL=SSA_data.loc[SSA_data['State Code']=='FL ']
     GA=SSA_data.loc[SSA_data['State Code']=='GA ']
     KY=SSA_data.loc[SSA_data['State Code']=='KY ']
     MS=SSA_data.loc[SSA_data['State Code']=='MS ']
     NC=SSA_data.loc[SSA_data['State Code']=='NC ']
     SC=SSA_data.loc[SSA_data['State Code']=='SC ']
     TN=SSA_data.loc[SSA_data['State Code']=='TN ']
Separated ATL by state.

6.)  MA=SSA_data.loc[SSA_data['State Code']=='MA ']
     ME=SSA_data.loc[SSA_data['State Code']=='ME ']
     NH=SSA_data.loc[SSA_data['State Code']=='NH ']
     VT=SSA_data.loc[SSA_data['State Code']=='VT ']
     RI=SSA_data.loc[SSA_data['State Code']=='RI ']
     CT=SSA_data.loc[SSA_data['State Code']=='CT ']
Separated BOS by state.

7.)  IL=SSA_data.loc[SSA_data['State Code']=='IL ']
     IN=SSA_data.loc[SSA_data['State Code']=='IN ']
     MI=SSA_data.loc[SSA_data['State Code']=='MI ']
     MN=SSA_data.loc[SSA_data['State Code']=='MN ']
     OH=SSA_data.loc[SSA_data['State Code']=='OH ']
     WI=SSA_data.loc[SSA_data['State Code']=='WI ']
separated CHI by state.

8.)  AR=SSA_data.loc[SSA_data['State Code']=='AR ']
     LA=SSA_data.loc[SSA_data['State Code']=='LA ']
     NM=SSA_data.loc[SSA_data['State Code']=='NM ']
     OK=SSA_data.loc[SSA_data['State Code']=='OK ']
     TX=SSA_data.loc[SSA_data['State Code']=='TX ']
Separated DAL by state.
     
9.)  CO=SSA_data.loc[SSA_data['State Code']=='CO ']
     MT=SSA_data.loc[SSA_data['State Code']=='MT ']
     ND=SSA_data.loc[SSA_data['State Code']=='ND ']
     SD=SSA_data.loc[SSA_data['State Code']=='SD ']
     UT=SSA_data.loc[SSA_data['State Code']=='UT ']
     WY=SSA_data.loc[SSA_data['State Code']=='WY ']
Separated DEN by state.
     
10.) IA=SSA_data.loc[SSA_data['State Code']=='IA ']
     KS=SSA_data.loc[SSA_data['State Code']=='KS ']
     MO=SSA_data.loc[SSA_data['State Code']=='MO ']
     NE=SSA_data.loc[SSA_data['State Code']=='NE ']
Separated KCM by state.

11.) NJ=SSA_data.loc[SSA_data['State Code']=='NJ ']
     NY=SSA_data.loc[SSA_data['State Code']=='NY ']
Separated NYC by state.

12.) DC=SSA_data.loc[SSA_data['State Code']=='DC ']
     DE=SSA_data.loc[SSA_data['State Code']=='DE ']
     MD=SSA_data.loc[SSA_data['State Code']=='MD ']
     PA=SSA_data.loc[SSA_data['State Code']=='PA ']
     VA=SSA_data.loc[SSA_data['State Code']=='VA ']
     WV=SSA_data.loc[SSA_data['State Code']=='WV ']
Separated PHL by state.

13.) AK=SSA_data.loc[SSA_data['State Code']=='AK ']
     ID=SSA_data.loc[SSA_data['State Code']=='ID ']
     OR=SSA_data.loc[SSA_data['State Code']=='OR ']
     WA=SSA_data.loc[SSA_data['State Code']=='WA ']
Separated SEA by state.

14.) AZ=SSA_data.loc[SSA_data['State Code']=='AZ ']
     CA=SSA_data.loc[SSA_data['State Code']=='CA ']
     HI=SSA_data.loc[SSA_data['State Code']=='HI ']
     NV=SSA_data.loc[SSA_data['State Code']=='NV ']
Separated SFO by state.

15.) SA_agg = SSA_data.groupby(['Region Code','Date_numeric'])['Population age 18-64'].mean()
Grouped population by year and plotted by region.  

16.) SSA_agg = SSA_data.groupby(['Region Code','Date_numeric'])['Percent of Adult Population Receiving SSA Adult Disability Benefits'].mean()
Grouped those receiving disability by year and plotted by region.

# D.) Other Potential Data Sets:

The data did not nessessarily have to come from the Social Security Administration, it could have come from a wide variety of sources.  
This set is already tidied up and gives us exactly what we need to solve the problem.

Data source:  https://catalog.data.gov/dataset/ssa-disability-claim-data
Further information is provided at: https://www.ssa.gov/disability/data/ssa-sa-fywl.htm#TechnicalDocumentation 

# E.) Initial Findings:

Itialially found that population growth bewteen both states and regions was highly corelated with one another.  There were few states that displayed trend that were counter to the rest of the data set.  There were also a few outliers in 2013 that were not explained in the supporting documentation.  


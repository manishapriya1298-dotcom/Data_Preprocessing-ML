# Data_Preprocessing-ML

import pandas as pd  
df=pd.read_csv("file_path.csv")  
**To verify the datatypes of columns**  
df.info()  
**To change the datatype Date and Time**  
df['DATE_SALE']=pd.todate_time(df['DATE_SALE'],format="%d-%m-%Y")  
df['DATE_BUILD']=pd.todate_time(df['DATE_BUILD'],format="%d-%m-%Y")  
**To find the columns with null values**  
df.isna().sum() #N_BEDROOM N_BATHROOM QS_OVERALL has null values  
**To change the null values in N_BEDROOM N_BATHROOM to 0**  
df['N_BEDROOM'].fillna(0,inplace=True)  
df['N_BATHROOM'].fillna(0,inplace=True)  
**To change the null values in QS_OVERALL**    
cal=["QS_ROOMS","QS_BATHROOM","QS_BEDROOM"]  
def a(i):  
 if pd.isna(i['QS_OVERALL']):  
  return i[cal].mean()  
 else:    
  return i['QS_OVERALL']  
df['QS_OVERALL']=df.apply(a,axis=1)# axis=1 to verify  columnwise  
**To deal with the spelling mistakes**  
df["AREA"]=df["AREA"].replace({"Ana Nagar":"Anna Nagar", "Ann Nagar":"Anna Nagar","Adyr":"Adyar","TNagar":"T Nagar","Karapakam":"Karapakkam","Velchery":"Velachery","KKNagar":"KK Nagar"
                               "Chrompt":"Chrompet",
                               "Chrmpet":"Chrompet",
                               "Chormpet":"Chrompet",
                              })   
df["SALE_COND"]=df["SALE_COND"].replace({"Ab Normal":"AbNormal","Partiall":"Partial","PartiaLl":"Partial","Adj Land":"AdjLand"})   
df["PARK_FACIL"]=df["PARK_FACIL"].replace({"Noo":"No"})   
df["BUILDTYPE"]=df["BUILDTYPE"].replace({"Comercial":"Commercial","Others":"Other"})   
df["UTILITY_AVAIL"]=df["UTILITY_AVAIL"].replace({"AllPub":"All Pub","NoSewr ":"No sewage"})    

**To change the complete data to numerics**   
from sklearn.preprocessing import LabelEncoder  
encode= LabelEncoder()  
for j in df.select_dtypes(include="object").columns:  
  df[j]=encode.fit_transform(df[j])  
**To get a copy of the final data**  
df.to_csv("House.csv")   




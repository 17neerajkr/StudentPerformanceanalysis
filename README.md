DAY 1 : UNDERSTOOD THAT DATA SET AND CLEANING THAT DATA BY USING AN PANDAS 


  

    

      
1

      
Load your data
Always the first step

    

    

      

        # import pandas library

        import pandas as pd


        # load your csv file

        df = pd.read_csv("your_file.csv")
      

    

  


  

    

      
2

      
Explore your data
Understand what you have before cleaning

    

    

      

        # see first 5 rows

        df.head()


        # see shape — (rows, columns)

        print(df.shape)


        # see column names and data types

        df.info()


        # see statistics summary

        df.describe()
      

    

  


  

    

      
3

      
Find and fix missing values
Rows with empty/blank cells

    

    

      

        # count missing values per column

        df.isnull().sum()


        # option 1 — remove rows with missing values

        df = df.dropna()


        # option 2 — fill missing with average

        df = df.fillna(df.mean())


        # verify — should show 0

        print(df.isnull().sum().sum())
      

    

  


  

    

      
4

      
Find and fix duplicate rows
Rows that appear more than once

    

    

      

        # count duplicate rows

        print(df.duplicated().sum())


        # remove duplicate rows

        df = df.drop_duplicates()


        # verify — should show 0

        print(df.duplicated().sum())
      

    

  


  

    

      
5

      
Fix column names
Make names clean and consistent

    

    

      

        # make all column names lowercase

        df.columns = df.columns.str.lower()


        # remove spaces from column names

        df.columns = df.columns.str.replace(" ", "_")


        # see all column names

        print(df.columns)
      

    

  


  

    

      
6

      
Fix data types
Make sure numbers are numbers, dates are dates

    

    

      

        # check data types

        df.dtypes


        # convert a column to number

        df["column"] = pd.to_numeric(df["column"])


        # convert a column to date

        df["date"] = pd.to_datetime(df["date"])
      

    

  


  

    

      
7

      
Final check — data is clean!
Verify everything before analysis

    

    

      

        # check shape — rows should be less

        print(df.shape)


        # check no missing values

        print(df.isnull().sum().sum())


        # check no duplicates

        print(df.duplicated().sum())


        # save clean data to new file

        df.to_csv("clean_data.csv", index=False)
      

    

  





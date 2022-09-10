# election_analysis_challenge
#Colorado Pilot County Election Analysis 

##Overview of Election Audit:
The purpose of this analysis project is to build a proof of concept into automatically counting and tallying voting results. 
The initial scope of the audit was for 3 counties within Colorado during the latest elections.  The project was scoped to calculate the number of votes per county and percentage of total votes for that county.  Additionally, the project also was to 
include a listing of each candidate, their number of votes and percentage of the total of votes.  

##Election Audit Results 
* How many votes were cast in this congressional election? 
    - The total number of votes cast was: 369,711
* Which county had the largest number of votes? 
    - Denver County 
    - Total Voter Turnout: 306,055
* Candidate breakdown 
    - Charles Casper Stockham: 23.0% (85,213)
    - Diana DeGette: 73.8% (272,892)
    - Raymon Anthony Doane: 3.1% (11,606)
* Election results 
    - Winner: Diana DeGette
    - Vote Count: 272,892
    - Percentage of Total: 73.8%

##Election Audit Summary 
For the provided dataset, the pilot program returned accurate information and correctly declared the winner of the election.  It 
is expected that with minimal modifications, this script could be used for any election. 

Currently, the program is built to look for a particular file in a specific location.  
~~~~
# Add a variable to load a file from a path.
file_to_load = os.path.join("resources", "election_results.csv")
# Add a variable to save the file to a path.
file_to_save = os.path.join("analysis", "election_analysis.txt")
~~~~
If election boards throughout the state (or country) would need to utilize this tool, it would be better for them to identify 
where their files are stored to read from.  Research on Stackoverflow.com (https://stackoverflow.com/questions/22939211/what-is-the-proper-way-to-take-a-directory-path-as-user-input) shows that code similar to the below example can be implemented to allow users to specify their source file and location:

~~~~~
str =""       #initializing string variable for raw data input

#print os.getcwd()
#f = open("C:/Users/larece.johnson/Desktop/BostonLog.log.2014-04-02.log","r+")

str = raw_input("Enter the name of your text file - please use / backslash when typing in directory path: ");  #User will enter the name of text file for me

f = open(str,"r+")
~~~~~

Additionally, for this to scale and allow remote election boards the ability to create and save their own results files, it would be necessary to create unique file names when the file is created, rather than writing to a common file. (This could 
potentially introduce the risk of overwriting another board's data).  This can be implemented by using the functions in the UUID
library. (https://www.pythoneasy.com/learn/python-how-to-create-a-unique-file-name-in-python)

An example of the code that could be implemented is below: 
~~~~
import uuid

print("Enter your Election Board name:") #prompts the user to enter election board name on the terminal

election_board = input() #initializes the election_board variable 

unique_filename = str(uuid.uuid4())

output_file_message = (
    f"\n Output File Name\n"
    f"----------------------\n"
    f"Your output file is named {election_board}{unique_filename}\n"
    f"The file can be downloaded from the //analysis directory\n"
    f"----------------------\n"
)
print(output_file_message) #this will display the file name to the terminal
~~~~

In order to reduce 'wait' time for the file to generate, it could also be possible to have the system modified to mail files to individuals at each county election board.  This is functionality that is 
available through external libraies such as smtplib (https://docs.python.org) as well as through integrations with commercial emailing products.  That is currently outside of the scope of this project's
requirements, and it is recommended that a stand alone project be considered to implement email notifications correctly. 

For larger elections, the number of votes will increase dramatically (as well as numbers of counties and candidates included). It is recommended that performance and load testing be done against this code with expected levels of data prior to releasing to the election boards.  The total number of votes for just the coordinated off year state elections was 1,557,457 votes.  Dependent on the election cycle, and what initiatives are being presented for voting may drive higher voter turnout.  It is essential to ensure that
the application is able to handle inbound data, outbound results, and analysis processing as efficiently as possible. 
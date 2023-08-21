# nosql-challenge

This challenge is about importing the data, updating the uk_food nosql database, and performing exploratory analysis queries on the database.

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. The editors of a food magazine, Eat Safe, Love, wants us to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

Following are the step-by-step descriptions on the written code.

### Part 1: Database and Jupyter Notebook Set Up

NoSQL_setup_starter.ipynb is used for this section of the challenge. 

1. Imported the data provided in the establishments.json file from the Terminal. Named the database uk_food and the collection establishments. 

2. Imported the needed libraries: PyMongo and Pretty Print (pprint).

3. Created an instance of the Mongo Client.

4. Confirmed that the code created the database and loaded the data properly:
	- Listed the databases created have in MongoDB. Confirmed that uk_food is listed.
	- Listed the collection(s) in the database to ensure that establishments is there.
	- Found and displayed one document in the establishments collection using find_one and display with pprint.

5. Assigned the establishments collection to a variable to prepare the collection for use.

### Part 2: Update the Database
Used NoSQL_setup_starter.ipynb for this section of the challenge.

The magazine editors have some requested modifications for the database before we can perform any queries or analysis for them. Made the following changes to the establishments collection:

1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following information to the database:

`{
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}`

2. Found the BusinessTypeID for "Restaurant/Cafe/Canteen" and returned only the BusinessTypeID and BusinessType fields.

3. Updated the new restaurant with the BusinessTypeID found.

4. The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Removed any establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted.

5. Some of the number values are stored as strings, when they should be stored as numbers.

	- Used update_many to convert latitude and longitude to decimal numbers.
	- Used update_many to convert RatingValue to integer numbers.


### Part 3: Exploratory Analysis

Eat Safe, Love has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Used NoSQL_analysis_starter.ipynb for this section of the challenge.

RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We will coerce non-numeric values to nulls during the database setup before converting ratings to integers.
The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.

Used the given instructions to find these results.

- Use count_documents to display the number of documents contained in the result.

- Display the first document in the results using pprint.

- Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

1. Which establishments have a hygiene score equal to 20?

2. Which establishments in London have a RatingValue greater than or equal to 4?

3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.




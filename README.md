# AirBnB MongoDB Analysis

#### Anas Moazzam

## Dataset Details

### Original Data
I sourced the data in this assignment from [Inside Airbnb](https://insideairbnb.com/get-the-data/), where data on Airbnb listings sorted by location can be accessed. Specfically in my case, the data provides information on listings in San Francisco, US. Some relevant pieces of data includes information on the host, the neighborhood, average ratings, the number of bed etc. The original form of this data was accessed as a [CSV file](https://github.com/dbdesign-students-spring2024/6-mongodb-analysis-anasmzzm/blob/main/data/listings.csv).

Here is some of the original data:

| id       | listing_url                                             | scrape_id  | last_scraped | source          | name                                               | description                                                                                                                                                                                                                                                                                                                       | ...  |
|----------|---------------------------------------------------------|------------|--------------|-----------------|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| 1094764  | [https://www.airbnb.com/rooms/1094764](https://www.airbnb.com/rooms/1094764) | 2.02403E+13 | 3/7/2024     | city scrape     | San Francisco Presidio Paradise!                  |                                                                                                                                                                                                                                                                                                                                   | ... |
| 38047206 | [https://www.airbnb.com/rooms/38047206](https://www.airbnb.com/rooms/38047206) | 2.02403E+13 | 3/7/2024     | previous scrape | 52 Vesta home                                      |                                                                                                                                                                                                                                                                                                                                   | ... |
| 43475468 | [https://www.airbnb.com/rooms/43475468](https://www.airbnb.com/rooms/43475468) | 2.02403E+13 | 3/7/2024     | previous scrape | Beautiful Mission District Home and Backyard       | Beautiful entire first floor of home with backyard in the sunny Mission District. Large studio, living room, and kitchen, washer and dryer included. Five minute walk to restaurants.                                                                                                                                 | ... |
| 6.4855E+17 | [https://www.airbnb.com/rooms/648549709021440854](https://www.airbnb.com/rooms/648549709021440854) | 2.02403E+13 | 3/7/2024     | city scrape     | LuxoStays \| ! Quiet Rm #Private Bathrm & VIEW    | This house is well-maintained, and has upgraded furnishings!<br /> <br />Conveniently located, this spacious apartment is only a couple of blocks from restaurants of different cuisines, grocery stores, farmers' markets and other stores that you'll need! <br /> <br />The nearest bus stop is 10 minutes away from the property and will take you. John McLaren Park is just a 5-minutes drive from our home.<br /> <br />Longer inquiries are very welcome. Inquire even if the calendar is blocked off. | ... |
| 47918229 | [https://www.airbnb.com/rooms/47918229](https://www.airbnb.com/rooms/47918229) | 2.02403E+13 | 3/7/2024     | city scrape     | Blueground \| Marina District, w/d, nr parks      | Feel at home wherever you choose to live with Blueground. You’ll love this stylish Marina District furnished two-bedroom apartment with its modern decor, fully equipped kitchen, and pretty living room. Ideally located, you’re close to all the best that San Francisco has to offer! (ID #SFO434)                                        | ... |
| 9.38317E+17 | [https://www.airbnb.com/rooms/938317240177880784](https://www.airbnb.com/rooms/938317240177880784) | 2.02403E+13 | 3/7/2024     | city scrape     | Presidio Heights Condo - 2bdrm/2 bath              | Relax in very well appointed two bedroom/two bath condo with incredible views in safe, quiet Presidio Heights neighborhood, conveniently located near Laurel Village shopping center and top rated restaurants.                                                                                                            | ... |
| 24823466 | [https://www.airbnb.com/rooms/24823466](https://www.airbnb.com/rooms/24823466) | 2.02403E+13 | 3/7/2024     | city scrape     | Live like a local in the heart of the City        | Stay and live in our home in Duboce Triangle while we are away this Summer. <br />Perfect place for someone who wants to relocate wants to explore the city or needs to find a permanent place in the Bay Area.                                                                                                               | ... |
| 53849558 | [https://www.airbnb.com/rooms/53849558](https://www.airbnb.com/rooms/53849558) | 2.02403E+13 | 3/7/2024     | city scrape     | Stunning 1-Bedroom Loft in Clock Tower Building   | Live like a local while residing in an iconic San Francisco landmark! Anyone who has driven across the Bay Bridge from SF to Oakland has seen the City’s most visible and historic Clock Tower building off to the right; a building that once housed the largest printing company on the West coast.                                                       | ... |
| 20077154 | [https://www.airbnb.com/rooms/20077154](https://www.airbnb.com/rooms/20077154) | 2.02403E+13 | 3/7/2024     | city scrape     | SF private room r                                  | Small room in a quiet house with own lock and key.<br /><br />Share common area, kitchen and bathroom with Airbnb guest. Host does not use them.<br /><br />This an old 1900's house with uneven heights. If you are on the taller side, please reconsider a different location. <br /><br />Bathroom is small; if you are large or tall please reconsider. <br /><br />The neighborhood is quiet with the occasional dog walkers. <br /><br />Next to the spacious Balboa Park and police station. <br /><br />Next to bus J,K,M to downtown. 29, 49, BART.                                                                                                                                                                                                                                             | ... |
| 30774802 | [https://www.airbnb.com/rooms/30774802](https://www.airbnb.com/rooms/30774802) | 2.02403E+13 | 3/7/2024     | city scrape     | Modern New place & furnished for Long term stay   | Modern, high-end remodeled entire guest house in law in the warmest neighborhood in San Francisco city.  Few minutes get attractions spot/medical/schools.  Bedroom C will be available on 10/8/2023<br />With very low rate you can peremptorily own your comforting place.  High ceiling; comfortable living. Kitchen-stove, microwave, refrigerator.  Easy free street parking.  Very safe residential neighborhood. Amenity limitation Laundry and washer, fee$5. Please email me confirm room availability-booking.                                                                                      | ... |
| 415498   | [https://www.airbnb.com/rooms/415498](https://www.airbnb.com/rooms/415498) | 2.02403E+13 | 3/7/2024     | city scrape     | Prime Location - Studio Apartment                  | Centrally located near  Polk  and Fillmore Streets , close to the greenery of Lafayette Park,  walk  to the many attractions of San Francisco from this functional studio.                                                                                                                                                                                                                 | ... |
| 24491303 | [https://www.airbnb.com/rooms/24491303](https://www.airbnb.com/| 24491303 | [https://www.airbnb.com/rooms/24491303](https://www.airbnb.com/rooms/24491303) | 2.02403E+13 | 3/7/2024     | city scrape     | SoMa Retreat                                      | Are you bored at Downtown SF’s small hotel rooms near the convention center? Are you exploring SF for the first time? Stay with this married DINK queer couple's place for an awesome retreat! 2SLGBTQIA+ friendly! Free Unlimited Latte! <br /><br />Conveniently located in the heart of SoMa, you will have your own private bedroom and private bathroom. <br /><br />You might have to share the living space with us but we are two working professionals that likely won’t be around too much.                                                                                           | ... |
| 7.2548E+17 | [https://www.airbnb.com/rooms/725479609346985276](https://www.airbnb.com/rooms/725479609346985276) | 2.02403E+13 | 3/7/2024     | city scrape     | 546D - Large Master Bedroom w/ Private Bath Fits 4 | South side of town in sunny micro-climate neighborhood of SF, near Balboa Park Bart station, near City College of San Francisco. Close to highway arteries going southbound or towards downtown.<br /><br />** This property hosts by a team of professional Co-hosting the large number listings in San Francisco Bay Area.  <br />*** Guest pleasure experience is our only goal!                                                                                                                                                                           | ... |
| 3442439  | [https://www.airbnb.com/rooms/3442439](https://www.airbnb.com/rooms/3442439) | 2.02403E+13 | 3/7/2024     | city scrape     | Spacious Bernal Heights In-law with private entry. | Spacious studio with separate keypad access. Contemporary space with radiant floor heat, wifi, television (Netflix/Amazon Prime) and deck/yard access. Located within walking distance of great shopping in Bernal Heights, Noe Valley, Glen Park, and the Mission districts. 1/2 block to public transportation and beautiful Holly Park. <br /><br />Kitchenette includes mini-fridge, microwave, toaster oven, electric kettle, and filtered water.<br /><br />There is street parking with no meters to worry about.                                                                                | ... |
| 53747035 | [https://www.airbnb.com/rooms/53747035](https://www.airbnb.com/rooms/53747035) | 2.02403E+13 | 3/7/2024     | city scrape     | Blueground \| Rincon Hill, gym & lounge, nr shops | Show up and start living from day one in San Francisco with this lovely one-bedroom Blueground apartment. You’ll love coming home to this thoughtfully furnished, beautifully designed, and fully-equipped Rincon Hill home. (ID #SFO763)                                                                                                                                                               | ... |
| 2802480  | [https://www.airbnb.com/rooms/2802480](https://www.airbnb.com/rooms/2802480) | 2.02403E+13 | 3/7/2024     | city scrape     | Marina Modern 2BR (30 day min)                    | Pristine contemporary flat just steps from Chestnut Street. Strikingly furnished, complete with chef's kitchen. Ideal location in arguably the most desirable neighborhood of San Francisco.                                                                                                                                                                                                         | ... |
| 48955947 | [https://www.airbnb.com/rooms/48955947](https://www.airbnb.com/rooms/48955947) | 2.02403E+13 | 3/7/2024     | city scrape     | Classic Pac Hts 1bd Victorian meets SF. Pet ok*   | Newly listed and available! <br />Delightful, light-filled 1bdm/1ba on a flat tree lined street that is centrally located in Pacific Heights! 1906 Queen Anne Victorian with soaring 11ft ceiling. Period charm combined with many modern upgrades for today's needs! Walkscore 98!                                                                                                                     | ... |
| 25376401 | [https://www.airbnb.com/rooms/25376401](https://www.airbnb.com/rooms/25376401) | 2.02403E+13 | 3/7/2024     | city scrape     | Cheerful Suite w/ Garden, Steps from Dolores Park | Private, clean, and cozy ensuite in Dolores Heights, one of the most sought after neighborhoods in San Francisco (Mark Zuckerburg's house is two blocks away):<br />Private: Entrance, Bedroom, & Spacious Bathroom<br />Shared: Deck and Garden<br />Heart of Castro <br />30 sec walk to Dolores Park, <br />5 min walk to Mission District, <br />7 min ride to downtown, <br />27 min ride to SFO<br />KEYLESS ENTRY<br />97 walk score; 89 transit score                                                       | ... |
| 53835580 | [https://www.airbnb.com/rooms/53835580](https://www.airbnb.com/rooms/53835580) | 2.02403E+13 | 3/7/2024     | city scrape     | Studio with Balcony & Stunning Bay Bridge View    | You will wake up to an amazing sunrise over the bay. Bright & spacious studio with balcony view of the Bay. Centrally located.<br />Quite neighborhood but only two blocks away from all the actions.                                                                                                                                                                                   | ... |
| 40490045 | [https://www.airbnb.com/rooms/40490045](https://www.airbnb.com/rooms/40490045) | 2.02403E+13 | 3/7/2024     | city scrape     | Queen bedroom by BART subway                       | Private queen bedroom in a quiet home. <br />Located in a family friendly neighborhood by CCSF, Balboa Park BART subway stop.<br />The bedroom has a queen bed, desk, TV, dresser, closet. Big windows with city views.<br />Shared the living room & kitchen with 2 working professionals.  <br />Living room has a sofa and TV.<br />The kitchen has a stove, oven, dishwasher, fridge, microwave. <br /><br />Walk 2 blocks to  CCSF, BART subway for a quick 15 mins ride to SOMA , financial district.<br />Walk 4 blocks to Whole Foods & restaurants.                                                            | ... |

### Data Scrubbing
 I decided that there was some data scrubbing necessary to properly do my MongoDB analysis. I used Python and Pandas, found in the [data_scrubbing notebook](https://github.com/dbdesign-students-spring2024/6-mongodb-analysis-anasmzzm/blob/main/data_scrubbing.ipynb), to carry out my preprocessing. Here are some of the changes I made:
- Got rid of unnecessary columns to reduce bulk and kept only the columns necessary to my analysis
- I verified that dropping all rows with NaN values would leave me with enough columns to carry out analysis and continued to drop any row with NaN values. I acknowledge, however, that this is not best practice if we were to be doing serious data science analysis.
- The neighbourhood column had lenghty and repetitive labels. I decided to make them more concise. For instance, "San Francisco, California, US" would just become "San Francisco".
- Finally, the price column was technically a string. I removed the $ sign from the prices and turned them into float data types.

Here is some of the cleaned data:
| id       | name                                                   | host_id   | host_name    | host_is_superhost | neighbourhood | price | beds | review_scores_rating |
|----------|--------------------------------------------------------|-----------|--------------|-------------------|---------------|-------|------|----------------------|
| 6.4855E+17 | LuxoStays | ! Quiet Rm #Private Bathrm & VIEW | 226555948 | Gi'Angelo    | f                 | San Francisco | 69    | 1    | 5                    |
| 9.38317E+17 | Presidio Heights Condo - 2bdrm/2 bath             | 51769509  | Turner       | t                 | San Francisco | 328   | 2    | 4.83                 |
| 53849558 | Stunning 1-Bedroom Loft in Clock Tower Building     | 3793516   | Audrey       | t                 | San Francisco | 175   | 1    | 4.86                 |
| 30774802 | Modern New place & furnished for Long term stay     | 230265204 | Athena       | t                 | San Francisco | 40    | 3    | 4.85                 |
| 3442439  | Spacious Bernal Heights In-law with private entry   | 17349647  | Candace And Joshua | t            | San Francisco | 125   | 1    | 4.96                 |
| 2802480  | Marina Modern 2BR (30 day min)                      | 14333760  | Alessandra   | f                 | San Francisco | 285   | 2    | 4.76                 |
| 48955947 | Classic Pac Hts 1bd Victorian meets SF. Pet ok*     | 91488071  | Dan And Jan  | t                 | San Francisco | 125   | 1    | 4.7                  |
| 25376401 | Cheerful Suite w/ Garden, Steps from Dolores Park    | 113405017 | Russell      | t                 | San Francisco | 208   | 1    | 4.95                 |
| 53835580 | Studio with Balcony & Stunning Bay Bridge View       | 25416774  | Maryam       | t                 | San Francisco | 155   | 1    | 5                    |
| 21596397 | Take it Easy on Potrero Hill                        | 4718164   | Serena Leilani | t               | San Francisco | 110   | 1    | 4.88                 |



## Analysis

1. show exactly two documents from the listings collection in any order

```mongodb
db.listings_clean.find().limit(2)
```

```mongodb
[
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a3'),
    id: Long('648549709021440854'),
    name: 'LuxoStays | ! Quiet Rm #Private Bathrm & VIEW',
    host_id: 226555948,
    host_name: "Gi'Angelo",
    host_is_superhost: false,
    neighbourhood: 'San Francisco',
    price: 69,
    beds: 1,
    review_scores_rating: 5
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a4'),
    id: Long('938317240177880784'),
    name: 'Presidio Heights Condo - 2bdrm/2 bath',
    host_id: 51769509,
    host_name: 'Turner',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 328,
    beds: 2,
    review_scores_rating: 4.83
  }
]
```

Essentially, this query returns two documents. There is no criteria or projection so the query will return all data included in the documents. This makes understanding the relationship between the columns and each datapoint much easier than compared to the raw data.

2. show exactly 10 documents in any order, but "prettyprint" in easier to read format, using the pretty() function.

```mongodb
 db.listings_clean.find().limit(10).pretty()
 ```

 ```mongodb
[
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a3'),
    id: Long('648549709021440854'),
    name: 'LuxoStays | ! Quiet Rm #Private Bathrm & VIEW',
    host_id: 226555948,
    host_name: "Gi'Angelo",
    host_is_superhost: false,
    neighbourhood: 'San Francisco',
    price: 69,
    beds: 1,
    review_scores_rating: 5
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a4'),
    id: Long('938317240177880784'),
    name: 'Presidio Heights Condo - 2bdrm/2 bath',
    host_id: 51769509,
    host_name: 'Turner',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 328,
    beds: 2,
    review_scores_rating: 4.83
  }
]
airbnb> db.listings.find().limit(10).pretty()

airbnb> db.listings_clean.find().limit(10).pretty()
[
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a3'),
    id: Long('648549709021440854'),
    name: 'LuxoStays | ! Quiet Rm #Private Bathrm & VIEW',
    host_id: 226555948,
    host_name: "Gi'Angelo",
    host_is_superhost: false,
    neighbourhood: 'San Francisco',
    price: 69,
    beds: 1,
    review_scores_rating: 5
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a4'),
    id: Long('938317240177880784'),
    name: 'Presidio Heights Condo - 2bdrm/2 bath',
    host_id: 51769509,
    host_name: 'Turner',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 328,
    beds: 2,
    review_scores_rating: 4.83
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a5'),
    id: 53849558,
    name: 'Stunning 1-Bedroom Loft in Clock Tower Building',
    host_id: 3793516,
    host_name: 'Audrey',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 175,
    beds: 1,
    review_scores_rating: 4.86
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a6'),
    id: 30774802,
    name: 'Modern New place & furnished  for Long term stay',
    host_id: 230265204,
    host_name: 'Athena',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 40,
    beds: 3,
    review_scores_rating: 4.85
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a7'),
    id: 3442439,
    name: 'Spacious Bernal Heights In-law with private entry.',
    host_id: 17349647,
    host_name: 'Candace And Joshua',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 125,
    beds: 1,
    review_scores_rating: 4.96
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a8'),
    id: 2802480,
    name: 'Marina Modern 2BR (30 day min)',
    host_id: 14333760,
    host_name: 'Alessandra',
    host_is_superhost: false,
    neighbourhood: 'San Francisco',
    price: 285,
    beds: 2,
    review_scores_rating: 4.76
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5a9'),
    id: 48955947,
    name: 'Classic Pac Hts 1bd Victorian meets SF. Pet ok*',
    host_id: 91488071,
    host_name: 'Dan And Jan',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 125,
    beds: 1,
    review_scores_rating: 4.7
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5aa'),
    id: 25376401,
    name: 'Cheerful Suite w/ Garden, Steps from Dolores Park',
    host_id: 113405017,
    host_name: 'Russell',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 208,
    beds: 1,
    review_scores_rating: 4.95
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5ab'),
    id: 53835580,
    name: 'Studio with Balcony & Stunning Bay Bridge View',
    host_id: 25416774,
    host_name: 'Maryam',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 155,
    beds: 1,
    review_scores_rating: 5
  },
  {
    _id: ObjectId('660e317abf61e9a36c3ac5ac'),
    id: 21596397,
    name: 'Take it Easy on Potrero Hill',
    host_id: 4718164,
    host_name: 'Serena Leilani',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 110,
    beds: 1,
    review_scores_rating: 4.88
  }
]
```

This query is similar to that in Question 1. If the raw data was much more dense, then this data would be much easier to read compared to the raw data due to the pretty() function.

3. choose two hosts (by reffering to their host_id values) who are superhosts (available in the host_is_superhost field), and show all of the listings offered by both of the two hosts
    - only show the name, price, neighbourhood, host_name, and host_is_superhost for each result

I first find two hosts that are superhosts.
```mongodb
db.listings_clean.find({ "host_is_superhost": true }, { "host_id": 1 }).limit(2)
```

```mongodb
[
  { _id: ObjectId('660e317abf61e9a36c3ac5a4'), host_id: 51769509 },
  { _id: ObjectId('660e317abf61e9a36c3ac5a5'), host_id: 3793516 }
]
```
This tells me that hosts with ID 51769509 and ID 3793516 are superhosts.

Next, I find all the listings from these superhosts and only include the price, neighbourhood, host_name.

```mongodb
db.listings_clean.find({host_is_superhost:true, "host_id": { $in: [51769509, 3793516] }},{"name": 1, "price": 1, "neighbourhood": 1, "host_name": 1, "host_is_superhost": 1, "_id": 0})
```

```mongodb
[
  {
    name: 'Presidio Heights Condo - 2bdrm/2 bath',
    host_name: 'Turner',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 328
  },
  {
    name: 'Stunning 1-Bedroom Loft in Clock Tower Building',
    host_name: 'Audrey',
    host_is_superhost: true,
    neighbourhood: 'San Francisco',
    price: 175
  }
]
```

To answer this question, I first had to find two superhosts. The first query looks for the first two superhosts in the data and returns their host_id. The following query had one criteria which would limit the listings to the specific host_id I wanted. It also contained a projection which limited the fields to name, price, neighbourhood, host_name, and host_is_superhost. This allows us to see that Turner and Audrey only have one Airbnb, but ran it well enough to be superhosts.


4. find all the unique host_name values (see the docs)
```mongodb
db.listings_clean.distinct("host_name")
```

```mongodb
[
  '1906 Mission',     'AC And Linda',      'Aaron',
  'Abel',             'Abhay',             'Abhi',
  'Ac',               'Ada',               'Adam',
  'Adam&Roz',         'Adamjake',          'Adrian',
  'Adriana',          'Ahmad',             'Ahmed',
  'Aida',             'Aidan',             'Aiden',
  'Aileen',           'Air Concierge',     'Aisling',
  'Aj',               'Akshay',            'Al',
  'Alan',             'Albert',            'Albina',
  'Ale',              'Alejandro (Alex)',  'Alek',
  'Alekhya',          'Aleksandra',        'Alene',
  'Alessandra',       'Alex',              'Alex & Daniel',
  'Alex & Lina',      'Alexia',            'Alice',
  'Alice & Ahmed',    'Alice/Peter',       'Alireza',
  'Alison',           'Alissa',            'Aljosha',
  'Allen',            'Allen Palomino &',  'Allison',
  'Alvaro',           'Alyssa',            'Amanda',
  'Amber',            'Ambrish',           'Ame',
  'Amelie',           'Amina And Olivier', 'Amir',
  'Amir Hossein',     'Amit',              'Amol',
  'Amsi',             'Amy',               'Amy& Michael',
  'Ana',              'Andi',              'Andre',
  'Andrea',           'Andrea & Luong',    'Andreas',
  'Andrew',           'Andy',              'Angela',
  'Angeline',         'Angelo',            'Angie',
  'Ani',              'Anil',              'Anirudh',
  'Anita',            'Anjali',            'Anjanette',
  'Anka',             'Ann',               'Anna',
  'Anna & Irene',     'Anna & Michael',    'Anne',
  'Annekarin',        'Annette',           'Annie',
  'Anniechen',        'Annria',            'Ant',
  'Antelope',         'Anthony',           'Anthony & Ava',
  'Antigone',         'Antoine',           'Antoni',
  'Antonia And Nick',
  ... 1312 more items
]
```

This query lists only unique host names so that names are not repeated. This would allow someone to see the individual names of Airbnb owners in San Francisco which can lead to interesting demographic analysis or equity analysis.

5. find all of the places that have more than 2 beds in a neighborhood of your choice (referred to as either the neighborhood or neighbourhood_group_cleansed fields in the data file), ordered by review_scores_rating descending
    - only show the name, beds, review_scores_rating, and price
    - if your data set only has blanks for all the neighborhood-related fields, or only one neighborhood value in all documents, you may pick another field to filter by - include an explanation and justification for this in your report.
    - if you run out of memory for this query, try filtering review_scores_rating that aren't empty ($ne); and lastly, if there's still an issue, you can set the beds to match exactly 2.

As I've cleaned the data to clean the 'neighbourhood' column, I know there are three neighborhoods in the listings: the general San Francisco area, Noe Valley, and Hayes Valley. I initially tried to do the two Valley neighborhoods, but perhaps due to my data scrubbing techniques, there wasn't any listings that met the criteria. I switched my focus to the general San Francisco area.

```mongodb
db.listings_clean.find({neighbourhood: "San Francisco", beds:{$gt:2}}, {_id:0, name:1, beds:1, review_scores_rating:1, price:1}).sort({"review_scores_rating":-1})
```

```mongodb
[
  {
    name: 'Spacious Luxury 2BD Loft in Downtown San Francisco',
    price: 250,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Gorgeous Seaside View Home w Deck, Piano',
    price: 294,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Chic Urban Oasis with Views near Bernal Peak',
    price: 327,
    beds: 7,
    review_scores_rating: 5
  },
  {
    name: '2+BR Noe Valley Home w/ Garden',
    price: 140,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Wyndham Canterbury Resort | 2BR/1BA Queen Suite',
    price: 262,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Wyndham Canterbury Resort | 2BR/1BA Queen Suite',
    price: 262,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: '3BR Family Home in Cole Valley',
    price: 395,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Telegraph Hill Shangri-La',
    price: 697,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: '3bd Close to BART & Glen Park',
    price: 160,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Luxurious and Modern Mission District Stunner!',
    price: 199,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Awesome View San Francisco !',
    price: 395,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: '"Market Street Hideaway: Ferry & SoMa Gateway"',
    price: 186,
    beds: 5,
    review_scores_rating: 5
  },
  {
    name: 'Historic 1924 Getaway in the Heart of Russian Hill',
    price: 245,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: "Welcome To *The Suites at Fisherman's Wharf* 2B#2",
    price: 249,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'GoldenGatePrk-2 miles, Nr Ocean, Zoo, SFSU &SGrove',
    price: 199,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Spacious, family friendly apartment near park',
    price: 300,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Stunning Noe Family Friendly House - Enhanced Cleaning',
    price: 1095,
    beds: 4,
    review_scores_rating: 5
  },
  {
    name: 'Penthouse on the Crest of Buena Vista Park-2bd/2ba',
    price: 245,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'Sunnyside Cinema: King bed + 2 twin, 2 desks, yard',
    price: 160,
    beds: 3,
    review_scores_rating: 5
  },
  {
    name: 'NEW! A+ Home | Sunny & Modern | Garage | Huge Yard',
    price: 129,
    beds: 4,
    review_scores_rating: 5
  }
]
```

This query returns all listings within the general San Francisco area that has more than 2 beds, as specified by the criteria. The data is returned in descending order by review_scores_rating. The projection limits the fields returned to name, beds, review_scores_rating, and price. This may be a useful query within the Airbnb app if someone were to be looking for accomodations that provides more than 2 beds, which would be ideal for big groups or families.


6. show the number of listings per host
```mongodb
db.listings_clean.aggregate({$group: {_id: "$host_id", count: {$sum:1}}})
```

```mongodb
[
  { _id: 197555079, count: 1 },
  { _id: 39035796, count: 1 },
  { _id: 491210273, count: 1 },
  { _id: 271698124, count: 2 },
  { _id: 14003785, count: 3 },
  { _id: 37199244, count: 1 },
  { _id: 56859317, count: 1 },
  { _id: 170427853, count: 1 },
  { _id: 34289429, count: 1 },
  { _id: 4306242, count: 1 },
  { _id: 8879720, count: 1 },
  { _id: 148590346, count: 1 },
  { _id: 51769509, count: 1 },
  { _id: 2410550, count: 1 },
  { _id: 7873769, count: 2 },
  { _id: 31668524, count: 1 },
  { _id: 5498141, count: 1 },
  { _id: 16108021, count: 1 },
  { _id: 13242738, count: 1 },
  { _id: 137698280, count: 1 }
]
```

This query counts the number of listings per host and then finds the sum. This would help Airbnb find out who their most successful or largest listers are.


7. find the average review_scores_rating per neighborhood, and only show those that are 4 or above, sorted in descending order of rating (see the docs)
    - if your data set only has blanks in the neighborhood-related fields, or only one neighborhood value in all documents, you may pick another field to break down the listings by - include an explanation and justification for this in your report.

```mongodb
db.listings_clean.aggregate([{$group:{_id: "$neighbourhood", avgRating: {$avg: "$review_scores_rating"}}}, {$match: {avgRating: {$gte:4}}}, {$sort: {avgRating:-1}}])
```

```mongodb
[
  { _id: 'Hayes Valley', avgRating: 4.81 },
  { _id: 'San Francisco', avgRating: 4.779726327312534 },
  { _id: 'Noe Valley', avgRating: 4.71 }
]
```

This query groups the listings by neighborhood and finds the average of review_scores_rating. It returns neighborhoods with an average rating above or equal to 4, and sorts the neighborhoods in descending order. In our case, we only had three neighborhoods, but all of them were listed. This may tell prospective tourists that San Francisco is a generally great area to visit, but specifically to get accomodation in  Hayes Valley, then the general San Francisco area, and last but not least Noe Valley.

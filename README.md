# Hash Tables

## Introduction
In order to store information efficiently, it is important to structure it in a way that makes the data easily re-accessible. When we have a two-pair tuple where the first index is a key and the second index is the information, similar to a dictionary, we need a way to efficiently store a large number of tuples in order to re-access them at a later time. Rather than placing all these tuples into a list and searching through them linearly, hash tables allow us to map keys to specific bins where we can store these tuples. This exponentially increases our search efficiency and allows us to find information much more quickly at the expense of additional setup time.

Think of it as a Marie-Kondo-approved method of organization, where you have a set of bins with different labels -- computer games, lego, books. For Mario Kart, you would put it in computer games, your LEGO airport shuttle model would be put in the bin labeled legos and finally, your collection of Harry Potter books would be put in the bin labeled books. This might take some time to set up, but because you have organized them into well-defined storage boxes, you will be able to look for your item very quickly as compared to searching sequentially through a big box of items where you might have to look through every single item before you find the lego piece. 

<img width="362" alt="Screen Shot 2021-10-10 at 10 48 50 AM" src="https://user-images.githubusercontent.com/86497342/136709437-f3897ce4-b1ed-4b42-b0a5-9315c93ab1e3.png">


## Packages
To run the notebook the following packages are required:
1. [NumPy](https://numpy.org/)
2. [pandas](https://pandas.pydata.org/)
3. [lolviz](https://github.com/parrt/lolviz)

To install these packages simply run the following commands in your terminal.
```
$ pip install numpy
$ pip install pandas
$ brew install graphviz
$ pip install lolviz
```

## The Data
The dataset used for this illustration contains the populations of all cities and towns in the state of California in 2010. The dataset contains four columns: name, type, county, and population. The source of the data can be found [here.](https://www.downloadexcelfiles.com/us_en/download-excel-file-list-cities-california-state#.YWMrCC1h30o) For our hash table implementation, we utilized the city name and population columns. 
<img width="961" alt="Screen Shot 2021-10-10 at 11 20 16 AM" src="https://user-images.githubusercontent.com/86497342/136708418-a89a5a71-8b57-4a47-a63b-cef2e627d86d.png">





## Implementation 
***Linear Search***<br>
We utilized linear search as a baseline search algorithm to look up terms within the dataset in linear time. 

***create_linear_table()***<br>
This function creates an unordered list of tuples containing all cities and their corresponding populations.

***linear_search()***<br>
This function looks through the list of tuples one by one and return the city's population with time complexity O(N), where N is the number of tuples in the list. 
Using linear search, it takes about 30 microseconds to find Yucca Valley's population. 

![Screen Shot 2021-10-10 at 11 48 48 AM](https://user-images.githubusercontent.com/86497342/136709479-109f4b48-ef70-41e0-ba61-2c41e0f2ae5c.png)


***Hash Table***<br>
Hash table consists of two main components: hash table and hash function.
A hash table is represented as a list of lists (a.k.a buckets). For our dataset we are creating a hash table with 26 buckets. Each bucket is a container corresponding to every letter in the English alphabet.

This is how an empty hash table looks in memory.

![Screen Shot 2021-10-10 at 10 29 54 AM](https://user-images.githubusercontent.com/86497342/136709504-df3e8038-b2cc-4f83-b354-5561a310865a.png)

***hashcode()***<br>
A hash function is an algorithm that produces an index of where a value can be found or stored in the hash table based on the actual data. The hash function in this example takes the first letter of each city name to give us the bucket index. The result of the hash function is analogous to the position of letters in the English alphabet. 

<img width="432" alt="Screen Shot 2021-10-10 at 11 06 26 AM" src="https://user-images.githubusercontent.com/86944952/136709260-f9564d97-7b15-45e5-a4bc-5c2a1417ffa7.png">

So the city names starting with ???A??? will be allotted a bucket index 0, ???B??? with 1 and so on till ???Z??? gets 25, and all the cities with their population will be stored in the allotted bucket.

***htable_put()***<br>
The htable_put function is used to actually map all of the city name keys to their corresponding buckets. The function employs the hashcode function to acquire a bucket index for the specific key given. Once the correct bucket is found, it is linearly searched to see if the key already exists within the bucket. If it does then its value is simply updated, otherwise the new key-value pair is linearly appended to the end of the bucket list.  For our data, you can see that our hashcode function puts all the cities in buckets based off of the first letter of their city name. 


<img width="200" alt="hashtable_put_example" src="https://user-images.githubusercontent.com/86497342/136709130-6a2466c2-4827-45f9-aae0-06f72612bb91.png">


***htable_get()***<br>
The htable_get function is our lookup function that takes in 2 parameters: the hash table created and the key of interest. The function first utilizes the hashcode function to get the index of the bucket where the key is located. It then searches linearly within that specific bucket to look for the key. If the key is found, the function will return its value, otherwise it will return None. 

For this particular example, you can see that using a hash table speeds up the time it takes to look up Yucca Valley???s population by about 4 times. 


![Screen Shot 2021-10-10 at 10 57 40 AM](https://user-images.githubusercontent.com/86497342/136708014-e34423a9-197d-4f27-81fc-6f58d0271410.png)


## Conclusion 
A hash table allows for efficient data lookups as it lets us search a single bucket that is comparatively smaller than the linear list and contains just the relevant data grouped as per the hash function. This saves a lot of searching time. The compromise is on the time taken to create the hash table in exchange for increased searching speed. The hash table creation takes more time as it segregates the data into buckets as compared to dumping the entire content in a list. But once the table is created every search operation takes a dramatically small amount of time as compared to the linear way of searching. It is a more organized way of storing and retrieving information especially when we have a large amount of data.

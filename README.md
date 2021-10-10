# Hashtables

## Introduction
In order to store information efficiently, it is important to structure it in a way that makes the data easily re-accessible. When we have a two-pair tuple where the first index is a key and the second index is the information, similar to a dictionary, we need a way to efficiently store a large number of tuples in order to re-access them at a later time. Rather than placing all these tuples into a list and searching through them linearly, hashtables allow us to map keys to specific bins where we can store these tuples. This exponentially increases our search efficiency and allows us to find information much more quickly at the expense of additional setup time.

Think of it as a Marie-Kondo-approved method of organization, where you have a set of bins with different labels -- computer games, lego, books. For Mario Kart, you would put it in computer games, your LEGO airport shuttle model would be put it in the bin labeled legos and finally, your collection of Harry Potter books would be put in the bin labeled books. This might take some time to set up, but because you have organized them into well-defined storage boxes, you will be able to look for your item very quickly as compared to searching sequentially through a big box of items where you might have to look through every single item before you find the lego piece. 

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
The dataset used for this illustration contains the populations of all cities and towns in the state of California in 2010. The dataset contains four columns: name, type, county, and population. The source of the data can be found [here.](https://www.downloadexcelfiles.com/us_en/download-excel-file-list-cities-california-state#.YWMrCC1h30o) For our hashtable implementation, we utilized the city name and population columns. 
<img width="961" alt="Screen Shot 2021-10-10 at 11 20 16 AM" src="https://user-images.githubusercontent.com/86497342/136708418-a89a5a71-8b57-4a47-a63b-cef2e627d86d.png">





## Implementation 
<b><u>Linear Search</u></b><br>
We utilized linear search as a baseline search algorithm to look up terms within the dataset in linear time. 

<b><u>create_linear_table()</u></b><br>
In the ‘create_linear_table’ function, we create an unordered list of tuples containing all cities and their corresponding populations appending all elements in a list structure. 

<b><u>linear_search()</u></b><br>
In the ‘linear_search’ function, it will look through the list of tuples one by one and return its populations with complexity O(N), in which N is the number of tuples in the list. 
Using linear search, it takes about 30 microseconds to find Yucca Valley's population. It is fast right, but it could be faster using the hash table. 

## Hashtable
Hash table consists of two main components: Hashtable and Hash Function.
A hashtable is represented as a list of lists (a.k.a buckets): For our dataset we are creating a hashtable with 26 buckets. Each bucket is a container corresponding to every letter in the English alphabet.

This is how an empty hash table looks in memory.

#### Hash Function
A hash function is an algorithm that produces an index of where a value can be found or stored in the hash table based on the actual data. The hash function in this example takes the first letter of each city name to give us the bucket index. The result of the hash function is analogous to the position of letters in the English alphabet. 

<img width="432" alt="Screen Shot 2021-10-10 at 11 06 26 AM" src="https://user-images.githubusercontent.com/86944952/136709260-f9564d97-7b15-45e5-a4bc-5c2a1417ffa7.png">

So the city names starting with ‘A’ will be allotted a bucket index 0, ‘B’ with 1 and so on till ‘Z’ gets 25, and all the cities with their population will be stored in the allotted bucket.it

***htable_put()***<br>
The hashtable put function is used to actually map all of the city name keys to their corresponding buckets. The function employs the hashcode function to acquire a bucket index for the specific key given. Once the correct bucket is found, it is linearly searched to see if the key already exists within the bucket. If it does then its value is simply updated, otherwise the new key-value pair is linearly appended to the end of the bucket list.  For our data, you can see that our hashcode function puts all the cities in buckets based off of the first letter of their city name. 


<img width="200" alt="hashtable_put_example" src="https://user-images.githubusercontent.com/86497342/136709130-6a2466c2-4827-45f9-aae0-06f72612bb91.png">


***htable_get()***<br>
The htable_get function is our lookup function that takes in 2 parameters: the hash table created and the key of interest. The function first utilizes the hashcode function to get the index of the bucket where the key is located. It then searches linearly within that specific bucket to look for the key. If the key is found, the function will return its value, otherwise it will return None. 

For this particular example, you can see that using a hash table speeds up the time it takes to look up Yucca Valley’s population by about 4 times. 


![Screen Shot 2021-10-10 at 10 57 40 AM](https://user-images.githubusercontent.com/86497342/136708014-e34423a9-197d-4f27-81fc-6f58d0271410.png)

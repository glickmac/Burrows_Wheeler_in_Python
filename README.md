### ABOUT
-----

This repository links to the article Burrows Wheeler in Python published in Towards Data Science. The python implementations of the Burrows Wheeler Transformation are located in the jupyter notebook (.ipynb file). Search using BWT is orders of magnitude faster than traditional search after the suffix array is generated. 

Sample usage (generate_all and find functions are located in `Burrows Wheeler in Python.ipynb` file):

```python
#%%timeit  ## ~2.44 s ± 377
# Alice in Wonderland Starting from Chapter 8 
import urllib3
url = 'https://www.gutenberg.org/files/11/11-0.txt'
http = urllib3.PoolManager()
text = http.urlopen("GET", url).data.decode()
chapters = text.split("THE END")[0].split("CHAPTER VIII")[2]


## 61235 Characters | 27432 Words | 3762 Lines
#characters = len(text)
#words = len(text.split(" "))
#lines = len(text.split("\n"))

bwt_data = generate_all(chapters)

## 3 instances of "Off with her head"
print("Number of Exact Matches: "+ str(len(find('Off with her head', chapters, mismatches=0, bwt_data=bwt_data))))

## 0 instances of "off with her head" CASE SENSITIVE
print("Number of Exact Matches: "+ str(len(find('off with her head', chapters, mismatches=0, bwt_data=bwt_data))))

### Mismatches = 2
## 5 instances of "Off with her/his head"
print("Number of Fuzzy Matches: "+ str(len(find('Off with her head', chapters, mismatches=2, bwt_data=bwt_data))))
```


### REQUIREMENTS
------------

* Python (version 3)
* urllib3 [For parsing Project Gutenberg]
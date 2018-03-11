# Create Stylist Word Cloud Using Python
## What is Word Cloud?

_Word cloud_ atau disebut juga _tag cloud_ adalah representasi visual dari data teks, biasanya digunakan untuk menggambarkan metadata keywords (tags) pada sebuah website/situs, untuk memvisualisasikan suatu bentuk teks secara bebas

To create word cloud, you can use the data obtained from my research by downloading the data [here](https://raw.githubusercontent.com/rizkynovyantika/marketingstrategies/master/word%20cloud%20/suggestion). 

## How to make Word Cloud in Python?

1. Remove unused words
2. Replace words
3. Counting the frequency of words (optional)
4. Creating Word CLoud
5. Styling Word CLoud (optional)

## Remove unused words

Data teks, biasanya terdapat kata yang tidak penting untuk dilakukan pembuatan word cloud oleh karena itu diperlukan syntax untuk melakukan penghapusan kata yang tidak digunakan. 

```python

infile = "/folder/infile.txt"
outfile = "/folder/outfile.txt"

delete_list = ["kita", "dan", "yg", "jangan", "jgn", "juga", "Yg"]
fin = open(infile)
fout = open(outfile, "w+")
for line in fin:
    for word in delete_list:
        line = line.replace(word, "")
    fout.write(line)
fin.close()
fout.close()

```

infile.txt merupakan data teks yang asli sebelum dihapus kata yang tidak akan digunakan dalam word cloud. sedangkan outfile.txt merupaka data teks hasil dari menghapus kata yang tidak digunakan dalam word cloud.

## Replace words

Sebuah teks yang diperoleh dari saran seseorang akan menghasilkan kata yang berbeda akan tetapi memiliki arti yang sama. sehingga untuk memperhemat pembendaharaan kata dalam word cloud diperlukan mengganti kata yang berbeda dengan arti kata yang sama dengan menjadikannya satu kata yang sama.

```python

with open('/folder/outfile.txt', 'r') as file :
    filedata = file.read()
filedata = filedata.replace("skill", "kemampuan").replace("Skill", "kemampuan").replace("skills", "kemampuan").replace("softskill", "kemampuan").replace("connection", "koneksi").replace("ipk", "IPK").replace("cv", "CV").replace("berdoa", "doa").replace("yg", " ").replace("communication", "komunikasi")
with open('/folder/outfile.txt', 'w') as file:
    file.write(filedata)

```


## Counting the frequency of words

Untuk mengetahui masing-masing jumlah kata yang sering muncul dalam saran yang diberikan pada data teks kita dapat menggunakan syntax seperti dibawah ini :

```python

import re
import string
frequency = {}
document_text = open('/home/kiki/Code/python/job/outfile.txt')
text_string = document_text.read().lower()
match_pattern = re.findall(r'\b[a-z]{3,15}\b', text_string)
 
for word in match_pattern:
    count = frequency.get(word,0)
    frequency[word] = count + 1
     
frequency_list = frequency.keys()
 
for words in frequency_list:
    print (words, frequency[words])

```

Berikut ini adalah gambar hasil dari perhitungan kata dalam data teks.

![Word Cloud](https://rizkynovyantika.github.io/images/create-stylist-word-cloud-using-python/1.png)

## Creating Word Cloud
Nah, ini dia tahap inti dari artikel ini yaitu pembuatan word cloud.

```python

import os
import matplotlib.pyplot as plt
from wordcloud import WordCloud

text = open('/folder/outfile.txt')
data = text.read()

%matplotlib inline

wordcloud = WordCloud(background_color='white', mode="RGB", width=1600, height=800).generate(data)

plt.figure(figsize=(20,10))
plt.title('what we need to get job?')
plt.imshow(wordcloud)
plt.axis("off")
plt.tight_layout(pad=0)
plt.show()

```
Berikut ini adalah gambar hasil word cloud data teks.

![Word Cloud](https://rizkynovyantika.github.io/images/create-stylist-word-cloud-using-python/2.png)


## Styling Word Cloud
Untuk membuat word cloud menjadi lebih menarik, kita dapat mengubah word cloud tersebut dengan berbagai bentuk yang kita inginkan. Dalam hal ini saya ingin membuat word cloud dengan tema pekerjaan. Dengan gambar asli seperti dibawah ini :

![Word Cloud](https://rizkynovyantika.github.io/images/create-stylist-word-cloud-using-python/3.png)
 
Berikut ini adalah syntax yang dapat digunakan untuk mengubah style dari word cloud.

```python

import sys
from os import path
from PIL import Image
import numpy as np
import matplotlib.pyplot as plt

from wordcloud import WordCloud, STOPWORDS
d = path.dirname(sys.argv[0])

# Read the whole text.
text = open(path.join(d,'/folder/outfile.txt')).read()

#read the mask image
job_mask = np.array(Image.open(path.join(d, "/folder/work.jpg")))

stopwords = set(STOPWORDS)
stopwords.add("said")

wc = WordCloud(background_color="white", max_words=2000, mask=job_mask, stopwords=stopwords)

# generate word cloud
wc.generate(text)

# store to file
wc.to_file(path.join(d, "/folder/baru.png"))

# show
plt.imshow(wc, interpolation='bilinear')
plt.axis("off")
plt.figure()
plt.imshow(job_mask, cmap=plt.cm.gray, interpolation='bilinear')
plt.axis("off")
plt.show()

```

Output dari style word cloud yang dibuat menggunakan syntax diatas adalah sebagai berikut :

![Word Cloud](https://rizkynovyantika.github.io/images/create-stylist-word-cloud-using-python/4.png)

gambar tersebut dapat disimpan dengan menggunakan format .png 
berikut ini adalah hasil dari styling word cloud yang telah dibuat.

![Word Cloud](https://rizkynovyantika.github.io/images/create-stylist-word-cloud-using-python/5.png)


author: "Rizky D. Novyantika"
title: "How to Create Stylist Word Cloud Using Python"
link : https://rizkynovyantika.github.io/post/how-to-create-stylist-word-cloud-using-python/ 

# Alat dan Bahan yang dibutuhkan :
1. Api Key Twitter (Cara Mendapatkan Api Key Twitter) 
2. Jupyter notebook
3. Library Tweepy

# Kode

1. Install Library Tweepy


```python
pip install tweepy
```

2. Import library yang dibutuhkan seperti yang di bawah ini


```python
import tweepy
from tweepy.streaming import StreamListener
from tweepy import OAuthHandler
from tweepy import Stream
import time
import json
```

3. Buatlah beberapa variabel untuk menyimpan API Token Twitter, kalian bisa copy paste script di bawah dan isikan variabel sesuai dengan API Key milik kalian.


```python
access_token = "<your access token>"
acces_token_secret = "<your access token secret>"
consumer_key = "<your consumer token>"
consumer_secret = "<your consumer token secret>"
```

4. Buatlah class StdoutListener


```python
class StdoutListener(StreamListener):
    def on_data(self,data):
        try:
            data = json.loads(data) # load data dalam format json
            tweet = data['text']    # ambil entitas text (Tweet)
            print(tweet)            # tampilkan text(Tweet)
            
            #simpan dan export file dalam .csv
            with open('tweet.csv', 'a', encoding='utf-8') as f:
                saveFile = open('hasil.csv','a')
                f.write(tweet)
                f.write('\n')
                f.close()
            return True
        except BaseException as e:
            print('Failed'(e))
   
    def on_error(self,status):
        print(status)
```

5. Terakhir, tuliskan code yang akan kita jalankan untuk menambang data dari API Twitter tersebut


```python
l = StdoutListener()
auth = OAuthHandler(consumer_key,consumer_secret)
auth.set_access_token(access_token,access_token_secret)
stream = Stream(auth,l)
stream.filter(track=['Gojek', 'Grab'])
```

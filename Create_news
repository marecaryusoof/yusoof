from googlesearch import search
import urllib3
from bs4 import BeautifulSoup as BS

IGNORE_TITLE = ['Access Denied','403 Forbidden']
NUM_OF_NEWS = 10

class Search_news:
    def __init__(self,keyword):
        self.keyword = keyword

    def get_results(self,start,stop,num):
        self.start = start
        self.stop = stop
        self.num = num
        self.srch_str = str(self.keyword) + " news"
        results= []
        try:
            for res in search(query=self.srch_str,tld='co.in',lang='en',num=self.num,start=self.start, stop=self.stop, pause=2):
                results.append(res)
            return results
        except:
            print("Error: Could not search")

    def get_title(self):
        begin=0
        end=NUM_OF_NEWS
        num=NUM_OF_NEWS
        res_cnt=0
        while res_cnt<=NUM_OF_NEWS:
            for news in self.get_results(begin,end,num):
                http = urllib3.PoolManager()
                req = http.request('GET',news)
                soup = BS(req.data, 'html.parser')
                try:
                    news_title = soup.title.string
                except:
                    continue
                if news_title not in IGNORE_TITLE:
                    res_cnt+=1
                    print(soup.title.string)
            begin=end
            end=NUM_OF_NEWS+begin-res_cnt
            num=NUM_OF_NEWS-res_cnt

if __name__=='__main__':
    search_key=''
    while search_key=='':
        search_key=input('What are you searching today? ')
        if search_key=='':
            print('Oops! You entered nothing')
    s1=Search_news(search_key)
    s1.get_title()

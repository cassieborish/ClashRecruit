
Using PRAW (Python Reddit API Wrapper) to extract data. Installed praw with pip install praw. Then wrote following function to extract active user count. It can extract count from any subreddit. Just need to substitute in sub_name.


```python
import praw
def getActiveUserCount(sub_name):
    reddit = praw.Reddit(client_id='CLIENT_ID',
                     client_secret='CLIENT_SECRET',
                     password='REDDIT_PASSWORD',
                     user_agent='testscript by /u/cborish',
                     username='REDDIT_USERNAME')
    subreddit = reddit.subreddit(sub_name)
    number = subreddit.active_user_count
    return number
```

I'm specifically interested in the subreddit clashofclansrecruit, so I run the function for that subreddit.


```python
numberOfUsers = getActiveUserCount("clashofclansrecruit")
print(numberOfUsers)
```

    84


Get the current date and time


```python
import datetime
print(datetime.datetime.today().strftime("%A %H"))
```

    Saturday 22



```python
import MySQLdb as mdb

con = mdb.connect('localhost', 'USER', 'PASSWORD', 'DATABASE');

with con:
    cur = con.cursor()
    cur.execute("DROP TABLE IF EXISTS activeUsers")
    cur.execute("CREATE TABLE activeUsers(Weekday VARCHAR(10), \
    Hour INT, \
    Users INT)")
    cur.execute("""INSERT INTO activeUsers(Weekday, Hour, Users) VALUES(%s, %s, %s)""", (datetime.datetime.today().strftime("%A"), datetime.datetime.today().strftime("%H"), numberOfUsers))
    
```

    /anaconda/lib/python3.6/site-packages/ipykernel_launcher.py:5: DeprecationWarning: context interface will be changed.  Use explicit conn.commit() or conn.rollback().
      """



```python
import MySQLdb as mdb

con = mdb.connect('localhost', 'root', '', 'DATABASE');

with con: 

    cur = con.cursor(mdb.cursors.DictCursor)
    cur.execute("SELECT * FROM activeUsers")

    rows = cur.fetchall()

    for row in rows:
        print(row["Weekday"], row["Hour"], row["Users"])
```

    Saturday 22 84


    /anaconda/lib/python3.6/site-packages/ipykernel_launcher.py:5: DeprecationWarning: context interface will be changed.  Use explicit conn.commit() or conn.rollback().
      """



```python

```

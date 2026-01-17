donc bon
deux premiers articles berk
on réécrit ?
quatre orm
4.5 rewrite draft
https://claude.ai/chat/0f9eb99e-2ac9-4e91-9215-88b49b275f13
5 perf benchmarks

peewee
they do have bit field...
UUID as hex or as bytes? Why VARCHAR in Sqlite
WAAAA y'a quand meme le many to many field dans peewee, la syntaxe a rien à voir
Write ahead journal

[sqlite is coded in c](https://sqlite.org/whyc.html)
[existence](https://sqlite.org/whyc.html)

tiens, sqlite3 est pas top?
https://github.com/rogerbinns/apsw

datomic
https://docs.datomic.com/datomic-overview.html

dbval (datomic in sqlite)
https://github.com/maxweber/dbval

why no rowid hmmm

entity === table === covering index
but why? because if you get the id once you're done no?

indexes in peewee
https://docs.peewee-orm.com/en/latest/peewee/models.html#model-indexes

sql scaling
https://use.expensify.com/blog/scaling-sqlite-to-4m-qps-on-a-single-server

can distribute it if you want
https://rqlite.io/

why index
https://sqlite.org/queryplanner.html
(video ?)
https://csharp-video-tutorials.blogspot.com/2012/09/advantages-and-disadvantages-of-indexes.html

more dod
https://www.youtube.com/watch?v=wG2Y42qArHY

hmm ok oh if you do es
https://volodymyrpotiichuk.com/blog/articles/event-sourcing
maybe you disable row_id and replay on user_id instead

tester cross-stream avec python
https://www.cross.stream/

```python
db = SqliteDatabase('my_app.db', pragmas={
    'journal_mode': 'wal',
    'foreign_keys': 1,
})
```

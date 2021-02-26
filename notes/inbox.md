# Inbox

Here is where I capture notes as I'm learning and then I figure out a spot for them later.

Recommendation Systems:
* Cloud SQL
* Cloud Dataproc

? What recommendation systems can we implement at work?
* Which providers to visit
* Which preventative services to get (gaps in care)
* Which searches to do (enhancements to shortcuts)
* Which services to explore costs
* What to do when you land on the no results screen

Study questions:

How do recommendation systems generally work?

The model is attacking two problems at the same time. First, it is trying to understand which items users rate highly. Second, it is trying to figure out which users are most like you. That way it can estimate things that you haven't tried, but might like, based on what users similar to you like, calibrated agains the quality of those items.

What is a good infrastructure framework for calculating recommendations?

We don't want to calculate recommendations at runtime ... that would be costly and take a long time. Instead, this is a good use case for a batch process. We can stream the data into a data warehouse, the have a weekly batch process that munges all of these data, puts them into a model, and then outputs the recommendations from that model into a relational database, such as Cloud SQL. Then, at run time, all the application has to do is pull a value from the database, which it can do very quickly.

When should you use the following Cloud storage solutions?
* Cloud Storage - unstructured data
* Cloud SQL - good for data that is transactional, is on the gigabyte scale, and can be managed in one database.
* Datastore
* Bigtable - real-time high throughput applications
* BigQuery - petabyte scall analytics with seconds latency
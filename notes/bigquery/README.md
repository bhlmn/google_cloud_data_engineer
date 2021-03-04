# BigQuery

## Things to know/document

Note that for many of these it is helpful to be able to do them:
* From the web UI
* Using the command line
* Using BigQuery's REST API (e.g., in Python)
* Using SQL within BigQuery!

### Working with data
- [ ] Connect to and use a public dataset
- [ ] Create your own datasets and tables
- [ ] Load data into tables from local sources and internet-based sources
- [ ] Process json-formatted data

### Machine Learning in BigQuery
Things to do in BigQuery ML:
- [ ] Create a training and evaluation dataset to be used for prediction
- [ ] Create a classification (logistic regression) model in BQML
- [ ] Evaluate the performance of the model
- [ ] Push predictions to production!

Creating a BigQuery ML model:
``` sql
create or replace model
    `dataset.model_name`
options (
    model_type = 'logistic_reg', 
    labels = ['label_column']
) as (
    select
        label_column, 
        feature1, 
        feature2, 
        ..., 
        featureN
    from
        table
    where
        date between ... # train on a subset of the data
);
```
After the model is trained, clicking "go to model" shows model details, information on training (loss, duration, learn rate), evaluation (precision, recall, PRC, log loss, ROC curve, confusion matrix), and the schema!

Evaluate the model on new data:
``` sql
select
    roc_auc,
    case
        when roc_auc > .9 then 'good'
        when roc_auc > .8 then 'fair'
        when roc_auc > .7 then 'not great'
    else 'poor' 
    end as model_quality
from
    ml.evaluate(model `dataset.model_name`, (
        select
            label_column, 
            feature1, 
            feature2, 
            ..., 
            featureN
        from
            table
        where
            date between ... # evaluate on a different subset of data
    ));
```

Make a prediction with a model. I think there is more that needs to be done here.
``` sql
select
    *
from
    ml.predict(model `dataset.model_name`, (
        select
            label_column, 
            feature1, 
            feature2, 
            ..., 
            featureN
        from
            table
        where
            date between ... # unseen test data
    ));
```

## Public Datasets
Google Cloud hosts public datasets for analytical exploration and ingestion into machine learning models: https://cloud.google.com/public-datasets/.
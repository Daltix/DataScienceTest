# Daltix Data Science Test

Make the matches!

## Objective

Your objective is to find product matches in a dataset of DIY products using data scraped from webshops by the Daltix team.
What you are given are a set of ~100K json objects (stored in .jsonl format) that can be found in `data/dataset.jsonl.gz`.

What you are required to provide is a github repository including the following

## Deliverable 1. Predictions

The predictions will be a single csv (`submission.csv`) that looks like the following:

```
daltix_id_1,daltix_id_2
aaff0aa6db24814ad25d5cb410ded08361ab32bcb953e1f81fd4f77affe7fe35,480e353eb638dbe8be37d04cf28b3b801eadccbd0ffaddec4f9bed10996d901f
```

Where each entry means that they are a match.

Note that when we say "match" we mean EXACT MATCH. It must be, without a doubt, **the same product**!


## Deliverable 2. Code

We will need in the repository the required code to generate the submission file. This code can be either .py files or jupyter notebooks (preferred).

Instructions on how to generate the submission are required, ideally in the repository README file.

Extra points for additional information including analysis, interesting findings or data visualizations.


## The Dataset

A sample entry looks like the following:

```json
{
    "DALTIX_ID": "aaff0aa6db24814ad25d5cb410ded08361ab32bcb953e1f81fd4f77affe7fe35",
    "DISPLAY_URL": "https://www.plan-it.be/nl/verf-laminaat-decoratie/woondecoratie/pictogrammen/signalisatie/pickup-pictogram-p621-heren/1409779",
    "SHOP": "planit",
    "NAME": "Pickup pictogram P621 \"Heren\"",
    "BRAND": "Pickup",
    "CONTENTS": [],
    "DESCRIPTION": "Pickup pictogram is zelfklevend, weerbestendig en eenvoudig aan te brengen. Het product heeft een direct herkenbare aanduiding en is geschikt voor gladde ondergronden. Deze pictogram is 10 maal 10 centimeters en heeft als opdruk \"Heren\".",
    "SPECIFICATIONS": {
        "Formaat": "\"10 x 10cm\"",
        "Gebruik": "\"Voor bewegwijzering of verbodsaanduiding\"",
        "Materiaal": "\"Zelfklevend vinyl\""
    },
    "PRODUCT_ID": "1409779"
}
```
As you can see, with each entry you have the following fields:

#### DALTIX_ID

This is the identifier that Daltix uses for a single product. It is our own internally generated ID.

#### DISPLAY_URL

This is a url that if you visit it shows the current state of the product on a webshop. This is great for visually inspecting
your matches. *Do not be tempted to crawl these urls as it is against the rules of this hackathon*

#### SHOP

This is the shop code of the shop that the product belongs to.

#### NAME

This is the name of the product. It is what would appear as the title of a product page when you visit it on the webshop.

#### BRAND

Exactly what it sounds like. This is quite sparsely populated.

#### CONTENTS

In some cases, we have a dictionary of contents that is a non-standardized dictionary.

#### DESCRIPTION

A longer description of the product that is usually presented underneath the name on the webshop.

#### SPECIFICATIONS

A non-standardized key-value pair of arbitrary but specific attributes of the product.

#### PRODUCT_ID

The identifier that the shop has given this product.

## Evaluation dataset

The validation dataset (y_true.csv) is provided as well, that way multiple approaches can be tested.

This will be done using an F1 score implemented as the following (this is not the full evaluation code, just a definition of the F1):

```py
len_validation = len(validation_set)
len_submission = len(submission_set)
tp = len(submission_set.intersection(validation_set))
fp = len(submission_set - validation_set)
recall = tp/len_validation
precision = tp/len_submission
fpr = fp/len_submission

f1 = 2/((1/recall) + (1/precision))
```

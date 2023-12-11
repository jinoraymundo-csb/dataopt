# DATAOPT Final Exams

1. Start with `finals` directory
2. Download the sample dataset [here](https://raw.githubusercontent.com/jinoraymundo-csb/dataopt/master/Finals/companies.json) and save it on `finals` folder
3. add a `scripts` folder under `finals` folder
4. name your file as `FE_<lastname>_<firstname>.js` e.g. `FE_raymundo_jinopaulo.js`
5. execute the following docker commands on the terminal:
```
docker run --name dataopt-finals --rm -p 27017:27017 -v ${PWD}/scripts:/scripts -d mongo:latest
docker cp companies.json dataopt-finals:/tmp/companies.json
docker exec -it dataopt-finals bash
mongoimport --db company --file /tmp/companies.json
```

> 300 documents should have been inserted

## Questions
1. Find all `company` that has `category_code` == "web", get only the "name" field (127 documents)
2. Find all `company` that has more than 100 "employees", get only the "name" and "number_of_employees" fields (45 documents)
3. Find all `company` that "Peter Thiel" has worked with, get only the "name" and "permalink" fields (4 documents)
4. Find all company names that is a competitor of "Facebook" (7 documents)
5. Find all `company` that has an office in city: "Seattle" and state_code: "WA", get only the "name" and "description" fields (16 documents)

## Deliverables
1. on the file `scripts/FE_raymundo_jinopaulo.js` (example):

```
db = db.getSiblingDB('company');

var query01Filter = {};
var query01Options = {};
var query01 = db.companies.find(query01Filter, query01Options)
printjson(query01);
print(`Question 01 count: ${query01.count()}`);

...

var query10Filter = {};
var query10Options = {};
var query10 = db.companies.find(query10Filter, query10Options)
printjson(query10);
print(`Question 10 count: ${query10.count()}`);
```

2. To test your answers:
```
docker exec -it dataopt-finals bash
mongosh scripts/FE_raymundo_jinopaulo.js
```


## Cleanup
1. Once done with the exam, issue the following commands:
```
docker stop dataopt-finals
```

2. (optional) to start the container again:
```
docker start dataopt-finals
```


### Sample Schema:
```
{
  "_id": {
    "$oid": "52cdef7c4bab8bd675297d8a"
  },
  "name": "Wetpaint",
  "permalink": "abc2",
  "crunchbase_url": "http://www.crunchbase.com/company/wetpaint",
  "homepage_url": "http://wetpaint-inc.com",
  "blog_url": "http://digitalquarters.net/",
  "blog_feed_url": "http://digitalquarters.net/feed/",
  "twitter_username": "BachelrWetpaint",
  "category_code": "web",
  "number_of_employees": 47,
  "founded_year": 2005,
  "founded_month": 10,
  "founded_day": 17,
  "deadpooled_year": 1,
  "tag_list": "wiki, seattle, elowitz, media-industry, media-platform, social-distribution-system",
  "alias_list": "",
  "email_address": "info@wetpaint.com",
  "phone_number": "206.859.6300",
  "description": "Technology Platform Company",
  "created_at": {
    "$date": 1180075887000
  },
  "updated_at": "Sun Dec 08 07:15:44 UTC 2013",
  "overview": "<p>Wetpaint is a technology platform company that uses its proprietary state-of-the-art technology and expertise in social media to build and monetize audiences for digital publishers. Wetpaint’s own online property, Wetpaint Entertainment, an entertainment news site that attracts more than 12 million unique visitors monthly and has over 2 million Facebook fans, is a proof point to the company’s success in building and engaging audiences. Media companies can license Wetpaint’s platform which includes a dynamic playbook tailored to their individual needs and comprehensive training. Founded by Internet pioneer Ben Elowitz, and with offices in New York and Seattle, Wetpaint is backed by Accel Partners, the investors behind Facebook.</p>",
  "image": {
    "available_sizes": [
      [
        [
          150,
          75
        ],
        "assets/images/resized/0000/3604/3604v14-max-150x150.jpg"
      ],
      [
        [
          250,
          125
        ],
        "assets/images/resized/0000/3604/3604v14-max-250x250.jpg"
      ],
      [
        [
          450,
          225
        ],
        "assets/images/resized/0000/3604/3604v14-max-450x450.jpg"
      ]
    ]
  },
  "products": [
    {
      "name": "Wikison Wetpaint",
      "permalink": "wetpaint-wiki"
    },
    {
      "name": "Wetpaint Social Distribution System",
      "permalink": "wetpaint-social-distribution-system"
    }
  ],
  "relationships": [
    {
      "is_past": false,
      "title": "Co-Founder and VP, Social and Audience Development",
      "person": {
        "first_name": "Michael",
        "last_name": "Howell",
        "permalink": "michael-howell"
      }
    },
    {
      "is_past": false,
      "title": "Co-Founder/CEO/Board of Directors",
      "person": {
        "first_name": "Ben",
        "last_name": "Elowitz",
        "permalink": "ben-elowitz"
      }
    },
    {
      "is_past": false,
      "title": "COO/Board of Directors",
      "person": {
        "first_name": "Rob",
        "last_name": "Grady",
        "permalink": "rob-grady"
      }
    },
    {
      "is_past": false,
      "title": "SVP, Strategy and Business Development",
      "person": {
        "first_name": "Chris",
        "last_name": "Kollas",
        "permalink": "chris-kollas"
      }
    },
    {
      "is_past": false,
      "title": "Board",
      "person": {
        "first_name": "Theresia",
        "last_name": "Ranzetta",
        "permalink": "theresia-ranzetta"
      }
    },
    {
      "is_past": false,
      "title": "Board Member",
      "person": {
        "first_name": "Gus",
        "last_name": "Tai",
        "permalink": "gus-tai"
      }
    },
    {
      "is_past": false,
      "title": "Board",
      "person": {
        "first_name": "Len",
        "last_name": "Jordan",
        "permalink": "len-jordan"
      }
    },
    {
      "is_past": false,
      "title": "Head of Technology and Product",
      "person": {
        "first_name": "Alex",
        "last_name": "Weinstein",
        "permalink": "alex-weinstein"
      }
    },
    {
      "is_past": true,
      "title": "CFO",
      "person": {
        "first_name": "Bert",
        "last_name": "Hogue",
        "permalink": "bert-hogue"
      }
    },
    {
      "is_past": true,
      "title": "CFO/ CRO",
      "person": {
        "first_name": "Brian",
        "last_name": "Watkins",
        "permalink": "brian-watkins"
      }
    },
    {
      "is_past": true,
      "title": "Senior Vice President, Marketing",
      "person": {
        "first_name": "Rob",
        "last_name": "Grady",
        "permalink": "rob-grady"
      }
    },
    {
      "is_past": true,
      "title": "VP, Technology and Product",
      "person": {
        "first_name": "Werner",
        "last_name": "Koepf",
        "permalink": "werner-koepf"
      }
    },
    {
      "is_past": true,
      "title": "VP Marketing",
      "person": {
        "first_name": "Kevin",
        "last_name": "Flaherty",
        "permalink": "kevin-flaherty"
      }
    },
    {
      "is_past": true,
      "title": "VP User Experience",
      "person": {
        "first_name": "Alex",
        "last_name": "Berg",
        "permalink": "alex-berg"
      }
    },
    {
      "is_past": true,
      "title": "VP Engineering",
      "person": {
        "first_name": "Steve",
        "last_name": "McQuade",
        "permalink": "steve-mcquade"
      }
    },
    {
      "is_past": true,
      "title": "Executive Editor",
      "person": {
        "first_name": "Susan",
        "last_name": "Mulcahy",
        "permalink": "susan-mulcahy"
      }
    },
    {
      "is_past": true,
      "title": "VP Business Development",
      "person": {
        "first_name": "Chris",
        "last_name": "Kollas",
        "permalink": "chris-kollas"
      }
    }
  ],
  "competitions": [
    {
      "competitor": {
        "name": "Wikia",
        "permalink": "wikia"
      }
    },
    {
      "competitor": {
        "name": "JotSpot",
        "permalink": "jotspot"
      }
    },
    {
      "competitor": {
        "name": "Socialtext",
        "permalink": "socialtext"
      }
    },
    {
      "competitor": {
        "name": "Ning by Glam Media",
        "permalink": "ning"
      }
    },
    {
      "competitor": {
        "name": "Soceeo",
        "permalink": "soceeo"
      }
    },
    {
      "competitor": {
        "name": "Yola",
        "permalink": "yola"
      }
    },
    {
      "competitor": {
        "name": "SocialGO",
        "permalink": "socialgo"
      }
    },
    {
      "competitor": {
        "name": "IslamNor",
        "permalink": "islamnor"
      }
    }
  ],
  "providerships": [],
  "total_money_raised": "$39.8M",
  "funding_rounds": [
    {
      "id": 888,
      "round_code": "a",
      "source_url": "http://seattlepi.nwsource.com/business/246734_wiki02.html",
      "source_description": "",
      "raised_amount": 5250000,
      "raised_currency_code": "USD",
      "funded_year": 2005,
      "funded_month": 10,
      "funded_day": 1,
      "investments": [
        {
          "company": null,
          "financial_org": {
            "name": "Frazier Technology Ventures",
            "permalink": "frazier-technology-ventures"
          },
          "person": null
        },
        {
          "company": null,
          "financial_org": {
            "name": "Trinity Ventures",
            "permalink": "trinity-ventures"
          },
          "person": null
        }
      ]
    },
    {
      "id": 889,
      "round_code": "b",
      "source_url": "http://pulse2.com/2007/01/09/wiki-builder-website-wetpaint-welcomes-95m-funding/",
      "source_description": "",
      "raised_amount": 9500000,
      "raised_currency_code": "USD",
      "funded_year": 2007,
      "funded_month": 1,
      "funded_day": 1,
      "investments": [
        {
          "company": null,
          "financial_org": {
            "name": "Accel Partners",
            "permalink": "accel-partners"
          },
          "person": null
        },
        {
          "company": null,
          "financial_org": {
            "name": "Frazier Technology Ventures",
            "permalink": "frazier-technology-ventures"
          },
          "person": null
        },
        {
          "company": null,
          "financial_org": {
            "name": "Trinity Ventures",
            "permalink": "trinity-ventures"
          },
          "person": null
        }
      ]
    },
    {
      "id": 2312,
      "round_code": "c",
      "source_url": "http://www.accel.com/news/news_one_up.php?news_id=185",
      "source_description": "Accel",
      "raised_amount": 25000000,
      "raised_currency_code": "USD",
      "funded_year": 2008,
      "funded_month": 5,
      "funded_day": 19,
      "investments": [
        {
          "company": null,
          "financial_org": {
            "name": "DAG Ventures",
            "permalink": "dag-ventures"
          },
          "person": null
        },
        {
          "company": null,
          "financial_org": {
            "name": "Accel Partners",
            "permalink": "accel-partners"
          },
          "person": null
        },
        {
          "company": null,
          "financial_org": {
            "name": "Trinity Ventures",
            "permalink": "trinity-ventures"
          },
          "person": null
        },
        {
          "company": null,
          "financial_org": {
            "name": "Frazier Technology Ventures",
            "permalink": "frazier-technology-ventures"
          },
          "person": null
        }
      ]
    }
  ],
  "investments": [],
  "acquisition": {
    "price_amount": 30000000,
    "price_currency_code": "USD",
    "term_code": "cash_and_stock",
    "source_url": "http://allthingsd.com/20131216/viggle-tries-to-bulk-up-its-social-tv-business-by-buying-wetpaint/?mod=atdtweet",
    "source_description": " Viggle Tries to Bulk Up Its Social TV Business by Buying Wetpaint",
    "acquired_year": 2013,
    "acquired_month": 12,
    "acquired_day": 16,
    "acquiring_company": {
      "name": "Viggle",
      "permalink": "viggle"
    }
  },
  "acquisitions": [],
  "offices": [
    {
      "description": "",
      "address1": "710 - 2nd Avenue",
      "address2": "Suite 1100",
      "zip_code": "98104",
      "city": "Seattle",
      "state_code": "WA",
      "country_code": "USA",
      "latitude": 47.603122,
      "longitude": -122.333253
    },
    {
      "description": "",
      "address1": "270 Lafayette Street",
      "address2": "Suite 505",
      "zip_code": "10012",
      "city": "New York",
      "state_code": "NY",
      "country_code": "USA",
      "latitude": 40.7237306,
      "longitude": -73.9964312
    }
  ],
  "milestones": [
    {
      "id": 5869,
      "description": "Wetpaint named in Lead411's Hottest Seattle Companies list",
      "stoned_year": 2010,
      "stoned_month": 6,
      "stoned_day": 8,
      "source_url": "http://www.lead411.com/seattle-companies.html",
      "source_text": null,
      "source_description": "LEAD411 LAUNCHES \"HOTTEST SEATTLE COMPANIES\" AWARDS",
      "stoneable_type": "Company",
      "stoned_value": null,
      "stoned_value_type": null,
      "stoned_acquirer": null,
      "stoneable": {
        "name": "Wetpaint",
        "permalink": "wetpaint"
      }
    },
    {
      "id": 8702,
      "description": "Site-Builder Wetpaint Makes One For Itself, Using the Demand Media Playbook",
      "stoned_year": 2010,
      "stoned_month": 9,
      "stoned_day": 6,
      "source_url": "http://mediamemo.allthingsd.com/20100906/site-builder-wetpaint-makes-one-for-itself-using-the-demand-media-playbook/",
      "source_text": null,
      "source_description": "All Things D",
      "stoneable_type": "Company",
      "stoned_value": null,
      "stoned_value_type": null,
      "stoned_acquirer": null,
      "stoneable": {
        "name": "Wetpaint",
        "permalink": "wetpaint"
      }
    }
  ],
  "video_embeds": [],
  "screenshots": [
    {
      "available_sizes": [
        [
          [
            150,
            86
          ],
          "assets/images/resized/0016/0929/160929v2-max-150x150.png"
        ],
        [
          [
            250,
            143
          ],
          "assets/images/resized/0016/0929/160929v2-max-250x250.png"
        ],
        [
          [
            450,
            258
          ],
          "assets/images/resized/0016/0929/160929v2-max-450x450.png"
        ]
      ],
      "attribution": null
    }
  ],
  "external_links": [
    {
      "external_url": "http://www.geekwire.com/2011/rewind-ben-elowitz-wetpaint-ceo-building-type-media-company",
      "title": "GeekWire interview: Rewind - Ben Elowitz, Wetpaint CEO, on building a new type of media company"
    },
    {
      "external_url": "http://techcrunch.com/2012/06/17/search-and-social-how-two-will-soon-become-one/",
      "title": "Guest post by CEO Ben Elowitz in TechCrunch"
    },
    {
      "external_url": "http://allthingsd.com/20120516/what-to-expect-when-facebook-is-expecting-five-predictions-for-facebooks-first-public-year/",
      "title": "Guest post by CEO Ben Elowitz in AllThingsD"
    },
    {
      "external_url": "http://adage.com/article/digitalnext/facebook-biggest-player-advertising-s-540-billion-world/235708/",
      "title": "Guest post by CEO Ben Elowitz in AdAge"
    },
    {
      "external_url": "http://www.businessinsider.com/facebook-captures-14-percent-of-our-online-attention-but-only-4-percent-of-ad-spending-online-2012-6",
      "title": "Guest post by CEO Ben Elowitz in Business Insider"
    },
    {
      "external_url": "http://allfacebook.com/wetpaint-media-data_b75963",
      "title": "AllFacebook coverage of Wetpaint"
    },
    {
      "external_url": "http://adage.com/article/digital/celeb-site-wetpaint-shows-media-profit-facebook/237828/",
      "title": "Profile of Wetpaint in Ad Age"
    },
    {
      "external_url": "http://allthingsd.com/20121018/how-to-boost-your-facebook-traffic-tips-and-tricks-from-wetpaint/",
      "title": "Interview with Wetpaint CEO Ben Elowitz in All Things D"
    },
    {
      "external_url": "http://www.xconomy.com/seattle/2012/10/19/wetpaint-starts-licensing-its-facebook-based-media-distribution-tech/",
      "title": "Profile of Wetpaint in Xconomy"
    }
  ],
  "partners": []
}
```
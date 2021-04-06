# Countries-regions-stats-Covid-19-API


# API is for:
Data scientists, statisticians, developers, machines, programs, and other websites to be able to quickly fetch up to date culculated rates on the COVID-19 epidemic in specific country and region.  This dynamically generated REST API with Flask and Python returns agregated and culculated monthly rates on spesific country and region based on live cases, vaccination, historical data. This can be used to build tools and systems that are used for advanced rates/ratios analysis and for countries/regions  ranking building in public dashboards and charts.


# How to use API: 
- Cases data on specific country ( Example request:  Get /cases/United Kingdom )
- Cases data on specific country and region of that country ( Example request:  Get /cases/Germany/Bayern )
- Vaccines data on specific country ( Example request:  Get /vaccines/United Kingdom )
- Vaccines data on specific country and region of that country ( Example request:  Get /vaccines/Germany/Bayern )
- Deaths data on specific country ( Example request:  Get /deaths/United Kingdom )
- Deaths data on specific country and region of that country ( Example request:  Get /deaths/Germany/Bayern )
- Total deaths and death rate per 1000 population on specific country ( Example request:  Get /deaths/total/United Kingdom )
- Country with the most cases  (Example request:  Get /cases/most/United Kingdom )
- Country with the least cases (Example request:  Get /cases/least/United Kingdom )

# Data sources
- https://covid-api.mmediagroup.fr/v1
- https://github.com/M-Media-Group/Covid-19-API


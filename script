from flask import Flask, render_template, request, jsonify
 
import json
import requests
import requests_cache
 
requests_cache.install_cache('covid-19_api_cache', backend='sqlite', expire_after = 36000)
 
app = Flask(__name__)
 
cases_url_template = 'https://covid-api.mmediagroup.fr/v1/cases?country={country}'
vaccines_url_template = 'https://covid-api.mmediagroup.fr/v1/vaccines?country={country}'
history_url_template = 'https://covid-api.mmediagroup.fr/v1/history?country={country}&status=deaths'
cases_all_url = 'https://covid-api.mmediagroup.fr/v1/cases'

#returns welcome message and info about application
@app.route('/')
def index():
  html = '<h1>Welcome to our Covid-19 data application.</h1><br><h2>Navigation:</h2> <br>Covid case data by county: /cases/[country] <br>Covid case data by country and region: /cases/[country]/[region] <br>Covid vaccine data by county: /vaccines/[country] <br>Covid deaths data by county: /deaths/[country] <br>Total covid deaths and death rate per 1000 population by country: /deaths/total/[country] <br> The country with the most covid deaths: /cases/most <br> The country with the least covid deaths: /cases/least <br>'
  return html

#returns cases data for specific country (x)
@app.route('/cases/<x>', methods=['GET'])
def cases_per_country(x):
    my_country = request.args.get('country', x)
    cases_url = cases_url_template.format(country = my_country)
    resp = requests.get(cases_url)
    if resp.ok:
        return jsonify(resp.json())
    else:
        print(resp.reason)


#returns cases data for specific country (x) and region of that country (y)
@app.route('/cases/<x>/<y>', methods=['GET'])
def cases_per_country_region(x,y):
    my_country = request.args.get('country', x)
    cases_url = cases_url_template.format(country = my_country)
    resp = requests.get(cases_url)
    a = resp.json()
    if y in a.keys():
        return (a[y])
    else:
        return jsonify({'error':'region not found!'}), 404

#returns vaccines data for specific country (x) 
@app.route('/vaccines/<x>', methods=['GET'])
def vaccine_per_country(x):
    my_country = request.args.get('country', x)
    vaccines_url = vaccines_url_template.format(country = my_country)
    resp = requests.get(vaccines_url)
    if resp.ok:
        return jsonify(resp.json())
    else:
        print(resp.reason)

#returns deaths data for specific country (x) 
@app.route('/deaths/<x>', methods=['GET'])
def deaths_per_country(x):
    my_country = request.args.get('country', x)
    history_url = history_url_template.format(country = my_country)
    resp = requests.get(history_url)
    if resp.ok:
        return jsonify(resp.json())
    else:
        print(resp.reason)

#returns total deaths, and death rate per 1000 population for specific country (x)
@app.route('/deaths/total/<x>', methods=['GET'])
def total_deaths_per_country(x):
    my_country = request.args.get('country', x)
    history_url = history_url_template.format(country = my_country)
    resp = requests.get(history_url)
    b = resp.json()["All"]
    values = b["dates"].values()
    rate =sum(values)/len(b["dates"])*1000/b["population"]
    result = "Total deaths in " + x + ": " + str(sum(values))+ ";   Average historical death rate per 1000 population: " +str(round(rate,2))
    if resp.ok:
        return result
    else:
        print(resp.reason)

#returns the country with the most cases
@app.route('/cases/most', methods=['GET'])
def most_cases():
    resp = requests.get(cases_all_url)
    worst_country = "None"
    most = 0
    for x in resp.json():
      if x != ("Global"):
        current = resp.json()[x]["All"]["confirmed"]
        if current>most:
          most = current
          worst_country = str(x)
        else:
          pass
      else:
          pass
    result = "The country with the most cases is: " + worst_country + " with " + str(most) + "cases in total"
    if resp.ok:
        return result
    else:
        print(resp.reason)

#returns the country with the least cases
@app.route('/cases/least', methods=['GET'])
def least_cases():
    resp = requests.get(cases_all_url)
    best_country = "None"
    least = 1000000000000
    for x in resp.json():
      if x != ("Global"):
        current = resp.json()[x]["All"]["confirmed"]
        if current<least:
          least = current
          best_country = str(x)
        else:
          pass
      else:
          pass
    result = "The country with the least cases is: " + best_country + " with " + str(least) + "cases in total"
    if resp.ok:
        return result
    else:
        print(resp.reason)


if __name__=="__main__":
    app.run(host='0.0.0.0')

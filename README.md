# WeatherDetector

## This is a Django project " Weather Detector System " responsible to detect the temperature ,humidity,pressure,,and cooordinate of longitude and latitude
 
 This is the starting point of our system for giving you a possibility of searching an information of a city you want

![image](https://user-images.githubusercontent.com/103323625/181232867-4a3faa7a-30f2-4dfa-b61d-41dd72192c43.png)

As we see here after put your desired city in the search box you get information about it 


![image](https://user-images.githubusercontent.com/103323625/181233370-7a19102b-1d12-4f96-bb71-c6307b81c13e.png)


```python
from django.shortcuts import render
import json
import urllib.request


def index(request):
    if request.method == 'POST':
        city = request.POST['city']
        res = urllib.request.urlopen('https://api.openweathermap.org/data/2.5/weather?q='+city+'&appid=9739c58454b85887b8b2143420cd8e4a').read()
        json_data = json.loads(res)
        
        data ={
            "country_code": str(json_data['sys']['country']),
            "coordinate": str(json_data['coord']['lon']) + ' ' +
            str(json_data['coord']['lat']),
            "temp": str(json_data['main']['temp'])+'k',
            "pressure": str(json_data['main']['pressure']),
            "humidity": str(json_data['main']['humidity']),
        }
    else:
        city = ''
        data = {}    
    return render(request, 'index.html', {'city':city, 'data':data})



```
